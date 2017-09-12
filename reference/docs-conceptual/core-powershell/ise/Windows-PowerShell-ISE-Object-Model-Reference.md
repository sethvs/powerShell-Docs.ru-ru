---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Справочник по объектной модели интегрированной среды сценариев Windows PowerShell"
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
ms.openlocfilehash: 624ddca3895ba3e24bf52a27babdb07e8714baae
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="windows-powershell-ise-object-model-reference"></a><span data-ttu-id="cc277-103">Справочник по объектной модели интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc277-103">Windows PowerShell ISE Object Model Reference</span></span>
  
## <a name="object-model-reference"></a><span data-ttu-id="cc277-104">Справочник по объектной модели</span><span class="sxs-lookup"><span data-stu-id="cc277-104">Object Model Reference</span></span>
 <span data-ttu-id="cc277-105">Этот раздел содержит справку по базовым классам, определяющим различные объекты в интегрированной среде скриптов (ISE) Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="cc277-105">This section provides a reference on the underlying classes that define the various objects inWindows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="cc277-106">Упорядочение объектов в соответствии с их иерархией рассматривается в статье [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="cc277-106">To see the objects organized in their hierarchy, see [The ISE Object Model Hierarchy](The-ISE-Object-Model-Hierarchy.md).</span></span>

 <span data-ttu-id="cc277-107">[Объект ISEAddOnTool](The-ISEAddOnTool-Object.md) Примеры: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.</span><span class="sxs-lookup"><span data-stu-id="cc277-107">[The ISEAddOnTool Object](The-ISEAddOnTool-Object.md) Examples: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.</span></span>

 <span data-ttu-id="cc277-108">[Объект ISEAddOnTool](The-ISEAddOnTool-Object.md) [Объект ISEEditor](The-ISEEditor-Object.md) Примеры: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.</span><span class="sxs-lookup"><span data-stu-id="cc277-108">[The ISEAddOnTool Object](The-ISEAddOnTool-Object.md) [The ISEEditor Object](The-ISEEditor-Object.md) Examples: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.</span></span>

 <span data-ttu-id="cc277-109">[Объект ISEFile](The-ISEFile-Object.md) Примеры: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].</span><span class="sxs-lookup"><span data-stu-id="cc277-109">[The ISEFile Object](The-ISEFile-Object.md) Examples: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].</span></span>

 <span data-ttu-id="cc277-110">[Объект ISEFileCollection](The-ISEFileCollection-Object.md) Примеры: $psISE.PowerShellTabs.Files.</span><span class="sxs-lookup"><span data-stu-id="cc277-110">[The ISEFileCollection Object](The-ISEFileCollection-Object.md) Examples: $psISE.PowerShellTabs.Files.</span></span>

 <span data-ttu-id="cc277-111">[Объект ISEMenuItem](The-ISEMenuItem-Object.md) Примеры: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].</span><span class="sxs-lookup"><span data-stu-id="cc277-111">[The ISEMenuItem Object](The-ISEMenuItem-Object.md) Examples: $psISE.CurrentPowerShellTab.AddOnsMenu , $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].</span></span>

 <span data-ttu-id="cc277-112">[Объект ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md) Пример: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.</span><span class="sxs-lookup"><span data-stu-id="cc277-112">[The ISEMenuItemCollection Object](The-ISEMenuItemCollection-Object.md) Example: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.</span></span>

 <span data-ttu-id="cc277-113">[Объект ISEOptions](The-ISEOptions-Object.md) Примеры: $psISE.Options, $psISE.Options.DefaultOptions.</span><span class="sxs-lookup"><span data-stu-id="cc277-113">[The ISEOptions Object](The-ISEOptions-Object.md) Examples: $psISE.Options, $psISE.Options.DefaultOptions.</span></span>

 <span data-ttu-id="cc277-114">[Объект ObjectModelRoot](The-ObjectModelRoot-Object.md) Пример: корневой объект $psISE.</span><span class="sxs-lookup"><span data-stu-id="cc277-114">[The ObjectModelRoot Object](The-ObjectModelRoot-Object.md) Example: The root $psISE object.</span></span>

 <span data-ttu-id="cc277-115">[Объект PowerShellTab](The-PowerShellTab-Object.md) Примеры: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].</span><span class="sxs-lookup"><span data-stu-id="cc277-115">[The PowerShellTab Object](The-PowerShellTab-Object.md) Examples: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].</span></span>

 <span data-ttu-id="cc277-116">[Объект PowerShellTabCollection](The-PowerShellTabCollection-Object.md) Пример: $psISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="cc277-116">[The PowerShellTabCollection Object](The-PowerShellTabCollection-Object.md) Example: $psISE.PowerShellTabs.</span></span>

## <a name="see-also"></a><span data-ttu-id="cc277-117">См. также</span><span class="sxs-lookup"><span data-stu-id="cc277-117">See Also</span></span>
- [<span data-ttu-id="cc277-118">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc277-118">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
