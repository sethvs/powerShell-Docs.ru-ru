---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Изменение состояния компьютера
ms.assetid: 8093268b-27f8-4a49-8871-142c5cc33f01
ms.openlocfilehash: 3d3983c6d9e9b11db62bd71805da51be83331fdb
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="changing-computer-state"></a><span data-ttu-id="72f94-103">Изменение состояния компьютера</span><span class="sxs-lookup"><span data-stu-id="72f94-103">Changing Computer State</span></span>

<span data-ttu-id="72f94-104">Чтобы сбросить компьютер в Windows PowerShell, используйте стандартную программу командной строки или класс инструментария WMI.</span><span class="sxs-lookup"><span data-stu-id="72f94-104">To reset a computer in Windows PowerShell, use either a standard command-line tool or a WMI class.</span></span> <span data-ttu-id="72f94-105">Хотя Windows PowerShell используется только для запуска программы, сведения об изменении состояния электропитания для компьютера в Windows PowerShell иллюстрируют некоторые важные особенности работы с внешними средствами в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72f94-105">Although you are using Windows PowerShell only to run the tool, learning how to change a computer's power state in Windows PowerShell illustrates some of the important details about working with external tools in Windows PowerShell.</span></span>

### <a name="locking-a-computer"></a><span data-ttu-id="72f94-106">Блокировка компьютера</span><span class="sxs-lookup"><span data-stu-id="72f94-106">Locking a Computer</span></span>

<span data-ttu-id="72f94-107">Единственным способом непосредственной блокировки компьютера с помощью стандартных средств является вызов функции **LockWorkstation()** в **user32.dll**:</span><span class="sxs-lookup"><span data-stu-id="72f94-107">The only way to lock a computer directly with the standard available tools is to call the **LockWorkstation()** function in **user32.dll**:</span></span>

```
rundll32.exe user32.dll,LockWorkStation
```

<span data-ttu-id="72f94-108">Эта команда немедленно блокирует рабочую станцию.</span><span class="sxs-lookup"><span data-stu-id="72f94-108">This command immediately locks the workstation.</span></span> <span data-ttu-id="72f94-109">Она использует *rundll32.exe*, который запускает библиотеки DLL Windows (и сохраняет их библиотеки для многократного использования), чтобы запустить user32.dll — библиотеку функций управления Windows.</span><span class="sxs-lookup"><span data-stu-id="72f94-109">It uses *rundll32.exe*, which runs Windows DLLs (and saves their libraries for repeated use) to run user32.dll, a library of Windows management functions.</span></span>

<span data-ttu-id="72f94-110">Если рабочая станция блокируется при включенном быстром переключении пользователей, например в Windows XP, компьютер отображает экран входа в систему вместо того, чтобы запустить заставку текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="72f94-110">When you lock a workstation while Fast User Switching is enabled, such as on Windows XP, the computer displays the user logon screen rather than starting the current user's screensaver.</span></span>

<span data-ttu-id="72f94-111">Чтобы завершить работу конкретных сеансов на сервере терминалов, используйте программу командной строки **tsshutdn.exe**.</span><span class="sxs-lookup"><span data-stu-id="72f94-111">To shut down particular sessions on a Terminal Server, use the **tsshutdn.exe** command-line tool.</span></span>

### <a name="logging-off-the-current-session"></a><span data-ttu-id="72f94-112">Выход из текущего сеанса</span><span class="sxs-lookup"><span data-stu-id="72f94-112">Logging Off the Current Session</span></span>

