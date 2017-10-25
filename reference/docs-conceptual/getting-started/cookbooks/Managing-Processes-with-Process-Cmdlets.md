---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Управление процессами с помощью командлетов Process"
ms.assetid: 5038f612-d149-4698-8bbb-999986959e31
ms.openlocfilehash: 3786fb77167746d6a477dffdd4ea13e863c99964
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-processes-with-process-cmdlets"></a><span data-ttu-id="99046-103">Управление процессами с помощью командлетов Process</span><span class="sxs-lookup"><span data-stu-id="99046-103">Managing Processes with Process Cmdlets</span></span>
<span data-ttu-id="99046-104">Командлеты Process в Windows PowerShell позволяют управлять локальными и удаленными процессами в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99046-104">You can use the Process cmdlets in Windows PowerShell to manage local and remote processes in Windows PowerShell.</span></span>

## <a name="getting-processes-get-process"></a><span data-ttu-id="99046-105">Получение процессов (Get-Process)</span><span class="sxs-lookup"><span data-stu-id="99046-105">Getting Processes (Get-Process)</span></span>
<span data-ttu-id="99046-106">Для получения процессов, запущенных на локальном компьютере, выполните командет **Get-Process** без параметров.</span><span class="sxs-lookup"><span data-stu-id="99046-106">To get the processes running on the local computer, run a **Get-Process** with no parameters.</span></span>

<span data-ttu-id="99046-107">Отдельные процессы можно получить, указав их имена или идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="99046-107">You can get particular processes by specifying their process names or process IDs.</span></span> <span data-ttu-id="99046-108">Следующая команда возвращает процесс Idle:</span><span class="sxs-lookup"><span data-stu-id="99046-108">The following command gets the Idle process:</span></span>

```
PS> Get-Process -id 0
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

<span data-ttu-id="99046-109">То, что в некоторых ситуациях командлеты не возвращают данные, является нормальным. Однако если при указании процесса по его идентификатору **Get-Process** не находит совпадений, он выдает ошибку, так как стандартной целью является получение известного выполняющегося процесса.</span><span class="sxs-lookup"><span data-stu-id="99046-109">Although it is normal for cmdlets to return no data in some situations, when you specify a process by its ProcessId, **Get-Process** generates an error if it finds no matches, because the usual intent is to retrieve a known running process.</span></span> <span data-ttu-id="99046-110">Если процесс с указанным идентификатором отсутствует, весьма вероятно, что идентификатор неправильный или нужный процесс уже завершился:</span><span class="sxs-lookup"><span data-stu-id="99046-110">If there is no process with that Id, it is likely that the Id is incorrect or that the process of interest has already exited:</span></span>

```
PS> Get-Process -Id 99
Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

<span data-ttu-id="99046-111">Параметр Name командлета Get-Process можно использовать для указания подмножества процессов на основе имени процесса.</span><span class="sxs-lookup"><span data-stu-id="99046-111">You can use the Name parameter of the Get-Process cmdlet to specify a subset of processes based on the process name.</span></span> <span data-ttu-id="99046-112">Параметр Name может принимать несколько имен в виде списка с разделителями-запятыми и поддерживает использование подстановочных знаков, что позволяет задавать шаблоны имен.</span><span class="sxs-lookup"><span data-stu-id="99046-112">The Name parameter can take multiple names in a comma-separated list and it supports the use of wildcards, so you can type name patterns.</span></span>

<span data-ttu-id="99046-113">Например, следующая команда возвращает процессы, имена которых начинаются с "ex.".</span><span class="sxs-lookup"><span data-stu-id="99046-113">For example, the following command gets process whose names begin with "ex."</span></span>

