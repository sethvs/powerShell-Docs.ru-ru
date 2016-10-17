# Get-PSRepository

Возвращает информацию о зарегистрированных репозиториях, которая есть на компьютере.

## Описание

Командлет Get-PSRepository возвращает репозитории модуля PowerShell, зарегистрированные для текущего пользователя на компьютере.

Для каждого зарегистрированного репозитория Get-PSRepository возвращает объект PSRepository, который при необходимости может быть передан в командлет Unregister-PSRepository для отмены регистрации зарегистрированного репозитория.

## Синтаксис командлета
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## Ссылка на раздел справки по командлету в Интернете

[Get-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517127)

## Примеры команд

```powershell

# Properties of Get-PSRepository returned object
Get-PSRepository PSGallery | Format-List * -Force

Name                      : PSGallery
SourceLocation            : https://www.powershellgallery.com/api/v2/
Trusted                   : False
Registered                : True
InstallationPolicy        : Untrusted
PackageManagementProvider : NuGet
PublishLocation           : https://www.powershellgallery.com/api/v2/package/
ScriptSourceLocation      : https://www.powershellgallery.com/api/v2/items/psscript/
ScriptPublishLocation     : https://www.powershellgallery.com/api/v2/package/
ProviderOptions           : {}

# Get all registered repositories
Get-PSRepository

# Get a specific registered repository
Get-PSRepository PSGallery

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/

# Get registered repository with wildcards
Get-PSRepository *Gallery*

```

<!--HONumber=Aug16_HO3-->


