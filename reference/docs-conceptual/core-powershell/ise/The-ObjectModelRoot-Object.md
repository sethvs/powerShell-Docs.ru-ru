---
ms.date: 08/25/2017
keywords: powershell,командлет
title: Объект ObjectModelRoot
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="233e1-103">Объект ObjectModelRoot</span><span class="sxs-lookup"><span data-stu-id="233e1-103">The ObjectModelRoot Object</span></span>

<span data-ttu-id="233e1-104">Объект **$PsISE**, который является основным корневым объектом в интегрированной среде скриптов Windows PowerShell® (ISE), — это экземпляр класса Microsoft.PowerShell.Host.ISE.ObjectModelRoot.</span><span class="sxs-lookup"><span data-stu-id="233e1-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span>
<span data-ttu-id="233e1-105">В этом разделе описаны свойства объекта **ObjectModelRoot**.</span><span class="sxs-lookup"><span data-stu-id="233e1-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="233e1-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="233e1-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="233e1-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="233e1-107">CurrentFile</span></span>

> <span data-ttu-id="233e1-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-109">Свойство только для чтения, которое получает файл, связанный с этим объектом узла, находящимся в данный момент в фокусе.</span><span class="sxs-lookup"><span data-stu-id="233e1-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="233e1-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="233e1-110">CurrentPowerShellTab</span></span>

> <span data-ttu-id="233e1-111">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-112">Свойство только для чтения, которое получает вкладку PowerShell, находящуюся в фокусе.</span><span class="sxs-lookup"><span data-stu-id="233e1-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="233e1-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="233e1-113">CurrentVisibleHorizontalTool</span></span>

> <span data-ttu-id="233e1-114">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-115">Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в горизонтальной области инструментов в нижней части редактора.</span><span class="sxs-lookup"><span data-stu-id="233e1-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="233e1-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="233e1-116">CurrentVisibleVerticalTool</span></span>

> <span data-ttu-id="233e1-117">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-118">Свойство только для чтения, которое получает видимую в данный момент надстройку интегрированной среды сценариев Windows PowerShell, которая находится в вертикальной области инструментов в правой части редактора.</span><span class="sxs-lookup"><span data-stu-id="233e1-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="233e1-119">Параметры</span><span class="sxs-lookup"><span data-stu-id="233e1-119">Options</span></span>

> <span data-ttu-id="233e1-120">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-121">Свойство только для чтения, которое получает различные параметры, изменяющие настройки в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="233e1-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="233e1-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="233e1-122">PowerShellTabs</span></span>

> <span data-ttu-id="233e1-123">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="233e1-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="233e1-124">Свойство только для чтения, которое получает коллекцию вкладок PowerShell, открытых в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="233e1-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="233e1-125">По умолчанию этот объект содержит одну вкладку PowerShell. Тем не менее можно добавить в этот объект больше вкладок PowerShell с помощью сценариев или меню в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="233e1-125">By default, this object contains one PowerShell tab. However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="233e1-126">См. также</span><span class="sxs-lookup"><span data-stu-id="233e1-126">See Also</span></span>

- [<span data-ttu-id="233e1-127">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="233e1-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="233e1-128">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="233e1-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)