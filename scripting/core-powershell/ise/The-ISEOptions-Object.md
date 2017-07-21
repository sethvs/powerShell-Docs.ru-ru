---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEOptions"
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: 56bdd5999b46b6e29e762c2d9a2060cebe3a1299
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-iseoptions-object"></a><span data-ttu-id="ed08f-103">Объект ISEOptions</span><span class="sxs-lookup"><span data-stu-id="ed08f-103">The ISEOptions Object</span></span>
  <span data-ttu-id="ed08f-104">Объект **ISEOptions** представляет различные параметры для интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-104">The **ISEOptions** object represents various settings for Windows PowerShell ISE.</span></span> <span data-ttu-id="ed08f-105">Он является экземпляром класса **Microsoft.PowerShell.Host.ISE.ISEOptions**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-105">It is an instance of the **Microsoft.PowerShell.Host.ISE.ISEOptions** class.</span></span>

 <span data-ttu-id="ed08f-106">Объект **ISEOptions** предоставляет следующие методы и свойства.</span><span class="sxs-lookup"><span data-stu-id="ed08f-106">The **ISEOptions** object provides the following methods and properties.</span></span>

 <span data-ttu-id="ed08f-107">**Методы**</span><span class="sxs-lookup"><span data-stu-id="ed08f-107">**Methods**</span></span>