<span data-ttu-id="72f94-113">Выйти из сеанса в локальной системе можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="72f94-113">You can use several different techniques to log off of a session on the local system.</span></span> <span data-ttu-id="72f94-114">Самый простой заключается в использовании программы командной строки удаленного рабочего стола или служб терминалов — **logoff.exe** (для получения дополнительных сведений введите **logoff /?** в командной строке Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="72f94-114">The simplest way is to use the Remote Desktop/Terminal Services command-line tool, **logoff.exe** (For details, at the Windows PowerShell prompt, type **logoff /?**).</span></span> <span data-ttu-id="72f94-115">Чтобы выйти из текущего активного сеанса, введите **logoff** без аргументов.</span><span class="sxs-lookup"><span data-stu-id="72f94-115">To log off the current active session, type **logoff** with no arguments.</span></span>

<span data-ttu-id="72f94-116">Можно также использовать средство **shutdown.exe** с параметром выхода:</span><span class="sxs-lookup"><span data-stu-id="72f94-116">You can also use the **shutdown.exe** tool with its logoff option:</span></span>

```
shutdown.exe -l
```

<span data-ttu-id="72f94-117">Третий вариант — использование инструментария WMI.</span><span class="sxs-lookup"><span data-stu-id="72f94-117">A third option is to use WMI.</span></span> <span data-ttu-id="72f94-118">Класс Win32_OperatingSystem имеет метод Win32Shutdown.</span><span class="sxs-lookup"><span data-stu-id="72f94-118">The Win32_OperatingSystem class has a Win32Shutdown method.</span></span> <span data-ttu-id="72f94-119">Вызов метода с флагом 0 инициирует выход из системы:</span><span class="sxs-lookup"><span data-stu-id="72f94-119">Invoking the method with the 0 flag initiates logoff:</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(0)
```

<span data-ttu-id="72f94-120">Дополнительные сведения и другие возможности метода Win32Shutdown см. в статье Win32Shutdown Method of the Win32_OperatingSystem Class (Метод Win32Shutdown класса Win32_OperatingSystem) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="72f94-120">For more information, and to find other features of the Win32Shutdown method, see "Win32Shutdown Method of the Win32_OperatingSystem Class" in MSDN.</span></span>

### <a name="shutting-down-or-restarting-a-computer"></a><span data-ttu-id="72f94-121">Завершение работы или перезапуск компьютера</span><span class="sxs-lookup"><span data-stu-id="72f94-121">Shutting Down or Restarting a Computer</span></span>

<span data-ttu-id="72f94-122">Завершение работы и перезапуск компьютеров обычно относятся к схожим типам задач.</span><span class="sxs-lookup"><span data-stu-id="72f94-122">Shutting down and restarting computers are generally the same types of task.</span></span> <span data-ttu-id="72f94-123">Средства, завершающие работу компьютера, обычно также перезапускают его и наоборот.</span><span class="sxs-lookup"><span data-stu-id="72f94-123">Tools that shut down a computer will generally restart it as well—and vice versa.</span></span> <span data-ttu-id="72f94-124">Существует два варианта непосредственной перезагрузки компьютера из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72f94-124">There are two straightforward options for restarting a computer from Windows PowerShell.</span></span> <span data-ttu-id="72f94-125">Используйте Tsshutdn.exe или Shutdown.exe с соответствующими аргументами.</span><span class="sxs-lookup"><span data-stu-id="72f94-125">Use either Tsshutdn.exe or Shutdown.exe with appropriate arguments.</span></span> <span data-ttu-id="72f94-126">Подробные сведения об использовании можно получить, запустив **tsshutdn.exe /?**</span><span class="sxs-lookup"><span data-stu-id="72f94-126">You can get detailed usage information from **tsshutdn.exe /?**</span></span> <span data-ttu-id="72f94-127">или **shutdown.exe /?**.</span><span class="sxs-lookup"><span data-stu-id="72f94-127">or **shutdown.exe /?**.</span></span>

<span data-ttu-id="72f94-128">Для завершения работы и перезапуска можно также использовать **Win32_OperatingSystem** прямо из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72f94-128">You can also perform shutdown and restart operations by using **Win32_OperatingSystem** directly from Windows PowerShell as well.</span></span>

<span data-ttu-id="72f94-129">Чтобы завершить работу компьютера, используйте метод Win32Shutdown с флагом **1**.</span><span class="sxs-lookup"><span data-stu-id="72f94-129">To shut down the computer, use the Win32Shutdown method with the **1** flag.</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(1)
```

<span data-ttu-id="72f94-130">Чтобы перезапустить операционную систему, используйте метод Win32Shutdown с флагом **2**.</span><span class="sxs-lookup"><span data-stu-id="72f94-130">To restart the operating system, use the Win32Shutdown method with the **2** flag.</span></span>

```powershell
(Get-WmiObject -Class Win32_OperatingSystem -ComputerName .).Win32Shutdown(2)
```