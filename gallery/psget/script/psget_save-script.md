# Save-Script

Командлет Save-Script позволяет просмотреть файл сценария, сохранив его в указанном расположении.

## Описание

Командлет Save-Script сохраняет указанный скрипт.

## Синтаксис командлета

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## Ссылка на раздел справки по командлету в Интернете

[Save-Script](http://go.microsoft.com/fwlink/?LinkId=619786)

## Примеры команд

### Пример 1. Сохранение скрипта из репозитория
Эта команда сохраняет последнюю версию скрипта Fabrikam-ClientScript из репозитория GalleryINT в локальную папку C:\ScriptSharingDemo.

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### Пример 2. Сохранение версии скрипта по конвейеру из командлета Find-Script

Первая команда находит версию 1.5 скрипта Fabrikam-ClientScript в репозитории GalleryINT и сохраняет ее в папку C:\ScriptSharingDemo.

Вторая команда проверяет метаданные сохраненного скрипта.

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```


<!--HONumber=Aug16_HO3-->


