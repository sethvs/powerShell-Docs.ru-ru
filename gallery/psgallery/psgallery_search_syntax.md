---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: psgallery_систаксис_поиска
ms.openlocfilehash: 337b4b1e702994fcbc456eb31a2d8632f5220d09
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="7c833-103">Синтаксис поиска по коллекции</span><span class="sxs-lookup"><span data-stu-id="7c833-103">Gallery Search Syntax</span></span>

<span data-ttu-id="7c833-104">Коллекция PowerShell содержит текстовое окно поиска, где можно использовать слова, фразы и выражения с ключевыми словами, чтобы сузить результаты поиска.</span><span class="sxs-lookup"><span data-stu-id="7c833-104">PowerShell Gallery offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="7c833-105">Поиск по ключевым словам</span><span class="sxs-lookup"><span data-stu-id="7c833-105">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="7c833-106">Поисковая система пытается показать соответствующие документы, содержащие все три ключевые слова.</span><span class="sxs-lookup"><span data-stu-id="7c833-106">Search will do its best effort to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="7c833-107">Поиск с использованием ключевых слов и фраз</span><span class="sxs-lookup"><span data-stu-id="7c833-107">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="7c833-108">При вводе фразы, заключенной в кавычки (""), выполняется поиск конкретной фразы, а не отдельных ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="7c833-108">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="7c833-109">Соответствующие документы обычно содержат точную фразу azure sql, включая варианты (с другим регистром букв, например Azure SQL), а также обычно содержат слово "развертывание".</span><span class="sxs-lookup"><span data-stu-id="7c833-109">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="7c833-110">Фильтрация по полям</span><span class="sxs-lookup"><span data-stu-id="7c833-110">Filtering on fields</span></span>

<span data-ttu-id="7c833-111">Вы можете выполнять поиск конкретного идентификатора элемента (ID, Id или id) или других полей, указывая перед условиями поиска имя поля.</span><span class="sxs-lookup"><span data-stu-id="7c833-111">You can search for a specific item ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="7c833-112">В настоящее время для поиска доступны следующие поля: Id, Version, Tags, Author, Owner, Functions, Cmdlets, DscResources и PowerShellVersion.</span><span class="sxs-lookup"><span data-stu-id="7c833-112">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="7c833-113">[В чем отличие между идентификатором и заголовком?</span><span class="sxs-lookup"><span data-stu-id="7c833-113">[What's the difference between ID and Title?</span></span> <span data-ttu-id="7c833-114">Идентификатор — это имя, используемое в консоли.</span><span class="sxs-lookup"><span data-stu-id="7c833-114">ID is the name you use in the console.</span></span> <span data-ttu-id="7c833-115">Заголовок — это то, что отображается в верхней части страницы элемента в результатах поиска.]</span><span class="sxs-lookup"><span data-stu-id="7c833-115">Title is what is shown at the top of the item page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="7c833-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="7c833-116">Examples</span></span>

    ID:"PSReadline"
    id:"AzureRM.Profile"

<span data-ttu-id="7c833-117">— поиск элементов со словами PSReadline или AzureRM.Profile в поле ID;</span><span class="sxs-lookup"><span data-stu-id="7c833-117">finds items with "PSReadline" or "AzureRM.Profile" in their ID field respectively.</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="7c833-118">— еще один способ поиска элементов со словом AzureRM.Profile в поле ID.</span><span class="sxs-lookup"><span data-stu-id="7c833-118">is another way to find items with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="7c833-119">Фильтр Id — это сопоставление вложенных строк, поэтому при следующем поиске:</span><span class="sxs-lookup"><span data-stu-id="7c833-119">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="7c833-120">вы получите такие результаты, как AzureRM.Profile и Azure.Storage;</span><span class="sxs-lookup"><span data-stu-id="7c833-120">You'll get results like 'AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="7c833-121">можно также выполнить поиск с несколькими ключевыми словами в одном поле;</span><span class="sxs-lookup"><span data-stu-id="7c833-121">You can also search for multiple keywords in a single field.</span></span> <span data-ttu-id="7c833-122">вы также можете сочетать разные поля.</span><span class="sxs-lookup"><span data-stu-id="7c833-122">Or mix and match fields.</span></span>

    id:azure tags:intellisense
    id:azure id:storage

<span data-ttu-id="7c833-123">Можно выполнять поиск следующих фраз.</span><span class="sxs-lookup"><span data-stu-id="7c833-123">And you can perform phrase searches:</span></span>

    id:"azure.storage"


<span data-ttu-id="7c833-124">Чтобы найти все элементы с тегом DSC:</span><span class="sxs-lookup"><span data-stu-id="7c833-124">To search all items with DSC tag.</span></span>

    Tags:"DSC"

<span data-ttu-id="7c833-125">Чтобы найти все элементы с указанной функцией:</span><span class="sxs-lookup"><span data-stu-id="7c833-125">To search all items with the specified function.</span></span>

    Functions:"Update-AzureRM"

<span data-ttu-id="7c833-126">Чтобы найти все элементы с указанным командлетом:</span><span class="sxs-lookup"><span data-stu-id="7c833-126">To search all items with the specified cmdlet.</span></span>

    Cmdlets:"Get-AzureRmEnvironment"

<span data-ttu-id="7c833-127">Чтобы найти все элементы с указанным именем ресурса DSC:</span><span class="sxs-lookup"><span data-stu-id="7c833-127">To search all items with the specified DSC Resource name.</span></span>

    DscResources:"xArchive"

<span data-ttu-id="7c833-128">Чтобы найти все элементы с указанной версией PowerShellVersion:</span><span class="sxs-lookup"><span data-stu-id="7c833-128">To search all items with the specified PowerShellVersion</span></span>

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


<span data-ttu-id="7c833-129">Наконец, если вы используете поле, которое не поддерживается, например commands, мы просто проигнорируем его и выполним поиск по всем полям.</span><span class="sxs-lookup"><span data-stu-id="7c833-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="7c833-130">Поэтому следующий запрос</span><span class="sxs-lookup"><span data-stu-id="7c833-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="7c833-131">интерпретируется точно так же, как этот запрос:</span><span class="sxs-lookup"><span data-stu-id="7c833-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage