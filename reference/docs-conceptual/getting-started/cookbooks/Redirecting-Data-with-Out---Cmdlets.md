---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Перенаправление данных с помощью командлетов Out"
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: e570ca1c2c665a4a5d23abb50d4102a012b160e9
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="redirecting-data-with-out--cmdlets"></a><span data-ttu-id="b0987-103">Перенаправление данных с помощью командлетов Out-*</span><span class="sxs-lookup"><span data-stu-id="b0987-103">Redirecting Data with Out-* Cmdlets</span></span>
<span data-ttu-id="b0987-104">Windows PowerShell предоставляет несколько командлетов, позволяющих напрямую управлять выходными данными.</span><span class="sxs-lookup"><span data-stu-id="b0987-104">Windows PowerShell provides several cmdlets that let you control data output directly.</span></span> <span data-ttu-id="b0987-105">Эти командлеты обладают двумя важными характеристиками.</span><span class="sxs-lookup"><span data-stu-id="b0987-105">These cmdlets share two important characteristics.</span></span>

<span data-ttu-id="b0987-106">Во-первых, в общем случае они преобразуют данные в некоторую форму текста.</span><span class="sxs-lookup"><span data-stu-id="b0987-106">First, they generally transform data to some form of text.</span></span> <span data-ttu-id="b0987-107">Это вызвано тем, что они выводят данные в системные компоненты, принимающие текстовые входные данные.</span><span class="sxs-lookup"><span data-stu-id="b0987-107">They do this because they output the data to system components that require text input.</span></span> <span data-ttu-id="b0987-108">Поэтому они должны представлять объекты в виде текста.</span><span class="sxs-lookup"><span data-stu-id="b0987-108">This means they need to represent the objects as text.</span></span> <span data-ttu-id="b0987-109">Таким образом, текст форматируется в том виде, в котором отображается в окне консоли Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0987-109">Therefore, the text is formatted as you see it in the Windows PowerShell console window.</span></span>

<span data-ttu-id="b0987-110">Во-вторых, эти командлеты используют глагол **Out** Windows PowerShell, так как отправляют сведения из Windows PowerShell в другое место.</span><span class="sxs-lookup"><span data-stu-id="b0987-110">Second, these cmdlets use the Windows PowerShell verb **Out** because they send information out from Windows PowerShell to somewhere else.</span></span> <span data-ttu-id="b0987-111">Командлет **Out-Host** не является исключением: отображение основного окна выходит за пределы Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0987-111">The **Out-Host** cmdlet is no exception: the host window display is outside of Windows PowerShell.</span></span> <span data-ttu-id="b0987-112">Это важно, так как при отправке данных из Windows PowerShell они фактически удаляются.</span><span class="sxs-lookup"><span data-stu-id="b0987-112">This is important because when data is sent out of Windows PowerShell, it is actually removed.</span></span> <span data-ttu-id="b0987-113">Это можно увидеть, если попытаться создать конвейер, выводящий страницы данных в основное окно, а затем попробовать отформатировать их в виде списка, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="b0987-113">You can see this if you try to create a pipeline that pages data to the host window, and then attempt to format it as a list, as shown here:</span></span>

```
PS> Get-Process | Out-Host -Paging | Format-List
```

<span data-ttu-id="b0987-114">Можно ожидать, что команда отобразит страницы сведений о процессах в формате списка.</span><span class="sxs-lookup"><span data-stu-id="b0987-114">You might expect the command to display pages of process information in list format.</span></span> <span data-ttu-id="b0987-115">Вместо этого она отображает табличный список по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="b0987-115">Instead, it displays the default tabular list:</span></span>

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="b0987-116">Командлет **Out-Host** отправляет данные непосредственно в консоль, поэтому команда **Format-List** не получает ничего для форматирования.</span><span class="sxs-lookup"><span data-stu-id="b0987-116">The **Out-Host** cmdlet sends the data directly to the console, so the **Format-List** command never receives anything to format.</span></span>

