# Создание ресурса DSC на языке C`#`

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Как правило, настраиваемый ресурс настройки требуемого состояния (DSC) Windows PowerShell реализуется в сценарии PowerShell. Кроме того, для реализации настраиваемого ресурса DSC можно писать командлеты на языке C#. Вводные сведения о написании командлетов на языке C# см. в статье [Написание командлетов Windows PowerShell](https://technet.microsoft.com/en-us/library/dd878294.aspx)..

Процесс создания схемы MOF и структуры папок, импорта и применения настраиваемого ресурса DSC (кроме реализации ресурса на языке C# в форме командлетов) соответствует описанию в статье [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md)..

## Создание ресурса на основе командлетов
В этом примере мы реализуем простой ресурс, управляющий текстовым файлом и его содержимым.

### Создание схемы MOF

Ниже дано определение ресурса MOF.

```
[ClassVersion("1.0.0"), FriendlyName("xDemoFile")]
class MSFT_XDemoFile : OMI_BaseResource
{
                [Key, Description("path")] String Path;
                [Write, Description("Should the file be present"), ValueMap{"Present","Absent"}, Values{"Present","Absent"}] String Ensure;
                [Write, Description("Contentof file.")] String Content;                   
};
```

### Настройка проекта Visual Studio
#### Настройка проекта командлета

1. Откройте Visual Studio.
1. Создайте проект C# и укажите имя.
1. Выберите в списке доступных шаблонов проектов **библиотеку классов**.
1. Нажмите кнопку **ОК**..
1. Добавьте в проект ссылку на сборку System.Automation.Management.dll.
1. Измените имя сборки в соответствии с именем ресурса. В данном случае сборка должна называться **MSFT_XDemoFile**..

### Написание кода командлета

Следующий код на языке C# реализует командлеты **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**.

```C#
Get-TargetResource
       [OutputType(typeof(System.Collections.Hashtable))]
       [Cmdlet(VerbsCommon.Get, "TargetResource")]
       public class GetTargetResource : PSCmdlet
       {
              [Parameter(Mandatory = true)]
              public string Path { get; set; }
 
///<summary>
/// Implement the logic to write the current state of the resource as a 
/// Hash table with keys being the resource properties 
/// and the Values are the corresponding current values on the target machine.
 
///</summary>
              protected override void ProcessRecord()
              {
// Download the zip file at the end of this blog to see sample implementation.
 }
 
Set-TargetResouce
         [OutputType(typeof(void))]
    [Cmdlet(VerbsCommon.Set, "TargetResource")]
    public class SetTargetResource : PSCmdlet
    {
        privatestring _ensure;
        privatestring _content;
        
[Parameter(Mandatory = true)]
        public string Path { get; set; }
        
[Parameter(Mandatory = false)]      
       [ValidateSet("Present", "Absent", IgnoreCase = true)]
       public string Ensure {
            get
            {
                // set the default to present.
               return (this._ensure ?? "Present");
            }
            set
            {
                this._ensure = value;
            }
           } 
            public string Content {
            get { return (string.IsNullOrEmpty(this._content) ? "" : this._content); }
            set { this._content = value; }
        }
 
///<summary>
        /// Implement the logic to set the state of the machine to the desired state.
        ///</summary>
        protected override void ProcessRecord()
        {
//Implement the set method of the resource 
/* Uncomment this section if your resource needs a machine reboot.
PSVariable DscMachineStatus = new PSVariable("DSCMachineStatus", 1, ScopedItemOptions.AllScope);
                this.SessionState.PSVariable.Set(DscMachineStatus);
*/     
  }
    }
Test-TargetResource    
       [Cmdlet("Test", "TargetResource")]
    [OutputType(typeof(Boolean))]
    public class TestTargetResource : PSCmdlet
    {   
        
        private string _ensure;
        private string _content;
 
        [Parameter(Mandatory = true)]
        public string Path { get; set; }
 
        [Parameter(Mandatory = false)]
        [ValidateSet("Present", "Absent", IgnoreCase = true)]
        public string Ensure
        {
            get
            {
                // set the default to present.
                return (this._ensure ?? "Present");
            }
            set
            {
                this._ensure = value;
            }
        }
 
        [Parameter(Mandatory = false)]
        public string Content
        {
            get { return (string.IsNullOrEmpty(this._content) ? "“:this._content);}
            set { this._content = value; }
        }
 
///<summary>
/// Write a Boolean value which indicates whether the current machine is in    
/// desired state or not.
        ///</summary>
        protected override void ProcessRecord()
        {
                // Implement the test method of the resource.
        }
}
```

### Развертывание ресурса

Скомпилированный DLL-файл необходимо сохранить в структуре файлов аналогично ресурсу на основе сценария. Ниже показана структура папок для этого ресурса.

```
$env: psmodulepath (folder)
    |- MyDscResources (folder)
        |- MyDscResources.psd1 (file, required)     
        |- DSCResources (folder)
            |- MSFT_XDemoFile (folder)
                |- MSFT_XDemoFile.psd1 (file, optional)
                |- MSFT_XDemoFile.dll (file, required)
                |- MSFT_XDemoFile.schema.mof (file, required)
```

### См. также
#### Концепции
[Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md)
#### Прочие ресурсы
[Запись командлета Windows PowerShell](https://msdn.microsoft.com/en-us/library/dd878294.aspx)


<!--HONumber=May16_HO2-->


