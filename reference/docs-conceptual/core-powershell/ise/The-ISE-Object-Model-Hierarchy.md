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
# <a name="the-ise-object-model-hierarchy"></a>Иерархия объектной модели интегрированной среды сценариев
  В этом разделе демонстрируется иерархия объектов, которые входят в состав интегрированной среды сценариев Windows PowerShell (ISE). Интегрированная среда сценариев Windows PowerShell входит в состав Windows PowerShell 3.0 и Windows PowerShell 4.0. Щелкните объект, чтобы перейти к справочной документации для класса, определяющего объект.

##  <a name="psise-object"></a>**Объект $psISE**
 Объект **$psISE** — это [корневой объект](The-ObjectModelRoot-Object.md) иерархии объектов интегрированной среды сценариев Windows PowerShell. Располагаясь на верхнем уровне, он предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.CurrentFile]()**

-   **[$psISE.CurrentPowerShellTab]()**

-   **[$psISE.CurrentVisibleHorizontalTool]()**

-   **[$psISE.CurrentVisibleVerticalTool]()**

-   **[$psISE.Options]()**

-   **[$psISE.PowerShellTabs]()**

##  <a name="psisecurrentfilethe-isefile-objectmd"></a>**[$psISE.CurrentFile](The-ISEFile-Object.md)**
 Объект **$PsISE.CurrentFile** является экземпляром класса [ISEFile](The-ISEFile-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.CurrentFile.DisplayName](The-ISEFile-Object.md)**

-   **[$psISE.CurrentFile.Editor](The-ISEEditor-Object.md)** Этот объект является экземпляром класса [ISEEditor](The-ISEEditor-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:

    -   **[$psISE.CurrentFile.Editor.CanGoToMatch](The-ISEEditor-Object.md)**

    -   **[CaretColumn](The-ISEEditor-Object.md)**

    -   **[CaretLine](The-ISEEditor-Object.md)**

    -   **[$psISE.CurrentFile.Editor.CaretLineText](The-ISEEditor-Object.md)**

    -   **[LineCount](The-ISEEditor-Object.md)**

    -   **[SelectedText](The-ISEEditor-Object.md)**

    -   **[Text](The-ISEEditor-Object.md)**

-   **[EncodingThe-ISEFile-Object.md]()**

-   **[FullPathThe-ISEFile-Object.md]()**

-   **[IsSavedThe-ISEFile-Object.md]()**

-   **[IsUntitledThe-ISEFile-Object.md]()**

##  <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>**[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)**
 Объект **$psISE.CurrentPowerShellTab** является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.CurrentPowerShellTab.AddOnsMenu](The-ISEMenuItem-Object.md)** Этот объект является экземпляром класса [ISEMenuItem](The-ISEMenuItem-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.ActionThe-ISEMenuItem-Object.md]()**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayNameThe-ISEMenuItem-Object.md]()**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.ShortcutThe-ISEMenuItem-Object.md]()**

    -   **[$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus](The-ISEMenuItemCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.CanInvokeThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.ConsolePane](The-ISEEditor-Object.md)** Этот объект является экземпляром класса [ISEEditor](The-ISEEditor-Object.md) и предоставляет доступ к следующим объектам для создания сценариев:

    -   **[$psISE.CurrentPowerShellTab.ConsolePane.CanGoToMatchThe-ISEEditor-Object.md]()**

    -   **[CaretColumnThe-ISEEditor-Object.md]()**

    -   **[CaretLineThe-ISEEditor-Object.md]()**

    -   **[$psISE.CurrentPowerShellTab.ConsolePane.CaretLineTextThe-ISEEditor-Object.md]()**

    -   **[LineCountThe-ISEEditor-Object.md]()**

    -   **[SelectedTextThe-ISEEditor-Object.md]()**

    -   **[TextThe-ISEEditor-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.DisplayNameThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.ExpandedScriptThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.Files](The-ISEFileCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.PromptThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.ShowCommandsThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.Snippets](The-ISESnippetCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.StatusTextThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.VerticalAddOnToolsPaneOpenedThe-PowerShellTab-Object.md]()**

-   **[$psISE.CurrentPowerShellTab.VisibleHorizontalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

-   **[$psISE.CurrentPowerShellTab.VisibleVerticalAddOnTools](The-ISEAddOnToolCollection-Object.md)**

##  <a name="psisecurrentvisiblehorizontaltool"></a>**$psISE.CurrentVisibleHorizontalTool**
 Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md). Он представляет установленную надстройку, закрепленную в верхней части окна интегрированной среды сценариев Windows PowerShell. Этот объект предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**

-   **[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**

-   **[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**

##  <a name="psisecurrentvisibleverticaltool"></a>**$psISE.CurrentVisibleVerticalTool**
 Объект **$PsISE.CurrentVisibleHorizontalTool** является экземпляром класса [ISEAddOnTool](The-ISEAddOnTool-Object.md). Он представляет установленную надстройку, закрепленную в правой части окна интегрированной среды сценариев Windows PowerShell. Этот объект предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.CurrentVisibleHorizontalTool.ControlThe-ISEAddOnTool-Object.md]()**

-   **[$psISE.CurrentVisibleHorizontalTool.IsVisibleThe-ISEAddOnTool-Object.md]()**

-   **[$psISE.CurrentVisibleHorizontalTool.NameThe-ISEAddOnTool-Object.md]()**

##  <a name="psiseoptions"></a>**$psISE.Options**
 Объект **$psISE.Options** предоставляет доступ к следующим объектам для создания сценариев:

-   **[$psISE.Options.AutoSaveMinuteIntervalThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ConsolePaneBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ConsolePaneTextForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ConsolePaneTextBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ConsoleTokenColorsThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.DebugBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.DebugForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.DefaultOptions](The-ISEOptions-Object.md)**

-   **[$psISE.Options.ErrorBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ErrorForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.FontNameThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.FontsizeThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.IntellisenseTimeoutInSecondsThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.MRUCountThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ScriptPaneBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ScriptPaneForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.SelectedScriptPaneStateThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowDefaultSnippetsThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowIntellisenseInConsolePaneThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowIntellisenseInScriptPaneThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowLineNumbersThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowOutliningThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowToolBarThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowWarningBeforeSavingOnRunThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ShowWarningForDuplicateFilesThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.TokenColorsThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.UseEnterToSelectConsolePaneIntellisenseThe-ISEOptions-Object.md]()**

-   **[$psISE.Options. UseEnterToSelectScriptPaneIntellisenseThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.UseLocalHelpThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.VerboseBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.VerboseForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.WarningBackgroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.WarningForegroundColorThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.XmlTokenColorsThe-ISEOptions-Object.md]()**

-   **[$psISE.Options.ZoomThe-ISEOptions-Object.md]()**

##  <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>**[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)**
 Объект **$PsISE.PowerShellTabs** является экземпляром класса [PowerShellTabCollection](The-PowerShellTabCollection-Object.md). Это коллекция всех открытых вкладок PowerShell, представляющих доступные среды выполнения Windows PowerShell на локальном компьютере или на подключенных удаленных компьютерах. Каждый элемент в коллекции является экземпляром класса [PowerShellTab](The-PowerShellTab-Object.md).

## <a name="see-also"></a>См. также
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md)

