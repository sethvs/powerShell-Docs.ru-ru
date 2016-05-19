---
title: Объект ISEFile
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
---
# Объект ISEFile
  Объект **ISEFile** представляет файл в интегрированной среде сценариев (ISE) Windows PowerShell®. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEFile. В этом разделе перечислены его члены (методы и свойства). Объект **$PsISE.CurrentFile** и все файлы в коллекции "Файлы" на вкладке PowerShell являются экземплярами класса Microsoft.PowerShell.Host.ISE.ISEFile.

## Методы

###  <a name="save-override"></a> Save( [saveEncoding] )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Сохраняет файл на диске.

 **[saveEncoding]** — необязательный; [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
 Необязательный параметр кодировки символов, используемый для сохраненного файла. Значение по умолчанию — **UTF8**..

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

###  <a name="saveas"></a> SaveAs(filename, [saveEncoding])
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Сохраняет файл с указанным именем файла и кодировкой.

 **filename** — строка
 Имя, используемое для сохранения файла.

 **[saveEncoding]** — необязательный; [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
 Необязательный параметр кодировки символов, используемый для сохраненного файла. Значение по умолчанию — **UTF8**..

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

## Свойства

###  <a name="Displayname"></a> DisplayName
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает строку, содержащую отображаемое имя этого файла. Имя отображается на вкладке **Файл** в верхней части окна редактора. Наличие звездочки (*) в конце имени указывает, что файл содержит изменения, которые не были сохранены.

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

 Логическое свойство только для чтения, которое возвращает значение**$true**, если файл был сохранен после последнего изменения.

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

###  <a name="IsUntitled"></a> IsUntitled
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое возвращает значение **$true**, если для файла не было задано имя.

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## См. также
 [Объект ISEFileCollection](The-ISEFileCollection-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


