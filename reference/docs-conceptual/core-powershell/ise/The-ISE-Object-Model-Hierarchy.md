---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Иерархия объектной модели интегрированной среды сценариев"
ms.assetid: bc3300e4-9c17-4f00-a621-c8867126e3b3
ms.openlocfilehash: b6e251eac7db56896490362392e0a1c4c10a8d4a
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="50c3f-103">Иерархия объектной модели интегрированной среды сценариев</span><span class="sxs-lookup"><span data-stu-id="50c3f-103">The ISE Object Model Hierarchy</span></span>
  <span data-ttu-id="50c3f-104">В этом разделе демонстрируется иерархия объектов, которые входят в состав интегрированной среды сценариев Windows PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="50c3f-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="50c3f-105">Интегрированная среда сценариев Windows PowerShell входит в состав Windows PowerShell 3.0 и Windows PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="50c3f-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span> <span data-ttu-id="50c3f-106">Щелкните объект, чтобы перейти к справочной документации для класса, определяющего объект.</span><span class="sxs-lookup"><span data-stu-id="50c3f-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

##  <a name="psise-object"></a><span data-ttu-id="50c3f-107">**Объект $psISE**</span><span class="sxs-lookup"><span data-stu-id="50c3f-107">**$psISE Object**</span></span>
 <span data-ttu-id="50c3f-108">Объект **$psISE** — это [корневой объект](The-ObjectModelRoot-Object.md) иерархии объектов интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50c3f-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span> <span data-ttu-id="50c3f-109">Располагаясь на верхнем уровне, он предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-109">Located at the top level, it makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-110">**[$psISE.CurrentFile]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-110">**[$psISE.CurrentFile]()**</span></span>

-   <span data-ttu-id="50c3f-111">**[$psISE.CurrentPowerShellTab]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-111">**[$psISE.CurrentPowerShellTab]()**</span></span>

-   <span data-ttu-id="50c3f-112">**[$psISE.CurrentVisibleHorizontalTool]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-112">**[$psISE.CurrentVisibleHorizontalTool]()**</span></span>

-   <span data-ttu-id="50c3f-113">**[$psISE.CurrentVisibleVerticalTool]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-113">**[$psISE.CurrentVisibleVerticalTool]()**</span></span>

-   <span data-ttu-id="50c3f-114">**[$psISE.Options]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-114">**[$psISE.Options]()**</span></span>

-   <span data-ttu-id="50c3f-115">**[$psISE.PowerShellTabs]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-115">**[$psISE.PowerShellTabs]()**</span></span>

