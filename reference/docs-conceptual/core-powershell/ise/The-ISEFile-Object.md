---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEFile"
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 0e1c09c4a92868448d76cc7b4954d250773ce2f2
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-isefile-object"></a><span data-ttu-id="30d53-103">Объект ISEFile</span><span class="sxs-lookup"><span data-stu-id="30d53-103">The ISEFile Object</span></span>
  <span data-ttu-id="30d53-104">Объект **ISEFile** представляет файл в интегрированной среде скриптов (ISE) Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="30d53-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="30d53-105">Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEFile.</span><span class="sxs-lookup"><span data-stu-id="30d53-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="30d53-106">В этом разделе перечислены его члены (методы и свойства).</span><span class="sxs-lookup"><span data-stu-id="30d53-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="30d53-107">Объект **$PsISE.CurrentFile** и все файлы в коллекции "Файлы" на вкладке PowerShell являются экземплярами класса Microsoft.PowerShell.Host.ISE.ISEFile.</span><span class="sxs-lookup"><span data-stu-id="30d53-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="30d53-108">Методы</span><span class="sxs-lookup"><span data-stu-id="30d53-108">Methods</span></span>

###  <span data-ttu-id="30d53-109"><a name="save-override"></a> Save\( \]saveEncoding\[ \)</span><span class="sxs-lookup"><span data-stu-id="30d53-109"><a name="save-override"></a> Save\( \[saveEncoding\] \)</span></span>
  <span data-ttu-id="30d53-110">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-111">Сохраняет файл на диске.</span><span class="sxs-lookup"><span data-stu-id="30d53-111">Saves the file to disk.</span></span>

 <span data-ttu-id="30d53-112">**\[saveEncoding\]** — необязательный [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
. Необязательный параметр кодировки символов, используемый для сохраненного файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-112">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
 An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="30d53-113">Значение по умолчанию — **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="30d53-113">The default value is **UTF8**.</span></span>

 <span data-ttu-id="30d53-114">**Исключения**</span><span class="sxs-lookup"><span data-stu-id="30d53-114">**Exceptions**</span></span>
 -   <span data-ttu-id="30d53-115">**System.IO.IOException**: не удалось сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="30d53-115">**System.IO.IOException**: The file could not be saved.</span></span>

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

###  <span data-ttu-id="30d53-116"><a name="saveas"></a>SaveAs\(filename, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="30d53-116"><a name="saveas"></a> SaveAs\(filename, \[saveEncoding\]\)</span></span>
  <span data-ttu-id="30d53-117">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-118">Сохраняет файл с указанным именем файла и кодировкой.</span><span class="sxs-lookup"><span data-stu-id="30d53-118">Saves the file with the specified file name and encoding.</span></span>

 <span data-ttu-id="30d53-119">**filename** — строка. Имя, используемое для сохранения файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-119">**filename** - String The name to be used to save the file.</span></span>

 <span data-ttu-id="30d53-120">**\[saveEncoding\]** — необязательный [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
. Необязательный параметр кодировки символов, используемый для сохраненного файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-120">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx)
 An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="30d53-121">Значение по умолчанию — **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="30d53-121">The default value is **UTF8**.</span></span>

 <span data-ttu-id="30d53-122">**Исключения**</span><span class="sxs-lookup"><span data-stu-id="30d53-122">**Exceptions**</span></span>
 -   <span data-ttu-id="30d53-123">**System.ArgumentNullException**: параметр **filename** имеет значение NULL.</span><span class="sxs-lookup"><span data-stu-id="30d53-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>

-   <span data-ttu-id="30d53-124">**System.ArgumentException**: параметр **filename** пуст.</span><span class="sxs-lookup"><span data-stu-id="30d53-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>

-   <span data-ttu-id="30d53-125">**System.IO.IOException**: не удалось сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="30d53-125">**System.IO.IOException**: The file could not be saved.</span></span>

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## <a name="properties"></a><span data-ttu-id="30d53-126">Свойства</span><span class="sxs-lookup"><span data-stu-id="30d53-126">Properties</span></span>

###  <span data-ttu-id="30d53-127"><a name="Displayname"></a> DisplayName</span><span class="sxs-lookup"><span data-stu-id="30d53-127"><a name="Displayname"></a> DisplayName</span></span>
  <span data-ttu-id="30d53-128">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-129">Свойство только для чтения, которое получает строку, содержащую отображаемое имя этого файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="30d53-130">Имя отображается на вкладке **Файл** в верхней части окна редактора.</span><span class="sxs-lookup"><span data-stu-id="30d53-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="30d53-131">Наличие звездочки \(\*\) в конце имени указывает, что в файле есть изменения, которые не были сохранены.</span><span class="sxs-lookup"><span data-stu-id="30d53-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

###  <span data-ttu-id="30d53-132"><a name="Editor"></a> Editor</span><span class="sxs-lookup"><span data-stu-id="30d53-132"><a name="Editor"></a> Editor</span></span>
  <span data-ttu-id="30d53-133">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-134">Свойство только для чтения, которое получает [объект редактора](The-ISEEditor-Object.md), используемый для указанного файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

###  <span data-ttu-id="30d53-135"><a name="Encoding"></a> Encoding</span><span class="sxs-lookup"><span data-stu-id="30d53-135"><a name="Encoding"></a> Encoding</span></span>
  <span data-ttu-id="30d53-136">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-137">Свойство только для чтения, которое получает исходную кодировку файла.</span><span class="sxs-lookup"><span data-stu-id="30d53-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="30d53-138">Это объект **System.Text.Encoding**.</span><span class="sxs-lookup"><span data-stu-id="30d53-138">This is a **System.Text.Encoding** object.</span></span>

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

###  <span data-ttu-id="30d53-139"><a name="FullPath"></a> FullPath</span><span class="sxs-lookup"><span data-stu-id="30d53-139"><a name="FullPath"></a> FullPath</span></span>
  <span data-ttu-id="30d53-140">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-141">Свойство только для чтения, которое получает строку, указывающую полный путь к открытому файлу.</span><span class="sxs-lookup"><span data-stu-id="30d53-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

###  <span data-ttu-id="30d53-142"><a name="IsSaved"></a> IsSaved</span><span class="sxs-lookup"><span data-stu-id="30d53-142"><a name="IsSaved"></a> IsSaved</span></span>
  <span data-ttu-id="30d53-143">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-144">Логическое свойство только для чтения, которое возвращает значение **$true**, если файл был сохранен после последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="30d53-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

###  <span data-ttu-id="30d53-145"><a name="IsUntitled"></a> IsUntitled</span><span class="sxs-lookup"><span data-stu-id="30d53-145"><a name="IsUntitled"></a> IsUntitled</span></span>
  <span data-ttu-id="30d53-146">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="30d53-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="30d53-147">Свойство только для чтения, которое возвращает значение **$true**, если для файла не задано имя.</span><span class="sxs-lookup"><span data-stu-id="30d53-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## <a name="see-also"></a><span data-ttu-id="30d53-148">См. также</span><span class="sxs-lookup"><span data-stu-id="30d53-148">See Also</span></span>
- [<span data-ttu-id="30d53-149">Объект ISEFileCollection</span><span class="sxs-lookup"><span data-stu-id="30d53-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md) 
- [<span data-ttu-id="30d53-150">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="30d53-150">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="30d53-151">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="30d53-151">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="30d53-152">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="30d53-152">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
