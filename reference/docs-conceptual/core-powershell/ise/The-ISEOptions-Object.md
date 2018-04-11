---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект ISEOptions
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: e756da21aaa5465f7fa6a90563b4180f0c89e87b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-iseoptions-object"></a>Объект ISEOptions

Объект **ISEOptions** представляет различные параметры для интегрированной среды сценариев Windows PowerShell. Он является экземпляром класса **Microsoft.PowerShell.Host.ISE.ISEOptions**.

Объект **ISEOptions** предоставляет следующие методы и свойства.

## <a name="methods"></a>Методы

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors \(\)

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Восстанавливает значения по умолчанию для цветов маркеров в области консоли.

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults \(\)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Восстанавливает значения по умолчанию для всех параметров в области консоли. Кроме того, сбрасывает поведение различных предупреждений, включающих стандартный флажок, который отключает повторный вывод сообщения.

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors \(\)

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Восстанавливает значения по умолчанию для цветов маркеров в области сценариев.

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors \(\)

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Восстанавливает значения по умолчанию для цветов маркеров XML-элементов, отображаемых в интегрированной среде сценариев Windows PowerShell. См. также [XmlTokenColors](#xmltokencolors).

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Свойства

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает интервал (в минутах) между операциями автоматического сохранения файлов интегрированной средой сценариев Windows PowerShell. Значение по умолчанию — 2 минуты. Значение представлено целым числом.

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.  Сведения для более поздних версий см. в разделе [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Задает цвет фона для области команд. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a>CommandPaneUp

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.

Указывает, находится ли область команд над областью вывода.

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает цвет фона для области консоли. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает цвет переднего плана для текста в области консоли.

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает цвет фона для текста в области консоли.

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a>ConsoleTokenColors

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает цвета маркеров IntelliSense в области консоли интегрированной среды сценариев Windows PowerShell. Это свойство является объектом словаря, который содержит пары "имя — значение" для типов и цветов маркеров для области консоли. Сведения об изменении цвета маркеров IntelliSense в области сценариев см. в разделе [TokenColors](#tokencolors). Сведения о восстановлении значений по умолчанию для цветов см. в разделе [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors). Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет фона для сообщений отладки, отображаемых в области консоли. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет переднего плана для сообщений отладки, отображаемых в области консоли. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a>DefaultOptions

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Коллекция свойств, задающих значения по умолчанию, используемые при выполнении методов сброса (Reset).

```powershell
# Displays the name of the default options. This example is from ISE 4.0.
$psISE.Options.DefaultOptions

SelectedScriptPaneState                   : Top
ShowDefaultSnippets                       : True
ShowToolBar                               : True
ShowOutlining                             : True
ShowLineNumbers                           : True
TokenColors                               : {[Attribute, #FF00BFFF], [Command, #FF0000FF], [CommandArgument, #FF8A2BE2], [CommandParameter, #FF000080]...}
ConsoleTokenColors                        : {[Attribute, #FFB0C4DE], [Command, #FFE0FFFF], [CommandArgument, #FFEE82EE], [CommandParameter, #FFFFE4B5]...}
XmlTokenColors                            : {[Comment, #FF006400], [CommentDelimiter, #FF008000], [ElementName, #FF8B0000], [MarkupExtension, #FFFF8C00]...}
DefaultOptions                            : Microsoft.PowerShell.Host.ISE.ISEOptions
FontSize                                  : 9
Zoom                                      : 100
FontName                                  : Lucida Console
ErrorForegroundColor                      : #FFFF0000
ErrorBackgroundColor                      : #00FFFFFF
WarningForegroundColor                    : #FFFF8C00
WarningBackgroundColor                    : #00FFFFFF
VerboseForegroundColor                    : #FF00FFFF
VerboseBackgroundColor                    : #00FFFFFF
DebugForegroundColor                      : #FF00FFFF
DebugBackgroundColor                      : #00FFFFFF
ConsolePaneBackgroundColor                : #FF012456
ConsolePaneTextBackgroundColor            : #FF012456
ConsolePaneForegroundColor                : #FFF5F5F5
ScriptPaneBackgroundColor                 : #FFFFFFFF
ScriptPaneForegroundColor                 : #FF000000
ShowWarningForDuplicateFiles              : True
ShowWarningBeforeSavingOnRun              : True
UseLocalHelp                              : True
AutoSaveMinuteInterval                    : 2
MruCount                                  : 10
ShowIntellisenseInConsolePane             : True
ShowIntellisenseInScriptPane              : True
UseEnterToSelectInConsolePaneIntellisense : True
UseEnterToSelectInScriptPaneIntellisense  : True
IntellisenseTimeoutInSeconds              : 3
```

### <a name="errorbackgroundcolor"></a>ErrorBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет фона для сообщений об ошибках, отображаемых в области консоли. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет переднего плана для сообщений об ошибках, отображаемых в области консоли. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a>FontName

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает название текущего шрифта в области сценариев и в области консоли.

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a>FontSize

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Указывает размер шрифта в виде целого числа. Используется в области сценариев, области команд и области вывода. Допустимый диапазон значений — от 8 до 32.

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает интервал (в секундах), в течение которого IntelliSense пытается разрешить текущий вводимый текст. По завершении указанного интервала время ожидания IntelliSense истекает, и компонент позволяет продолжить ввод текста. Значение по умолчанию — 3 секунды. Значение представлено целым числом.

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Задает число недавно открывавшихся файлов, которые интегрированная среда сценариев Windows PowerShell отслеживает и отображает в нижней части меню **Открытие файла**. Значение по умолчанию — 10. Значение представлено целым числом.

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.  Сведения для более поздних версий см. в разделе [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Свойство для чтения и записи, которое получает или задает цвет фона самой области вывода. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.  Сведения для более поздних версий см. в разделе [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

Свойство для чтения и записи, которое изменяет цвет переднего плана текста в области вывода в интегрированной среде сценариев Windows PowerShell 2.0.

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor

Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.  Сведения для более поздних версий см. в разделе [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

Свойство для чтения и записи, которое изменяет цвет фона текста в области вывода.

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство для чтения и записи, которое получает или задает цвет фона для файлов. Это экземпляр класса **System.Windows.Media.Color**.

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство для чтения и записи, которое получает или задает цвет переднего плана для файлов, не являющихся сценариями, в области сценариев.
Чтобы задать цвет переднего плана для файлов сценариев, используйте [TokenColors](#tokencolors).

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство для чтения и записи, которое получает или задает положение области сценариев на экране. Строка может иметь значение Maximized, Top или Right.

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, содержит ли список фрагментов **CTRL+J** начальный набор, который включен в Windows PowerShell. Если задано значение **$false**, в списке **CTRL+J** отображаются только определенные пользователем фрагменты. По умолчанию используется значение **$true**.

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, предлагает ли IntelliSense синтаксис, параметры и значения в области консоли. По умолчанию используется значение **$true**.

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, предлагает ли IntelliSense синтаксис, параметры и значения в области сценариев. По умолчанию используется значение **$true**.

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>ShowLineNumbers

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, отображаются ли в левом поле области сценариев номера строк. По умолчанию используется значение **$true**.

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, отображаются ли в области сценариев расширяемые и свертываемые скобки рядом с фрагментами кода в левом поле. Когда они отображаются, можно щелкнуть значок "минус" \(-\) рядом с блоком текста, чтобы свернуть, или значок "плюс" \(+\), чтобы развернуть блок текста. По умолчанию используется значение **$true**.

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>ShowToolBar

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Указывает, отображается ли в верхней части окна интегрированной среды сценариев Windows PowerShell панель инструментов ISE. По умолчанию используется значение **$true**.

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Указывает, отображается ли предупреждение, когда сценарий сохраняется автоматически перед запуском. По умолчанию используется значение **$true**.

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Указывает, отображается ли предупреждение при открытии одного и того же файла на разных вкладках PowerShell. Если задано значение **$true**, при открытии одного файла на нескольких вкладках отображается сообщение: "Копия данного файла открыта на другой вкладке Windows PowerShell. Изменения, внесенные в данный файл, отразятся на всех его открытых копиях". По умолчанию используется значение **$true**.

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a>TokenColors

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвета маркеров IntelliSense в области сценариев интегрированной среды сценариев Windows PowerShell. Это свойство является объектом словаря, который содержит пары "имя — значение" для типов и цветов маркеров для области сценариев. Сведения об изменении цветов маркеров IntelliSense в области консоли см. в разделе [ConsoleTokenColors](#consoletokencolors). Сведения о восстановлении значений по умолчанию для цветов см. в разделе [RestoreDefaultTokenColors](#restoredefaulttokencolors). Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, можно ли использовать клавишу ВВОД для выбора варианта, предложенного IntelliSense, в области консоли. По умолчанию используется значение **$true**.

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, можно ли использовать клавишу ВВОД для выбора варианта, предложенного IntelliSense, в области сценариев. По умолчанию используется значение **$true**.

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a>UseLocalHelp

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает, выводится ли на экран локальная справка или справка библиотеки TechNet в Интернете при нажатии клавиши F1, когда курсор находится в ключевом слове. Если задано значение **$true**, во всплывающем окне отображается содержимое локальной справки. Можно установить файлы справки, выполнив команду `Update-Help`. Если задано значение **$false**, в браузере открывается страница библиотеки TechNet.

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет фона для подробных сообщений, отображаемых в области консоли. Это объект **System.Windows.Media.Color**.

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет переднего плана для подробных сообщений, отображаемых в области консоли. Это объект **System.Windows.Media.Color**.

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет фона для текста предупреждений, отображаемых в области консоли. Это объект **System.Windows.Media.Color**.

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Задает цвет переднего плана для текста предупреждений, отображаемых в области вывода. Это объект **System.Windows.Media.Color**.

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает объект словаря, который содержит пары "имя — значение" для типов и цветов маркеров для XML-содержимого, которое отображается в интегрированной среде сценариев Windows PowerShell. Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable. См. также [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a>Масштабирование

Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.

Указывает относительный размер текста в области консоли и сценариев. Значение по умолчанию — 100. Чем больше это значение, тем больше размер отображаемого текста в интегрированной среде сценариев Windows PowerShell. Значение представлено целым числом в диапазоне от 20 до 400.

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>См. также

- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)