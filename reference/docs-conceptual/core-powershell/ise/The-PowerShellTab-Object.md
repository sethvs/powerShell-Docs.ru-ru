---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект PowerShellTab"
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: 15d9a7474e4c2cf2a9ff8edb88802106489cdba1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="2189e-103">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="2189e-103">The PowerShellTab Object</span></span>
  <span data-ttu-id="2189e-104">Объект **PowerShellTab** представляет среду выполнения Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2189e-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="2189e-105">Методы</span><span class="sxs-lookup"><span data-stu-id="2189e-105">Methods</span></span>

### <a name="invoke-script-"></a><span data-ttu-id="2189e-106">Invoke\( Script \)</span><span class="sxs-lookup"><span data-stu-id="2189e-106">Invoke\( Script \)</span></span>
  <span data-ttu-id="2189e-107">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-108">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2189e-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="2189e-109">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="2189e-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="2189e-110">Он не возвращает объекты или значения.</span><span class="sxs-lookup"><span data-stu-id="2189e-110">It does not return any object or value.</span></span> <span data-ttu-id="2189e-111">Если код изменяет какую-либо переменную, эти изменения сохраняются на вкладке, для которой была вызвана команда.</span><span class="sxs-lookup"><span data-stu-id="2189e-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

 <span data-ttu-id="2189e-112">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="2189e-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psise.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="2189e-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="2189e-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>
  <span data-ttu-id="2189e-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="2189e-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="2189e-115">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2189e-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="2189e-116">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="2189e-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="2189e-117">Выполняется блок сценария, и любое значение, возвращаемое при выполнении сценария, возвращается в среду выполнения, из которой вызывается команда.</span><span class="sxs-lookup"><span data-stu-id="2189e-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="2189e-118">Если время выполнения команды превышает значение времени ожидания, заданное параметром **millesecondsTimeout**, команда завершается ошибкой с исключением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="2189e-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

 <span data-ttu-id="2189e-119">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="2189e-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

 <span data-ttu-id="2189e-120">**\[useNewScope\]** — необязательный логический параметр; значение по умолчанию — **$true**. Если задано значение **$true**, создается новая область для выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="2189e-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true** If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="2189e-121">Параметр не изменяет среду выполнения вкладки PowerShell, которая указана командой.</span><span class="sxs-lookup"><span data-stu-id="2189e-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

 <span data-ttu-id="2189e-122">**\[millisecondsTimeout\]** — необязательный, целое число. Значение по умолчанию — **500**.</span><span class="sxs-lookup"><span data-stu-id="2189e-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="2189e-123">Если команда не завершается в течение указанного времени, то создается исключение **TimeoutException** с сообщением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="2189e-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

```
# create a new PowerShell tab and then switch back to the first
$PSise.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0]) 

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1',$false)
# You can switch to the other tab and type 'œ$x' to see that the value is saved there.

# This example sets a value in the other tab (in a different scope) 
# and returns it through the pipeline to this tab to store in $a
$a=$psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z') 
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
measure-command {$psISE.PowerShellTabs[1].InvokeSynchronous("sleep 10",$false,5000)}

```

## <a name="properties"></a><span data-ttu-id="2189e-124">Свойства</span><span class="sxs-lookup"><span data-stu-id="2189e-124">Properties</span></span>

### <a name="addonsmenu"></a><span data-ttu-id="2189e-125">AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="2189e-125">AddOnsMenu</span></span>
  <span data-ttu-id="2189e-126">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-127">Свойство только для чтения, которое получает меню надстроек для вкладки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2189e-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

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

### <a name="caninvoke"></a><span data-ttu-id="2189e-128">CanInvoke</span><span class="sxs-lookup"><span data-stu-id="2189e-128">CanInvoke</span></span>
  <span data-ttu-id="2189e-129">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-130">Логическое свойство только для чтения, которое возвращает значение **$true**, если сценарий может быть вызван с помощью метода [Invoke( Script )](#invoke-script-).</span><span class="sxs-lookup"><span data-stu-id="2189e-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke-script-) method.</span></span>

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

### <a name="consolepane"></a><span data-ttu-id="2189e-131">Consolepane</span><span class="sxs-lookup"><span data-stu-id="2189e-131">Consolepane</span></span>
  <span data-ttu-id="2189e-132">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="2189e-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="2189e-133">В Windows PowerShell ISE 2.0 это свойство называется **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="2189e-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

 <span data-ttu-id="2189e-134">Свойство только для чтения, которое получает объект [editor](../ise/The-ISEEditor-Object.md) области консоли.</span><span class="sxs-lookup"><span data-stu-id="2189e-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane

