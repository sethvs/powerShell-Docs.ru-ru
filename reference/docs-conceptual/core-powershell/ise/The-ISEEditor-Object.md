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
# <a name="the-iseeditor-object"></a>Объект ISEEditor
  Объект **ISEEditor** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEEditor. Область консоли — это объект **ISEEditor**. Каждый объект [ISEFile](The-ISEFile-Object.md) имеет связанный объект **ISEEditor**. В следующих разделах перечислены методы и свойства объекта **ISEEditor**.

## <a name="methods"></a>Методы

### <a name="clear"></a>Clear\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет текст в редакторе.

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a>EnsureVisible\(int lineNumber\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Прокручивает редактор таким образом, чтобы отображалась строка, соответствующая значению параметра **lineNumber**. Метод создает исключение, если указанный номер строки находится за пределами диапазона 1, последнего номера строки, который определяет допустимые номера строк.

 **lineNumber** — номер строки, которая будет отображена.

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a>Focus\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Помещает редактор в фокус.

```powershell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a>GetLineLength\(int lineNumber \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Получает длину строки (в виде целого числа) по указанному номеру строки.

 **lineNumber** — номер строки, длину которой необходимо получить.

 **Возвращаемое значение** — длина строки с указанным номером.

```powershell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a>GoToMatch\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Перемещает курсор в соответствующий знак, если свойству **CanGoToMatch** объекта редактора присвоено значение **$true**, которое присваивается, когда курсор находится непосредственно перед открывающей круглой, квадратной или фигурной скобкой (т. е. \(,\[,{) или сразу после закрывающей круглой, квадратной или фигурной скобки (т. е. \),\],}).  Курсор помещается перед открывающим символом или после закрывающего символа. Если свойство **CanGoToMatch** имеет значение **$false**, этот метод не выполняет никаких действий.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### <a name="inserttext-text-"></a>InsertText\( text \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Заменяет выделенную область текстом или вставляет текст в текущей позиции курсора.

 **text** — строка. Вставляемый текст.

 См. [пример сценария](#-scripting-example) далее в этом разделе.

### <a name="select-startline-startcolumn-endline-endcolumn-"></a>Select\( startLine, startColumn, endLine, endColumn \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выделяет текст в области, определяемой параметрами **startLine**, **startColumn**, **endLine** и **endColumn**.

 **startLine** — целое число. Строка, в которой начинается выделение.

 **startColumn** — целое число. Столбец в строке, в которой начинается выделение.

 **endLine** — целое число. Строка, в которой заканчивается выделение.

 **endColumn** — целое число. Столбец в строке, в которой заканчивается выделение.

 См. [пример сценария](#-scripting-example) далее в этом разделе.

### <a name="selectcaretline"></a>SelectCaretLine\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выделяет всю строку текста, в которой в данный момент находится курсор.

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a>SetCaretPosition\( lineNumber, columnNumber \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Задает положение курсора по номеру строки и номеру столбца. Метод создает исключение, если номер строки или номер столбца курсора находятся вне соответствующих допустимых диапазонов.

 **lineNumber** — целое число. Номер строки курсора.

 **columnNumber** — целое число. Номер столбца курсора.

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a>ToggleOutliningExpansion\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Выполняет свертывание или развертывание всех разделов структуры.

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a>Свойства

### <a name="cangotomatch"></a>CanGoToMatch
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Логическое свойство, доступное только для чтения, которое указывает, находится ли курсор рядом с круглой, квадратной или фигурной скобкой (\(\), \[\] или {}). Если курсор находится непосредственно перед открывающим символом или сразу после парного закрывающего символа, то это свойство имеет значение **$true**. В противном случае оно имеет значение **$false**.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a>CaretColumn
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает номер столбца, соответствующего позиции курсора.

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a>CaretLine
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает номер строки, содержащей курсор.

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a>CaretLineText
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает полную строку текста, содержащую курсор.

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a>LineCount
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает число строк из редактора.

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a>SelectedText
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает выделенный текст из редактора.

 См. [пример сценария](#-scripting-example) далее в этом разделе.

### <a name="text"></a>Текст
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство для чтения и записи, которое получает или задает текст в редакторе.

 См. [пример сценария](#-scripting-example) далее в этом разделе.

## <a name="scripting-example"></a>Пример сценария

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

## <a name="see-also"></a>См. также
- [Объект ISEFile](The-ISEFile-Object.md) 
- [Объект PowerShellTab](The-PowerShellTab-Object.md) 
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)

  
