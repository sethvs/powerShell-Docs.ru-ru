# Unregister-PSRepository

Отмена регистрации репозитория.

## Описание

Командлет Unregister-PSRepository отменяет регистрацию репозитория для текущего пользователя.
- Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.
- Пользователи могут повторно зарегистрировать PSGallery, просто выполнив команду `Register-PSRepository -Default`
- Так как PSGallery — это репозиторий для публикации по умолчанию в командлетах Publish-Module и Publish-Script, возникнет ошибка, если коллекция PSGallery недоступна в списке зарегистрированных репозиториев.

## Синтаксис командлета

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## Ссылка на раздел справки по командлету в Интернете

[Unregister-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517130)

## Примеры команд

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```

<!--HONumber=Aug16_HO3-->


