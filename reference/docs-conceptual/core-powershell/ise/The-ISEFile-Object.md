---
ms.date: 2017-06-05T00:00:00.000Z
keywords: "powershell,командлет"
title: "Объект ISEFile"
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 0e1c09c4a92868448d76cc7b4954d250773ce2f2
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="the-isefile-object"></a>Объект ISEFile
  Объект **ISEFile** представляет файл в интегрированной среде скриптов (ISE) Windows PowerShell®. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEFile. В этом разделе перечислены его члены (методы и свойства). Объект **$PsISE.CurrentFile** и все файлы в коллекции "Файлы" на вкладке PowerShell являются экземплярами класса Microsoft.PowerShell.Host.ISE.ISEFile.

## <a name="methods"></a>Методы

###  <a name="save-override"></a> Save\( \]saveEncoding\[ \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Сохраняет файл на диске.

 **\[saveEncoding\]** — необязательный параметр кодировки символов [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx), используемый для сохраненного файла. Значение по умолчанию — **UTF8**.

 **Исключения**
 -   **System.IO.IOException**: не удалось сохранить файл.

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

###  <a name="saveas"></a>SaveAs\(filename, \[saveEncoding\]\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Сохраняет файл с указанным именем файла и кодировкой.

 **filename** — строка. Имя, используемое для сохранения файла.

 **\[saveEncoding\]** — необязательный параметр кодировки символов [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx), используемый для сохраненного файла. Значение по умолчанию — **UTF8**.

 **Исключения**
 -   **System.ArgumentNullException**: параметр **filename** имеет значение NULL.

-   **System.ArgumentException**: параметр **filename** пуст.

-   **System.IO.IOException**: не удалось сохранить файл.

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## <a name="properties"></a>Свойства

###  <a name="Displayname"></a> DisplayName
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает строку, содержащую отображаемое имя этого файла. Имя отображается на вкладке **Файл** в верхней части окна редактора. Наличие звездочки \(\*\) в конце имени указывает, что в файле есть изменения, которые не были сохранены.

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

###  <a name="Editor"></a> Editor
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает [объект редактора](The-ISEEditor-Object.md), используемый для указанного файла.

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

###  <a name="Encoding"></a> Encoding
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает исходную кодировку файла. Это объект **System.Text.Encoding**.

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

###  <a name="FullPath"></a> FullPath
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает строку, указывающую полный путь к открытому файлу.

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

###  <a name="IsSaved"></a> IsSaved
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Логическое свойство только для чтения, которое возвращает значение **$true**, если файл был сохранен после последнего изменения.

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

###  <a name="IsUntitled"></a> IsUntitled
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое возвращает значение **$true**, если для файла не задано имя.

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## <a name="see-also"></a>См. также
- [Объект ISEFileCollection](The-ISEFileCollection-Object.md) 
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)

  
