# Set-PSRepository

Set-PSRepository задает значения для зарегистрированного репозитория.

## Описание

Командлет Set-PSRepository задает значения для зарегистрированного репозитория модулей.

## Синтаксис командлета

```powershell
Get-Command -Name Set-PSRepository -Module PowerShellGet -Syntax
```
## Ссылка на раздел справки по командлету в Интернете

[Set-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517128)

## Примеры команд

```powershell
PS C:\> Register-PSRepository -Name myRepository -SourceLocation "https://www.myget.org/F/powershellgetdemo/api/v2" -InstallationPolicy Trusted
PS C:\> Get-PSRepository
Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
myRepository              Trusted              https://www.myget.org/F/powershellgetdemo/api/v2

# Set installation Policy for a repository
PS C:\> Set-PSRepository -Name myRepository -InstallationPolicy Untrusted
PS C:\> Get-PSRepository

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
myRepository              Untrusted            https://www.myget.org/F/powershellgetdemo/api/v2
```


### Командлет Set-PSRepository с поддержкой совместного использования скриптов

Используйте командлеты Set-PSRepository для добавления **ScriptSourceLocation** и **ScriptPublishLocation** в PSRepository.
```powershell
# Add script sharing locations to an existing PSRepository using Set-PSRepository object.
Set-PSRepository -Name MyGallery `
                 -ScriptSourceLocation https://MyGallery.com/api/v2/items/psscript/ `
                 -ScriptPublishLocation https://MyGallery.com/api/v2/package/

Get-PSRepository -Name GalleryINT | Format-List * -Force

Name : GalleryINT
SourceLocation : https://MyGallery.com/api/v2/
Trusted : True
Registered : True
InstallationPolicy : Trusted
PackageManagementProvider : NuGet
PublishLocation : https://MyGallery.com/api/v2/package/
ScriptSourceLocation : https://MyGallery.com/api/v2/items/psscript/
ScriptPublishLocation : https://MyGallery.com/api/v2/package/
ProviderOptions : {}

```


<!--HONumber=Aug16_HO3-->


