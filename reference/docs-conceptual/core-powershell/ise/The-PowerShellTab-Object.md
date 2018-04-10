---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект PowerShellTab
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: c10f9106e31bb05828f1e76554ebe40ddb778340
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltab-object"></a>Объект PowerShellTab

Объект **PowerShellTab** представляет среду выполнения Windows PowerShell.

## <a name="methods"></a>Методы

### <a name="invoke-script-"></a>Invoke\( Script \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Выполняет заданный сценарий на вкладке PowerShell.

> [!NOTE]
> Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется. Он не возвращает объекты или значения. Если код изменяет какую-либо переменную, эти изменения сохраняются на вкладке, для которой была вызвана команда.

**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a>InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Выполняет заданный сценарий на вкладке PowerShell.

> [!NOTE]
> Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется. Выполняется блок сценария, и любое значение, возвращаемое при выполнении сценария, возвращается в среду выполнения, из которой вызывается команда. Если время выполнения команды превышает значение времени ожидания, заданное параметром **millesecondsTimeout**, команда завершается ошибкой с исключением "Время ожидания операции истекло".

**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.

**\[useNewScope\]** — необязательный логический параметр; значение по умолчанию — **$true**. Если задано значение **$true**, создается новая область для выполнения команды. Параметр не изменяет среду выполнения вкладки PowerShell, которая указана командой.

**\[millisecondsTimeout\]** — необязательный, целое число. Значение по умолчанию — **500**.
Если команда не завершается в течение указанного времени, то создается исключение **TimeoutException** с сообщением "Время ожидания операции истекло".

```powershell
# Create a new PowerShell tab and then switch back to the first
$psISE.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0])

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1', $false)
# You can switch to the other tab and type '$x' to see that the value is saved there.

# This example sets a value in the other tab (in a different scope)
# and returns it through the pipeline to this tab to store in $a
$a = $psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z')
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
Measure-Command {$psISE.PowerShellTabs[1].InvokeSynchronous('sleep 10', $false, 5000)}
```

## <a name="properties"></a>Свойства

### <a name="addonsmenu"></a>AddOnsMenu

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает меню надстроек для вкладки PowerShell.

```powershell
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

### <a name="caninvoke"></a>CanInvoke

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Логическое свойство только для чтения, которое возвращает значение **$true**, если сценарий может быть вызван с помощью метода [Invoke( Script )](#invoke-script-).

```powershell
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab.
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psISE.PowerShellTabs[1]
$secondTab.CanInvoke
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke
```

### <a name="consolepane"></a>Consolepane

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.  В Windows PowerShell ISE 2.0 это свойство называется **CommandPane**.

Свойство только для чтения, которое получает объект [editor](../ise/The-ISEEditor-Object.md) области консоли.

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a>DisplayName

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает или задает текст, выводимый на вкладке PowerShell. По умолчанию вкладкам назначаются имена "PowerShell #", где # — номер вкладки.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a>ExpandedScript

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Логическое свойство для чтения и записи, которое определяет, развернута или скрыта область сценариев.

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a>Файлы

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает [коллекцию файлов сценария](../ise/The-ISEFileCollection-Object.md), открытых на вкладке PowerShell.

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a>Выходные данные

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.  В более поздних версиях интегрированной среды сценариев Windows PowerShell для тех же целей можно использовать объект **ConsolePane**.

Свойство только для чтения, которое получает область вывода текущего [редактора](../ise/The-ISEEditor-Object.md).

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a>Prompt

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает текущий текст запроса. Примечание. Функция **Prompt** может быть переопределена профилем пользователя. Если результат отличается от простой строки, это свойство не возвращает никаких данных.

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a>ShowCommands

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Свойство для чтения и записи, которое указывает, отображается ли панель команд.

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a>StatusText

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает текст состояния вкладки **PowerShellTab**.

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a>HorizontalAddOnToolsPaneOpened

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Свойство только для чтения, которое указывает, открыта ли горизонтальная область инструментов надстроек.

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a>VerticalAddOnToolsPaneOpened

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Свойство только для чтения, которое указывает, открыта ли вертикальная область инструментов надстроек.

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a>См. также

- [Объект PowerShellTabCollection](The-PowerShellTabCollection-Object.md)
- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)