<span data-ttu-id="b0987-117">Правильный способ использования этой команды заключается в том, чтобы поместить командлет **Out-Host** в конце конвейера, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b0987-117">The correct way to structure this command is to put the **Out-Host** cmdlet at the end of the pipeline as shown below.</span></span> <span data-ttu-id="b0987-118">В результате перед разбиением на страницы и отображением данные процессов форматируются в виде списка.</span><span class="sxs-lookup"><span data-stu-id="b0987-118">This causes the process data to be formatted in a list before being paged and displayed.</span></span>

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="b0987-119">Это касается всех командлетов **Out**.</span><span class="sxs-lookup"><span data-stu-id="b0987-119">This applies to all of the **Out** cmdlets.</span></span> <span data-ttu-id="b0987-120">Командлет **Out** должен всегда находиться в конце конвейера.</span><span class="sxs-lookup"><span data-stu-id="b0987-120">An **Out** cmdlet should always appear at the end of the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="b0987-121">Все командлеты **Out** отображают выходные данные в виде текста, используя при этом действующее в окне консоли форматирование, включая ограничения длины строки.</span><span class="sxs-lookup"><span data-stu-id="b0987-121">All the **Out** cmdlets render output as text, using the formatting in effect for the console window, including line length limits.</span></span>

#### <a name="paging-console-output-out-host"></a><span data-ttu-id="b0987-122">Разбиение выходных данных консоли на страницы (Out-Host)</span><span class="sxs-lookup"><span data-stu-id="b0987-122">Paging Console Output (Out-Host)</span></span>
<span data-ttu-id="b0987-123">По умолчанию Windows PowerShell отправляет данные в основное окно. Именно это и делает командлет Out-Host.</span><span class="sxs-lookup"><span data-stu-id="b0987-123">By default, Windows PowerShell sends data to the host window, which is exactly what the Out-Host cmdlet does.</span></span> <span data-ttu-id="b0987-124">Как мы уже упоминали, основным назначением командлета Out-Host является разбиение на страницы.</span><span class="sxs-lookup"><span data-stu-id="b0987-124">The primary use for the Out-Host cmdlet is paging data as we discussed earlier.</span></span> <span data-ttu-id="b0987-125">Например, следующая команда использует Out-Host для разбиения выходных данных командлета Get-Command на страницы.</span><span class="sxs-lookup"><span data-stu-id="b0987-125">For example, the following command uses Out-Host to page the output of the Get-Command cmdlet:</span></span>

```
PS> Get-Command | Out-Host -Paging
```

<span data-ttu-id="b0987-126">Для разбиения на страницы также можно использовать функцию **more**.</span><span class="sxs-lookup"><span data-stu-id="b0987-126">You can also use the **more** function to page data.</span></span> <span data-ttu-id="b0987-127">В Windows PowerShell функция **more** вызывает **Out-Host -Paging**.</span><span class="sxs-lookup"><span data-stu-id="b0987-127">In Windows PowerShell, **more** is a function that calls **Out-Host -Paging**.</span></span> <span data-ttu-id="b0987-128">Следующая команда демонстрирует использование функции **more** для разбиения выходных данных Get-Command на страницы.</span><span class="sxs-lookup"><span data-stu-id="b0987-128">The following command demonstrates using the **more** function to page the output of Get-Command:</span></span>

```
PS> Get-Command | more
```

