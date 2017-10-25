---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Управление службами"
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: 9fd6c8bcfecc99756188409629ddf94b880aab91
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-services"></a><span data-ttu-id="1f6b5-103">Управление службами</span><span class="sxs-lookup"><span data-stu-id="1f6b5-103">Managing Services</span></span>
<span data-ttu-id="1f6b5-104">Существует восемь основных командлетов Service, предназначенных для широкого спектра задач обслуживания.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="1f6b5-105">Мы рассмотрим только вывод и изменение состояния выполнения для служб, но список командлетов Service можно получить с помощью **Get-Help \&#42;-Service**, а сведения о каждом из них можно найти с помощью **Get-Help<имя_командлета>**, например **Get-Help New-Service**.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-105">We will look only at listing and changing running state for services, but you can get a list Service cmdlets by using **Get-Help \&#42;-Service**, and you can find information about each Service cmdlet by using **Get-Help<Cmdlet-Name>**, such as **Get-Help New-Service**.</span></span>

## <a name="getting-services"></a><span data-ttu-id="1f6b5-106">Получение служб</span><span class="sxs-lookup"><span data-stu-id="1f6b5-106">Getting Services</span></span>
<span data-ttu-id="1f6b5-107">Получить службы на локальном или удаленном компьютере можно с помощью командлета **Get-Service**.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-107">You can get the services on a local or remote computer by using the **Get-Service** cmdlet.</span></span> <span data-ttu-id="1f6b5-108">Как и в случае с **Get-Process**, использование команды **Get-Service** без параметров возвращает все службы.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-108">As with **Get-Process**, using the **Get-Service** command without parameters returns all services.</span></span> <span data-ttu-id="1f6b5-109">Можно фильтровать по имени, даже используя звездочку как подстановочный знак:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```
PS> Get-Service -Name se*
Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="1f6b5-110">Так как реальное имя службы не всегда очевидно, может потребоваться найти службы по отображаемому имени.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="1f6b5-111">Это можно сделать с использованием определенного имени, подстановочных знаков или списка отображаемых имен:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

```
PS> Get-Service -DisplayName se*
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center
PS> Get-Service -DisplayName ServiceLayer,Server
Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="1f6b5-112">Параметр ComputerName командлета Get-Service можно использовать для получения служб на удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="1f6b5-113">Параметр ComputerName принимает несколько значений и подстановочные знаки, что позволяет получить службы на нескольких компьютерах с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="1f6b5-114">Например, приведенная ниже команда получает службы на удаленном компьютере Server01.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="1f6b5-115">Получение необходимых и зависимых служб</span><span class="sxs-lookup"><span data-stu-id="1f6b5-115">Getting Required and Dependent Services</span></span>
<span data-ttu-id="1f6b5-116">Командлет Get-Service имеет два параметра, которые удобно использовать при администрировании служб.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="1f6b5-117">Параметр DependentServices получает службы, которые зависят от данной службы.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="1f6b5-118">Параметр RequiredServices получает службы, от которых зависит данная служба.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="1f6b5-119">Эти параметры просто отображают значения свойств DependentServices и ServicesDependedOn (псевдоним RequiredServices) объекта System.ServiceProcess.ServiceController, возвращаемого Get-Service, но они упрощают работу с командами и получение этой информации.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="1f6b5-120">Приведенная ниже команда получает службы, необходимые службе LanmanWorkstation.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices
Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="1f6b5-121">Приведенная ниже команда получает службы, которым требуется служба LanmanWorkstation.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -DependentServices
Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="1f6b5-122">Вы даже можете получить все службы, имеющие зависимости.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="1f6b5-123">Следующая команда делает именно это, а затем она использует командлет Format-Table для отображения свойств Status, Name, RequiredServices и DependentServices для служб на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```
Get-Service -Name * | where {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="1f6b5-124">Остановка, запуск, приостановка и перезапуск служб</span><span class="sxs-lookup"><span data-stu-id="1f6b5-124">Stopping, Starting, Suspending, and Restarting Services</span></span>
<span data-ttu-id="1f6b5-125">Все командлеты Service имеют схожую общую форму.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="1f6b5-126">Службы можно указать по общему имени или отображаемому имени, они также принимают списки и подстановочные знаки в качестве значений.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="1f6b5-127">Для остановки очереди печати принтера используйте:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-127">To stop the print spooler, use:</span></span>

```
Stop-Service -Name spooler
```

<span data-ttu-id="1f6b5-128">Для запуска очереди печати принтера после ее остановки используйте:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-128">To start the print spooler after it is stopped, use:</span></span>

```
Start-Service -Name spooler
```

<span data-ttu-id="1f6b5-129">Для приостановки очереди печати принтера используйте:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-129">To suspend the print spooler, use:</span></span>

```
Suspend-Service -Name spooler
```

<span data-ttu-id="1f6b5-130">Командлет **Restart-Service** работает так же, как другие командлеты Service, но для него будет приведено несколько более сложных примеров.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-130">The **Restart-Service** cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="1f6b5-131">В самом простом случае указывается имя службы:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-131">In the simplest use, you specify the name of the service:</span></span>

```
PS> Restart-Service -Name spooler
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="1f6b5-132">Вы получите повторяющееся предупреждение о запуске очереди печати принтера.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="1f6b5-133">При выполнении операции службы, занимающей некоторое время, Windows PowerShell сообщит, что по-прежнему пытается выполнить задачу.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="1f6b5-134">Если требуется перезапустить несколько служб, можно получить список служб, отфильтровать его и выполнить перезапуск:</span><span class="sxs-lookup"><span data-stu-id="1f6b5-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

```
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

<span data-ttu-id="1f6b5-135">У этих командлетов Service нет параметра ComputerName, но их можно выполнить на удаленном компьютере с помощью командлета Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="1f6b5-136">Например, приведенная ниже команда перезапускает службу очередь печати принтера на удаленном компьютере Server01.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="1f6b5-137">Задание свойств служб</span><span class="sxs-lookup"><span data-stu-id="1f6b5-137">Setting Service Properties</span></span>
<span data-ttu-id="1f6b5-138">Командлет Set-Service изменяет свойства службы на локальном или удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-138">The Set-Service cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="1f6b5-139">Так как состояние службы является свойством, этот командлет можно использовать для запуска, остановки и приостановки службы.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span> <span data-ttu-id="1f6b5-140">Командлет Set-Service также имеет параметр StartupType, позволяющий изменять тип запуска службы.</span><span class="sxs-lookup"><span data-stu-id="1f6b5-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="1f6b5-141">Чтобы использовать командлет Set-Service в Windows Vista и более поздних версиях Windows, откройте среду Windows PowerShell, используя параметр "Запуск от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="1f6b5-141">To use Set-Service on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="1f6b5-142">Дополнительные сведения см. в статье [Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3).</span><span class="sxs-lookup"><span data-stu-id="1f6b5-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="1f6b5-143">См. также</span><span class="sxs-lookup"><span data-stu-id="1f6b5-143">See Also</span></span>
- <span data-ttu-id="1f6b5-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span><span class="sxs-lookup"><span data-stu-id="1f6b5-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span></span>
- <span data-ttu-id="1f6b5-145">[Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="1f6b5-145">[Set-Service [m2]](https://technet.microsoft.com/en-us/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>
- <span data-ttu-id="1f6b5-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span><span class="sxs-lookup"><span data-stu-id="1f6b5-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span></span>
- <span data-ttu-id="1f6b5-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span><span class="sxs-lookup"><span data-stu-id="1f6b5-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span></span>

