---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект ISEFile
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 276e8f04a827e18999b5b3ecb08f47de4f4b23b1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-isefile-object"></a>Объект ISEFile

Объект **ISEFile** представляет файл в интегрированной среде скриптов (ISE) Windows PowerShell®. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEFile. В этом разделе перечислены его члены (методы и свойства). Объект **$PsISE.CurrentFile** и все файлы в коллекции "Файлы" на вкладке PowerShell являются экземплярами класса Microsoft.PowerShell.Host.ISE.ISEFile.

## <a name="methods"></a>Методы

### <a name="save-saveencoding-"></a>Save\( \[saveEncoding\] \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Сохраняет файл на диске.

**\[saveEncoding\]** — необязательный параметр кодировки символов [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx), используемый для сохраненного файла. Значение по умолчанию — **UTF8**.

### <a name="exceptions"></a>Исключения

- **System.IO.IOException**: не удалось сохранить файл.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>SaveAs\(filename, \[saveEncoding\]\)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Сохраняет файл с указанным именем файла и кодировкой.

**filename** — строка. Имя, используемое для сохранения файла.

**\[saveEncoding\]** — необязательный параметр кодировки символов [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx), используемый для сохраненного файла. Значение по умолчанию — **UTF8**.

### <a name="exceptions"></a>Исключения

- **System.ArgumentNullException**: параметр **filename** имеет значение NULL.
- **System.ArgumentException**: параметр **filename** пуст.
- **System.IO.IOException**: не удалось сохранить файл.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Свойства

### <a name="displayname"></a>DisplayName

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает строку, содержащую отображаемое имя этого файла. Имя отображается на вкладке **Файл** в верхней части окна редактора. Наличие звездочки \(\*\) в конце имени указывает, что в файле есть изменения, которые не были сохранены.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Editor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает [объект редактора](The-ISEEditor-Object.md), используемый для указанного файла.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Encoding

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает исходную кодировку файла. Это объект **System.Text.Encoding**.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает строку, указывающую полный путь к открытому файлу.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Логическое свойство только для чтения, которое возвращает значение **$true**, если файл был сохранен после последнего изменения.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое возвращает значение **$true**, если для файла не задано имя.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>См. также

- [Объект ISEFileCollection](The-ISEFileCollection-Object.md)
- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)