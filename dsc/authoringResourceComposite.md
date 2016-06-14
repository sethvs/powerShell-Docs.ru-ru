---
title: Составные ресурсы: использование DSC как ресурса ms.date:  2016-05-16 keywords:  powershell,DSC description:  
ms.topic:  article author:  eslesar manager:  dongill ms.prod:  powershell
---

# Составные ресурсы: использование DSC как ресурса

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

На практике конфигурации часто становятся длинными и сложными — вызывают множество разных ресурсов и задают большое количество свойств. Для решения этой проблемы можно использовать настройку требуемого состояния (DSC) Windows PowerShell как ресурс для других конфигураций. Мы называем это составным ресурсом. Составной ресурс — это конфигурация DSC с возможностью настройки параметров. Параметры конфигурации выступают как свойства ресурса. Конфигурация сохраняется как файл с расширением **.schema.psm1** и применяется вместо MOF-схемы и ресурса сценария в типовом ресурсе DSC (дополнительные сведения о ресурсах DSC см. в статье [Ресурсы настройки требуемого состояния Windows PowerShell](resources.md).

## Создание составного ресурса

В нашем примере создается конфигурация, которая вызывает ряд существующих ресурсов для настройки виртуальных машин. Вместо указания значений для настройки в блоках конфигурации она принимает ряд параметров, которые будут использоваться в блоках конфигурации.

```powershell
Configuration xVirtualMachine
{
    param
    (
        # Name of VMs
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String[]] $VMName,

        # Name of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchName,

        # Type of Switch to create
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $SwitchType,

        # Source Path for VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDParentPath,

        # Destination path for diff VHD
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VHDPath,

        # Startup Memory for VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMStartupMemory,

        # State of the VM
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [String] $VMState
    )

    # Import the module that defines custom resources
    Import-DscResource -Module xComputerManagement,xHyper-V

    # Install the Hyper-V role
    WindowsFeature HyperV
    {
        Ensure = "Present"
        Name = "Hyper-V"
    }

    # Create the virtual switch
    xVMSwitch $SwitchName
    {
        Ensure = "Present"
        Name = $SwitchName
        Type = $SwitchType
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check for Parent VHD file
    File ParentVHDFile
    {
        Ensure = "Present"
        DestinationPath = $VHDParentPath
        Type = "File"
        DependsOn = "[WindowsFeature]HyperV"
    }

    # Check the destination VHD folder
    File VHDFolder
    {
        Ensure = "Present"
        DestinationPath = $VHDPath
        Type = "Directory"
        DependsOn = "[File]ParentVHDFile"
    }

    # Creae VM specific diff VHD
    foreach ($Name in $VMName)
    {
        xVHD "VHD$Name"
        {
            Ensure = "Present"
            Name = $Name
            Path = $VHDPath
            ParentPath = $VHDParentPath
            DependsOn = @("[WindowsFeature]HyperV",
                          "[File]VHDFolder")
        }
    }

    # Create VM using the above VHD
    foreach($Name in $VMName)
    {
        xVMHyperV "VMachine$Name"
        {
            Ensure = "Present"
            Name = $Name
            VhDPath = (Join-Path -Path $VHDPath -ChildPath $Name)
            SwitchName = $SwitchName
            StartupMemory = $VMStartupMemory
            State = $VMState
            MACAddress = $MACAddress
            WaitForIP = $true
            DependsOn = @("[WindowsFeature]HyperV",
                          "[xVHD]VHD$Name")
        }
    }
}
```

### Сохранение конфигурации как составного ресурса

Чтобы использовать параметризованную конфигурацию как ресурс DSC, сохраните ее в структуре папок, как и любой другой ресурс на базе MOF, и присвойте имя с расширением **. schema.psm1**. В этом примере мы назовем файл **xVirtualMachine.schema.psm1**. Кроме того, необходимо создать манифест с именем **xVirtualMachine.psd1**, содержащий указанную ниже строку. Он дополняет **MyDscResources.psd1** — манифест модуля для всех ресурсов в папке **MyDscResources**.

```powershell
RootModule = 'xVirtualMachine.schema.psm1'
```

После выполнения этих действия структура папок должна выглядеть следующим образом:

```
$env: psmodulepath
    |- MyDscResources
           MyDscResources.psd1
        |- DSCResources
            |- xVirtualMachine
                |- xVirtualMachine.psd1
                |- xVirtualMachine.schema.psm1
```

Теперь ресурс можно обнаружить с помощью командлета Get-DscResource, а его свойство — с помощью того же командлета или комбинации клавиш **Ctrl + Space**, активирующей автозаполнение в интегрированной среде сценариев Windows PowerShell.

## Применение составного ресурса

Теперь создадим конфигурацию, которая вызывает составной ресурс. Эта конфигурация вызывает составной ресурс xVirtualMachine для создания виртуальной машины, а затем ресурс **xComputer**, чтобы ее переименовать.

```powershell

configuration RenameVM
{

    Import-DscResource -Module TestCompositeResource
    Node localhost
    {
        xVirtualMachine VM
        {
            VMName = "Test"
            SwitchName = "Internal"
            SwitchType = "Internal"
            VhdParentPath = "C:\Demo\VHD\RTM.vhd"
            VHDPath = "C:\Demo\VHD"
            VMStartupMemory = 1024MB
            VMState = "Running"
        }
    }

    Node "192.168.10.1"
    {
        xComputer Name
        {
            Name = "SQL01"
            DomainName = "fourthcoffee.com"
        }
    }
}
```

## См. также
### Концепции
* [Написание пользовательских ресурсов DSC с использованием MOF](authoringResourceMOF.md)
* [Начало работы с настройкой требуемого состояния Windows PowerShell](overview.md)



<!--HONumber=Jun16_HO1-->