-   [<span data-ttu-id="ed08f-108">RestoreDefaultConsoleTokenColors()</span><span class="sxs-lookup"><span data-stu-id="ed08f-108">RestoreDefaultConsoleTokenColors()</span></span>](#rdctc)

-   [<span data-ttu-id="ed08f-109">RestoreDefaults()</span><span class="sxs-lookup"><span data-stu-id="ed08f-109">RestoreDefaults()</span></span>](#rd)

-   [<span data-ttu-id="ed08f-110">RestoreDefaultTokenColors()</span><span class="sxs-lookup"><span data-stu-id="ed08f-110">RestoreDefaultTokenColors()</span></span>](#rdtc)

-   [<span data-ttu-id="ed08f-111">RestoreDefaultXmlTokenColors()</span><span class="sxs-lookup"><span data-stu-id="ed08f-111">RestoreDefaultXmlTokenColors()</span></span>](#rdxtc)

 <span data-ttu-id="ed08f-112">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="ed08f-112">**Properties**</span></span>

-   [<span data-ttu-id="ed08f-113">AutoSaveMinuteInterval</span><span class="sxs-lookup"><span data-stu-id="ed08f-113">AutoSaveMinuteInterval</span></span>](#asmi)

-   [<span data-ttu-id="ed08f-114">CommandPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-114">CommandPaneBackgroundColor</span></span>](#cpbc)

-   [<span data-ttu-id="ed08f-115">CommandPaneUp</span><span class="sxs-lookup"><span data-stu-id="ed08f-115">CommandPaneUp</span></span>](#cpu)

-   [<span data-ttu-id="ed08f-116">ConsolePaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-116">ConsolePaneBackgroundColor</span></span>](#conpbc)

-   [<span data-ttu-id="ed08f-117">ConsolePaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-117">ConsolePaneForegroundColor</span></span>](#conpfc)

-   [<span data-ttu-id="ed08f-118">ConsolePaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-118">ConsolePaneTextBackgroundColor</span></span>](#conptbc)

-   [<span data-ttu-id="ed08f-119">ConsoleTokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-119">ConsoleTokenColors</span></span>](#contc)

-   [<span data-ttu-id="ed08f-120">DebugBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-120">DebugBackgroundColor</span></span>](#dbc)

-   [<span data-ttu-id="ed08f-121">DebugForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-121">DebugForegroundColor</span></span>](#dfc)

-   [<span data-ttu-id="ed08f-122">DefaultOptions</span><span class="sxs-lookup"><span data-stu-id="ed08f-122">DefaultOptions</span></span>](#do)

-   [<span data-ttu-id="ed08f-123">ErrorBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-123">ErrorBackgroundColor</span></span>](#ebc)

-   [<span data-ttu-id="ed08f-124">ErrorForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-124">ErrorForegroundColor</span></span>](#efc)

-   [<span data-ttu-id="ed08f-125">FontName</span><span class="sxs-lookup"><span data-stu-id="ed08f-125">FontName</span></span>](#fn)

-   [<span data-ttu-id="ed08f-126">FontSize</span><span class="sxs-lookup"><span data-stu-id="ed08f-126">FontSize</span></span>](#fs)

-   [<span data-ttu-id="ed08f-127">IntellisenseTimeoutInSeconds</span><span class="sxs-lookup"><span data-stu-id="ed08f-127">IntellisenseTimeoutInSeconds</span></span>](#itis)

-   [<span data-ttu-id="ed08f-128">MruCount</span><span class="sxs-lookup"><span data-stu-id="ed08f-128">MruCount</span></span>](#mc)

-   [<span data-ttu-id="ed08f-129">OutputPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-129">OutputPaneBackgroundColor</span></span>](#opbc)

-   [<span data-ttu-id="ed08f-130">OutputPaneTextForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-130">OutputPaneTextForegroundColor</span></span>](#optfc)

-   [<span data-ttu-id="ed08f-131">OutputPaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-131">OutputPaneTextBackgroundColor</span></span>](#optbc)

-   [<span data-ttu-id="ed08f-132">ScriptPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-132">ScriptPaneBackgroundColor</span></span>](#spbc)

-   [<span data-ttu-id="ed08f-133">ScriptPaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-133">ScriptPaneForegroundColor</span></span>](#spfc)

-   [<span data-ttu-id="ed08f-134">SelectedScriptPaneState</span><span class="sxs-lookup"><span data-stu-id="ed08f-134">SelectedScriptPaneState</span></span>](#ssps)

-   [<span data-ttu-id="ed08f-135">ShowDefaultSnippets</span><span class="sxs-lookup"><span data-stu-id="ed08f-135">ShowDefaultSnippets</span></span>](#sds)

-   [<span data-ttu-id="ed08f-136">ShowIntellisenseInConsolePane</span><span class="sxs-lookup"><span data-stu-id="ed08f-136">ShowIntellisenseInConsolePane</span></span>](#siicp)

-   [<span data-ttu-id="ed08f-137">ShowIntellisenseInScriptPane</span><span class="sxs-lookup"><span data-stu-id="ed08f-137">ShowIntellisenseInScriptPane</span></span>](#siisp)

-   [<span data-ttu-id="ed08f-138">ShowLineNumbers</span><span class="sxs-lookup"><span data-stu-id="ed08f-138">ShowLineNumbers</span></span>](#sln)

-   [<span data-ttu-id="ed08f-139">ShowOutlining</span><span class="sxs-lookup"><span data-stu-id="ed08f-139">ShowOutlining</span></span>](#so)

-   [<span data-ttu-id="ed08f-140">ShowToolBar</span><span class="sxs-lookup"><span data-stu-id="ed08f-140">ShowToolBar</span></span>](#stb)

-   [<span data-ttu-id="ed08f-141">ShowWarningBeforeSavingOnRun</span><span class="sxs-lookup"><span data-stu-id="ed08f-141">ShowWarningBeforeSavingOnRun</span></span>](#swbsor)

-   [<span data-ttu-id="ed08f-142">ShowWarningForDuplicateFiles</span><span class="sxs-lookup"><span data-stu-id="ed08f-142">ShowWarningForDuplicateFiles</span></span>](#swfdf)

-   [<span data-ttu-id="ed08f-143">TokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-143">TokenColors</span></span>](#tc)

-   [<span data-ttu-id="ed08f-144">UseEnterToSelectInConsolePaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="ed08f-144">UseEnterToSelectInConsolePaneIntellisense</span></span>](#uetsicpi)

-   [<span data-ttu-id="ed08f-145">UseEnterToSelectInScriptPaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="ed08f-145">UseEnterToSelectInScriptPaneIntellisense</span></span>](#uetsispi)

-   [<span data-ttu-id="ed08f-146">UseLocalHelp</span><span class="sxs-lookup"><span data-stu-id="ed08f-146">UseLocalHelp</span></span>](#ulh)

-   [<span data-ttu-id="ed08f-147">VerboseBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-147">VerboseBackgroundColor</span></span>](#vbc)

-   [<span data-ttu-id="ed08f-148">VerboseForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-148">VerboseForegroundColor</span></span>](#vfc)

-   [<span data-ttu-id="ed08f-149">WarningBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-149">WarningBackgroundColor</span></span>](#wbc)

-   [<span data-ttu-id="ed08f-150">WarningForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-150">WarningForegroundColor</span></span>](#wfc)

-   [<span data-ttu-id="ed08f-151">XmlTokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-151">XmlTokenColors</span></span>](#xtc)

-   [<span data-ttu-id="ed08f-152">Zoom</span><span class="sxs-lookup"><span data-stu-id="ed08f-152">Zoom</span></span>](#z)

## <a name="methods"></a><span data-ttu-id="ed08f-153">Методы</span><span class="sxs-lookup"><span data-stu-id="ed08f-153">Methods</span></span>

###  <span data-ttu-id="ed08f-154"><a name="rdctc"></a> RestoreDefaultConsoleTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="ed08f-154"><a name="rdctc"></a> RestoreDefaultConsoleTokenColors\(\)</span></span>
  <span data-ttu-id="ed08f-155">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-155">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-156">Восстанавливает значения по умолчанию для цветов маркеров в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-156">Restores the default values of the token colors in the Console pane.</span></span>

```
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = "red"
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

###  <span data-ttu-id="ed08f-157"><a name="rd"></a> RestoreDefaults\(\)</span><span class="sxs-lookup"><span data-stu-id="ed08f-157"><a name="rd"></a> RestoreDefaults\(\)</span></span>
  <span data-ttu-id="ed08f-158">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-159">Восстанавливает значения по умолчанию для всех параметров в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-159">Restores the default values of all options settings in the Console pane.</span></span> <span data-ttu-id="ed08f-160">Кроме того, сбрасывает поведение различных предупреждений, включающих стандартный флажок, который отключает повторный вывод сообщения.</span><span class="sxs-lookup"><span data-stu-id="ed08f-160">It also resets the behavior of various warning messages that provide the standard check box to prevent the message from being shown again.</span></span>

```
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = "orange"
$psISE.Options.RestoreDefaults()
```

###  <span data-ttu-id="ed08f-161"><a name="rdtc"></a> RestoreDefaultTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="ed08f-161"><a name="rdtc"></a> RestoreDefaultTokenColors\(\)</span></span>
  <span data-ttu-id="ed08f-162">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-163">Восстанавливает значения по умолчанию для цветов маркеров в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-163">Restores the default values of the token colors in the Script pane.</span></span>

```
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultTokenColors()
```

###  <span data-ttu-id="ed08f-164"><a name="rdxtc"></a> RestoreDefaultXmlTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="ed08f-164"><a name="rdxtc"></a> RestoreDefaultXmlTokenColors\(\)</span></span>
  <span data-ttu-id="ed08f-165">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-165">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-166">Восстанавливает значения по умолчанию для цветов маркеров XML-элементов, отображаемых в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-166">Restores the default values of the token colors for XML elements that are displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="ed08f-167">См. также [XmlTokenColors](#xtc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-167">Also see [XmlTokenColors](#xtc).</span></span>

```
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a><span data-ttu-id="ed08f-168">Свойства</span><span class="sxs-lookup"><span data-stu-id="ed08f-168">Properties</span></span>

###  <span data-ttu-id="ed08f-169"><a name="asmi"></a> AutoSaveMinuteInterval</span><span class="sxs-lookup"><span data-stu-id="ed08f-169"><a name="asmi"></a> AutoSaveMinuteInterval</span></span>
  <span data-ttu-id="ed08f-170">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-170">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-171">Задает интервал (в минутах) между операциями автоматического сохранения файлов интегрированной средой сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-171">Specifies the number of minutes between automatic save operations of your files by Windows PowerShell ISE.</span></span> <span data-ttu-id="ed08f-172">Значение по умолчанию — 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="ed08f-172">The default value is 2 minutes.</span></span> <span data-ttu-id="ed08f-173">Значение представлено целым числом.</span><span class="sxs-lookup"><span data-stu-id="ed08f-173">The value is an integer.</span></span>

```
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

###  <span data-ttu-id="ed08f-174"><a name="cpbc"></a> CommandPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-174"><a name="cpbc"></a> CommandPaneBackgroundColor</span></span>
  <span data-ttu-id="ed08f-175">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-175">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="ed08f-176">Сведения для более поздних версий см. в разделе [ConsolePaneBackgroundColor](#conpbc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-176">For later versions, see [ConsolePaneBackgroundColor](#conpbc).</span></span>

 <span data-ttu-id="ed08f-177">Задает цвет фона для области команд.</span><span class="sxs-lookup"><span data-stu-id="ed08f-177">Specifies the background color for the Command pane.</span></span> <span data-ttu-id="ed08f-178">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-178">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = "orange"
```

###  <span data-ttu-id="ed08f-179"><a name="cpu"></a> CommandPaneUp</span><span class="sxs-lookup"><span data-stu-id="ed08f-179"><a name="cpu"></a> CommandPaneUp</span></span>
  <span data-ttu-id="ed08f-180">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-180">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>

 <span data-ttu-id="ed08f-181">Указывает, находится ли область команд над областью вывода.</span><span class="sxs-lookup"><span data-stu-id="ed08f-181">Specifies whether the Command pane is located above the Output pane.</span></span>

```
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true

```

###  <span data-ttu-id="ed08f-182"><a name="conpbc"></a> ConsolePaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-182"><a name="conpbc"></a> ConsolePaneBackgroundColor</span></span>
  <span data-ttu-id="ed08f-183">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-183">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-184">Задает цвет фона для области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-184">Specifies the background color for the Console pane.</span></span> <span data-ttu-id="ed08f-185">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-185">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = "red"
```

###  <span data-ttu-id="ed08f-186"><a name="conpfc"></a> ConsolePaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-186"><a name="conpfc"></a> ConsolePaneForegroundColor</span></span>
  <span data-ttu-id="ed08f-187">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-187">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-188">Задает цвет переднего плана для текста в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-188">Specifies the foreground color of the text in the Console pane.</span></span>

```
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = "yellow"

```

###  <span data-ttu-id="ed08f-189"><a name="conptbc"></a> ConsolePaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-189"><a name="conptbc"></a> ConsolePaneTextBackgroundColor</span></span>
  <span data-ttu-id="ed08f-190">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-190">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-191">Задает цвет фона для текста в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-191">Specifies the background color of the text in the Console pane.</span></span>

```
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = "pink"
```

###  <span data-ttu-id="ed08f-192"><a name="contc"></a> ConsoleTokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-192"><a name="contc"></a> ConsoleTokenColors</span></span>
  <span data-ttu-id="ed08f-193">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-193">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-194">Задает цвета маркеров IntelliSense в области консоли интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-194">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Console pane.</span></span> <span data-ttu-id="ed08f-195">Это свойство является объектом словаря, который содержит пары "имя — значение" для типов и цветов маркеров для области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-195">This property is a dictionary object that contains name/value pairs of token types and colors for the Console pane.</span></span> <span data-ttu-id="ed08f-196">Сведения об изменении цвета маркеров IntelliSense в области сценариев см. в разделе [TokenColors](#tc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-196">To change the colors of the IntelliSense tokens in the Script pane, see [TokenColors](#tc).</span></span> <span data-ttu-id="ed08f-197">Сведения о восстановлении значений по умолчанию для цветов см. в разделе [RestoreDefaultConsoleTokenColors()](#rdctc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-197">To reset the colors to the default values, see [RestoreDefaultConsoleTokenColors()](#rdctc).</span></span> <span data-ttu-id="ed08f-198">Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span><span class="sxs-lookup"><span data-stu-id="ed08f-198">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = "magenta"

```

###  <span data-ttu-id="ed08f-199"><a name="dbc"></a> DebugBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-199"><a name="dbc"></a> DebugBackgroundColor</span></span>
  <span data-ttu-id="ed08f-200">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-200">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-201">Задает цвет фона для сообщений отладки, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-201">Specifies the background color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-202">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-202">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor ='#0000FF'
```

###  <span data-ttu-id="ed08f-203"><a name="dfc"></a> DebugForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-203"><a name="dfc"></a> DebugForegroundColor</span></span>
  <span data-ttu-id="ed08f-204">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-204">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-205">Задает цвет переднего плана для сообщений отладки, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-205">Specifies the foreground color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-206">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-206">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor ="yellow"
```

###  <span data-ttu-id="ed08f-207"><a name="do"></a> DefaultOptions</span><span class="sxs-lookup"><span data-stu-id="ed08f-207"><a name="do"></a> DefaultOptions</span></span>
  <span data-ttu-id="ed08f-208">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-208">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-209">Коллекция свойств, задающих значения по умолчанию, используемые при выполнении методов сброса (Reset).</span><span class="sxs-lookup"><span data-stu-id="ed08f-209">A collection of properties that specify the default values to be used when the Reset methods are used.</span></span>

```
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

###  <span data-ttu-id="ed08f-210"><a name="ebc"></a> ErrorBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-210"><a name="ebc"></a> ErrorBackgroundColor</span></span>
  <span data-ttu-id="ed08f-211">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-211">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-212">Задает цвет фона для сообщений об ошибках, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-212">Specifies the background color for error text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-213">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-213">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor="black"
```

###  <span data-ttu-id="ed08f-214"><a name="efc"></a> ErrorForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-214"><a name="efc"></a> ErrorForegroundColor</span></span>
  <span data-ttu-id="ed08f-215">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-215">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-216">Задает цвет переднего плана для сообщений об ошибках, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-216">Specifies the foreground color for error text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-217">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-217">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor ="green"
```

###  <span data-ttu-id="ed08f-218"><a name="fn"></a> FontName</span><span class="sxs-lookup"><span data-stu-id="ed08f-218"><a name="fn"></a> FontName</span></span>
  <span data-ttu-id="ed08f-219">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-219">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-220">Задает название текущего шрифта в области сценариев и в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-220">Specifies the font name currently in use in both the Script pane and the Console pane.</span></span>

```
# Changes the font used in both panes.
$psISE.Options.FontName = "courier new"
```

###  <span data-ttu-id="ed08f-221"><a name="fs"></a> FontSize</span><span class="sxs-lookup"><span data-stu-id="ed08f-221"><a name="fs"></a> FontSize</span></span>
  <span data-ttu-id="ed08f-222">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-222">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-223">Указывает размер шрифта в виде целого числа.</span><span class="sxs-lookup"><span data-stu-id="ed08f-223">Specifies the font size as an integer.</span></span> <span data-ttu-id="ed08f-224">Используется в области сценариев, области команд и области вывода.</span><span class="sxs-lookup"><span data-stu-id="ed08f-224">It is used in the Script pane, the Command pane, and the Output pane.</span></span> <span data-ttu-id="ed08f-225">Допустимый диапазон значений — от 8 до 32.</span><span class="sxs-lookup"><span data-stu-id="ed08f-225">The valid range of values is 8 through 32.</span></span>

```
# Changes the font size in all panes.
$psISE.Options.FontSize = 20

```

###  <span data-ttu-id="ed08f-226"><a name="itis"></a> IntellisenseTimeoutInSeconds</span><span class="sxs-lookup"><span data-stu-id="ed08f-226"><a name="itis"></a> IntellisenseTimeoutInSeconds</span></span>
  <span data-ttu-id="ed08f-227">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-227">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-228">Указывает интервал (в секундах), в течение которого IntelliSense пытается разрешить текущий вводимый текст.</span><span class="sxs-lookup"><span data-stu-id="ed08f-228">Specifies the number of seconds that IntelliSense uses to try to resolve the currently typed text.</span></span> <span data-ttu-id="ed08f-229">По завершении указанного интервала время ожидания IntelliSense истекает, и компонент позволяет продолжить ввод текста.</span><span class="sxs-lookup"><span data-stu-id="ed08f-229">After this number of seconds, IntelliSense times out and enables you to continue typing.</span></span> <span data-ttu-id="ed08f-230">Значение по умолчанию — 3 секунды.</span><span class="sxs-lookup"><span data-stu-id="ed08f-230">The default value is 3 seconds.</span></span> <span data-ttu-id="ed08f-231">Значение представлено целым числом.</span><span class="sxs-lookup"><span data-stu-id="ed08f-231">The value is an integer.</span></span>

```
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

###  <span data-ttu-id="ed08f-232"><a name="mc"></a> MruCount</span><span class="sxs-lookup"><span data-stu-id="ed08f-232"><a name="mc"></a> MruCount</span></span>
  <span data-ttu-id="ed08f-233">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-233">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-234">Задает число недавно открывавшихся файлов, которые интегрированная среда сценариев Windows PowerShell отслеживает и отображает в нижней части меню **Открытие файла**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-234">Specifies the number of recently opened files that Windows PowerShell ISE tracks and displays at the bottom of the **File Open** menu.</span></span> <span data-ttu-id="ed08f-235">Значение по умолчанию — 10.</span><span class="sxs-lookup"><span data-stu-id="ed08f-235">The default value is 10.</span></span> <span data-ttu-id="ed08f-236">Значение представлено целым числом.</span><span class="sxs-lookup"><span data-stu-id="ed08f-236">The value is an integer.</span></span>

```
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

###  <span data-ttu-id="ed08f-237"><a name="opbc"></a> OutputPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-237"><a name="opbc"></a> OutputPaneBackgroundColor</span></span>
  <span data-ttu-id="ed08f-238">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-238">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="ed08f-239">Сведения для более поздних версий см. в разделе [ConsolePaneBackgroundColor](#conpbc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-239">For later versions, see [ConsolePaneBackgroundColor](#conpbc).</span></span>

 <span data-ttu-id="ed08f-240">Свойство для чтения и записи, которое получает или задает цвет фона самой области вывода.</span><span class="sxs-lookup"><span data-stu-id="ed08f-240">The read/write property that gets or sets the background color for the Output pane itself.</span></span> <span data-ttu-id="ed08f-241">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-241">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = "gold"

```

###  <span data-ttu-id="ed08f-242"><a name="optfc"></a> OutputPaneTextForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-242"><a name="optfc"></a> OutputPaneTextForegroundColor</span></span>
  <span data-ttu-id="ed08f-243">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-243">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="ed08f-244">Сведения для более поздних версий см. в разделе [ConsolePaneForegroundColor](#conpfc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-244">For later versions, see [ConsolePaneForegroundColor](#conpfc).</span></span>

 <span data-ttu-id="ed08f-245">Свойство для чтения и записи, которое изменяет цвет переднего плана текста в области вывода в интегрированной среде сценариев Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="ed08f-245">The read/write property that changes the foreground color of the text in the Output pane in Windows PowerShell ISE 2.0.</span></span>

```
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = "blue"

```

###  <span data-ttu-id="ed08f-246"><a name="optbc"></a> OutputPaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-246"><a name="optbc"></a> OutputPaneTextBackgroundColor</span></span>
  <span data-ttu-id="ed08f-247">Этот компонент присутствует в интегрированной среде сценариев Windows PowerShell 2.0, но был удален или переименован в более поздних версиях интегрированной среды сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-247">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="ed08f-248">Сведения для более поздних версий см. в разделе [ConsolePaneTextBackgroundColor](#conptbc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-248">For later versions, see [ConsolePaneTextBackgroundColor](#conptbc).</span></span>

 <span data-ttu-id="ed08f-249">Свойство для чтения и записи, которое изменяет цвет фона текста в области вывода.</span><span class="sxs-lookup"><span data-stu-id="ed08f-249">The read/write property that changes the background color of the text in the Output pane.</span></span>

```
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = "pink"
```

###  <span data-ttu-id="ed08f-250"><a name="spbc"></a> ScriptPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-250"><a name="spbc"></a> ScriptPaneBackgroundColor</span></span>
  <span data-ttu-id="ed08f-251">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-251">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-252">Свойство для чтения и записи, которое получает или задает цвет фона для файлов.</span><span class="sxs-lookup"><span data-stu-id="ed08f-252">The read/write property that gets or sets the background color for files.</span></span> <span data-ttu-id="ed08f-253">Это экземпляр класса **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-253">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```

# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = ”yellow”

```

###  <span data-ttu-id="ed08f-254"><a name="spfc"></a> ScriptPaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-254"><a name="spfc"></a> ScriptPaneForegroundColor</span></span>
  <span data-ttu-id="ed08f-255">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-255">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-256">Свойство для чтения и записи, которое получает или задает цвет переднего плана для файлов, не являющихся сценариями, в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-256">The read/write property that gets or sets the foreground color for non-script files in the Script pane.</span></span>
<span data-ttu-id="ed08f-257">Чтобы задать цвет переднего плана для файлов сценариев, используйте свойство [TokenColors](The-ISEOptions-Object.md#tc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-257">To set the foreground color for script files, use the [TokenColors](The-ISEOptions-Object.md#tc) property.</span></span>

```
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = "green"

```

###  <span data-ttu-id="ed08f-258"><a name="ssps"></a> SelectedScriptPaneState</span><span class="sxs-lookup"><span data-stu-id="ed08f-258"><a name="ssps"></a> SelectedScriptPaneState</span></span>
  <span data-ttu-id="ed08f-259">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-259">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-260">Свойство для чтения и записи, которое получает или задает положение области сценариев на экране.</span><span class="sxs-lookup"><span data-stu-id="ed08f-260">The read/write property that gets or sets the position of the Script pane on the display.</span></span> <span data-ttu-id="ed08f-261">Строка может иметь значение Maximized, Top или Right.</span><span class="sxs-lookup"><span data-stu-id="ed08f-261">The string can be either "Maximized", "Top", or "Right".</span></span>

```
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = "Top"
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = "Right"
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = "Maximized"

```

###  <span data-ttu-id="ed08f-262"><a name="sds"></a> ShowDefaultSnippets</span><span class="sxs-lookup"><span data-stu-id="ed08f-262"><a name="sds"></a> ShowDefaultSnippets</span></span>
  <span data-ttu-id="ed08f-263">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-263">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-264">Указывает, содержит ли список фрагментов **CTRL+J** начальный набор, который включен в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-264">Specifies whether the **CTRL+J** list of snippets includes the starter set that is included in Windows PowerShell.</span></span> <span data-ttu-id="ed08f-265">Если задано значение **$false**, в списке **CTRL+J** отображаются только определенные пользователем фрагменты.</span><span class="sxs-lookup"><span data-stu-id="ed08f-265">When set to **$false**, only user-defined snippets appear in the **CTRL+J** list.</span></span> <span data-ttu-id="ed08f-266">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-266">The default value is **$true**.</span></span>

```
# Hide the default snippets from the CTRL+J list.
$psISe.Options.ShowDefaultSnippets = $false
```

###  <span data-ttu-id="ed08f-267"><a name="siicp"></a> ShowIntellisenseInConsolePane</span><span class="sxs-lookup"><span data-stu-id="ed08f-267"><a name="siicp"></a> ShowIntellisenseInConsolePane</span></span>
  <span data-ttu-id="ed08f-268">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-268">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-269">Указывает, предлагает ли IntelliSense синтаксис, параметры и значения в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-269">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Console pane.</span></span> <span data-ttu-id="ed08f-270">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-270">The default value is **$true**.</span></span>

```
# Turn off IntelliSense in the console pane.
$psISe.Options.ShowIntellisenseInConsolePane = $false
```

###  <span data-ttu-id="ed08f-271"><a name="siisp"></a> ShowIntellisenseInScriptPane</span><span class="sxs-lookup"><span data-stu-id="ed08f-271"><a name="siisp"></a> ShowIntellisenseInScriptPane</span></span>
  <span data-ttu-id="ed08f-272">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-272">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-273">Указывает, предлагает ли IntelliSense синтаксис, параметры и значения в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-273">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Script pane.</span></span> <span data-ttu-id="ed08f-274">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-274">The default value is **$true**.</span></span>

```
# Turn off IntelliSense in the Script pane.
$psISe.Options.ShowIntellisenseInScriptPane = $false
```

###  <span data-ttu-id="ed08f-275"><a name="sln"></a> ShowLineNumbers</span><span class="sxs-lookup"><span data-stu-id="ed08f-275"><a name="sln"></a> ShowLineNumbers</span></span>
  <span data-ttu-id="ed08f-276">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-276">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-277">Указывает, отображаются ли в левом поле области сценариев номера строк.</span><span class="sxs-lookup"><span data-stu-id="ed08f-277">Specifies whether the Script pane displays line numbers in the left margin.</span></span> <span data-ttu-id="ed08f-278">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-278">The default value is **$true**.</span></span>

```
# Turn off line numbers in the Script pane.
$psISe.Options.ShowLineNumbers = $false
```

###  <span data-ttu-id="ed08f-279"><a name="so"></a> ShowOutlining</span><span class="sxs-lookup"><span data-stu-id="ed08f-279"><a name="so"></a> ShowOutlining</span></span>
  <span data-ttu-id="ed08f-280">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-280">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-281">Указывает, отображаются ли в области сценариев расширяемые и свертываемые скобки рядом с фрагментами кода в левом поле.</span><span class="sxs-lookup"><span data-stu-id="ed08f-281">Specifies whether the Script pane displays expandable and collapsible brackets next to sections of code in the left margin.</span></span> <span data-ttu-id="ed08f-282">Когда они отображаются, можно щелкнуть значок "минус" \(-\) рядом с блоком текста, чтобы свернуть, или значок "плюс" \(+\), чтобы развернуть блок текста.</span><span class="sxs-lookup"><span data-stu-id="ed08f-282">When they are displayed, you can click the minus \(-\) icons next to a block of text to collapse it or click the plus \(+\) icon to expand a block of text.</span></span> <span data-ttu-id="ed08f-283">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-283">The default value is **$true**.</span></span>

```
# Turn off outlining in the Script pane.
$psISe.Options.ShowOutlining = $false
```

###  <span data-ttu-id="ed08f-284"><a name="stb"></a> ShowToolBar</span><span class="sxs-lookup"><span data-stu-id="ed08f-284"><a name="stb"></a> ShowToolBar</span></span>
  <span data-ttu-id="ed08f-285">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-285">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-286">Указывает, отображается ли в верхней части окна интегрированной среды сценариев Windows PowerShell панель инструментов ISE.</span><span class="sxs-lookup"><span data-stu-id="ed08f-286">Specifies whether the ISE toolbar appears at the top of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="ed08f-287">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-287">The default value is **$true**.</span></span>

```
# Show the toolbar.
$psISe.Options.ShowToolBar = $true
```

###  <span data-ttu-id="ed08f-288"><a name="swbsor"></a> ShowWarningBeforeSavingOnRun</span><span class="sxs-lookup"><span data-stu-id="ed08f-288"><a name="swbsor"></a> ShowWarningBeforeSavingOnRun</span></span>
  <span data-ttu-id="ed08f-289">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-289">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-290">Указывает, отображается ли предупреждение, когда сценарий сохраняется автоматически перед запуском.</span><span class="sxs-lookup"><span data-stu-id="ed08f-290">Specifies whether a warning message appears when a script is saved automatically before it is run.</span></span> <span data-ttu-id="ed08f-291">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-291">The default value is **$true**.</span></span>

```
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun=$true

```

###  <span data-ttu-id="ed08f-292"><a name="swfdf"></a> ShowWarningForDuplicateFiles</span><span class="sxs-lookup"><span data-stu-id="ed08f-292"><a name="swfdf"></a> ShowWarningForDuplicateFiles</span></span>
  <span data-ttu-id="ed08f-293">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-293">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-294">Указывает, отображается ли предупреждение при открытии одного и того же файла на разных вкладках PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-294">Specifies whether a warning message appears when the same file is opened in different PowerShell tabs.</span></span> <span data-ttu-id="ed08f-295">Если задано значение **$true**, при открытии одного файла на нескольких вкладках отображается сообщение: "Копия данного файла открыта на другой вкладке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-295">If set to **$true**, to open the same file in multiple tabs displays this message: "A copy of this file is open in another Windows PowerShell tab.</span></span> <span data-ttu-id="ed08f-296">Изменения, внесенные в данный файл, отразятся на всех его открытых копиях".</span><span class="sxs-lookup"><span data-stu-id="ed08f-296">Changes made to this file will affect all open copies."</span></span> <span data-ttu-id="ed08f-297">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-297">The default value is **$true**.</span></span>

```
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true

```

###  <span data-ttu-id="ed08f-298"><a name="tc"></a> TokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-298"><a name="tc"></a> TokenColors</span></span>
  <span data-ttu-id="ed08f-299">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-299">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-300">Задает цвета маркеров IntelliSense в области сценариев интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-300">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Script pane.</span></span> <span data-ttu-id="ed08f-301">Это свойство является объектом словаря, который содержит пары "имя — значение" для типов и цветов маркеров для области сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-301">This property is a dictionary object that contains name/value pairs of token types and colors for the Script pane.</span></span> <span data-ttu-id="ed08f-302">Сведения об изменении цветов маркеров IntelliSense в области консоли см. в разделе [ConsoleTokenColors](#contc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-302">To change the colors of the IntelliSense tokens in the Console pane, see [ConsoleTokenColors](#contc).</span></span> <span data-ttu-id="ed08f-303">Сведения о восстановлении значений по умолчанию см. в разделе [RestoreDefaultTokenColors()](#rdtc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-303">To reset the colors to the default values, see [RestoreDefaultTokenColors()](#rdtc).</span></span> <span data-ttu-id="ed08f-304">Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span><span class="sxs-lookup"><span data-stu-id="ed08f-304">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"

```

###  <span data-ttu-id="ed08f-305"><a name="uetsicpi"></a> UseEnterToSelectInConsolePaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="ed08f-305"><a name="uetsicpi"></a> UseEnterToSelectInConsolePaneIntellisense</span></span>
  <span data-ttu-id="ed08f-306">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-306">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-307">Указывает, можно ли использовать клавишу ВВОД для выбора варианта, предложенного IntelliSense, в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-307">Specifies whether you can use the Enter key to select an IntelliSense provided option in the Console pane.</span></span> <span data-ttu-id="ed08f-308">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-308">The default value is **$true**.</span></span>

```
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$false

```

###  <span data-ttu-id="ed08f-309"><a name="uetsispi"></a> UseEnterToSelectInScriptPaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="ed08f-309"><a name="uetsispi"></a> UseEnterToSelectInScriptPaneIntellisense</span></span>
  <span data-ttu-id="ed08f-310">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-310">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-311">Указывает, можно ли использовать клавишу ВВОД для выбора варианта, предложенного IntelliSense, в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-311">Specifies whether you can use the Enter key to select an IntelliSense-provided option in the Script pane.</span></span> <span data-ttu-id="ed08f-312">По умолчанию используется значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-312">The default value is **$true**.</span></span>

```
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$true

```

###  <span data-ttu-id="ed08f-313"><a name="ulh"></a> UseLocalHelp</span><span class="sxs-lookup"><span data-stu-id="ed08f-313"><a name="ulh"></a> UseLocalHelp</span></span>
  <span data-ttu-id="ed08f-314">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-314">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-315">Указывает, выводится ли на экран локальная справка или справка библиотеки TechNet в Интернете при нажатии клавиши F1, когда курсор находится в ключевом слове.</span><span class="sxs-lookup"><span data-stu-id="ed08f-315">Specifies whether the locally installed Help or the online TechNet Library Help appears when you press F1 with the cursor positioned in a keyword.</span></span> <span data-ttu-id="ed08f-316">Если задано значение **$true**, во всплывающем окне отображается содержимое локальной справки.</span><span class="sxs-lookup"><span data-stu-id="ed08f-316">If set to **$true**, then a pop-up window shows content from the locally installed Help.</span></span> <span data-ttu-id="ed08f-317">Можно установить файлы справки, выполнив команду `Update-Help`.</span><span class="sxs-lookup"><span data-stu-id="ed08f-317">You can install the Help files by running the `Update-Help` command.</span></span> <span data-ttu-id="ed08f-318">Если задано значение **$false**, в браузере открывается страница библиотеки TechNet.</span><span class="sxs-lookup"><span data-stu-id="ed08f-318">If set to **$false**, then your browser opens to a page in the TechNet Library.</span></span>

```
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp=$false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp=$true

```

###  <span data-ttu-id="ed08f-319"><a name="vbc"></a> VerboseBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-319"><a name="vbc"></a> VerboseBackgroundColor</span></span>
  <span data-ttu-id="ed08f-320">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-320">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-321">Задает цвет фона для подробных сообщений, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-321">Specifies the background color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-322">Это объект **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-322">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

###  <span data-ttu-id="ed08f-323"><a name="vfc"></a> VerboseForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-323"><a name="vfc"></a> VerboseForegroundColor</span></span>
  <span data-ttu-id="ed08f-324">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-324">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-325">Задает цвет переднего плана для подробных сообщений, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-325">Specifies the foreground color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-326">Это объект **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-326">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor =”yellow”
```

###  <span data-ttu-id="ed08f-327"><a name="wbc"></a> WarningBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-327"><a name="wbc"></a> WarningBackgroundColor</span></span>
  <span data-ttu-id="ed08f-328">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-328">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-329">Задает цвет фона для текста предупреждений, отображаемых в области консоли.</span><span class="sxs-lookup"><span data-stu-id="ed08f-329">Specifies the background color for warning text that appears in the Console pane.</span></span> <span data-ttu-id="ed08f-330">Это объект **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-330">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor ='#0000FF'
```

###  <span data-ttu-id="ed08f-331"><a name="wfc"></a> WarningForegroundColor</span><span class="sxs-lookup"><span data-stu-id="ed08f-331"><a name="wfc"></a> WarningForegroundColor</span></span>
  <span data-ttu-id="ed08f-332">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="ed08f-332">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ed08f-333">Задает цвет переднего плана для текста предупреждений, отображаемых в области вывода.</span><span class="sxs-lookup"><span data-stu-id="ed08f-333">Specifies the foreground color for warning text that appears in the Output pane.</span></span> <span data-ttu-id="ed08f-334">Это объект **System.Windows.Media.Color**.</span><span class="sxs-lookup"><span data-stu-id="ed08f-334">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor =”yellow”
```

###  <span data-ttu-id="ed08f-335"><a name="xtc"></a> XmlTokenColors</span><span class="sxs-lookup"><span data-stu-id="ed08f-335"><a name="xtc"></a> XmlTokenColors</span></span>
  <span data-ttu-id="ed08f-336">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-336">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-337">Указывает объект словаря, который содержит пары "имя — значение" для типов и цветов маркеров для XML-содержимого, которое отображается в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-337">Specifies a dictionary object that contains name/value pairs of token types and colors for XML content that is displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="ed08f-338">Можно задать цвета для следующих маркеров: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span><span class="sxs-lookup"><span data-stu-id="ed08f-338">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span> <span data-ttu-id="ed08f-339">См. также [RestoreDefaultXmlTokenColors()](#rdxtc).</span><span class="sxs-lookup"><span data-stu-id="ed08f-339">Also see [RestoreDefaultXmlTokenColors()](#rdxtc).</span></span>

```
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = "green"
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = "magenta"

```

###  <span data-ttu-id="ed08f-340"><a name="z"></a> Zoom</span><span class="sxs-lookup"><span data-stu-id="ed08f-340"><a name="z"></a> Zoom</span></span>
  <span data-ttu-id="ed08f-341">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="ed08f-341">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="ed08f-342">Указывает относительный размер текста в области консоли и сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed08f-342">Specifies the relative size of text in both the Console and Script panes.</span></span> <span data-ttu-id="ed08f-343">Значение по умолчанию — 100.</span><span class="sxs-lookup"><span data-stu-id="ed08f-343">The default value is 100.</span></span> <span data-ttu-id="ed08f-344">Чем больше это значение, тем больше размер отображаемого текста в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed08f-344">Smaller values cause the text in Windows PowerShell ISE to appear smaller while larger numbers cause text to appear larger.</span></span> <span data-ttu-id="ed08f-345">Значение представлено целым числом в диапазоне от 20 до 400.</span><span class="sxs-lookup"><span data-stu-id="ed08f-345">The value is an integer that ranges from 20 to 400.</span></span>

```
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a><span data-ttu-id="ed08f-346">См. также</span><span class="sxs-lookup"><span data-stu-id="ed08f-346">See Also</span></span>
- [<span data-ttu-id="ed08f-347">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed08f-347">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="ed08f-348">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed08f-348">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)

