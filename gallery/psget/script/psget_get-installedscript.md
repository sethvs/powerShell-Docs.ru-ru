# Get-InstalledScript

Возвращает установленные сценарии на компьютере.

## Описание

Командлет Get-InstalledScript возвращает установленные на компьютере сценарии PowerShell.

Для каждого установленного сценария Get-InstalledScript возвращает объект PSRepositoryItemInfo, который при необходимости можно передать командлету Uninstall-Script для удаления установленных сценариев.

- Get-InstalledScript может фильтровать сценарии по имени и версии.
- Get-InstalledScript позволяет фильтровать сценарии с помощью следующих параметров версии: MinimumVersion, MaximumVersion, RequiredVersion, AllVersions.
  - Эти параметры являются взаимоисключающими (кроме MinmimumVersion и MaximumVersion).
  - Эти параметры версии допускаются только с единственным именем сценария без каких-либо подстановочных знаков.
  - Если параметр RequiredVersion не указан, командлет Get-InstalledScript возвращает последнюю версию сценария не ниже указанной минимальной версии или последнюю версию сценария, если минимальная версия не указана. 
  - Если параметр RequiredVersion указан, Get-InstalledScript возвращает только версию установленного сценария, которая точно совпадает с указанной версией.

## Синтаксис командлета

```powershell
Get-Command -Name Get-InstalledScript -Module PowerShellGet -Syntax
```

## Ссылка на раздел справки по командлету в Интернете

[Get-InstalledScript](http://go.microsoft.com/fwlink/?LinkId=619790)

## Примеры команд

```powershell

# Get all scripts installed using PowerShellGet cmdlets
Get-InstalledScript

# Get a specific installed script
Get-InstalledScript Show-Tree

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.0      Show-Tree                           PSGallery            Script to show the layout of PowerShell namespaces (Tr...

# Get installed script with wildcards
Get-InstalledScript -Name *Azure*

# Get all versions of an installed script
Get-InstalledScript -Name Connect-O365 -AllVersions

# Get installed script with MinimumVersion
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1

# Get installed script with MaximumVersion
Get-InstalledScript -Name Connect-O365 -MaximumVersion 1.6.3

# Get installed script with version range
Get-InstalledScript -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.3

# Get installed script with RequiredVersion
Get-InstalledScript -Name Connect-O365 -RequiredVersion 1.4

# Properties of Get-InstalledScript returned object
Get-InstalledScript Show-Tree | Format-List * -Force

Name                       : Show-Tree
Version                    : 1.0.0
Type                       : Script
Description                : Script to show the layout of PowerShell namespaces (Trees) using ASCII
Author                     : Jeffrey Snover
CompanyName                : jsnover
Copyright                  : (C) Microsoft Corporation. All rights reserved.
PublishedDate              : 2/15/2016 10:15:35 PM
InstalledDate              : 5/4/2016 11:44:13 PM
UpdatedDate                :
LicenseUri                 :
ProjectUri                 :
IconUri                    :
Tags                       : {Nano, PSScript}
Includes                   : {Function, RoleCapability, Command, DscResource...}
PowerShellGetFormatVersion :
ReleaseNotes               :
Dependencies               : {}
RepositorySourceLocation   : https://www.powershellgallery.com/api/v2/
Repository                 : PSGallery
PackageManagementProvider  : NuGet
AdditionalMetadata         : {description, installeddate, tags, PackageManagementProvider...}
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


```

<!--HONumber=Aug16_HO3-->


