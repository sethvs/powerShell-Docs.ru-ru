---
title: "Объект ISEEditor"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0101daf8-4e31-4e4c-ab89-01d95dcb8f46
translationtype: Human Translation
ms.sourcegitcommit: fe3d7885b7c031a24a737f58523c8018cfc36146
ms.openlocfilehash: a735582afc1293108cfa16d4137648e0e65b564f

---

# Объект ISEEditor
  Объект **ISEEditor** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEEditor. Область консоли — это объект **ISEEditor**. Каждый объект [ISEFile](The-ISEFile-Object.md) имеет связанный объект **ISEEditor**. В следующих разделах перечислены методы и свойства объекта **ISEEditor**.

## Методы

### Очистить\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет текст в редакторе.

```PowerShell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### EnsureVisible\(int lineNumber\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Прокручивает редактор таким образом, чтобы отображалась строка, соответствующая значению параметра **lineNumber**. Метод создает исключение, если указанный номер строки находится за пределами диапазона 1, последнего номера строки, который определяет допустимые номера строк.

 **lineNumber**
. Номер строки, которая будет отображена.

```PowerShell
# Scrolls the text in the Script pane so that the fifth line is in view. 
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### Focus\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Помещает редактор в фокус.

```PowerShell
# Sets focus to the Console pane. 
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### GetLineLength\(int lineNumber \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Получает длину строки (в виде целого числа) по указанному номеру строки.

 **lineNumber**
. Номер строки, длину которой необходимо получить.

 **Возвращаемое значение**
. Длина строки с указанным номером.

```PowerShell
# Gets the length of the first line in the text of the Command pane. 
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### GoToMatch\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Перемещает курсор в соответствующий знак, если свойству **CanGoToMatch** объекта редактора присвоено значение **$true**, которое присваивается, когда курсор находится непосредственно перед открывающей круглой, квадратной или фигурной скобкой (т. е. \(,\[,{) или сразу после закрывающей круглой, квадратной или фигурной скобки (т. е. \),\],}).  Курсор помещается перед открывающим символом или после закрывающего символа. Если свойство **CanGoToMatch** имеет значение **$false**, этот метод не выполняет никаких действий. См. раздел [CanGoToMatch](#cangotomatch).

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace.
```

### InsertText\( text \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Заменяет выделенную область текстом или вставляет текст в текущей позиции курсора.

 **text** — строка. Вставляемый текст.

 См. [пример сценария](#example) далее в этом разделе.

### Select\( startLine, startColumn, endLine, endColumn \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выделяет текст в области, определяемой параметрами **startLine**, **startColumn**, **endLine** и **endColumn**.

 **startLine** — целое число. Строка, в которой начинается выделение.

 **startColumn** — целое число. Столбец в строке, в которой начинается выделение.

 **endLine** — целое число. Строка, в которой заканчивается выделение.

 **endColumn** — целое число. Столбец в строке, в которой заканчивается выделение.

 См. [пример сценария](#example) далее в этом разделе.

### SelectCaretLine\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выделяет всю строку текста, в которой в данный момент находится курсор.

```PowerShell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1) 
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### SetCaretPosition\( lineNumber, columnNumber \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Задает положение курсора по номеру строки и номеру столбца. Метод создает исключение, если номер строки или номер столбца курсора находятся вне соответствующих допустимых диапазонов.

 **lineNumber** — целое число. Номер строки курсора.

 **columnNumber** — целое число. Номер столбца курсора.

```PowerShell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### ToggleOutliningExpansion\(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Выполняет свертывание или развертывание всех разделов структуры.

```PowerShell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## Свойства

###  <a name="CanGoToMatch"></a> CanGoToMatch
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Логическое свойство, доступное только для чтения, которое указывает, находится ли курсор рядом с круглой, квадратной или фигурной скобкой (\(\), \[\], {}). Если курсор находится непосредственно перед открывающим символом или сразу после парного закрывающего символа, то это свойство имеет значение **$true**. В противном случае оно имеет значение **$false**.

```PowerShell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

###  <a name="CaretColumn"></a> CaretColumn
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает номер столбца, соответствующего позиции курсора.

```PowerShell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

###  <a name="CaretLine"></a> CaretLine
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает номер строки, содержащей курсор.

```PowerShell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

###  <a name="caretlinetext"></a> CaretLineText
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает полную строку текста, содержащую курсор.

```PowerShell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

###  <a name="LineCount"></a> LineCount
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает число строк из редактора.

```PowerShell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

###  <a name="SelectedText"></a> SelectedText
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает выделенный текст из редактора.

 См. [пример сценария](#example) далее в этом разделе.

###  <a name="Text"></a> Текст
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство для чтения и записи, которое получает или задает текст в редакторе.

 См. [пример сценария](#example) далее в этом разделе.

##  <a name="example"></a> Пример сценария

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

## См. также
 [Объект ISEFile](The-ISEFile-Object.md) 
 [Объект PowerShellTab](The-PowerShellTab-Object.md) 
 [Объектная модель интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  



<!--HONumber=Oct16_HO2-->