<span data-ttu-id="b0987-129">Если включить в функцию more одно или несколько имен файлов в качестве аргументов, она считывает указанные файлы, разбивает их содержимое на страницы и передает его на узел:</span><span class="sxs-lookup"><span data-stu-id="b0987-129">If you include one or more filenames as arguments to the more function, the function will read the specified files and page their contents to the host:</span></span>

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a><span data-ttu-id="b0987-130">Удаление выходных данных (Out-Null)</span><span class="sxs-lookup"><span data-stu-id="b0987-130">Discarding Output (Out-Null)</span></span>
<span data-ttu-id="b0987-131">Командлет **Out-Null** предназначен для немедленного удаления всех получаемых входных данных.</span><span class="sxs-lookup"><span data-stu-id="b0987-131">The **Out-Null** cmdlet is designed to immediately discard any input it receives.</span></span> <span data-ttu-id="b0987-132">Это удобно для удаления посторонних данных, получаемых при выполнении команды.</span><span class="sxs-lookup"><span data-stu-id="b0987-132">This is useful for discarding unnecessary data that you get as a side-effect of running a command.</span></span> <span data-ttu-id="b0987-133">При вводе следующей команды никакие данные не возвращаются:</span><span class="sxs-lookup"><span data-stu-id="b0987-133">When type the following command, you do not get anything back from the command:</span></span>

```
PS> Get-Command | Out-Null
```

<span data-ttu-id="b0987-134">Командлет **Out-Null** не удаляет выходные данные ошибок.</span><span class="sxs-lookup"><span data-stu-id="b0987-134">The **Out-Null** cmdlet does not discard error output.</span></span> <span data-ttu-id="b0987-135">Например, если ввести следующую команду, появляется сообщение о том, что Windows PowerShell не распознает Is-NotACommand.</span><span class="sxs-lookup"><span data-stu-id="b0987-135">For example, if you enter the following command, a message is displayed informing you that Windows PowerShell does not recognize 'Is-NotACommand':</span></span>

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a><span data-ttu-id="b0987-136">Печать данных (Out-Printer)</span><span class="sxs-lookup"><span data-stu-id="b0987-136">Printing Data (Out-Printer)</span></span>
<span data-ttu-id="b0987-137">Данные можно распечатать с помощью командлета **Out-Printer**.</span><span class="sxs-lookup"><span data-stu-id="b0987-137">You can print data by using the **Out-Printer** cmdlet.</span></span> <span data-ttu-id="b0987-138">Если имя принтера не задано, командлет **Out-Printer** использует принтер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b0987-138">The **Out-Printer** cmdlet will use your default printer if you do not provide a printer name.</span></span> <span data-ttu-id="b0987-139">Можно использовать любой принтер, совместимый с Windows, указав его отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="b0987-139">You can use any Windows-based printer by specifying its display name.</span></span> <span data-ttu-id="b0987-140">Сопоставление портов и даже наличие физического принтера при этом не требуется.</span><span class="sxs-lookup"><span data-stu-id="b0987-140">There is no need for any kind of printer port mapping or even a real physical printer.</span></span> <span data-ttu-id="b0987-141">Например, при наличии установленных средств Microsoft Office Document Imaging можно отправить данные в файл образа, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="b0987-141">For example, if you have the Microsoft Office document imaging tools installed, you can send the data to an image file by typing:</span></span>

```
PS> Get-Command Get-Command | Out-Printer -Name "Microsoft Office Document Image Writer"
```

#### <a name="saving-data-out-file"></a><span data-ttu-id="b0987-142">Сохранение данных (Out-File)</span><span class="sxs-lookup"><span data-stu-id="b0987-142">Saving Data (Out-File)</span></span>
<span data-ttu-id="b0987-143">С помощью командлета **Out-File** выходные данные можно отправить в файл, а не в окно консоли.</span><span class="sxs-lookup"><span data-stu-id="b0987-143">You can send output to a file instead of the console window by using the **Out-File** cmdlet.</span></span> <span data-ttu-id="b0987-144">Следующая команда отправляет список процессов в файл **C:\\temp\\processlist.txt**:</span><span class="sxs-lookup"><span data-stu-id="b0987-144">The following command line sends a list of processes to the file **C:\\temp\\processlist.txt**:</span></span>

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

