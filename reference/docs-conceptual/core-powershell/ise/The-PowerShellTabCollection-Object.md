---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект PowerShellTabCollection"
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: dcdc16ae126453b6ade64917ac4950cc05e5f8ad
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="f6ed4-103">Объект PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="f6ed4-103">The PowerShellTabCollection Object</span></span>
  <span data-ttu-id="f6ed4-104">Объект коллекции **PowerShellTabCollection** — это коллекция объектов **PowerShellTab**.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="f6ed4-105">Каждый объект **PowerShellTab** функционирует как отдельная среда выполнения.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="f6ed4-106">Он является экземпляром класса Microsoft.PowerShell.Host.ISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="f6ed4-107">Примером является объект **$psISE.PowerShellTabs**.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="f6ed4-108">Методы</span><span class="sxs-lookup"><span data-stu-id="f6ed4-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="f6ed4-109">Add \(\)</span><span class="sxs-lookup"><span data-stu-id="f6ed4-109">Add\(\)</span></span>
  <span data-ttu-id="f6ed4-110">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="f6ed4-111">Добавляет новую вкладку PowerShell в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="f6ed4-112">Метод возвращает вновь добавленную вкладку.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-112">It returns the newly added tab.</span></span>

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="f6ed4-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="f6ed4-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="f6ed4-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="f6ed4-115">Удаляет вкладку, которая указана параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

 <span data-ttu-id="f6ed4-116">**psTab** — удаляемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-116">**psTab** The PowerShell tab to remove.</span></span>

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="f6ed4-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="f6ed4-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="f6ed4-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="f6ed4-119">Выбирает вкладку PowerShell, которая задается параметром **psTab**, чтобы сделать ее активной вкладкой PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

 <span data-ttu-id="f6ed4-120">**psTab** — выбираемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6ed4-120">**psTab** The PowerShell tab to select.</span></span>

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a><span data-ttu-id="f6ed4-121">См. также</span><span class="sxs-lookup"><span data-stu-id="f6ed4-121">See Also</span></span>
- [<span data-ttu-id="f6ed4-122">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="f6ed4-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="f6ed4-123">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6ed4-123">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="f6ed4-124">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6ed4-124">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="f6ed4-125">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="f6ed4-125">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  