##  <a name="psisecurrentfilethe-isefile-objectmd"></a><span data-ttu-id="50c3f-116">**[$psISE.CurrentFile](The-ISEFile-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-116">**[$psISE.CurrentFile](The-ISEFile-Object.md)**</span></span>
 <span data-ttu-id="50c3f-117">Объект **$PsISE.CurrentFile** является экземпляром класса [ISEFile](The-ISEFile-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-117">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class and makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-118">**[$psISE.CurrentFile.DisplayName](The-ISEFile-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-118">**[$psISE.CurrentFile.DisplayName](The-ISEFile-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-119">**[$psISE.CurrentFile.Editor](The-ISEEditor-Object.md)** Этот объект является экземпляром класса [ISEEditor](The-ISEEditor-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-119">**[$psISE.CurrentFile.Editor](The-ISEEditor-Object.md)**  This object is an instance of the [ISEEditor](The-ISEEditor-Object.md) class and makes the following objects available for scripting:</span></span>

    -   <span data-ttu-id="50c3f-120">**[$psISE.CurrentFile.Editor.CanGoToMatch](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-120">**[$psISE.CurrentFile.Editor.CanGoToMatch](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-121">**[CaretColumn](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-121">**[CaretColumn](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-122">**[CaretLine](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-122">**[CaretLine](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-123">**[$psISE.CurrentFile.Editor.CaretLineText](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-123">**[$psISE.CurrentFile.Editor.CaretLineText](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-124">**[LineCount](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-124">**[LineCount](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-125">**[SelectedText](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-125">**[SelectedText](The-ISEEditor-Object.md)**</span></span>

    -   <span data-ttu-id="50c3f-126">**[Text](The-ISEEditor-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-126">**[Text](The-ISEEditor-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-127">**[EncodingThe-ISEFile-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-127">**[EncodingThe-ISEFile-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-128">**[FullPathThe-ISEFile-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-128">**[FullPathThe-ISEFile-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-129">**[IsSavedThe-ISEFile-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-129">**[IsSavedThe-ISEFile-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-130">**[IsUntitledThe-ISEFile-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-130">**[IsUntitledThe-ISEFile-Object.md]()**</span></span>

##  <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a><span data-ttu-id="50c3f-131">**[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-131">**[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)**</span></span>
 <span data-ttu-id="50c3f-132">Объект **$psISE.CurrentPowerShellTab** является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-132">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class and makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-133">**[$psISE.CurrentPowerShellTab.AddOnsMenu](The-ISEMenuItem-Object.md)** Этот объект является экземпляром класса [ISEMenuItem](The-ISEMenuItem-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-133">**[$psISE.CurrentPowerShellTab.AddOnsMenu](The-ISEMenuItem-Object.md)**  This object is an instance of the [ISEMenuItem](The-ISEMenuItem-Object.md) class and makes the following objects available for scripting:</span></span>

    -   <span data-ttu-id="50c3f-134">**[$psISE.CurrentPowerShellTab.AddOnsMenu.ActionThe-ISEMenuItem-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-134">**[$psISE.CurrentPowerShellTab.AddOnsMenu.ActionThe-ISEMenuItem-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-135">**[$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayNameThe-ISEMenuItem-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-135">**[$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayNameThe-ISEMenuItem-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-136">**[$psISE.CurrentPowerShellTab.AddOnsMenu.ShortcutThe-ISEMenuItem-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-136">**[$psISE.CurrentPowerShellTab.AddOnsMenu.ShortcutThe-ISEMenuItem-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-137">**[$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus](The-ISEMenuItemCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-137">**[$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus](The-ISEMenuItemCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-138">**[$psISE.CurrentPowerShellTab.CanInvokeThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-138">**[$psISE.CurrentPowerShellTab.CanInvokeThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-139">**[$psISE.CurrentPowerShellTab.ConsolePane](The-ISEEditor-Object.md)** Этот объект является экземпляром класса [ISEEditor](The-ISEEditor-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-139">**[$psISE.CurrentPowerShellTab.ConsolePane](The-ISEEditor-Object.md)**  This object is an instance of the [ISEEditor](The-ISEEditor-Object.md) class and makes the following objects available for scripting:</span></span>

    -   <span data-ttu-id="50c3f-140">**[$psISE.CurrentPowerShellTab.ConsolePane.CanGoToMatchThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-140">**[$psISE.CurrentPowerShellTab.ConsolePane.CanGoToMatchThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-141">**[CaretColumnThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-141">**[CaretColumnThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-142">**[CaretLineThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-142">**[CaretLineThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-143">**[$psISE.CurrentPowerShellTab.ConsolePane.CaretLineTextThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-143">**[$psISE.CurrentPowerShellTab.ConsolePane.CaretLineTextThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-144">**[LineCountThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-144">**[LineCountThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-145">**[SelectedTextThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-145">**[SelectedTextThe-ISEEditor-Object.md]()**</span></span>

    -   <span data-ttu-id="50c3f-146">**[TextThe-ISEEditor-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-146">**[TextThe-ISEEditor-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-147">**[$psISE.CurrentPowerShellTab.DisplayNameThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-147">**[$psISE.CurrentPowerShellTab.DisplayNameThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-148">**[$psISE.CurrentPowerShellTab.ExpandedScriptThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-148">**[$psISE.CurrentPowerShellTab.ExpandedScriptThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-149">**[$psISE.CurrentPowerShellTab.Files](The-ISEFileCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-149">**[$psISE.CurrentPowerShellTab.Files](The-ISEFileCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-150">**[$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-150">**[$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-151">**[$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-151">**[$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-152">**[$psISE.CurrentPowerShellTab.PromptThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-152">**[$psISE.CurrentPowerShellTab.PromptThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-153">**[$psISE.CurrentPowerShellTab.ShowCommandsThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-153">**[$psISE.CurrentPowerShellTab.ShowCommandsThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-154">**[$psISE.CurrentPowerShellTab.Snippets](The-ISESnippetCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-154">**[$psISE.CurrentPowerShellTab.Snippets](The-ISESnippetCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-155">**[$psISE.CurrentPowerShellTab.StatusTextThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-155">**[$psISE.CurrentPowerShellTab.StatusTextThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-156">**[$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-156">**[$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-157">**[$psISE.CurrentPowerShellTab.VerticalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-157">**[$psISE.CurrentPowerShellTab.VerticalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-158">**[$psISE.CurrentPowerShellTab.VisibleHorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-158">**[$psISE.CurrentPowerShellTab.VisibleHorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-159">**[$psISE.CurrentPowerShellTab.VisibleVerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-159">**[$psISE.CurrentPowerShellTab.VisibleVerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**</span></span>

##  <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="50c3f-160">**$psISE.CurrentVisibleHorizontalTool**</span><span class="sxs-lookup"><span data-stu-id="50c3f-160">**$psISE.CurrentVisibleHorizontalTool**</span></span>
 <span data-ttu-id="50c3f-161">Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).</span><span class="sxs-lookup"><span data-stu-id="50c3f-161">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span> <span data-ttu-id="50c3f-162">Он представляет установленную надстройку, закрепленную в верхней части окна интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50c3f-162">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="50c3f-163">Этот объект предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-163">This object makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-164">**[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-164">**[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-165">**[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-165">**[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-166">**[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-166">**[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**</span></span>

##  <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="50c3f-167">**$psISE.CurrentVisibleVerticalTool**</span><span class="sxs-lookup"><span data-stu-id="50c3f-167">**$psISE.CurrentVisibleVerticalTool**</span></span>
 <span data-ttu-id="50c3f-168">Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md).</span><span class="sxs-lookup"><span data-stu-id="50c3f-168">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span> <span data-ttu-id="50c3f-169">Он представляет установленную надстройку, закрепленную в правой части окна интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50c3f-169">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="50c3f-170">Этот объект предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-170">This object makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-171">**[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-171">**[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-172">**[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-172">**[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-173">**[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-173">**[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**</span></span>

##  <a name="psiseoptions"></a><span data-ttu-id="50c3f-174">**$psISE.Options**</span><span class="sxs-lookup"><span data-stu-id="50c3f-174">**$psISE.Options**</span></span>
 <span data-ttu-id="50c3f-175">Объект **$psISE.Options** предоставляет доступ к следующим объектам для создания сценариев:</span><span class="sxs-lookup"><span data-stu-id="50c3f-175">The **$psISE.Options** object makes the following objects available for scripting:</span></span>

-   <span data-ttu-id="50c3f-176">**[$psISE.Options.AutoSaveMinuteIntervalThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-176">**[$psISE.Options.AutoSaveMinuteIntervalThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-177">**[$psISE.Options.ConsolePaneBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-177">**[$psISE.Options.ConsolePaneBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-178">**[$psISE.Options.ConsolePaneTextForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-178">**[$psISE.Options.ConsolePaneTextForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-179">**[$psISE.Options.ConsolePaneTextBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-179">**[$psISE.Options.ConsolePaneTextBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-180">**[$psISE.Options.ConsoleTokenColorsThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-180">**[$psISE.Options.ConsoleTokenColorsThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-181">**[$psISE.Options.DebugBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-181">**[$psISE.Options.DebugBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-182">**[$psISE.Options.DebugForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-182">**[$psISE.Options.DebugForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-183">**[$psISE.Options.DefaultOptions](The-ISEOptions-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-183">**[$psISE.Options.DefaultOptions](The-ISEOptions-Object.md)**</span></span>

-   <span data-ttu-id="50c3f-184">**[$psISE.Options.ErrorBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-184">**[$psISE.Options.ErrorBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-185">**[$psISE.Options.ErrorForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-185">**[$psISE.Options.ErrorForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-186">**[$psISE.Options.FontNameThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-186">**[$psISE.Options.FontNameThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-187">**[$psISE.Options.FontsizeThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-187">**[$psISE.Options.FontsizeThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-188">**[$psISE.Options.IntellisenseTimeoutInSecondsThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-188">**[$psISE.Options.IntellisenseTimeoutInSecondsThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-189">**[$psISE.Options.MRUCountThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-189">**[$psISE.Options.MRUCountThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-190">**[$psISE.Options.ScriptPaneBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-190">**[$psISE.Options.ScriptPaneBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-191">**[$psISE.Options.ScriptPaneForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-191">**[$psISE.Options.ScriptPaneForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-192">**[$psISE.Options.SelectedScriptPaneStateThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-192">**[$psISE.Options.SelectedScriptPaneStateThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-193">**[$psISE.Options.ShowDefaultSnippetsThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-193">**[$psISE.Options.ShowDefaultSnippetsThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-194">**[$psISE.Options.ShowIntellisenseInConsolePaneThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-194">**[$psISE.Options.ShowIntellisenseInConsolePaneThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-195">**[$psISE.Options.ShowIntellisenseInScriptPaneThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-195">**[$psISE.Options.ShowIntellisenseInScriptPaneThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-196">**[$psISE.Options.ShowLineNumbersThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-196">**[$psISE.Options.ShowLineNumbersThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-197">**[$psISE.Options.ShowOutliningThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-197">**[$psISE.Options.ShowOutliningThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-198">**[$psISE.Options.ShowToolBarThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-198">**[$psISE.Options.ShowToolBarThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-199">**[$psISE.Options.ShowWarningBeforeSavingOnRunThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-199">**[$psISE.Options.ShowWarningBeforeSavingOnRunThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-200">**[$psISE.Options.ShowWarningForDuplicateFilesThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-200">**[$psISE.Options.ShowWarningForDuplicateFilesThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-201">**[$psISE.Options.TokenColorsThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-201">**[$psISE.Options.TokenColorsThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-202">**[$psISE.Options.UseEnterToSelectConsolePaneIntellisenseThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-202">**[$psISE.Options.UseEnterToSelectConsolePaneIntellisenseThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-203">**[$psISE.Options. UseEnterToSelectScriptPaneIntellisenseThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-203">**[$psISE.Options. UseEnterToSelectScriptPaneIntellisenseThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-204">**[$psISE.Options.UseLocalHelpThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-204">**[$psISE.Options.UseLocalHelpThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-205">**[$psISE.Options.VerboseBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-205">**[$psISE.Options.VerboseBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-206">**[$psISE.Options.VerboseForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-206">**[$psISE.Options.VerboseForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-207">**[$psISE.Options.WarningBackgroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-207">**[$psISE.Options.WarningBackgroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-208">**[$psISE.Options.WarningForegroundColorThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-208">**[$psISE.Options.WarningForegroundColorThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-209">**[$psISE.Options.XmlTokenColorsThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-209">**[$psISE.Options.XmlTokenColorsThe-ISEOptions-Object.md]()**</span></span>

-   <span data-ttu-id="50c3f-210">**[$psISE.Options.ZoomThe-ISEOptions-Object.md]()**</span><span class="sxs-lookup"><span data-stu-id="50c3f-210">**[$psISE.Options.ZoomThe-ISEOptions-Object.md]()**</span></span>

##  <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a><span data-ttu-id="50c3f-211">**[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)**</span><span class="sxs-lookup"><span data-stu-id="50c3f-211">**[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)**</span></span>
 <span data-ttu-id="50c3f-212">Объект **$PsISE.PowerShellTabs** является экземпляром класса [PowerShellTabCollection](The-PowerShellTabCollection-Object.md).</span><span class="sxs-lookup"><span data-stu-id="50c3f-212">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span> <span data-ttu-id="50c3f-213">Это коллекция всех открытых вкладок PowerShell, представляющих доступные среды выполнения Windows PowerShell на локальном компьютере или на подключенных удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="50c3f-213">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span> <span data-ttu-id="50c3f-214">Каждый элемент в коллекции является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).</span><span class="sxs-lookup"><span data-stu-id="50c3f-214">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="50c3f-215">См. также</span><span class="sxs-lookup"><span data-stu-id="50c3f-215">See Also</span></span>
- [<span data-ttu-id="50c3f-216">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="50c3f-216">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="50c3f-217">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="50c3f-217">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)

