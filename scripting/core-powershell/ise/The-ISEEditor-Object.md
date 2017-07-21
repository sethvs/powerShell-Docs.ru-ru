---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEEditor"
ms.assetid: 0101daf8-4e31-4e4c-ab89-01d95dcb8f46
ms.openlocfilehash: 41f2a6f7684275ad9d6d967ea67b64ca02c1c100
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="a677b-103">Объект ISEEditor</span><span class="sxs-lookup"><span data-stu-id="a677b-103">The ISEEditor Object</span></span>
  <span data-ttu-id="a677b-104">Объект **ISEEditor** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEEditor.</span><span class="sxs-lookup"><span data-stu-id="a677b-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="a677b-105">Область консоли — это объект **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="a677b-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="a677b-106">Каждый объект [ISEFile](The-ISEFile-Object.md) имеет связанный объект **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="a677b-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="a677b-107">В следующих разделах перечислены методы и свойства объекта **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="a677b-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="a677b-108">Методы</span><span class="sxs-lookup"><span data-stu-id="a677b-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="a677b-109">Clear\(\)</span><span class="sxs-lookup"><span data-stu-id="a677b-109">Clear\(\)</span></span>
  <span data-ttu-id="a677b-110">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-111">Удаляет текст в редакторе.</span><span class="sxs-lookup"><span data-stu-id="a677b-111">Clears the text in the editor.</span></span>

```PowerShell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="a677b-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="a677b-112">EnsureVisible\(int lineNumber\)</span></span>
  <span data-ttu-id="a677b-113">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-114">Прокручивает редактор таким образом, чтобы отображалась строка, соответствующая значению параметра **lineNumber**.</span><span class="sxs-lookup"><span data-stu-id="a677b-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="a677b-115">Метод создает исключение, если указанный номер строки находится за пределами диапазона 1, последнего номера строки, который определяет допустимые номера строк.</span><span class="sxs-lookup"><span data-stu-id="a677b-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

 <span data-ttu-id="a677b-116">**lineNumber**
. Номер строки, которая будет отображена.</span><span class="sxs-lookup"><span data-stu-id="a677b-116">**lineNumber**
 The number of the line that is to be made visible.</span></span>

```PowerShell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="a677b-117">Focus\(\)</span><span class="sxs-lookup"><span data-stu-id="a677b-117">Focus\(\)</span></span>
  <span data-ttu-id="a677b-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-119">Помещает редактор в фокус.</span><span class="sxs-lookup"><span data-stu-id="a677b-119">Sets the focus to the editor.</span></span>

