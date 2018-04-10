---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="c1546-103">Объект ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="c1546-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="c1546-104">Объект **ISEAddOnToolCollection** — это коллекция объектов **ISEAddOnTool**.</span><span class="sxs-lookup"><span data-stu-id="c1546-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="c1546-105">Примером является объект **$psISE.CurrentPowerShellTab.VerticalAddOnTools**.</span><span class="sxs-lookup"><span data-stu-id="c1546-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="c1546-106">Методы</span><span class="sxs-lookup"><span data-stu-id="c1546-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="c1546-107">Add\( Name, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="c1546-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="c1546-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="c1546-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="c1546-109">Добавляет новую надстройку в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="c1546-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="c1546-110">Метод возвращает добавленную надстройку.</span><span class="sxs-lookup"><span data-stu-id="c1546-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="c1546-111">Перед выполнением этой команды необходимо установить надстройку на локальном компьютере и загрузить сборку.</span><span class="sxs-lookup"><span data-stu-id="c1546-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="c1546-112">**Name** — строка. Задает отображаемое имя надстройки, добавляемой в интегрированную среду скриптов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1546-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="c1546-113">**ControlType** — тип. Определяет добавляемый элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c1546-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="c1546-114">**\[IsVisible\]** — необязательный логический параметр. Если задано значение **$true**, надстройка сразу же отображается в связанной области инструментов.</span><span class="sxs-lookup"><span data-stu-id="c1546-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="c1546-115">Remove\( Item \)</span><span class="sxs-lookup"><span data-stu-id="c1546-115">Remove\( Item \)</span></span>

<span data-ttu-id="c1546-116">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="c1546-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="c1546-117">Удаляет указанную надстройку из коллекции.</span><span class="sxs-lookup"><span data-stu-id="c1546-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="c1546-118">**Item** — Microsoft.PowerShell.Host.ISE.ISEAddOnTool. Указывает объект, удаляемый из интегрированной среды скриптов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1546-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="c1546-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="c1546-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="c1546-120">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="c1546-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="c1546-121">Выбирает вкладку PowerShell, указанную параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="c1546-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="c1546-122">**psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Выбираемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1546-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="c1546-123">Remove\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="c1546-123">Remove\( psTab \)</span></span>

<span data-ttu-id="c1546-124">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="c1546-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="c1546-125">Удаляет вкладку PowerShell, указанную параметром **psTab**.</span><span class="sxs-lookup"><span data-stu-id="c1546-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="c1546-126">**psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Удаляемая вкладка PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1546-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="c1546-127">См. также</span><span class="sxs-lookup"><span data-stu-id="c1546-127">See Also</span></span>

- [<span data-ttu-id="c1546-128">Объект PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="c1546-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="c1546-129">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1546-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="c1546-130">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="c1546-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)