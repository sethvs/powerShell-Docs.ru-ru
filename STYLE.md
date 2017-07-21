# <a name="style-guide-for-powershell-docs"></a><span data-ttu-id="30cc5-101">Руководство по стилю для оформления документации PowerShell-Docs</span><span class="sxs-lookup"><span data-stu-id="30cc5-101">Style guide for PowerShell-Docs</span></span>


## <a name="titlesheadings"></a><span data-ttu-id="30cc5-102">Названия и заголовки</span><span class="sxs-lookup"><span data-stu-id="30cc5-102">Titles/Headings</span></span>

* <span data-ttu-id="30cc5-103">После названий и заголовков (всего, что начинается с \#) должна следовать новая строка.</span><span class="sxs-lookup"><span data-stu-id="30cc5-103">Titles/headings (anything preprended by \#) should be followed with a newline</span></span>
* <span data-ttu-id="30cc5-104">В заголовках с прописной следует писать только первое слово и имена собственные.</span><span class="sxs-lookup"><span data-stu-id="30cc5-104">Only the first letter of a title and any proper nouns in that title should be capitalized</span></span>
* <span data-ttu-id="30cc5-105">В документе должен быть только один заголовок H1.</span><span class="sxs-lookup"><span data-stu-id="30cc5-105">Only 1 H1 per document</span></span>
* <span data-ttu-id="30cc5-106">При редактировании справочных материалов заголовки H2 используются в соответствии с требованиями модуля platyPS. Такую структуру нельзя менять, так как это приведет к ошибкам сборки.</span><span class="sxs-lookup"><span data-stu-id="30cc5-106">When editing reference content, the H2s are prescribed by platyPS and should not be added or removed as it will cause a build break</span></span>
* <span data-ttu-id="30cc5-107">Используйте только стиль заголовков с \# (а не = или \-).</span><span class="sxs-lookup"><span data-stu-id="30cc5-107">Only use \# style headers (as opposed to = or \- style headers)</span></span>

### <a name="correct"></a><span data-ttu-id="30cc5-108">Правильно</span><span class="sxs-lookup"><span data-stu-id="30cc5-108">Correct</span></span>

```
# Header 1

## Header 2

### Header 3

```

### <a name="incorrect"></a><span data-ttu-id="30cc5-109">Неправильно</span><span class="sxs-lookup"><span data-stu-id="30cc5-109">Incorrect</span></span>

```
Header 1
========

Header 2
--------

### Header 3
```

## <a name="syntax"></a><span data-ttu-id="30cc5-110">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="30cc5-110">Syntax</span></span>

* <span data-ttu-id="30cc5-111">Описывая использование командлета в абзаце, используйте \\`, чтобы выделить его имя.</span><span class="sxs-lookup"><span data-stu-id="30cc5-111">When talking about a cmdlet in paragraph, use \\` to highlight cmdlet names</span></span>
  * <span data-ttu-id="30cc5-112">Правильный пример: командлет `Write-Host` может...</span><span class="sxs-lookup"><span data-stu-id="30cc5-112">Correct Example: This `Write-Host` Cmdlet can ...</span></span>
  * <span data-ttu-id="30cc5-113">Неправильный пример: командлет **Write-Host** может... и конвейер для сохранения данных командлета...</span><span class="sxs-lookup"><span data-stu-id="30cc5-113">Incorrect Example: This **Write-Host** Cmdlet can ... and pipeline to out-file Cmdlet to ...</span></span>
* <span data-ttu-id="30cc5-114">Оформляя статью (не справочные материалы), представляйте первый экземпляр имени командлета в виде ссылки на документацию по командлетам.</span><span class="sxs-lookup"><span data-stu-id="30cc5-114">When writing an article (as opposed to reference content), the first instance of a cmdlet name should be a link to the cmdlet documentation</span></span>
* <span data-ttu-id="30cc5-115">Во всех блоках синтаксиса нужно использовать &#96;&#96;&#96;PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30cc5-115">All PowerShell syntax blocks should use &#96;&#96;&#96;powershell</span></span>
* <span data-ttu-id="30cc5-116">Не начинайте команды PowerShell с текста "`PS C:\>`".</span><span class="sxs-lookup"><span data-stu-id="30cc5-116">Do not start PowerShell commands with "`PS C:\>`"</span></span>
  * <span data-ttu-id="30cc5-117">Правильный пример:</span><span class="sxs-lookup"><span data-stu-id="30cc5-117">Correct Example:</span></span>
  ```powershell
  Get-Process
  ```
  * <span data-ttu-id="30cc5-118">Неправильный пример:</span><span class="sxs-lookup"><span data-stu-id="30cc5-118">Incorrect Example:</span></span>
  ```powershell
  PS C:\> Get-Process
  ```
* <span data-ttu-id="30cc5-119">Выходные данные, созданные с помощью команд PowerShell, должны быть закомментированы, чтобы предотвратить выделение синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="30cc5-119">Output emitted by PowerShell commands should be commented to prevent it from recieving syntax highlighting</span></span>
* <span data-ttu-id="30cc5-120">Имена свойств и имена параметров должны быть выделены **полужирным шрифтом**.</span><span class="sxs-lookup"><span data-stu-id="30cc5-120">Property names and parameter names should be in **bold**</span></span>
* <span data-ttu-id="30cc5-121">Командлеты PowerShell: [Pascal Cased](https://en.wikipedia.org/wiki/PascalCase).</span><span class="sxs-lookup"><span data-stu-id="30cc5-121">PowerShell cmdlets are "[Pascal Cased](https://en.wikipedia.org/wiki/PascalCase)".</span></span> <span data-ttu-id="30cc5-122">Глаголы и существительные разделены дефисом.</span><span class="sxs-lookup"><span data-stu-id="30cc5-122">Verbs are seperated from nouns by a hyphen.</span></span>

## <a name="lists"></a><span data-ttu-id="30cc5-123">Списки</span><span class="sxs-lookup"><span data-stu-id="30cc5-123">Lists</span></span>

* <span data-ttu-id="30cc5-124">Не ставьте в конце элементов списка точку (только если они не содержат несколько предложений).</span><span class="sxs-lookup"><span data-stu-id="30cc5-124">Do not end list items with a period (unless they contain multiple sentences)</span></span>
* <span data-ttu-id="30cc5-125">Если список содержит несколько предложений, текст можно оформить с использованием заголовка 3/4/5 (если применимо).</span><span class="sxs-lookup"><span data-stu-id="30cc5-125">If your list contains multiple sentences, consider using a header 3/4/5 (as applicable) underneath your primary idea</span></span>

## <a name="links"></a><span data-ttu-id="30cc5-126">Ссылки</span><span class="sxs-lookup"><span data-stu-id="30cc5-126">Links</span></span>

* <span data-ttu-id="30cc5-127">Ссылки всегда отмечаются с использованием синтаксиса MarkDown `[friendlyname](url)`.</span><span class="sxs-lookup"><span data-stu-id="30cc5-127">Links are always marked up using MarkDown syntax `[friendlyname](url)`</span></span>
* <span data-ttu-id="30cc5-128">У ссылок должно быть понятное имя (если применимо); лучше всего, если это будет заголовок связанной страницы.</span><span class="sxs-lookup"><span data-stu-id="30cc5-128">Links should have a a friendly name when applicable, most likely the title of the linked page</span></span>
  * <span data-ttu-id="30cc5-129">**Исключение**: ссылки, ведущие на сторонние сайты, должны быть представлены только URL-адресами.</span><span class="sxs-lookup"><span data-stu-id="30cc5-129">**Exception**: Links going towards non-Microsoft sites should only have a URL</span></span>
* <span data-ttu-id="30cc5-130">Все элементы в разделе "Связанные ссылки" в нижней части страницы должны быть оформлены как гиперссылки.</span><span class="sxs-lookup"><span data-stu-id="30cc5-130">All items in the "related links" section at the bottom should be hyperlinked.</span></span> 

## <a name="line-breaks"></a><span data-ttu-id="30cc5-131">Разрывы строк</span><span class="sxs-lookup"><span data-stu-id="30cc5-131">Line breaks</span></span>

* <span data-ttu-id="30cc5-132">Включайте семантические разрывы строк.</span><span class="sxs-lookup"><span data-stu-id="30cc5-132">You must include semantic line breaks</span></span>
* <span data-ttu-id="30cc5-133">Длину строк нужно ограничивать 100 символами (этот вопрос открыт и требует проверки).</span><span class="sxs-lookup"><span data-stu-id="30cc5-133">You should limit lines to 100char (Open item: tooling to help us validate this)</span></span>
* <span data-ttu-id="30cc5-134">Вы МОЖЕТЕ удалять дополнительные разрывы для PS4+, но НЕ для PS3 (требуется проверка).</span><span class="sxs-lookup"><span data-stu-id="30cc5-134">You CAN remove additional line breaks for PS4+, NOT ps3 (needs validation)</span></span>
