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
# <a name="the-powershelltab-object"></a><span data-ttu-id="7cf73-103">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="7cf73-103">The PowerShellTab Object</span></span>

<span data-ttu-id="7cf73-104">Объект **PowerShellTab** представляет среду выполнения Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cf73-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="7cf73-105">Методы</span><span class="sxs-lookup"><span data-stu-id="7cf73-105">Methods</span></span>

### <a name="invoke-script-"></a><span data-ttu-id="7cf73-106">Invoke\( Script \)</span><span class="sxs-lookup"><span data-stu-id="7cf73-106">Invoke\( Script \)</span></span>

<span data-ttu-id="7cf73-107">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-108">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cf73-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf73-109">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="7cf73-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="7cf73-110">Он не возвращает объекты или значения.</span><span class="sxs-lookup"><span data-stu-id="7cf73-110">It does not return any object or value.</span></span> <span data-ttu-id="7cf73-111">Если код изменяет какую-либо переменную, эти изменения сохраняются на вкладке, для которой была вызвана команда.</span><span class="sxs-lookup"><span data-stu-id="7cf73-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

<span data-ttu-id="7cf73-112">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="7cf73-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="7cf73-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="7cf73-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>

<span data-ttu-id="7cf73-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="7cf73-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7cf73-115">Выполняет заданный сценарий на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cf73-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="7cf73-116">Этот метод работает только для других вкладок PowerShell, но не для вкладки PowerShell, с которой он выполняется.</span><span class="sxs-lookup"><span data-stu-id="7cf73-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="7cf73-117">Выполняется блок сценария, и любое значение, возвращаемое при выполнении сценария, возвращается в среду выполнения, из которой вызывается команда.</span><span class="sxs-lookup"><span data-stu-id="7cf73-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="7cf73-118">Если время выполнения команды превышает значение времени ожидания, заданное параметром **millesecondsTimeout**, команда завершается ошибкой с исключением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="7cf73-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

<span data-ttu-id="7cf73-119">**Script** — System.Management.Automation.ScriptBlock или строка. Блок сценария для запуска.</span><span class="sxs-lookup"><span data-stu-id="7cf73-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

<span data-ttu-id="7cf73-120">**\[useNewScope\]** — необязательный логический параметр; значение по умолчанию — **$true**. Если задано значение **$true**, создается новая область для выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="7cf73-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true** If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="7cf73-121">Параметр не изменяет среду выполнения вкладки PowerShell, которая указана командой.</span><span class="sxs-lookup"><span data-stu-id="7cf73-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

<span data-ttu-id="7cf73-122">**\[millisecondsTimeout\]** — необязательный, целое число. Значение по умолчанию — **500**.</span><span class="sxs-lookup"><span data-stu-id="7cf73-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="7cf73-123">Если команда не завершается в течение указанного времени, то создается исключение **TimeoutException** с сообщением "Время ожидания операции истекло".</span><span class="sxs-lookup"><span data-stu-id="7cf73-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

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

## <a name="properties"></a><span data-ttu-id="7cf73-124">Свойства</span><span class="sxs-lookup"><span data-stu-id="7cf73-124">Properties</span></span>

### <a name="addonsmenu"></a><span data-ttu-id="7cf73-125">AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="7cf73-125">AddOnsMenu</span></span>

<span data-ttu-id="7cf73-126">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-127">Свойство только для чтения, которое получает меню надстроек для вкладки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cf73-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

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

### <a name="caninvoke"></a><span data-ttu-id="7cf73-128">CanInvoke</span><span class="sxs-lookup"><span data-stu-id="7cf73-128">CanInvoke</span></span>

<span data-ttu-id="7cf73-129">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-130">Логическое свойство только для чтения, которое возвращает значение **$true**, если сценарий может быть вызван с помощью метода [Invoke( Script )](#invoke-script-).</span><span class="sxs-lookup"><span data-stu-id="7cf73-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke-script-) method.</span></span>

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

### <a name="consolepane"></a><span data-ttu-id="7cf73-131">Consolepane</span><span class="sxs-lookup"><span data-stu-id="7cf73-131">Consolepane</span></span>

<span data-ttu-id="7cf73-132">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="7cf73-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="7cf73-133">В Windows PowerShell ISE 2.0 это свойство называется **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="7cf73-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