```

### <a name="displayname"></a><span data-ttu-id="2189e-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="2189e-135">DisplayName</span></span>
  <span data-ttu-id="2189e-136">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-137">Свойство только для чтения, которое получает или задает текст, выводимый на вкладке PowerShell. По умолчанию вкладкам назначаются имена "PowerShell #", где # — номер вкладки.</span><span class="sxs-lookup"><span data-stu-id="2189e-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab. By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```
$newTab = $psise.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="expandedscript"></a><span data-ttu-id="2189e-138">ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="2189e-138">ExpandedScript</span></span>
  <span data-ttu-id="2189e-139">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-139">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-140">Логическое свойство для чтения и записи, которое определяет, развернута или скрыта область сценариев.</span><span class="sxs-lookup"><span data-stu-id="2189e-140">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```
# Toggle the expanded script property to see its effect.
$PSise.CurrentPowerShellTab.ExpandedScript=!$PSise.CurrentPowerShellTab.ExpandedScript

```

### <a name="files"></a><span data-ttu-id="2189e-141">Файлы</span><span class="sxs-lookup"><span data-stu-id="2189e-141">Files</span></span>
  <span data-ttu-id="2189e-142">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-142">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-143">Свойство только для чтения, которое получает [коллекцию файлов сценария](../ise/The-ISEFileCollection-Object.md), открытых на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2189e-143">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb" 
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a><span data-ttu-id="2189e-144">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="2189e-144">Output</span></span>
  <span data-ttu-id="2189e-145">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="2189e-145">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="2189e-146">В более поздних версиях интегрированной среды сценариев Windows PowerShell для тех же целей можно использовать объект **ConsolePane**.</span><span class="sxs-lookup"><span data-stu-id="2189e-146">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

 <span data-ttu-id="2189e-147">Свойство только для чтения, которое получает область вывода текущего [редактора](../ise/The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="2189e-147">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```
# Clears the text in the Output pane.
$psise.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a><span data-ttu-id="2189e-148">Prompt</span><span class="sxs-lookup"><span data-stu-id="2189e-148">Prompt</span></span>
  <span data-ttu-id="2189e-149">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-149">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-150">Свойство только для чтения, которое получает текущий текст запроса.</span><span class="sxs-lookup"><span data-stu-id="2189e-150">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="2189e-151">Примечание. Функция **Prompt** может быть переопределена профилем пользователя.</span><span class="sxs-lookup"><span data-stu-id="2189e-151">Note: the **Prompt** function can be overridden by the user'™s profile.</span></span> <span data-ttu-id="2189e-152">Если результат отличается от простой строки, это свойство не возвращает никаких данных.</span><span class="sxs-lookup"><span data-stu-id="2189e-152">If the result is other than a simple string, then this property returns nothing.</span></span>

```
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a><span data-ttu-id="2189e-153">ShowCommands</span><span class="sxs-lookup"><span data-stu-id="2189e-153">ShowCommands</span></span>
  <span data-ttu-id="2189e-154">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="2189e-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="2189e-155">Свойство для чтения и записи, которое указывает, отображается ли панель команд.</span><span class="sxs-lookup"><span data-stu-id="2189e-155">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $True
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands=$True}
```

### <a name="statustext"></a><span data-ttu-id="2189e-156">StatusText</span><span class="sxs-lookup"><span data-stu-id="2189e-156">StatusText</span></span>
  <span data-ttu-id="2189e-157">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="2189e-157">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2189e-158">Свойство только для чтения, которое получает текст состояния вкладки **PowerShellTab**.</span><span class="sxs-lookup"><span data-stu-id="2189e-158">The read-only property that gets the **PowerShellTab** status text.</span></span>

```
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a><span data-ttu-id="2189e-159">HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="2189e-159">HorizontalAddOnToolsPaneOpened</span></span>
  <span data-ttu-id="2189e-160">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="2189e-160">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="2189e-161">Свойство только для чтения, которое указывает, открыта ли горизонтальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="2189e-161">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```
# Gets the current state of the horizontal Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a><span data-ttu-id="2189e-162">VerticalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="2189e-162">VerticalAddOnToolsPaneOpened</span></span>
  <span data-ttu-id="2189e-163">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="2189e-163">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="2189e-164">Свойство только для чтения, которое указывает, открыта ли вертикальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="2189e-164">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands=$True
# Gets the current state of the vertical Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="2189e-165">См. также</span><span class="sxs-lookup"><span data-stu-id="2189e-165">See Also</span></span>
- [<span data-ttu-id="2189e-166">Объект PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="2189e-166">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md) 
- [<span data-ttu-id="2189e-167">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2189e-167">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="2189e-168">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2189e-168">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="2189e-169">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="2189e-169">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  