```
PS> Get-Process -Name ex*
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

<span data-ttu-id="99046-114">Поскольку класс System.Diagnostics.Process .NET является основой для процессов Windows PowerShell, он удовлетворяет некоторым соглашениям, используемым System.Diagnostics.Process.</span><span class="sxs-lookup"><span data-stu-id="99046-114">Because the .NET System.Diagnostics.Process class is the foundation for Windows PowerShell processes, it follows some of the conventions used by System.Diagnostics.Process.</span></span> <span data-ttu-id="99046-115">Одно из таких соглашений требует, чтобы имя процесса для исполняемого файла никогда не содержало ".exe" в конце имени этого файла.</span><span class="sxs-lookup"><span data-stu-id="99046-115">One of those conventions is that the process name for an executable never includes the ".exe" at the end of the executable name.</span></span>

<span data-ttu-id="99046-116">**Get-Process** также принимает несколько значений для параметра Name.</span><span class="sxs-lookup"><span data-stu-id="99046-116">**Get-Process** also accepts multiple values for the Name parameter.</span></span>

```
PS> Get-Process -Name exp*,power* 
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="99046-117">Параметр ComputerName командлета Get-Process можно использовать для получения процессов на удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="99046-117">You can use the ComputerName parameter of Get-Process to get processes on remote computers.</span></span> <span data-ttu-id="99046-118">Например, следующая команда получает процессы PowerShell на локальном (представленным "localhost") и двух удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="99046-118">For example, the following command gets the PowerShell processes on the local computer (represented by "localhost") and on two remote computers.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

<span data-ttu-id="99046-119">Имена компьютеров в этих данных не указаны, однако они хранятся в свойстве MachineName объектов процесса, возвращаемых Get-Process.</span><span class="sxs-lookup"><span data-stu-id="99046-119">The computer names are not evident in this display, but they are stored in the MachineName property of the process objects that Get-Process returns.</span></span> <span data-ttu-id="99046-120">Следующая команда использует командлет Format-Table для отображения свойств ID, ProcessName и MachineName (ComputerName) объектов процесса.</span><span class="sxs-lookup"><span data-stu-id="99046-120">The following command uses the Format-Table cmdlet to display the process ID, ProcessName and MachineName (ComputerName) properties of the process objects.</span></span>

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName
  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

<span data-ttu-id="99046-121">Эта более сложная команда добавляет в стандартные отображаемые данные Get-Process свойство MachineName.</span><span class="sxs-lookup"><span data-stu-id="99046-121">This more complex command adds the MachineName property to the standard Get-Process display.</span></span> <span data-ttu-id="99046-122">Обратный апостроф (\\`) (ASCII 96) является символом продолжения Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99046-122">The backtick (\\`)(ASCII 96) is the Windows PowerShell continuation character.</span></span>

