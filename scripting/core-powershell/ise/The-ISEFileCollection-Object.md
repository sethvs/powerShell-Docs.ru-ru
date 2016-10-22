---
title: "Объект ISEFileCollection"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
translationtype: Human Translation
ms.sourcegitcommit: fe3d7885b7c031a24a737f58523c8018cfc36146
ms.openlocfilehash: 109d93df4ebe6dbc354d333e038846ad2c3cb984

---

# Объект ISEFileCollection
  Объект **ISEFileCollection**  — это коллекция объектов **ISEFile**. Примером является коллекция $psISE.CurrentPowerShellTab.Files.

## Методы

### Add\( \[fullPath\] \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Создает и возвращает новый файл без имени и добавляет его в коллекцию. Свойство **IsUntitled** созданного файла имеет значение **$true**.

 **\[fullPath\]** — необязательная строка. Полный путь к файлу. Исключение возникает, если включен параметр **fullPath** и относительный путь или если вместо полного пути используется имя файла.

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### Remove\( File, \[Force\] \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет указанный файл из текущей вкладки PowerShell.

 **File** — строка. Файл ISEFile, удаляемый из коллекции. Если файл не был сохранен, этот метод создает исключение. Используйте параметр **Force** для принудительного удаления несохраненного файла.

 **\[Force\]** — необязательное логическое значение. Если задано значение **$true**, предоставляет разрешение на удаление файла, даже если он не был сохранен с момента последнего использования. Значение по умолчанию — **$false**.

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### SetSelectedFile\( selectedFile \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выбирает файл, который задается параметром **selectedFile**.

 **selectedFile** — Microsoft.PowerShell.Host.ISE.ISEFile. Выбираемый файл ISEFile.

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## См. также
 [Объект ISEFile](The-ISEFile-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  



<!--HONumber=Oct16_HO2-->


