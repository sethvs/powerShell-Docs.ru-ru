---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Общие сведения о конвейере Windows PowerShell"
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 6d152e52d2fcfb9dd592eb9ac40500615f2186cb
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="understanding-the-windows-powershell-pipeline"></a><span data-ttu-id="fff24-103">Общие сведения о конвейере Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fff24-103">Understanding the Windows PowerShell Pipeline</span></span>
<span data-ttu-id="fff24-104">Конвейер участвует в работе практически всех аспектов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fff24-104">Piping works virtually everywhere in Windows PowerShell.</span></span> <span data-ttu-id="fff24-105">Хотя вы видите текст на экране, Windows PowerShell не передает текст между командами.</span><span class="sxs-lookup"><span data-stu-id="fff24-105">Although you see text on the screen, Windows PowerShell does not pipe text between commands.</span></span> <span data-ttu-id="fff24-106">Вместо этого он передает объекты.</span><span class="sxs-lookup"><span data-stu-id="fff24-106">Instead, it pipes objects.</span></span>

<span data-ttu-id="fff24-107">Нотация, используемая для конвейеров, аналогична нотации в других оболочках, поэтому на первый взгляд нововведения Windows PowerShell могут остаться незамеченными.</span><span class="sxs-lookup"><span data-stu-id="fff24-107">The notation used for pipelines is similar to that used in other shells, so at first glance, it may not be apparent that Windows PowerShell introduces something new.</span></span> <span data-ttu-id="fff24-108">Например, если вы используете командлет **Out-Host** для принудительного постраничного отображения выходных данных из другой команды, на экране они имеют вид обычного текста, разбитого на страницы.</span><span class="sxs-lookup"><span data-stu-id="fff24-108">For example, if you use the **Out-Host** cmdlet to force a page-by-page display of output from another command, the output looks just like the normal text displayed on the screen, broken up into pages:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="fff24-109">Команду Out-Host -Paging удобно использовать при наличии длинных выходных данных, которые нужно отображать медленно.</span><span class="sxs-lookup"><span data-stu-id="fff24-109">The Out-Host -Paging command is a useful pipeline element whenever you have lengthy output that you would like to display slowly.</span></span> <span data-ttu-id="fff24-110">Это особенно полезно, если операция потребляет много ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="fff24-110">It is especially useful if the operation is very CPU-intensive.</span></span> <span data-ttu-id="fff24-111">Так как обработка передается в командлет Out-Host, когда в нем готова целая страница для отображения, командлеты, расположенные перед ним в конвейере, прекращают работу, пока не станет доступна следующая страница выходных данных.</span><span class="sxs-lookup"><span data-stu-id="fff24-111">Because processing is transferred to the Out-Host cmdlet when it has a complete page ready to display, cmdlets that precede it in the pipeline halt operation until the next page of output is available.</span></span> <span data-ttu-id="fff24-112">Это можно увидеть, используя диспетчер задач Windows для наблюдения за использованием Windows PowerShell ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="fff24-112">You can see this if you use the Windows Task Manager to monitor CPU and memory use by Windows PowerShell.</span></span>

<span data-ttu-id="fff24-113">Выполните следующую команду: **Get-ChildItem C:\\Windows -Recurse**.</span><span class="sxs-lookup"><span data-stu-id="fff24-113">Run the following command: **Get-ChildItem C:\\Windows -Recurse**.</span></span> <span data-ttu-id="fff24-114">Сравните использование ЦП и памяти с этой командой: **Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging**.</span><span class="sxs-lookup"><span data-stu-id="fff24-114">Compare the CPU and memory usage to this command: **Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging**.</span></span> <span data-ttu-id="fff24-115">На экране отображается текст, однако это вызвано тем, что объекты в окне консоли необходимо представлять в виде текста.</span><span class="sxs-lookup"><span data-stu-id="fff24-115">What you see on the screen is text, but that is because it is necessary to represent objects as text in a console window.</span></span> <span data-ttu-id="fff24-116">Это просто представление того, что действительно происходит внутри Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fff24-116">This is just a representation of what is really going on inside Windows PowerShell.</span></span> <span data-ttu-id="fff24-117">Рассмотрим, например, командлет Get-Location.</span><span class="sxs-lookup"><span data-stu-id="fff24-117">For example, consider the Get-Location cmdlet.</span></span> <span data-ttu-id="fff24-118">Если ввести **Get-Location**, когда текущим расположением является корень диска C, отображаются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fff24-118">If you type **Get-Location** while your current location is the root of the C drive, you would see the following output:</span></span>

```
PS> Get-Location

Path
----
C:\
```

