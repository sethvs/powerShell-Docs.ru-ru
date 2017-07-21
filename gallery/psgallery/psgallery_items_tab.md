---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "psgallery_вкладка_элементы"
ms.openlocfilehash: 8424c4729436a78fec3fdbb405591fcd3c6bc6a6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a name="items-tab"></a><span data-ttu-id="c80e6-103">Вкладка "Элементы"</span><span class="sxs-lookup"><span data-stu-id="c80e6-103">Items Tab</span></span>
==========

<span data-ttu-id="c80e6-104">На вкладке "Элементы" отображаются все доступные элементы в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c80e6-104">The Items Tab displays all available items in the PowerShell Gallery.</span></span>

<span data-ttu-id="c80e6-105">Чтобы просмотреть только модули в коллекции PowerShell, щелкните "Модули" в раскрывающемся списке на вкладке Items "Элементы".</span><span class="sxs-lookup"><span data-stu-id="c80e6-105">To see only Modules in the PowerShell Gallery, click Modules in the Items Tab drop down.</span></span>  <span data-ttu-id="c80e6-106">Аналогично, чтобы просмотреть только скрипты в коллекции PowerShell, щелкните "Скрипты" в раскрывающемся списке на вкладке "Элементы".</span><span class="sxs-lookup"><span data-stu-id="c80e6-106">Similarly, to see only Scripts in the PowerShell Gallery, click Scripts in the Items Tab drop down.</span></span>  

<span data-ttu-id="c80e6-107">Чтобы узнать больше о каком-либо элементе, щелкните его.</span><span class="sxs-lookup"><span data-stu-id="c80e6-107">To see more details about a particular item, click the item.</span></span>

<span data-ttu-id="c80e6-108">Существует несколько способов сортировки элементов.</span><span class="sxs-lookup"><span data-stu-id="c80e6-108">There are several ways to sort the items:</span></span>

##<a name="filter-by"></a><span data-ttu-id="c80e6-109">Раздел "Фильтровать по"</span><span class="sxs-lookup"><span data-stu-id="c80e6-109">Filter By##</span></span>
<span data-ttu-id="c80e6-110">В разделе "Фильтровать по" можно отфильтровать результаты по следующим параметрам.</span><span class="sxs-lookup"><span data-stu-id="c80e6-110">The Filter By section allows users to filter the results by:</span></span>
* <span data-ttu-id="c80e6-111">Тип элемента</span><span class="sxs-lookup"><span data-stu-id="c80e6-111">Item Type:</span></span>
    * <span data-ttu-id="c80e6-112">Модули</span><span class="sxs-lookup"><span data-stu-id="c80e6-112">Modules</span></span>
    * <span data-ttu-id="c80e6-113">Сценарии</span><span class="sxs-lookup"><span data-stu-id="c80e6-113">Scripts</span></span>
* <span data-ttu-id="c80e6-114">Категория:</span><span class="sxs-lookup"><span data-stu-id="c80e6-114">Category:</span></span>
    * <span data-ttu-id="c80e6-115">Командлет</span><span class="sxs-lookup"><span data-stu-id="c80e6-115">Cmdlet</span></span>
    * <span data-ttu-id="c80e6-116">Ресурс DSC</span><span class="sxs-lookup"><span data-stu-id="c80e6-116">DSC Resource</span></span>
    * <span data-ttu-id="c80e6-117">Функция</span><span class="sxs-lookup"><span data-stu-id="c80e6-117">Function</span></span>
    * <span data-ttu-id="c80e6-118">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="c80e6-118">Workflow</span></span>

<span data-ttu-id="c80e6-119">Примечание. Фильтры находят все, в чем содержится их условие. И только это.</span><span class="sxs-lookup"><span data-stu-id="c80e6-119">Note: Filters are inclusive.</span></span>  
<span data-ttu-id="c80e6-120">Пример. Элемент, содержащий как командлеты, так и функции, будет отображаться как при выборе категорий "Командлет" или "Функция" по-отдельности, так и при выборе обеих категорий.</span><span class="sxs-lookup"><span data-stu-id="c80e6-120">Example: An item containing both Cmdlets and Functions will appear if either Cmdlet or Function (or both) are checked.</span></span>  <span data-ttu-id="c80e6-121">Если ни одна из этих категорий не выбрана, элемент не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="c80e6-121">If neither are selected, the item will not appear.</span></span>  
<span data-ttu-id="c80e6-122">Аналогично, если выбираются все категории, будут отображаться только элементы, содержащие хотя бы одну из этих категорий.</span><span class="sxs-lookup"><span data-stu-id="c80e6-122">Similarly, if all categories are selected, only items containing one of those categories will appear.</span></span> <span data-ttu-id="c80e6-123">**Элементы, которые не принадлежат ни к одной из этих категорий, отображаться не будут.**</span><span class="sxs-lookup"><span data-stu-id="c80e6-123">**Items that do not belong to any of those categories will not appear.**</span></span>

##<a name="sort-by"></a><span data-ttu-id="c80e6-124">Список "Сортировать по"</span><span class="sxs-lookup"><span data-stu-id="c80e6-124">Sort By##</span></span> 
<span data-ttu-id="c80e6-125">Раскрывающийся список "Сортировать по" позволяет сортировать результаты по следующим параметрам.</span><span class="sxs-lookup"><span data-stu-id="c80e6-125">The Sort By drop down allows users to sort the results by:</span></span>
* <span data-ttu-id="c80e6-126">"Популярность" — определяется по числу скачиваний.</span><span class="sxs-lookup"><span data-stu-id="c80e6-126">Popularity - Popularity is determined by Download Count.</span></span>
* <span data-ttu-id="c80e6-127">A–Z — в алфавитном порядке по имени элемента.</span><span class="sxs-lookup"><span data-stu-id="c80e6-127">A-Z - Alphabetically by item name.</span></span>
* <span data-ttu-id="c80e6-128">"Последние" — элементы располагаются в порядке их даты публикации.</span><span class="sxs-lookup"><span data-stu-id="c80e6-128">Recent - Items appear in order of publish date.</span></span>


##<a name="search-box"></a><span data-ttu-id="c80e6-129">Поле поиска</span><span class="sxs-lookup"><span data-stu-id="c80e6-129">Search Box##</span></span>
<span data-ttu-id="c80e6-130">Поле поиска позволяет искать элементы по ключевым словам.</span><span class="sxs-lookup"><span data-stu-id="c80e6-130">The Search Box allows users to search the items on keywords.</span></span>  
<span data-ttu-id="c80e6-131">Подробности см. в статье [Синтаксис поиска](./psgallery_search_syntax.md).</span><span class="sxs-lookup"><span data-stu-id="c80e6-131">See [Search Syntax](./psgallery_search_syntax.md) for more details.</span></span>

