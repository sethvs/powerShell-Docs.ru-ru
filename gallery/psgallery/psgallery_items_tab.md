---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "psgallery_вкладка_элементы"
ms.openlocfilehash: 8704091542de5c19817ab0b4f77fd98987084b5d
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="items-tab"></a><span data-ttu-id="60d22-103">Вкладка "Элементы"</span><span class="sxs-lookup"><span data-stu-id="60d22-103">Items Tab</span></span>

<span data-ttu-id="60d22-104">На [вкладке "Элементы"](https://www.powershellgallery.com/items) отображаются все доступные элементы в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60d22-104">The [Items tab](https://www.powershellgallery.com/items) displays all available items in the PowerShell Gallery.</span></span>

<span data-ttu-id="60d22-105">Есть несколько способов фильтрации, сортировки и поиска элементов.</span><span class="sxs-lookup"><span data-stu-id="60d22-105">There are several ways to filter, sort, and search the items.</span></span>
<span data-ttu-id="60d22-106">Чтобы узнать больше о каком-либо элементе, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="60d22-106">To see more details about a particular item, click the item.</span></span>

## <a name="filter-by"></a><span data-ttu-id="60d22-107">Фильтровать по</span><span class="sxs-lookup"><span data-stu-id="60d22-107">Filter By</span></span>

<span data-ttu-id="60d22-108">В раскрывающемся списке в разделе "Фильтровать по" можно отфильтровать результаты по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="60d22-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
* <span data-ttu-id="60d22-109">"Включить предварительные выпуски";</span><span class="sxs-lookup"><span data-stu-id="60d22-109">Include Prerelease</span></span>
* <span data-ttu-id="60d22-110">"Только стабильные".</span><span class="sxs-lookup"><span data-stu-id="60d22-110">Stable Only</span></span>

<span data-ttu-id="60d22-111">Сведения о параметрах "Предварительный выпуск" и "Стабильный" см. в статье о [добавленной функции управления предварительными выпусками в PowerShellGet и коллекции PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) в блоге команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60d22-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="60d22-112">Установив флажки в раскрывающемся списке, можно отфильтровать результаты по:</span><span class="sxs-lookup"><span data-stu-id="60d22-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
* <span data-ttu-id="60d22-113">Типы элементов</span><span class="sxs-lookup"><span data-stu-id="60d22-113">Item Types</span></span>
  - <span data-ttu-id="60d22-114">Модуль</span><span class="sxs-lookup"><span data-stu-id="60d22-114">Module</span></span>
  - <span data-ttu-id="60d22-115">Скрипт</span><span class="sxs-lookup"><span data-stu-id="60d22-115">Script</span></span>
* <span data-ttu-id="60d22-116">Категории</span><span class="sxs-lookup"><span data-stu-id="60d22-116">Categories</span></span>
  - <span data-ttu-id="60d22-117">Командлет</span><span class="sxs-lookup"><span data-stu-id="60d22-117">Cmdlet</span></span>
  - <span data-ttu-id="60d22-118">Ресурс DSC</span><span class="sxs-lookup"><span data-stu-id="60d22-118">DSC Resource</span></span>
  - <span data-ttu-id="60d22-119">Функция</span><span class="sxs-lookup"><span data-stu-id="60d22-119">Function</span></span>
  - <span data-ttu-id="60d22-120">Возможность роли</span><span class="sxs-lookup"><span data-stu-id="60d22-120">Role Capability</span></span>
  - <span data-ttu-id="60d22-121">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="60d22-121">Workflow</span></span>

<span data-ttu-id="60d22-122">Чтобы просмотреть только модули в коллекции PowerShell, щелкните "Модуль" в списке типов элементов.</span><span class="sxs-lookup"><span data-stu-id="60d22-122">To see only modules in the PowerShell Gallery, check Module in the Item Types.</span></span>
<span data-ttu-id="60d22-123">Аналогичным образом, чтобы просмотреть только скрипты в коллекции PowerShell, щелкните "Скрипт" в списке с типами элементов.</span><span class="sxs-lookup"><span data-stu-id="60d22-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Item Types.</span></span>

> [!NOTE]
> <span data-ttu-id="60d22-124">При обработке фильтрами используется инклюзивный подход.</span><span class="sxs-lookup"><span data-stu-id="60d22-124">Filters are inclusive.</span></span>
> <span data-ttu-id="60d22-125">Пример. Элемент, содержащий как командлеты, так и функции, будет отображаться как при выборе категорий "Командлет" или "Функция" (как по-отдельности, так и вместе).</span><span class="sxs-lookup"><span data-stu-id="60d22-125">Example: An item containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="60d22-126">Если ни одна из этих категорий не выбрана, элемент не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="60d22-126">If neither are selected, the item will not appear.</span></span>
> <span data-ttu-id="60d22-127">Аналогично, если выбираются все категории, будут отображаться только элементы, содержащие хотя бы одну из этих категорий.</span><span class="sxs-lookup"><span data-stu-id="60d22-127">Similarly, if all categories are selected, only items containing one of those categories will appear.</span></span>
> <span data-ttu-id="60d22-128">**Элементы, которые не принадлежат ни к одной из этих категорий, отображаться не будут.**</span><span class="sxs-lookup"><span data-stu-id="60d22-128">**Items that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="60d22-129">Сортировать по</span><span class="sxs-lookup"><span data-stu-id="60d22-129">Sort By</span></span>

<span data-ttu-id="60d22-130">Раскрывающийся список "Сортировать по" позволяет сортировать результаты по следующим параметрам:</span><span class="sxs-lookup"><span data-stu-id="60d22-130">The Sort By drop-down allows users to sort the results by:</span></span>
* <span data-ttu-id="60d22-131">"Популярность" — определяется по числу скачиваний;</span><span class="sxs-lookup"><span data-stu-id="60d22-131">Popularity - Popularity is determined by Download Count</span></span>
* <span data-ttu-id="60d22-132">A–Z — в алфавитном порядке по имени элемента;</span><span class="sxs-lookup"><span data-stu-id="60d22-132">A-Z - Alphabetically by item name</span></span>
* <span data-ttu-id="60d22-133">"Последние" — элементы располагаются в порядке даты их публикации.</span><span class="sxs-lookup"><span data-stu-id="60d22-133">Recent - Items appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="60d22-134">Поле поиска</span><span class="sxs-lookup"><span data-stu-id="60d22-134">Search Box</span></span>

<span data-ttu-id="60d22-135">Поле поиска позволяет искать элементы по ключевым словам.</span><span class="sxs-lookup"><span data-stu-id="60d22-135">The Search Box allows users to search the items on keywords.</span></span>
<span data-ttu-id="60d22-136">Дополнительные сведения см. в статье [Синтаксис поиска по коллекции](psgallery_search_syntax.md).</span><span class="sxs-lookup"><span data-stu-id="60d22-136">For more information, see [Gallery Search Syntax](psgallery_search_syntax.md).</span></span>
