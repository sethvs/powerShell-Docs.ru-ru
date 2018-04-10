---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: Усовершенствования подсистемы PowerShell в WMF 5.1
ms.openlocfilehash: 3c69c4e13f64683f743eb78b0c9e177ff5b3a771
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
#<a name="powershell-engine-improvements"></a><span data-ttu-id="0489f-103">Усовершенствования подсистемы PowerShell</span><span class="sxs-lookup"><span data-stu-id="0489f-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="0489f-104">В WMF 5.1 были реализованы перечисленные ниже улучшения основной подсистемы PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0489f-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>


## <a name="performance"></a><span data-ttu-id="0489f-105">Производительность</span><span class="sxs-lookup"><span data-stu-id="0489f-105">Performance</span></span> ##

<span data-ttu-id="0489f-106">Производительность улучшена в некоторых важных аспектах:</span><span class="sxs-lookup"><span data-stu-id="0489f-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="0489f-107">Запуск</span><span class="sxs-lookup"><span data-stu-id="0489f-107">Startup</span></span>
- <span data-ttu-id="0489f-108">Передача данных по конвейеру в такие командлеты, как ForEach-Object и Where-Object, выполняется примерно на 50 % быстрее.</span><span class="sxs-lookup"><span data-stu-id="0489f-108">Pipelining to cmdlets like ForEach-Object and Where-Object is approximately 50% faster</span></span>

<span data-ttu-id="0489f-109">Примеры некоторых улучшений (результаты могут различаться в зависимости от оборудования):</span><span class="sxs-lookup"><span data-stu-id="0489f-109">Some example improvements (your results may vary depending on your hardware):</span></span>

| <span data-ttu-id="0489f-110">Сценарий</span><span class="sxs-lookup"><span data-stu-id="0489f-110">Scenario</span></span> | <span data-ttu-id="0489f-111">Время в версии 5.0 (мс)</span><span class="sxs-lookup"><span data-stu-id="0489f-111">5.0 Time (ms)</span></span> | <span data-ttu-id="0489f-112">Время в версии 5.1 (мс)</span><span class="sxs-lookup"><span data-stu-id="0489f-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="0489f-113">900</span><span class="sxs-lookup"><span data-stu-id="0489f-113">900</span></span> | <span data-ttu-id="0489f-114">250</span><span class="sxs-lookup"><span data-stu-id="0489f-114">250</span></span> |
| <span data-ttu-id="0489f-115">Самый первый запуск PowerShell: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="0489f-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="0489f-116">30 000</span><span class="sxs-lookup"><span data-stu-id="0489f-116">30000</span></span> | <span data-ttu-id="0489f-117">13 000</span><span class="sxs-lookup"><span data-stu-id="0489f-117">13000</span></span> |
| <span data-ttu-id="0489f-118">Построение кэша анализа команд: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="0489f-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="0489f-119">7000</span><span class="sxs-lookup"><span data-stu-id="0489f-119">7000</span></span> | <span data-ttu-id="0489f-120">520</span><span class="sxs-lookup"><span data-stu-id="0489f-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="0489f-121">1400</span><span class="sxs-lookup"><span data-stu-id="0489f-121">1400</span></span> | <span data-ttu-id="0489f-122">750</span><span class="sxs-lookup"><span data-stu-id="0489f-122">750</span></span> |

> <span data-ttu-id="0489f-123">Примечание. Одно из изменений, связанных с запуском, может повлиять на некоторые неподдерживаемые сценарии.</span><span class="sxs-lookup"><span data-stu-id="0489f-123">Note One change related to startup might impact some unsupported scenarios.</span></span>
> <span data-ttu-id="0489f-124">PowerShell больше не считывает файлы `$pshome\*.ps1xml` — эти файлы были преобразованы в C# во избежание накладных расходов (файловых и ресурсов ЦП), связанных с обработкой XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="0489f-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span>
<span data-ttu-id="0489f-125">Эти файлы по-прежнему существуют для поддержки параллельно установленной версии 2, поэтому изменение их содержимого сказывается только на версии 2, но не на версии 5.</span><span class="sxs-lookup"><span data-stu-id="0489f-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span>
<span data-ttu-id="0489f-126">Обратите внимание на то, что изменение содержимого этих файлов никогда не поддерживалось.</span><span class="sxs-lookup"><span data-stu-id="0489f-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="0489f-127">Еще одним явным изменением является то, как PowerShell кэширует экспортируемые команды и другую информацию для модулей, установленных в системе.</span><span class="sxs-lookup"><span data-stu-id="0489f-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span>
<span data-ttu-id="0489f-128">Ранее этот кэш хранился в каталоге `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span><span class="sxs-lookup"><span data-stu-id="0489f-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span>
<span data-ttu-id="0489f-129">В WMF 5.1 этот кэш является отдельным файлом `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="0489f-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="0489f-130">Дополнительные сведения см. в статье [Кэш анализа модуля](scenarios-features.md#module-analysis-cache).</span><span class="sxs-lookup"><span data-stu-id="0489f-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>