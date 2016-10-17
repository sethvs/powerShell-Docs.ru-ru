# Get-InstalledModule

Возвращает установленные модули на компьютере.

## Описание

Командлет Get-InstalledModule возвращает модули PowerShell, которые были установлены командлетом Install-Module.

Для каждого установленного модуля Get-InstalledModule возвращает объект PSRepositoryItemInfo, который при необходимости можно передать командлету Uninstall-Module для удаления установленных модулей.

- Get-InstalledModule может фильтровать модули по имени и версии.
- Get-InstalledModule позволяет фильтровать модули при помощи следующих параметров версии: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Эти параметры являются взаимоисключающими (кроме MinmimumVersion и MaximumVersion).
  - Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.
  - Если параметр RequiredVersion не указан, командлет Get-InstalledModule возвращает последнюю версию установленного модуля, которая не ниже указанной минимальной версии, или последнюю версию модуля, если минимальная версия не указана. 
  - Если параметр RequiredVersion указан, Get-InstalledModule возвращает только версию установленного модуля, которая точно совпадает с указанной версией.

## Синтаксис командлета
```powershell
Get-Command -Name Get-InstalledModule -Module PowerShellGet -Syntax
```

## Ссылка на раздел справки по командлету в Интернете

[Get-InstalledModule](http://go.microsoft.com/fwlink/?LinkId=526863)

## Примеры команд

```powershell

# Get all modules installed using PowerShellGet cmdlets
Get-InstalledModule

# Get a specific installed module
Get-InstalledModule DJoin

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        DJoin                               PSGallery            This is a PowerShell frontend to the DJOIN.exe c...

# Get installed module with wildcards
Get-InstalledModule -Name AzureRM*

# Get all versions of an installed module
Get-InstalledModule -Name AzureRM.Automation -AllVersions

# Get installed module with MinimumVersion
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0

# Get installed module with MaximumVersion
Get-InstalledModule -Name AzureRM.Automation -MaximumVersion 1.0.8

# Get installed module with version range
Get-InstalledModule -Name AzureRM.Automation -MinimumVersion 1.0.0 -MaximumVersion 1.0.8

# Get installed module with RequiredVersion
Get-InstalledScript -Name AzureRM.Automation -RequiredVersion 1.0.3

# Properties of Get-InstalledModule returned object
Get-InstalledModule DJoin | Format-List * -Force

Name                       : DJoin
Version                    : 1.0
Type                       : Module
Description                : This is a PowerShell frontend to the DJOIN.exe command which provides better
                             discoverability and usability.
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 7:12:37 PM
InstalledDate              : 4/5/2016 4:13:39 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSModule}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Modules\DJoin\1.0

```



## Свойства InstalledDate и UpdatedDate в объекте PSGetRepositoryItemInfo

    During the install operation:
        InstalledDate: current DateTime (Get-Date) value
        UpdatedDate: null

    During the Update operation:
        InstalledDate: InstalledDate from the previous installation otherwise current DateTime (Get-Date) value
        UpdatedDate: current DateTime (Get-Date) value

```powershell
Install-Module -Name ContosoServer -RequiredVersion 1.0 -Repository INT
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM


\Update-Module -Name ContosoServer
Get-InstalledModule -Name ContosoServer | Format-Table Name, InstalledDate, UpdatedDate

Name          InstalledDate         UpdatedDate
----          -------------         -----------
ContosoServer 2/29/2016 11:59:14 AM 2/29/2016 12:00:15 PM
```

<!--HONumber=Aug16_HO3-->