```PowerShell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="a677b-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="a677b-120">GetLineLength\(int lineNumber \)</span></span>
  <span data-ttu-id="a677b-121">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-122">Получает длину строки (в виде целого числа) по указанному номеру строки.</span><span class="sxs-lookup"><span data-stu-id="a677b-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

 <span data-ttu-id="a677b-123">**lineNumber**
. Номер строки, длину которой необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="a677b-123">**lineNumber**
 The number of the line of which to get the length.</span></span>

 <span data-ttu-id="a677b-124">**Возвращаемое значение**
. Длина строки с указанным номером.</span><span class="sxs-lookup"><span data-stu-id="a677b-124">**Returns**
 The line length for the line at the specified line number.</span></span>

```PowerShell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="a677b-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="a677b-125">GoToMatch\(\)</span></span>
  <span data-ttu-id="a677b-126">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="a677b-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="a677b-127">Перемещает курсор в соответствующий знак, если свойству **CanGoToMatch** объекта редактора присвоено значение **$true**, которое присваивается, когда курсор находится непосредственно перед открывающей круглой, квадратной или фигурной скобкой (т. е. \(,\[,{) или сразу после закрывающей круглой, квадратной или фигурной скобки (т. е. \),\],}).</span><span class="sxs-lookup"><span data-stu-id="a677b-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="a677b-128">Курсор помещается перед открывающим символом или после закрывающего символа.</span><span class="sxs-lookup"><span data-stu-id="a677b-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="a677b-129">Если свойство **CanGoToMatch** имеет значение **$false**, этот метод не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="a677b-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span> <span data-ttu-id="a677b-130">См. раздел [CanGoToMatch](#cangotomatch).</span><span class="sxs-lookup"><span data-stu-id="a677b-130">See [CanGoToMatch](#cangotomatch).</span></span>

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### <a name="inserttext-text-"></a><span data-ttu-id="a677b-131">InsertText\( text \)</span><span class="sxs-lookup"><span data-stu-id="a677b-131">InsertText\( text \)</span></span>
  <span data-ttu-id="a677b-132">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-132">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-133">Заменяет выделенную область текстом или вставляет текст в текущей позиции курсора.</span><span class="sxs-lookup"><span data-stu-id="a677b-133">Replaces the selection with text or inserts text at the current caret position.</span></span>

 <span data-ttu-id="a677b-134">**text** — строка. Вставляемый текст.</span><span class="sxs-lookup"><span data-stu-id="a677b-134">**text** - String The text to insert.</span></span>

 <span data-ttu-id="a677b-135">См. [пример сценария](#example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a677b-135">See the [Scripting Example](#example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="a677b-136">Select\( startLine, startColumn, endLine, endColumn \)</span><span class="sxs-lookup"><span data-stu-id="a677b-136">Select\( startLine, startColumn, endLine, endColumn \)</span></span>
  <span data-ttu-id="a677b-137">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-137">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-138">Выделяет текст в области, определяемой параметрами **startLine**, **startColumn**, **endLine** и **endColumn**.</span><span class="sxs-lookup"><span data-stu-id="a677b-138">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

 <span data-ttu-id="a677b-139">**startLine** — целое число. Строка, в которой начинается выделение.</span><span class="sxs-lookup"><span data-stu-id="a677b-139">**startLine** - Integer The line where the selection starts.</span></span>

 <span data-ttu-id="a677b-140">**startColumn** — целое число. Столбец в строке, в которой начинается выделение.</span><span class="sxs-lookup"><span data-stu-id="a677b-140">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

 <span data-ttu-id="a677b-141">**endLine** — целое число. Строка, в которой заканчивается выделение.</span><span class="sxs-lookup"><span data-stu-id="a677b-141">**endLine** - Integer The line where the selection ends.</span></span>

 <span data-ttu-id="a677b-142">**endColumn** — целое число. Столбец в строке, в которой заканчивается выделение.</span><span class="sxs-lookup"><span data-stu-id="a677b-142">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

 <span data-ttu-id="a677b-143">См. [пример сценария](#example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a677b-143">See the  [Scripting Example](#example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="a677b-144">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="a677b-144">SelectCaretLine\(\)</span></span>
  <span data-ttu-id="a677b-145">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-145">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-146">Выделяет всю строку текста, в которой в данный момент находится курсор.</span><span class="sxs-lookup"><span data-stu-id="a677b-146">Selects the entire line of text that currently contains the caret.</span></span>

```PowerShell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="a677b-147">SetCaretPosition\( lineNumber, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="a677b-147">SetCaretPosition\( lineNumber, columnNumber \)</span></span>
  <span data-ttu-id="a677b-148">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-148">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-149">Задает положение курсора по номеру строки и номеру столбца.</span><span class="sxs-lookup"><span data-stu-id="a677b-149">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="a677b-150">Метод создает исключение, если номер строки или номер столбца курсора находятся вне соответствующих допустимых диапазонов.</span><span class="sxs-lookup"><span data-stu-id="a677b-150">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

 <span data-ttu-id="a677b-151">**lineNumber** — целое число. Номер строки курсора.</span><span class="sxs-lookup"><span data-stu-id="a677b-151">**lineNumber** - Integer The caret line number.</span></span>

 <span data-ttu-id="a677b-152">**columnNumber** — целое число. Номер столбца курсора.</span><span class="sxs-lookup"><span data-stu-id="a677b-152">**columnNumber** - Integer The caret column number.</span></span>

```PowerShell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="a677b-153">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="a677b-153">ToggleOutliningExpansion\(\)</span></span>
  <span data-ttu-id="a677b-154">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="a677b-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="a677b-155">Выполняет свертывание или развертывание всех разделов структуры.</span><span class="sxs-lookup"><span data-stu-id="a677b-155">Causes all the outline sections to expand or collapse.</span></span>

```PowerShell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="a677b-156">Свойства</span><span class="sxs-lookup"><span data-stu-id="a677b-156">Properties</span></span>

###  <span data-ttu-id="a677b-157"><a name="CanGoToMatch"></a> CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="a677b-157"><a name="CanGoToMatch"></a> CanGoToMatch</span></span>
  <span data-ttu-id="a677b-158">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="a677b-158">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="a677b-159">Логическое свойство, доступное только для чтения, которое указывает, находится ли курсор рядом с круглой, квадратной или фигурной скобкой (\(\), \[\] или {}).</span><span class="sxs-lookup"><span data-stu-id="a677b-159">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="a677b-160">Если курсор находится непосредственно перед открывающим символом или сразу после парного закрывающего символа, то это свойство имеет значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="a677b-160">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="a677b-161">В противном случае оно имеет значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="a677b-161">Otherwise, it is **$false**.</span></span>

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

###  <span data-ttu-id="a677b-162"><a name="CaretColumn"></a> CaretColumn</span><span class="sxs-lookup"><span data-stu-id="a677b-162"><a name="CaretColumn"></a> CaretColumn</span></span>
  <span data-ttu-id="a677b-163">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-163">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-164">Свойство только для чтения, которое получает номер столбца, соответствующего позиции курсора.</span><span class="sxs-lookup"><span data-stu-id="a677b-164">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```PowerShell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

###  <span data-ttu-id="a677b-165"><a name="CaretLine"></a> CaretLine</span><span class="sxs-lookup"><span data-stu-id="a677b-165"><a name="CaretLine"></a> CaretLine</span></span>
  <span data-ttu-id="a677b-166">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-166">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-167">Свойство только для чтения, которое получает номер строки, содержащей курсор.</span><span class="sxs-lookup"><span data-stu-id="a677b-167">The read-only property that gets the number of the line that contains the caret.</span></span>

```PowerShell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

###  <span data-ttu-id="a677b-168"><a name="CaretLineText"></a> CaretLineText</span><span class="sxs-lookup"><span data-stu-id="a677b-168"><a name="CaretLineText"></a> CaretLineText</span></span>
  <span data-ttu-id="a677b-169">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-169">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-170">Свойство только для чтения, которое получает полную строку текста, содержащую курсор.</span><span class="sxs-lookup"><span data-stu-id="a677b-170">The read-only property that gets the complete line of text that contains the caret.</span></span>

```PowerShell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

###  <span data-ttu-id="a677b-171"><a name="LineCount"></a> LineCount</span><span class="sxs-lookup"><span data-stu-id="a677b-171"><a name="LineCount"></a> LineCount</span></span>
  <span data-ttu-id="a677b-172">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-172">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-173">Свойство только для чтения, которое получает число строк из редактора.</span><span class="sxs-lookup"><span data-stu-id="a677b-173">The read-only property that gets the line count from the editor.</span></span>

```PowerShell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

###  <span data-ttu-id="a677b-174"><a name="SelectedText"></a> SelectedText</span><span class="sxs-lookup"><span data-stu-id="a677b-174"><a name="SelectedText"></a> SelectedText</span></span>
  <span data-ttu-id="a677b-175">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-175">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-176">Свойство только для чтения, которое получает выделенный текст из редактора.</span><span class="sxs-lookup"><span data-stu-id="a677b-176">The read-only property that gets the selected text from the editor.</span></span>

 <span data-ttu-id="a677b-177">См. [пример сценария](#example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a677b-177">See the  [Scripting Example](#example) later in this topic.</span></span>

###  <span data-ttu-id="a677b-178"><a name="Text"></a> Text</span><span class="sxs-lookup"><span data-stu-id="a677b-178"><a name="Text"></a> Text</span></span>
  <span data-ttu-id="a677b-179">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a677b-179">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="a677b-180">Свойство для чтения и записи, которое получает или задает текст в редакторе.</span><span class="sxs-lookup"><span data-stu-id="a677b-180">The read/write property that gets or sets the text in the editor.</span></span>

 <span data-ttu-id="a677b-181">См. [пример сценария](#example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="a677b-181">See the [Scripting Example](#example) later in this topic.</span></span>

##  <span data-ttu-id="a677b-182"><a name="example"></a> Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a677b-182"><a name="example"></a> Scripting Example</span></span>

```PowerShell
# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase. 
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor = $psISE.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line. 
$endColumn= $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1,1,3,$endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a><span data-ttu-id="a677b-183">См. также</span><span class="sxs-lookup"><span data-stu-id="a677b-183">See Also</span></span>
- [<span data-ttu-id="a677b-184">Объект ISEFile</span><span class="sxs-lookup"><span data-stu-id="a677b-184">The ISEFile Object</span></span>](The-ISEFile-Object.md) 
- [<span data-ttu-id="a677b-185">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="a677b-185">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="a677b-186">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a677b-186">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="a677b-187">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a677b-187">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="a677b-188">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="a677b-188">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
