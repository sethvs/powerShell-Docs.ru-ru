---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ObjectModelRoot"
ms.assetid: 13fcf7ee-b18f-4499-a2b4-ccfc4484cd88
ms.openlocfilehash: 7684ccb2ca785fae539aa919e36823c1e5b86cec
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="55af3-103">Объект ObjectModelRoot</span><span class="sxs-lookup"><span data-stu-id="55af3-103">The ObjectModelRoot Object</span></span>
  <span data-ttu-id="55af3-104">Объект **$PsISE**, который является основным корневым объектом в интегрированной среде скриптов Windows PowerShell® (ISE), — это экземпляр класса Microsoft.PowerShell.Host.ISE.ObjectModelRoot.</span><span class="sxs-lookup"><span data-stu-id="55af3-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span> <span data-ttu-id="55af3-105">В этом разделе описаны свойства объекта **ObjectModelRoot**.</span><span class="sxs-lookup"><span data-stu-id="55af3-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="55af3-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="55af3-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="55af3-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="55af3-107">CurrentFile</span></span>
  <span data-ttu-id="55af3-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-109">Свойство только для чтения, которое получает файл, связанный с этим объектом узла, находящимся в данный момент в фокусе.</span><span class="sxs-lookup"><span data-stu-id="55af3-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="55af3-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="55af3-110">CurrentPowerShellTab</span></span>
  <span data-ttu-id="55af3-111">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-112">Свойство только для чтения, которое получает вкладку PowerShell, находящуюся в фокусе.</span><span class="sxs-lookup"><span data-stu-id="55af3-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="55af3-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="55af3-113">CurrentVisibleHorizontalTool</span></span>
  <span data-ttu-id="55af3-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-115">Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в горизонтальной области инструментов в нижней части редактора.</span><span class="sxs-lookup"><span data-stu-id="55af3-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="55af3-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="55af3-116">CurrentVisibleVerticalTool</span></span>
  <span data-ttu-id="55af3-117">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-118">Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в вертикальной области инструментов в правой части редактора.</span><span class="sxs-lookup"><span data-stu-id="55af3-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="55af3-119">Параметры</span><span class="sxs-lookup"><span data-stu-id="55af3-119">Options</span></span>
  <span data-ttu-id="55af3-120">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-121">Свойство только для чтения, которое получает различные параметры, изменяющие настройки в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55af3-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="55af3-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="55af3-122">PowerShellTabs</span></span>
  <span data-ttu-id="55af3-123">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="55af3-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="55af3-124">Свойство только для чтения, которое получает коллекцию вкладок PowerShell, открытых в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55af3-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="55af3-125">По умолчанию этот объект содержит одну вкладку PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55af3-125">By default, this object contains one PowerShell tab.</span></span> <span data-ttu-id="55af3-126">Тем не менее можно добавить в этот объект больше вкладок PowerShell с помощью сценариев или меню в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55af3-126">However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="55af3-127">См. также</span><span class="sxs-lookup"><span data-stu-id="55af3-127">See Also</span></span>
- [<span data-ttu-id="55af3-128">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="55af3-128">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="55af3-129">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="55af3-129">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="55af3-130">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="55af3-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
