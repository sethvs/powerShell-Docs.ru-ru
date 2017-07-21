---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект PowerShellTab"
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: d4e9374202d352a30b3eb46bcf1e4e40dea49822
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="1d2a1-103">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="1d2a1-103">The PowerShellTab Object</span></span>
  <span data-ttu-id="1d2a1-104">Объект **PowerShellTab** представляет среду выполнения Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="1d2a1-105">Методы</span><span class="sxs-lookup"><span data-stu-id="1d2a1-105">Methods</span></span>

###  <span data-ttu-id="1d2a1-106"><a name="invoke"></a> Invoke\( Script \)</span><span class="sxs-lookup"><span data-stu-id="1d2a1-106"><a name="invoke"></a> Invoke\( Script \)</span></span>
  <span data-ttu-id="1d2a1-107">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-108">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
>  <span data-ttu-id="1d2a1-109">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="1d2a1-110">Он не возвращает объекты или значения.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-110">It does not return any object or value.</span></span> <span data-ttu-id="1d2a1-111">Если код изменяет какую-либо переменную, эти изменения сохраняются на вкладке, для которой была вызвана команда.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

 <span data-ttu-id="1d2a1-112">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psise.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="1d2a1-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="1d2a1-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>
  <span data-ttu-id="1d2a1-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="1d2a1-115">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
>  <span data-ttu-id="1d2a1-116">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="1d2a1-117">Выполняется блок сценария, и любое значение, возвращаемое при выполнении сценария, возвращается в среду выполнения, из которой вызывается команда.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="1d2a1-118">Если время выполнения команды превышает значение времени ожидания, заданное параметром **millesecondsTimeout**, команда завершается ошибкой с исключением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="1d2a1-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

 <span data-ttu-id="1d2a1-119">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

 <span data-ttu-id="1d2a1-120">**\[useNewScope\]** — необязательный логический параметр; значение по умолчанию — **$true**
. Если задано значение **$true**, создается новая область для выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true**
 If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="1d2a1-121">Параметр не изменяет среду выполнения вкладки PowerShell, которая указана командой.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

 <span data-ttu-id="1d2a1-122">**\[millisecondsTimeout\]** — необязательный, целое число. Значение по умолчанию — **500**.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="1d2a1-123">Если команда не завершается в течение указанного времени, то создается исключение **TimeoutException** с сообщением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="1d2a1-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

```
# create a new PowerShell tab and then switch back to the first
$PSise.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0]) 

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1',$false)
# You can switch to the other tab and type “$x” to see that the value is saved there.

# This example sets a value in the other tab (in a different scope) 
# and returns it through the pipeline to this tab to store in $a
$a=$psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z') 
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
measure-command {$psISE.PowerShellTabs[1].InvokeSynchronous("sleep 10",$false,5000)}

```

## <a name="properties"></a><span data-ttu-id="1d2a1-124">Свойства</span><span class="sxs-lookup"><span data-stu-id="1d2a1-124">Properties</span></span>

###  <span data-ttu-id="1d2a1-125"><a name="AddOnsMenu"></a> AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="1d2a1-125"><a name="AddOnsMenu"></a> AddOnsMenu</span></span>
  <span data-ttu-id="1d2a1-126">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-127">Свойство только для чтения, которое получает меню надстроек для вкладки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

```
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

###  <span data-ttu-id="1d2a1-128"><a name="CanExecute"></a> CanInvoke</span><span class="sxs-lookup"><span data-stu-id="1d2a1-128"><a name="CanExecute"></a> CanInvoke</span></span>
  <span data-ttu-id="1d2a1-129">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-130">Логическое свойство только для чтения, которое возвращает значение **$true**, если сценарий может быть вызван с помощью метода [Invoke( Script )](#invoke).</span><span class="sxs-lookup"><span data-stu-id="1d2a1-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke) method.</span></span>

```
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab. 
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psise.PowerShellTabs[1] 
$secondTab.CanInvoke 
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke

```

###  <span data-ttu-id="1d2a1-131"><a name="Commandpane"></a> Consolepane</span><span class="sxs-lookup"><span data-stu-id="1d2a1-131"><a name="Commandpane"></a> Consolepane</span></span>
  <span data-ttu-id="1d2a1-132">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="1d2a1-133">В Windows PowerShell ISE 2.0 это свойство называется **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

 <span data-ttu-id="1d2a1-134">Свойство только для чтения, которое получает объект [editor](../ise/The-ISEEditor-Object.md) области консоли.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane

```

###  <span data-ttu-id="1d2a1-135"><a name="Displayname"></a> DisplayName</span><span class="sxs-lookup"><span data-stu-id="1d2a1-135"><a name="Displayname"></a> DisplayName</span></span>
  <span data-ttu-id="1d2a1-136">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-137">Свойство только для чтения, которое получает или задает текст, выводимый на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab.</span></span> <span data-ttu-id="1d2a1-138">По умолчанию вкладкам назначаются имена "PowerShell #", где # — номер вкладки.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-138">By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```
