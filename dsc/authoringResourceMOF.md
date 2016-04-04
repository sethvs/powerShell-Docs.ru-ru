# Написание пользовательских ресурсов DSC с использованием MOF

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

В этом разделе мы определим схему для настраиваемого ресурса настройки требуемого состояния (DSC) Windows PowerShell в MOF-файле и реализуем этот ресурс в файле сценария Windows PowerShell. Этот ресурс применяется для создания и обслуживания веб-сайтов.

## Создание схемы MOF

Схема определяет свойства ресурса, которые можно настроить с помощью сценария DSC.

### Структура папок для ресурса MOF

Для реализации настраиваемого ресурса DSC в схеме MOF создайте указанную ниже структуру папок. Схема MOF определяется в файле Demo_IISWebsite.schema.mof, а сценарий ресурса — в файле Demo_IISWebsite.ps1. При необходимости можно создать файл манифеста (PSD1) для модуля.

```
$env: psmodulepath (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

Обратите внимание, что папку DSCResources необходимо создать в папке верхнего уровня, а имя папки для каждого ресурса должно совпадать с именем ресурса.

### Содержание MOF-файла

Приведем пример файла MOF, который можно использовать как настраиваемый ресурс веб-сайта. Чтобы воспользоваться этим примером, сохраните данную схему в файле с именем *Demo_IISWebsite.schema.mof*.

```
[ClassVersion("1.0.0"), FriendlyName("Website")] 
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

В представленном выше коде обратите внимание на следующее.

* `FriendlyName` определяет имя, которое можно использовать для ссылки на этот настраиваемый ресурс в сценариях DSC. В этом примере `Website` — эквивалент понятного имени `Archive` для встроенного ресурса архива.
* Класс, определяемый для настраиваемого ресурса, должен быть производным от `OMI_BaseResource`.
* Квалификатор типа `[Key]` в свойстве означает, что это свойство служит для уникальной идентификации экземпляра ресурса. Свойство `[Key]` также является обязательным.
* Квалификатор `[Required]` означает, что свойство является обязательным (значение необходимо указывать в любом сценарии настройки, где используется ресурс).
* Квалификатор `[write]` означает, что свойство не является обязательным при использовании настраиваемого ресурса в сценарии настройки. Квалификатор `[read]` означает, что свойство не может задаваться конфигурацией и предназначено только для целей отчетности.
* `Values` ограничивает значения, которые могут быть присвоены свойству, списком значений, определенных в `ValueMap`. Дополнительные сведения см. в статье [ValueMap и квалификаторы значений](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).
* Для сохранения единообразия встроенных ресурсов DSC рекомендуется включать в ресурс свойство `Ensure`.
* Имя настраиваемого ресурса должно иметь формат `classname.schema.mof`, где `classname` — это идентификатор, следующий за ключевым словом `class` в определении схемы.

### Создание сценария ресурсов

Сценарий ресурса реализует логику ресурса. В этот модуль необходимо включить три функции: **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**. Все три функции должны принимать набор параметров, идентичный набору свойств, заданных в схеме MOF для вашего ресурса. В этом документе такой набор свойств называется "свойства ресурса". Сохраните эти три функции в файл <ResourceName>.psm1. В следующем примере функции сохраняются в файл с именем Demo_IISWebsite.psm1.

> **Примечание**. Многократное выполнение одного и того же сценария настройки для ресурса не вызывает ошибок, а состояние ресурса остается таким же, как при однократном выполнении. Для этого функции **Get-TargetResource** и **Test-TargetResource** не должны изменять ресурс, а вызов функции **Set-TargetResource** с одними и теми же параметрами больше одного раза подряд должен быть эквивалентен однократному вызову этой функции.

В реализации функции **Get-TargetResource** используйте значения свойств основных ресурсов, предоставляемых в качестве параметров, для проверки состояния указанного экземпляра ресурса. Эта функция должна возвращать хэш-таблицу со списком всех свойств ресурса в виде ключей и фактических значений этих свойств в виде соответствующих значений. Пример кода:

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource 
{
    param 
    (       
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name; 
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }
  
        $getTargetResourceResult;
}
```

В зависимости от того, какие значения заданы для свойств ресурса в сценарии конфигурации, **Set-TargetResource** должен выполнять одно из следующих действий:

* Создание веб-сайта
* Обновление существующего веб-сайта
* Удаление существующего веб-сайта

Это демонстрируется в следующем примере:

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine. 
function Set-TargetResource 
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param 
    (       
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )
 
    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

И наконец, функция **Test-TargetResource** должна принимать тот же набор параметров, что и функции **Get-TargetResource** и **Set-TargetResource**. В собственной реализации функции **Test-TargetResource** проверьте состояние экземпляра ресурса, заданное основными параметрами. Если фактическое состояние экземпляра ресурса не соответствует значениям, указанным в наборе параметров, возвращается **$false**. В противном случае возвращается **$true**.

Следующий код реализует функцию **Test-TargetResource**:

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to 
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result 
}
```

**Примечание**. Чтобы упростить отладку, используйте в реализации трех предыдущих функций командлет **Write-Verbose**. Он записывает текст в поток подробных сообщений. По умолчанию поток подробных сообщений не отображается, однако его можно вывести на экран, изменив значение переменной **$VerbosePreference** или применив в командлетах DSC параметр **Verbose** со значением new.

### Создание манифеста модуля

Командлет **New-ModuleManifest** позволяет определить файл <ResourceName>.psd1 для модуля настраиваемого ресурса. При вызове этого командлета необходимо сослаться на модуль сценария (PSM1-файл), описанный в предыдущем разделе. Включите в список функций для экспорта функции **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**. Пример файла манифеста:

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

<!--HONumber=Feb16_HO4-->


