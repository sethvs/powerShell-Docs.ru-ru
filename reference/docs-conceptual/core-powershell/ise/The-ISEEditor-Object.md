---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEEditor"
ms.openlocfilehash: 149eda44fea5b02324442970324e3010015e7ae5
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="65300-103">Объект ISEEditor</span><span class="sxs-lookup"><span data-stu-id="65300-103">The ISEEditor Object</span></span>
  <span data-ttu-id="65300-104">Объект **ISEEditor** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEEditor.</span><span class="sxs-lookup"><span data-stu-id="65300-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="65300-105">Область консоли — это объект **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="65300-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="65300-106">Каждый объект [ISEFile](The-ISEFile-Object.md) имеет связанный объект **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="65300-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="65300-107">В следующих разделах перечислены методы и свойства объекта **ISEEditor**.</span><span class="sxs-lookup"><span data-stu-id="65300-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="65300-108">Методы</span><span class="sxs-lookup"><span data-stu-id="65300-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="65300-109">Clear\(\)</span><span class="sxs-lookup"><span data-stu-id="65300-109">Clear\(\)</span></span>
  <span data-ttu-id="65300-110">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-111">Удаляет текст в редакторе.</span><span class="sxs-lookup"><span data-stu-id="65300-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="65300-112">EnsureVisible\(int lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="65300-112">EnsureVisible\(int lineNumber\)</span></span>
  <span data-ttu-id="65300-113">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-114">Прокручивает редактор таким образом, чтобы отображалась строка, соответствующая значению параметра **lineNumber**.</span><span class="sxs-lookup"><span data-stu-id="65300-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="65300-115">Метод создает исключение, если указанный номер строки находится за пределами диапазона 1, последнего номера строки, который определяет допустимые номера строк.</span><span class="sxs-lookup"><span data-stu-id="65300-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

 <span data-ttu-id="65300-116">**lineNumber** — номер строки, которая будет отображена.</span><span class="sxs-lookup"><span data-stu-id="65300-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="65300-117">Focus\(\)</span><span class="sxs-lookup"><span data-stu-id="65300-117">Focus\(\)</span></span>
  <span data-ttu-id="65300-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-119">Помещает редактор в фокус.</span><span class="sxs-lookup"><span data-stu-id="65300-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="65300-120">GetLineLength\(int lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="65300-120">GetLineLength\(int lineNumber \)</span></span>
  <span data-ttu-id="65300-121">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-122">Получает длину строки (в виде целого числа) по указанному номеру строки.</span><span class="sxs-lookup"><span data-stu-id="65300-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

 <span data-ttu-id="65300-123">**lineNumber** — номер строки, длину которой необходимо получить.</span><span class="sxs-lookup"><span data-stu-id="65300-123">**lineNumber** The number of the line of which to get the length.</span></span>

 <span data-ttu-id="65300-124">**Возвращаемое значение** — длина строки с указанным номером.</span><span class="sxs-lookup"><span data-stu-id="65300-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="65300-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="65300-125">GoToMatch\(\)</span></span>
  <span data-ttu-id="65300-126">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="65300-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="65300-127">Перемещает курсор в соответствующий знак, если свойству **CanGoToMatch** объекта редактора присвоено значение **$true**, которое присваивается, когда курсор находится непосредственно перед открывающей круглой, квадратной или фигурной скобкой (т. е. \(,\[,{) или сразу после закрывающей круглой, квадратной или фигурной скобки (т. е. \),\],}).</span><span class="sxs-lookup"><span data-stu-id="65300-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="65300-128">Курсор помещается перед открывающим символом или после закрывающего символа.</span><span class="sxs-lookup"><span data-stu-id="65300-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="65300-129">Если свойство **CanGoToMatch** имеет значение **$false**, этот метод не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="65300-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### <a name="inserttext-text-"></a><span data-ttu-id="65300-130">InsertText\( text \)</span><span class="sxs-lookup"><span data-stu-id="65300-130">InsertText\( text \)</span></span>
  <span data-ttu-id="65300-131">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-132">Заменяет выделенную область текстом или вставляет текст в текущей позиции курсора.</span><span class="sxs-lookup"><span data-stu-id="65300-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

 <span data-ttu-id="65300-133">**text** — строка. Вставляемый текст.</span><span class="sxs-lookup"><span data-stu-id="65300-133">**text** - String The text to insert.</span></span>

 <span data-ttu-id="65300-134">См. [пример сценария](#-scripting-example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="65300-134">See the [Scripting Example](#-scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="65300-135">Select\( startLine, startColumn, endLine, endColumn \)</span><span class="sxs-lookup"><span data-stu-id="65300-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>
  <span data-ttu-id="65300-136">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-137">Выделяет текст в области, определяемой параметрами **startLine**, **startColumn**, **endLine** и **endColumn**.</span><span class="sxs-lookup"><span data-stu-id="65300-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

 <span data-ttu-id="65300-138">**startLine** — целое число. Строка, в которой начинается выделение.</span><span class="sxs-lookup"><span data-stu-id="65300-138">**startLine** - Integer The line where the selection starts.</span></span>

 <span data-ttu-id="65300-139">**startColumn** — целое число. Столбец в строке, в которой начинается выделение.</span><span class="sxs-lookup"><span data-stu-id="65300-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

 <span data-ttu-id="65300-140">**endLine** — целое число. Строка, в которой заканчивается выделение.</span><span class="sxs-lookup"><span data-stu-id="65300-140">**endLine** - Integer The line where the selection ends.</span></span>

 <span data-ttu-id="65300-141">**endColumn** — целое число. Столбец в строке, в которой заканчивается выделение.</span><span class="sxs-lookup"><span data-stu-id="65300-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

 <span data-ttu-id="65300-142">См. [пример сценария](#-scripting-example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="65300-142">See the  [Scripting Example](#-scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="65300-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="65300-143">SelectCaretLine\(\)</span></span>
  <span data-ttu-id="65300-144">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-145">Выделяет всю строку текста, в которой в данный момент находится курсор.</span><span class="sxs-lookup"><span data-stu-id="65300-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="65300-146">SetCaretPosition\( lineNumber, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="65300-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>
  <span data-ttu-id="65300-147">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-148">Задает положение курсора по номеру строки и номеру столбца.</span><span class="sxs-lookup"><span data-stu-id="65300-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="65300-149">Метод создает исключение, если номер строки или номер столбца курсора находятся вне соответствующих допустимых диапазонов.</span><span class="sxs-lookup"><span data-stu-id="65300-149">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

 <span data-ttu-id="65300-150">**lineNumber** — целое число. Номер строки курсора.</span><span class="sxs-lookup"><span data-stu-id="65300-150">**lineNumber** - Integer The caret line number.</span></span>

 <span data-ttu-id="65300-151">**columnNumber** — целое число. Номер столбца курсора.</span><span class="sxs-lookup"><span data-stu-id="65300-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="65300-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="65300-152">ToggleOutliningExpansion\(\)</span></span>
  <span data-ttu-id="65300-153">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="65300-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="65300-154">Выполняет свертывание или развертывание всех разделов структуры.</span><span class="sxs-lookup"><span data-stu-id="65300-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="65300-155">Свойства</span><span class="sxs-lookup"><span data-stu-id="65300-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="65300-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="65300-156">CanGoToMatch</span></span>
  <span data-ttu-id="65300-157">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="65300-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="65300-158">Логическое свойство, доступное только для чтения, которое указывает, находится ли курсор рядом с круглой, квадратной или фигурной скобкой (\(\), \[\] или {}).</span><span class="sxs-lookup"><span data-stu-id="65300-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="65300-159">Если курсор находится непосредственно перед открывающим символом или сразу после парного закрывающего символа, то это свойство имеет значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="65300-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="65300-160">В противном случае оно имеет значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="65300-160">Otherwise, it is **$false**.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="65300-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="65300-161">CaretColumn</span></span>
  <span data-ttu-id="65300-162">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-163">Свойство только для чтения, которое получает номер столбца, соответствующего позиции курсора.</span><span class="sxs-lookup"><span data-stu-id="65300-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="65300-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="65300-164">CaretLine</span></span>
  <span data-ttu-id="65300-165">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-166">Свойство только для чтения, которое получает номер строки, содержащей курсор.</span><span class="sxs-lookup"><span data-stu-id="65300-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="65300-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="65300-167">CaretLineText</span></span>
  <span data-ttu-id="65300-168">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-169">Свойство только для чтения, которое получает полную строку текста, содержащую курсор.</span><span class="sxs-lookup"><span data-stu-id="65300-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="65300-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="65300-170">LineCount</span></span>
  <span data-ttu-id="65300-171">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-172">Свойство только для чтения, которое получает число строк из редактора.</span><span class="sxs-lookup"><span data-stu-id="65300-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="65300-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="65300-173">SelectedText</span></span>
  <span data-ttu-id="65300-174">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-175">Свойство только для чтения, которое получает выделенный текст из редактора.</span><span class="sxs-lookup"><span data-stu-id="65300-175">The read-only property that gets the selected text from the editor.</span></span>

 <span data-ttu-id="65300-176">См. [пример сценария](#-scripting-example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="65300-176">See the  [Scripting Example](#-scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="65300-177">Текст</span><span class="sxs-lookup"><span data-stu-id="65300-177">Text</span></span>
  <span data-ttu-id="65300-178">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="65300-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="65300-179">Свойство для чтения и записи, которое получает или задает текст в редакторе.</span><span class="sxs-lookup"><span data-stu-id="65300-179">The read/write property that gets or sets the text in the editor.</span></span>

 <span data-ttu-id="65300-180">См. [пример сценария](#-scripting-example) далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="65300-180">See the [Scripting Example](#-scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="65300-181">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="65300-181">Scripting Example</span></span>

```powershell
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

## <a name="see-also"></a><span data-ttu-id="65300-182">См. также</span><span class="sxs-lookup"><span data-stu-id="65300-182">See Also</span></span>
- [<span data-ttu-id="65300-183">Объект ISEFile</span><span class="sxs-lookup"><span data-stu-id="65300-183">The ISEFile Object</span></span>](The-ISEFile-Object.md) 
- [<span data-ttu-id="65300-184">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="65300-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="65300-185">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="65300-185">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="65300-186">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="65300-186">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="65300-187">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="65300-187">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