$newTab = $psise.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

###  <span data-ttu-id="1d2a1-139"><a name="ExpandedScript"></a> ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="1d2a1-139"><a name="ExpandedScript"></a> ExpandedScript</span></span>
  <span data-ttu-id="1d2a1-140">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-141">Логическое свойство для чтения и записи, которое определяет, развернута или скрыта область сценариев.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-141">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```
# Toggle the expanded script property to see its effect.
$PSise.CurrentPowerShellTab.ExpandedScript=!$PSise.CurrentPowerShellTab.ExpandedScript

```

###  <span data-ttu-id="1d2a1-142"><a name="Files"></a> Files</span><span class="sxs-lookup"><span data-stu-id="1d2a1-142"><a name="Files"></a> Files</span></span>
  <span data-ttu-id="1d2a1-143">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-144">Свойство только для чтения, которое получает [коллекцию файлов сценария](../ise/The-ISEFileCollection-Object.md), открытых на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-144">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb" 
# Gets the line count
$newFile.Editor.LineCount
```

###  <span data-ttu-id="1d2a1-145"><a name="Output"></a> Output</span><span class="sxs-lookup"><span data-stu-id="1d2a1-145"><a name="Output"></a> Output</span></span>
  <span data-ttu-id="1d2a1-146">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-146">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="1d2a1-147">В более поздних версиях интегрированной среды сценариев Windows PowerShell для тех же целей можно использовать объект **ConsolePane**.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-147">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

 <span data-ttu-id="1d2a1-148">Свойство только для чтения, которое получает область вывода текущего [редактора](../ise/The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="1d2a1-148">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```
# Clears the text in the Output pane.
$psise.CurrentPowerShellTab.output.clear()
```

###  <span data-ttu-id="1d2a1-149"><a name="Prompt"></a> Prompt</span><span class="sxs-lookup"><span data-stu-id="1d2a1-149"><a name="Prompt"></a> Prompt</span></span>
  <span data-ttu-id="1d2a1-150">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-150">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-151">Свойство только для чтения, которое получает текущий текст запроса.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-151">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="1d2a1-152">Примечание. Функция **Prompt** может быть переопределена профилем пользователя.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-152">Note: the **Prompt** function can be overridden by the user’s profile.</span></span> <span data-ttu-id="1d2a1-153">Если результат отличается от простой строки, это свойство не возвращает никаких данных.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-153">If the result is other than a simple string, then this property returns nothing.</span></span>

```
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

###  <span data-ttu-id="1d2a1-154"><a name="ShowCommands"></a> ShowCommands</span><span class="sxs-lookup"><span data-stu-id="1d2a1-154"><a name="ShowCommands"></a> ShowCommands</span></span>
  <span data-ttu-id="1d2a1-155">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-155">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="1d2a1-156">Свойство для чтения и записи, которое указывает, отображается ли панель команд.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-156">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $True
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands=$True}
```

###  <span data-ttu-id="1d2a1-157"><a name="StatusText"></a> StatusText</span><span class="sxs-lookup"><span data-stu-id="1d2a1-157"><a name="StatusText"></a> StatusText</span></span>
  <span data-ttu-id="1d2a1-158">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1d2a1-159">Свойство только для чтения, которое получает текст состояния вкладки **PowerShellTab**.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-159">The read-only property that gets the **PowerShellTab** status text.</span></span>

```
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

###  <span data-ttu-id="1d2a1-160"><a name="HorizontalAddOnToolsPaneOpened"></a> HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="1d2a1-160"><a name="HorizontalAddOnToolsPaneOpened"></a> HorizontalAddOnToolsPaneOpened</span></span>
  <span data-ttu-id="1d2a1-161">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-161">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="1d2a1-162">Свойство только для чтения, которое указывает, открыта ли горизонтальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-162">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```
# Gets the current state of the horizontal Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

###  <span data-ttu-id="1d2a1-163"><a name="VerticalAddOnToolsPaneOpened"></a> **VerticalAddOnToolsPaneOpened**</span><span class="sxs-lookup"><span data-stu-id="1d2a1-163"><a name="VerticalAddOnToolsPaneOpened"></a> **VerticalAddOnToolsPaneOpened**</span></span>
  <span data-ttu-id="1d2a1-164">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-164">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="1d2a1-165">Свойство только для чтения, которое указывает, открыта ли вертикальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="1d2a1-165">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands=$True
# Gets the current state of the vertical Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="1d2a1-166">См. также</span><span class="sxs-lookup"><span data-stu-id="1d2a1-166">See Also</span></span>
- [<span data-ttu-id="1d2a1-167">Объект PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="1d2a1-167">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md) 
- [<span data-ttu-id="1d2a1-168">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d2a1-168">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="1d2a1-169">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d2a1-169">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="1d2a1-170">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="1d2a1-170">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  