```
get-process powershell -computername localhost, Server01, Server02 | format-table -property Handles, `
                    @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}}, `
                    @{Label="PM(K)";Expression={[int]($_.PM/1024)}}, `
                    @{Label="WS(K)";Expression={[int]($_.WS/1024)}}, `
                    @{Label="VM(M)";Expression={[int]($_.VM/1MB)}}, `
                    @{Label="CPU(s)";Expression={if ($_.CPU -ne $()` 
                    {$_.CPU.ToString("N")}}}, `                                                                         
                    Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## <a name="stopping-processes-stop-process"></a><span data-ttu-id="99046-123">Остановка процессов (Stop-Process)</span><span class="sxs-lookup"><span data-stu-id="99046-123">Stopping Processes (Stop-Process)</span></span>
<span data-ttu-id="99046-124">Windows PowerShell позволяет гибко выводить списки процессов, но как обстоят дела с остановкой процесса?</span><span class="sxs-lookup"><span data-stu-id="99046-124">Windows PowerShell gives you flexibility for listing processes, but what about stopping a process?</span></span>

<span data-ttu-id="99046-125">Командлет **Stop-Process** принимает имя или идентификатор, указывающие останавливаемый процесс.</span><span class="sxs-lookup"><span data-stu-id="99046-125">The **Stop-Process** cmdlet takes a Name or Id to specify a process you want to stop.</span></span> <span data-ttu-id="99046-126">Возможность остановки процессов зависит от ваших разрешений.</span><span class="sxs-lookup"><span data-stu-id="99046-126">Your ability to stop processes depends on your permissions.</span></span> <span data-ttu-id="99046-127">Некоторые процессы остановить нельзя.</span><span class="sxs-lookup"><span data-stu-id="99046-127">Some processes cannot be stopped.</span></span> <span data-ttu-id="99046-128">Например, при попытке остановить неактивный процесс возникает ошибка:</span><span class="sxs-lookup"><span data-stu-id="99046-128">For example, if you try to stop the idle process, you get an error:</span></span>

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

<span data-ttu-id="99046-129">Можно также принудительно вывести запрос с помощью параметра **Confirm**.</span><span class="sxs-lookup"><span data-stu-id="99046-129">You can also force prompting with the **Confirm** parameter.</span></span> <span data-ttu-id="99046-130">Он особенно удобен при использовании подстановочного знака в имени процесса, так как случайно может быть определено соответствие с некоторыми процессами, которые не нужно останавливать:</span><span class="sxs-lookup"><span data-stu-id="99046-130">This parameter is particularly useful if you use a wildcard when specifying the process name, because you may accidentally match some processes you do not want to stop:</span></span>

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

<span data-ttu-id="99046-131">Сложную обработку процессов можно реализовать с помощью командлетов фильтрации объектов.</span><span class="sxs-lookup"><span data-stu-id="99046-131">Complex process manipulation is possible by using some of the object filtering cmdlets.</span></span> <span data-ttu-id="99046-132">Так как объект Process имеет свойство Responding, которое равно true, если он перестал отвечать, вы можете остановить все неотвечающие приложения с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="99046-132">Because a Process object has a Responding property that is true when it is no longer responding, you can stop all nonresponsive applications with the following command:</span></span>

```
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

<span data-ttu-id="99046-133">Аналогичный подход возможен и в других ситуациях.</span><span class="sxs-lookup"><span data-stu-id="99046-133">You can use the same approach in other situations.</span></span> <span data-ttu-id="99046-134">Предположим, например, что приложение дополнительной области уведомлений запускается автоматически при открытии другого приложения.</span><span class="sxs-lookup"><span data-stu-id="99046-134">For example, suppose a secondary notification area application automatically runs when users start another application.</span></span> <span data-ttu-id="99046-135">Эта процедура может работать неправильно в сеансах служб терминалов, однако вам все равно нужно сохранить ее в сеансах, выполняемых в консоли физического компьютера.</span><span class="sxs-lookup"><span data-stu-id="99046-135">You may find that this does not work correctly in Terminal Services sessions, but you still want to keep it in sessions that run on the physical computer console.</span></span> <span data-ttu-id="99046-136">Сеансы, подключенные к рабочему столу физического компьютера, всегда имеют идентификатор сеанса 0, поэтому можно остановить все экземпляры процесса, находящиеся в других сеансах, с помощью **Where-Object** и **SessionId** процесса:</span><span class="sxs-lookup"><span data-stu-id="99046-136">Sessions connected to the physical computer desktop always have a session ID of 0, so you can stop all instances of the process that are in other sessions by using **Where-Object** and the process, **SessionId**:</span></span>

```
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

<span data-ttu-id="99046-137">Командлет Stop-Process не использует параметр ComputerName.</span><span class="sxs-lookup"><span data-stu-id="99046-137">The Stop-Process cmdlet does not have a ComputerName parameter.</span></span> <span data-ttu-id="99046-138">Поэтому для выполнения команды остановки процесса на удаленном компьютере необходимо использовать командлет Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="99046-138">Therefore, to run a stop process command on a remote computer, you need to use the Invoke-Command cmdlet.</span></span> <span data-ttu-id="99046-139">Например, чтобы остановить процесс PowerShell на удаленном компьютере Server01, введите:</span><span class="sxs-lookup"><span data-stu-id="99046-139">For example, to stop the PowerShell process on the Server01 remote computer, type:</span></span>

```
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## <a name="stopping-all-other-windows-powershell-sessions"></a><span data-ttu-id="99046-140">Остановка всех остальных сеансов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="99046-140">Stopping All Other Windows PowerShell Sessions</span></span>
<span data-ttu-id="99046-141">В некоторых случаях может пригодиться возможность остановки всех выполняющихся сеансов Windows PowerShell, отличных от текущего.</span><span class="sxs-lookup"><span data-stu-id="99046-141">It may occasionally be useful to be able to stop all running Windows PowerShell sessions other than the current session.</span></span> <span data-ttu-id="99046-142">Если сеанс использует слишком много ресурсов или недоступен (он может выполняться удаленно или в другом сеансе), возможно, остановить его напрямую не получится.</span><span class="sxs-lookup"><span data-stu-id="99046-142">If a session is using too many resources or is inaccessible (it may be running remotely or in another desktop session), you may not be able to directly stop it.</span></span> <span data-ttu-id="99046-143">При попытке остановить все выполняющиеся сеансы может быть завершен текущий сеанс.</span><span class="sxs-lookup"><span data-stu-id="99046-143">If you try to stop all running sessions, however, the current session may be terminated instead.</span></span>

<span data-ttu-id="99046-144">Каждый сеанс Windows PowerShell имеет переменную среды PID, содержащую идентификатор процесса Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99046-144">Each Windows PowerShell session has an environment variable PID that contains the Id of the Windows PowerShell process.</span></span> <span data-ttu-id="99046-145">Можно проверить переменную $PID на наличие идентификатора каждого сеанса и завершить только сеансы Windows PowerShell с другим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="99046-145">You can check the $PID against the Id of each session and terminate only Windows PowerShell sessions that have a different Id.</span></span> <span data-ttu-id="99046-146">Следующая команда конвейера делает именно это и возвращает список завершенных сеансов (из-за использования параметра **PassThru**):</span><span class="sxs-lookup"><span data-stu-id="99046-146">The following pipeline command does this and returns the list of terminated sessions (because of the use of the **PassThru** parameter):</span></span>

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -
PassThru
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## <a name="starting-debugging-and-waiting-for-processes"></a><span data-ttu-id="99046-147">Запуск, отладка и ожидание процессов</span><span class="sxs-lookup"><span data-stu-id="99046-147">Starting, Debugging, and Waiting for Processes</span></span>
<span data-ttu-id="99046-148">Windows PowerShell также имеет командлеты для запуска (или перезапуска), отладки процесса и ожидания завершения процесса перед выполнением команды.</span><span class="sxs-lookup"><span data-stu-id="99046-148">Windows PowerShell also comes with cmdlets to start (or restart), debug a process, and wait for a process to complete before running a command.</span></span> <span data-ttu-id="99046-149">Дополнительные сведения об этих командлетах см. в разделах справки по каждому из них.</span><span class="sxs-lookup"><span data-stu-id="99046-149">For information about these cmdlets, see the cmdlet help topic for each cmdlet.</span></span>

## <a name="see-also"></a><span data-ttu-id="99046-150">См. также</span><span class="sxs-lookup"><span data-stu-id="99046-150">See Also</span></span>
- <span data-ttu-id="99046-151">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span><span class="sxs-lookup"><span data-stu-id="99046-151">[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)</span></span>
- <span data-ttu-id="99046-152">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span><span class="sxs-lookup"><span data-stu-id="99046-152">[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)</span></span>
- [<span data-ttu-id="99046-153">Start-Process</span><span class="sxs-lookup"><span data-stu-id="99046-153">Start-Process</span></span>](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
- [<span data-ttu-id="99046-154">Wait-Process</span><span class="sxs-lookup"><span data-stu-id="99046-154">Wait-Process</span></span>](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
- [<span data-ttu-id="99046-155">Debug-Process</span><span class="sxs-lookup"><span data-stu-id="99046-155">Debug-Process</span></span>](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
- [<span data-ttu-id="99046-156">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="99046-156">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)

