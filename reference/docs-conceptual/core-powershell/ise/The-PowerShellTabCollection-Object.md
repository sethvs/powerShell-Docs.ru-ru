---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="40ef8-103">Объект PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="40ef8-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="40ef8-104">Объект коллекции **PowerShellTabCollection** — это коллекция объектов **PowerShellTab**.</span><span class="sxs-lookup"><span data-stu-id="40ef8-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="40ef8-105">Каждый объект **PowerShellTab** функционирует как отдельная среда выполнения.</span><span class="sxs-lookup"><span data-stu-id="40ef8-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="40ef8-106">Он является экземпляром класса Microsoft.PowerShell.Host.ISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="40ef8-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="40ef8-107">Примером является объект **$psISE.PowerShellTabs**.</span><span class="sxs-lookup"><span data-stu-id="40ef8-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="40ef8-108">Методы</span><span class="sxs-lookup"><span data-stu-id="40ef8-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="40ef8-109">Add \(\)</span><span class="sxs-lookup"><span data-stu-id="40ef8-109">Add\(\)</span></span>

<span data-ttu-id="40ef8-110">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="40ef8-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="40ef8-111">Добавляет новую вкладку PowerShell в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="40ef8-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="40ef8-112">Метод возвращает вновь добавленную вкладку.</span><span class="sxs-lookup"><span data-stu-id="40ef8-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="40ef8-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="40ef8-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="40ef8-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="40ef8-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="40ef8-115">Удаляет вкладку, которая указана параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="40ef8-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="40ef8-116">**psTab** — удаляемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40ef8-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="40ef8-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="40ef8-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="40ef8-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="40ef8-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="40ef8-119">Выбирает вкладку PowerShell, которая задается параметром **psTab**, чтобы сделать ее активной вкладкой PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40ef8-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="40ef8-120">**psTab** — выбираемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40ef8-120">**psTab** The PowerShell tab to select.</span></span>

```powershell
# Save the current tab in a variable and rename it
$oldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName = 'Old Tab'
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab = $oldTab
```

## <a name="see-also"></a><span data-ttu-id="40ef8-121">См. также</span><span class="sxs-lookup"><span data-stu-id="40ef8-121">See Also</span></span>

- [<span data-ttu-id="40ef8-122">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="40ef8-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="40ef8-123">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="40ef8-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="40ef8-124">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="40ef8-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)