<span data-ttu-id="7cf73-134">Свойство только для чтения, которое получает объект [editor](../ise/The-ISEEditor-Object.md) области консоли.</span><span class="sxs-lookup"><span data-stu-id="7cf73-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a><span data-ttu-id="7cf73-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7cf73-135">DisplayName</span></span>

<span data-ttu-id="7cf73-136">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-137">Свойство только для чтения, которое получает или задает текст, выводимый на вкладке PowerShell. По умолчанию вкладкам назначаются имена "PowerShell #", где # — номер вкладки.</span><span class="sxs-lookup"><span data-stu-id="7cf73-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab. By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a><span data-ttu-id="7cf73-138">ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="7cf73-138">ExpandedScript</span></span>

<span data-ttu-id="7cf73-139">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-139">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-140">Логическое свойство для чтения и записи, которое определяет, развернута или скрыта область сценариев.</span><span class="sxs-lookup"><span data-stu-id="7cf73-140">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a><span data-ttu-id="7cf73-141">Файлы</span><span class="sxs-lookup"><span data-stu-id="7cf73-141">Files</span></span>

<span data-ttu-id="7cf73-142">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-142">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-143">Свойство только для чтения, которое получает [коллекцию файлов сценария](../ise/The-ISEFileCollection-Object.md), открытых на вкладке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7cf73-143">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a><span data-ttu-id="7cf73-144">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="7cf73-144">Output</span></span>

<span data-ttu-id="7cf73-145">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="7cf73-145">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="7cf73-146">В более поздних версиях интегрированной среды сценариев Windows PowerShell для тех же целей можно использовать объект **ConsolePane**.</span><span class="sxs-lookup"><span data-stu-id="7cf73-146">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

<span data-ttu-id="7cf73-147">Свойство только для чтения, которое получает область вывода текущего [редактора](../ise/The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="7cf73-147">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a><span data-ttu-id="7cf73-148">Prompt</span><span class="sxs-lookup"><span data-stu-id="7cf73-148">Prompt</span></span>

<span data-ttu-id="7cf73-149">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-149">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-150">Свойство только для чтения, которое получает текущий текст запроса.</span><span class="sxs-lookup"><span data-stu-id="7cf73-150">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="7cf73-151">Примечание. Функция **Prompt** может быть переопределена профилем пользователя.</span><span class="sxs-lookup"><span data-stu-id="7cf73-151">Note: the **Prompt** function can be overridden by the user'™s profile.</span></span> <span data-ttu-id="7cf73-152">Если результат отличается от простой строки, это свойство не возвращает никаких данных.</span><span class="sxs-lookup"><span data-stu-id="7cf73-152">If the result is other than a simple string, then this property returns nothing.</span></span>

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a><span data-ttu-id="7cf73-153">ShowCommands</span><span class="sxs-lookup"><span data-stu-id="7cf73-153">ShowCommands</span></span>

<span data-ttu-id="7cf73-154">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="7cf73-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7cf73-155">Свойство для чтения и записи, которое указывает, отображается ли панель команд.</span><span class="sxs-lookup"><span data-stu-id="7cf73-155">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a><span data-ttu-id="7cf73-156">StatusText</span><span class="sxs-lookup"><span data-stu-id="7cf73-156">StatusText</span></span>

<span data-ttu-id="7cf73-157">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7cf73-157">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7cf73-158">Свойство только для чтения, которое получает текст состояния вкладки **PowerShellTab**.</span><span class="sxs-lookup"><span data-stu-id="7cf73-158">The read-only property that gets the **PowerShellTab** status text.</span></span>

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a><span data-ttu-id="7cf73-159">HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="7cf73-159">HorizontalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="7cf73-160">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="7cf73-160">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7cf73-161">Свойство только для чтения, которое указывает, открыта ли горизонтальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="7cf73-161">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a><span data-ttu-id="7cf73-162">VerticalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="7cf73-162">VerticalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="7cf73-163">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="7cf73-163">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7cf73-164">Свойство только для чтения, которое указывает, открыта ли вертикальная область инструментов надстроек.</span><span class="sxs-lookup"><span data-stu-id="7cf73-164">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="7cf73-165">См. также</span><span class="sxs-lookup"><span data-stu-id="7cf73-165">See Also</span></span>

- [<span data-ttu-id="7cf73-166">Объект PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="7cf73-166">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md)
- [<span data-ttu-id="7cf73-167">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cf73-167">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7cf73-168">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="7cf73-168">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)