<span data-ttu-id="fff24-119">Если Windows PowerShell передал текст по конвейеру, при выполнении такой команды, как **Get-Location | Out-Host**, из **Get-Location** в **Out-Host** передается набор знаков в порядке их отображения на экране.</span><span class="sxs-lookup"><span data-stu-id="fff24-119">If Windows PowerShell pipelined text, issuing a command such as **Get-Location | Out-Host**, would pass from **Get-Location** to **Out-Host** a set of characters in the order they are displayed onscreen.</span></span> <span data-ttu-id="fff24-120">Другими словами, если бы вы пропустили информацию заголовка, **Out-Host** сначала получает знак "**C"**, затем знак "**:"**, а затем знак "**\\"**.</span><span class="sxs-lookup"><span data-stu-id="fff24-120">In other words, if you were to ignore the heading information, **Out-Host** would first receive the character '**C'**, then the character '**:'**, then the character '**\\'**.</span></span> <span data-ttu-id="fff24-121">Командлет **Out-Host** не может определить, какое значение следует сопоставить с выходными знаками командлета **Get-Location**.</span><span class="sxs-lookup"><span data-stu-id="fff24-121">The **Out-Host** cmdlet could not determine what meaning to associate with the characters output by the **Get-Location** cmdlet.</span></span>

<span data-ttu-id="fff24-122">Для взаимодействия команд в конвейере Windows PowerShell использует объекты, а не текст.</span><span class="sxs-lookup"><span data-stu-id="fff24-122">Instead of using text to let commands in a pipeline communicate, Windows PowerShell uses objects.</span></span> <span data-ttu-id="fff24-123">С точки зрения пользователя объекты упаковывают связанные данные в форму, которая упрощает обработку информации единым блоком и извлечение нужных элементов.</span><span class="sxs-lookup"><span data-stu-id="fff24-123">From the standpoint of a user, objects package related information into a form that makes it easier to manipulate the information as a unit, and extract specific items that you need.</span></span>

<span data-ttu-id="fff24-124">Команда **Get-Location** не возвращает текст, содержащий текущий путь.</span><span class="sxs-lookup"><span data-stu-id="fff24-124">The **Get-Location** command does not return text that contains the current path.</span></span> <span data-ttu-id="fff24-125">Она возвращает пакет данных, называемый объектом **PathInfo**, который содержит текущий путь и другую информацию.</span><span class="sxs-lookup"><span data-stu-id="fff24-125">It returns a package of information called a **PathInfo** object that contains the current path along with some other information.</span></span> <span data-ttu-id="fff24-126">После этого командлет **Out-Host** отправляет объект **PathInfo** на экран, а Windows PowerShell решает, какие сведения и каким образом следует отобразить, основываясь на правилах форматирования.</span><span class="sxs-lookup"><span data-stu-id="fff24-126">The **Out-Host** cmdlet then sends this **PathInfo** object to the screen, and Windows PowerShell decides what information to display and how to display it based on its formatting rules.</span></span>

<span data-ttu-id="fff24-127">На самом деле выходные данные заголовка из командлета **Get-Location** добавляются только в конце процесса — во время форматирования данных для вывода на экран.</span><span class="sxs-lookup"><span data-stu-id="fff24-127">In fact, the heading information output by the **Get-Location** cmdlet is added only at the end of the process, as part of the process of formatting the data for onscreen display.</span></span> <span data-ttu-id="fff24-128">На экране отображаются сводные сведения, а не полное представление выходного объекта.</span><span class="sxs-lookup"><span data-stu-id="fff24-128">What you see onscreen is a summary of information, and not a complete representation of the output object.</span></span>

<span data-ttu-id="fff24-129">Учитывая, что команда Windows PowerShell может выводить больше сведений, чем отображается в окне консоли, как можно получить непоказанные элементы?</span><span class="sxs-lookup"><span data-stu-id="fff24-129">Given that there may be more information output from a Windows PowerShell command than what we see displayed in the console window, how can you retrieve the non-visible elements?</span></span> <span data-ttu-id="fff24-130">Как просмотреть дополнительные данные?</span><span class="sxs-lookup"><span data-stu-id="fff24-130">How do you view the extra data?</span></span> <span data-ttu-id="fff24-131">И что делать, если требуется просмотреть данные в формате, отличном от стандартного для Windows PowerShell?</span><span class="sxs-lookup"><span data-stu-id="fff24-131">And what if you want to view the data in a format different than the one Windows PowerShell normally uses?</span></span>

<span data-ttu-id="fff24-132">В оставшейся части этой главы описано, как определить структуру конкретных объектов Windows PowerShell, выбирая определенные элементы и форматируя их для упрощения отображения, и как отправить эти сведения в альтернативные расположения вывода, такие как файлы и принтеры.</span><span class="sxs-lookup"><span data-stu-id="fff24-132">The rest of this chapter discusses how you can discover the structure of specific Windows PowerShell objects, selecting specific items and formatting them for easier display, and how to send this information to alternative output locations such as files and printers.</span></span>