<span data-ttu-id="b0987-145">Результаты использования командлета **Out-File** могут отличаться от ожидаемых, если вы привыкли к стандартному перенаправлению выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b0987-145">The results of using the **Out-File** cmdlet may not be what you expect if you are used to traditional output redirection.</span></span> <span data-ttu-id="b0987-146">Чтобы понять поведение командлета **Out-File**, необходимо помнить о контексте его выполнения.</span><span class="sxs-lookup"><span data-stu-id="b0987-146">To understand its behavior, you must be aware of the context in which the **Out-File** cmdlet operates.</span></span>

<span data-ttu-id="b0987-147">По умолчанию командлет **Out-File** создает файл в кодировке Юникод.</span><span class="sxs-lookup"><span data-stu-id="b0987-147">By default, the **Out-File** cmdlet creates a Unicode file.</span></span> <span data-ttu-id="b0987-148">В долгосрочной перспективе это лучший вариант по умолчанию, однако при нем средства, ожидающие файлы в кодировке ASCII, будут работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="b0987-148">This is the best default in the long run, but it means that tools that expect ASCII files will not work correctly with the default output format.</span></span> <span data-ttu-id="b0987-149">Формат вывода по умолчанию можно изменить на ASCII с помощью параметра **Encoding**:</span><span class="sxs-lookup"><span data-stu-id="b0987-149">You can change the default output format to ASCII by using the **Encoding** parameter:</span></span>

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

<span data-ttu-id="b0987-150">**Out-File** форматирует содержимое файлов, чтобы оно было похоже на выходные данные консоли.</span><span class="sxs-lookup"><span data-stu-id="b0987-150">**Out-file** formats file contents to look like console output.</span></span> <span data-ttu-id="b0987-151">В результате выходные данные усекаются, как в большинстве случаев и происходит в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="b0987-151">This causes the output to be truncated just as it is in a console window in most circumstances.</span></span> <span data-ttu-id="b0987-152">Например, если выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0987-152">For example, if you run the following command:</span></span>

```
PS> Get-Command | Out-File -FilePath c:\temp\output.txt
```

<span data-ttu-id="b0987-153">Результат будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="b0987-153">The output will look like this:</span></span>

```
CommandType     Name                            Definition                     
-----------     ----                            ----------                     
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

<span data-ttu-id="b0987-154">Чтобы получить выходные данные без принудительных переносов по словам по ширине экрана, можно использовать параметр **Width** для указания ширины строки.</span><span class="sxs-lookup"><span data-stu-id="b0987-154">To get output that does not force line wraps to match the screen width, you can use the **Width** parameter to specify line width.</span></span> <span data-ttu-id="b0987-155">Так как параметр **Width** — это 32-разрядное целое число, его максимальное значение равно 2147483647.</span><span class="sxs-lookup"><span data-stu-id="b0987-155">Because **Width** is a 32-bit integer parameter, the maximum value it can have is 2147483647.</span></span> <span data-ttu-id="b0987-156">Введите следующую команду, чтобы установить ширину строки в максимальное значение:</span><span class="sxs-lookup"><span data-stu-id="b0987-156">Type the following to set the line width to this maximum value:</span></span>

```
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

<span data-ttu-id="b0987-157">Командлет **Out-File** наиболее полезен, если требуется сохранить выходные данные в том виде, в котором они отображались бы на консоли.</span><span class="sxs-lookup"><span data-stu-id="b0987-157">The **Out-File** cmdlet is most useful when you want to save output as it would have displayed on the console.</span></span> <span data-ttu-id="b0987-158">Для более точного управления форматом выходных данных требуются более сложные средства.</span><span class="sxs-lookup"><span data-stu-id="b0987-158">For finer control over output format, you need more advanced tools.</span></span> <span data-ttu-id="b0987-159">Мы рассмотрим их в следующей главе, где приведены и дополнительные сведения о работе с объектами.</span><span class="sxs-lookup"><span data-stu-id="b0987-159">We will look at those in the next chapter, along with some details about object manipulation.</span></span>

