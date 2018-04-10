---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Устранение неполадок в DSC
ms.openlocfilehash: 6bb639febc3f413e909c3e61559059adb5c96389
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="troubleshooting-dsc"></a><span data-ttu-id="64fc8-103">Устранение неполадок в DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-103">Troubleshooting DSC</span></span>

><span data-ttu-id="64fc8-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="64fc8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="64fc8-105">В этом разделе описываются способы устранения неполадок в DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-105">This topic describes ways to troubleshoot DSC when problems arise.</span></span>

## <a name="winrm-dependency"></a><span data-ttu-id="64fc8-106">Зависимость от WinRM</span><span class="sxs-lookup"><span data-stu-id="64fc8-106">WinRM Dependency</span></span>

<span data-ttu-id="64fc8-107">Служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM.</span><span class="sxs-lookup"><span data-stu-id="64fc8-107">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="64fc8-108">По умолчанию WinRM не включен в Windows Server 2008 R2 и Windows 7.</span><span class="sxs-lookup"><span data-stu-id="64fc8-108">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="64fc8-109">Чтобы включить WinRM, выполните команду ```Set-WSManQuickConfig``` в сеансе Windows PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="64fc8-109">Run ```Set-WSManQuickConfig```, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="using-get-dscconfigurationstatus"></a><span data-ttu-id="64fc8-110">Использование Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="64fc8-110">Using Get-DscConfigurationStatus</span></span>

<span data-ttu-id="64fc8-111">Командлет [Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) получает сведения о состоянии конфигурации с целевого узла.</span><span class="sxs-lookup"><span data-stu-id="64fc8-111">The [Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) cmdlet gets information about configuration status from a target node.</span></span>
<span data-ttu-id="64fc8-112">Возвращается расширенный объект, который содержит высокоуровневые сведения о том, было ли выполнение конфигурации успешным.</span><span class="sxs-lookup"><span data-stu-id="64fc8-112">A rich object is returned that includes high-level information about whether or not the configuration run was successful or not.</span></span> <span data-ttu-id="64fc8-113">Можно детализировать объект для получения сведений о запуске конфигурации, например следующие.</span><span class="sxs-lookup"><span data-stu-id="64fc8-113">You can dig into the object to discover details about the configuration run such as:</span></span>

* <span data-ttu-id="64fc8-114">Все ресурсы, для которых возник сбой</span><span class="sxs-lookup"><span data-stu-id="64fc8-114">All of the resources that failed</span></span>
* <span data-ttu-id="64fc8-115">Любые ресурсы, запросившие перезагрузку</span><span class="sxs-lookup"><span data-stu-id="64fc8-115">Any resource that requested a reboot</span></span>
* <span data-ttu-id="64fc8-116">Параметры метаконфигурации во время выполнения конфигурации</span><span class="sxs-lookup"><span data-stu-id="64fc8-116">Meta-Configuration settings at time of configuration run</span></span>
* <span data-ttu-id="64fc8-117">Прочее</span><span class="sxs-lookup"><span data-stu-id="64fc8-117">Etc.</span></span>

<span data-ttu-id="64fc8-118">Следующий набор параметров возвращает сведения о состоянии для последнего выполнения конфигурации:</span><span class="sxs-lookup"><span data-stu-id="64fc8-118">The following parameter set returns the status information for the last configuration run:</span></span>

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>]
                            [-ThrottleLimit <int>]
                            [-AsJob]
                            [<CommonParameters>]
```
<span data-ttu-id="64fc8-119">Следующий набор параметров возвращает сведения о состоянии для всех предыдущих выполнений конфигурации:</span><span class="sxs-lookup"><span data-stu-id="64fc8-119">The following parameter set returns the status information for all previous configuration runs:</span></span>

```powershell
Get-DscConfigurationStatus  -All
                            [-CimSession <CimSession[]>]
                            [-ThrottleLimit <int>]
                            [-AsJob]
                            [<CommonParameters>]
```

## <a name="example"></a><span data-ttu-id="64fc8-120">Пример</span><span class="sxs-lookup"><span data-stu-id="64fc8-120">Example</span></span>

```powershell
PS C:\> $Status = Get-DscConfigurationStatus

PS C:\> $Status

Status      StartDate               Type            Mode    RebootRequested     NumberOfResources
------      ---------               ----            ----    ---------------     -----------------
Failure     11/24/2015  3:44:56     Consistency     Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName       :   MyService
DependsOn               :
ModuleName              :   PSDesiredStateConfiguration
ModuleVersion           :   1.1
PsDscRunAsCredential    :
ResourceID              :   [File]ServiceDll
SourceInfo              :   c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds       :   0.19
Error                   :   SourcePath must be accessible for current configuration. The related file/directory is:
                            \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState              :
InDesiredState          :   False
InitialState            :
InstanceName            :   ServiceDll
RebootRequested         :   False
ReosurceName            :   File
StartDate               :   11/24/2015  3:44:56
PSComputerName          :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a><span data-ttu-id="64fc8-121">Мой сценарий не запускается: диагностика ошибок в сценариях с помощью журналов DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-121">My script won’t run: Using DSC logs to diagnose script errors</span></span>

<span data-ttu-id="64fc8-122">Как и все программное обеспечение Windows, DSC записывает ошибки и события в [журналы](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , которые можно просмотреть в [средстве просмотра событий](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).</span><span class="sxs-lookup"><span data-stu-id="64fc8-122">Like all Windows software, DSC records errors and events in [logs](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) that can be viewed from the [Event Viewer](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).</span></span> <span data-ttu-id="64fc8-123">Анализ этих журналов может помочь в выявлении причины сбоя конкретной операции и избежать его в будущем.</span><span class="sxs-lookup"><span data-stu-id="64fc8-123">Examining these logs can help you understand why a particular operation failed, and how to prevent failure in the future.</span></span> <span data-ttu-id="64fc8-124">Написание сценариев настройки может быть непростой задачей. Чтобы упростить отслеживание ошибок, используйте ресурс журнала DSC, чтобы ход конфигурации отражался в аналитическом журнале событий DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-124">Writing configuration scripts can be tricky, so to make tracking errors easier as you author, use the DSC Log resource to track the progress of your configuration in the DSC Analytic event log.</span></span>

## <a name="where-are-dsc-event-logs"></a><span data-ttu-id="64fc8-125">Где находятся журналы событий DSC?</span><span class="sxs-lookup"><span data-stu-id="64fc8-125">Where are DSC event logs?</span></span>

<span data-ttu-id="64fc8-126">В средстве просмотра событий события DSC находятся в следующем разделе: **Журналы служб и приложений/Microsoft/Windows/Настройка требуемого состояния**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-126">In Event Viewer, DSC events are in: **Applications and Services Logs/Microsoft/Windows/Desired State Configuration**</span></span>

<span data-ttu-id="64fc8-127">Кроме того, для просмотра журналов событий можно запустить соответствующий командлет PowerShell [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx):</span><span class="sxs-lookup"><span data-stu-id="64fc8-127">The corresponding PowerShell cmdlet, [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), can also be run to view the event logs:</span></span>

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

<span data-ttu-id="64fc8-128">Как показано выше, основное имя журнала DSC — **Microsoft->Windows->DSC** (другие имена журналов в Windows для краткости здесь не показаны).</span><span class="sxs-lookup"><span data-stu-id="64fc8-128">As shown above, DSC’s primary log name is **Microsoft->Windows->DSC** (other log names under Windows are not shown here for brevity).</span></span> <span data-ttu-id="64fc8-129">Основное имя журнала добавляется к имени канала для получения полного имени журнала.</span><span class="sxs-lookup"><span data-stu-id="64fc8-129">The primary name is appended to the channel name to create the complete log name.</span></span> <span data-ttu-id="64fc8-130">DSC производит запись преимущественно в журналы трех типов: [операционные, аналитические и отладочные](https://technet.microsoft.com/library/cc722404.aspx).</span><span class="sxs-lookup"><span data-stu-id="64fc8-130">The DSC engine writes mainly into three types of logs: [Operational, Analytic, and Debug logs](https://technet.microsoft.com/library/cc722404.aspx).</span></span> <span data-ttu-id="64fc8-131">Так как аналитический и отладочный журналы по умолчанию отключены, их следует включить в средстве просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="64fc8-131">Since the analytic and debug logs are turned off by default, you should enable them in Event Viewer.</span></span> <span data-ttu-id="64fc8-132">Чтобы сделать это, откройте средство просмотра событий, введя "Show-EventLog" в Windows PowerShell или нажав кнопку **Пуск** и выбрав пункты **Панель управления**, **Администрирование** и **Средство просмотра событий**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-132">To do this, open Event Viewer by typing Show-EventLog in Windows PowerShell; or, click the **Start** button, click **Control Panel**, click **Administrative Tools**, and then click **Event Viewer**.</span></span> <span data-ttu-id="64fc8-133">В средстве просмотра событий в меню **Представление** выберите команду **Показать аналитический и отладочный журналы**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-133">On the **View** menu in Event viewer, click **Show Analytic and Debug Logs**.</span></span> <span data-ttu-id="64fc8-134">Имя журнала для аналитического канала — **Microsoft-Windows-Dsc/Analytic**, для отладочного канала — **Microsoft-Windows-Dsc/Debug**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-134">The log name for the analytic channel is **Microsoft-Windows-Dsc/Analytic**, and the debug channel is **Microsoft-Windows-Dsc/Debug**.</span></span> <span data-ttu-id="64fc8-135">Кроме того, для включения журналов можно воспользоваться средством [wevtutil](https://technet.microsoft.com/library/cc732848.aspx), как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="64fc8-135">You could also use the [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) utility to enable the logs, as shown in the following example.</span></span>

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a><span data-ttu-id="64fc8-136">Что содержат журналы DSC?</span><span class="sxs-lookup"><span data-stu-id="64fc8-136">What do DSC logs contain?</span></span>

<span data-ttu-id="64fc8-137">Журналы DSC разделяются на три канала в зависимости от важности сообщения.</span><span class="sxs-lookup"><span data-stu-id="64fc8-137">DSC logs are split over the three log channels based on the importance of the message.</span></span> <span data-ttu-id="64fc8-138">Операционный журнал в DSC содержит все сообщения об ошибках и может использоваться для выявления проблем.</span><span class="sxs-lookup"><span data-stu-id="64fc8-138">The operational log in DSC contains all error messages, and can be used to identify a problem.</span></span> <span data-ttu-id="64fc8-139">Аналитический журнал содержит больше событий, и с его помощью можно определить, где произошли ошибки.</span><span class="sxs-lookup"><span data-stu-id="64fc8-139">The analytic log has a higher volume of events, and can identify where error(s) occurred.</span></span> <span data-ttu-id="64fc8-140">Кроме того, этот канал содержит подробные сообщения (если они имеются).</span><span class="sxs-lookup"><span data-stu-id="64fc8-140">This channel also contains verbose messages (if any).</span></span> <span data-ttu-id="64fc8-141">Отладочный журнал помогает понять, как произошли ошибки.</span><span class="sxs-lookup"><span data-stu-id="64fc8-141">The debug log contains logs that can help you understand how the errors occurred.</span></span> <span data-ttu-id="64fc8-142">Сообщения о событиях DSC структурированы таким образом, что каждое сообщение о событии начинается с идентификатора задания, который уникальным образом представляет операцию DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-142">DSC event messages are structured such that every event message begins with a job ID that uniquely represents a DSC operation.</span></span> <span data-ttu-id="64fc8-143">В приведенном ниже примере предпринимается попытка получить сообщение из первого события, записанного в операционный журнал DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-143">The example below attempts to obtain the message from the first event logged into the operational DSC log.</span></span>

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

<span data-ttu-id="64fc8-144">События DSC записываются в определенной структуре, что позволяет пользователю собрать все события из одного задания DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-144">DSC events are logged in a particular structure that enables the user to aggregate events from one DSC job.</span></span> <span data-ttu-id="64fc8-145">Эта структура выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64fc8-145">The structure is as follows:</span></span>

<span data-ttu-id="64fc8-146">**Идентификатор задания: <Guid>**
**<Event Message>**</span><span class="sxs-lookup"><span data-stu-id="64fc8-146">**Job ID : <Guid>**
**<Event Message>**</span></span>

## <a name="gathering-events-from-a-single-dsc-operation"></a><span data-ttu-id="64fc8-147">Сбор событий для отдельной операции DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-147">Gathering events from a single DSC operation</span></span>

<span data-ttu-id="64fc8-148">Журналы событий DSC содержат события, созданные при выполнении различных операций DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-148">DSC event logs contain events generated by various DSC operations.</span></span> <span data-ttu-id="64fc8-149">Однако обычно вас интересуют сведения только для одной конкретной операции.</span><span class="sxs-lookup"><span data-stu-id="64fc8-149">However, you’ll usually be concerned with the detail about just one particular operation.</span></span> <span data-ttu-id="64fc8-150">Все журналы DSC можно группировать по свойству ID задания, которое является уникальным для каждой операции DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-150">All DSC logs can be grouped by the job ID property that is unique for every DSC operation.</span></span> <span data-ttu-id="64fc8-151">Идентификатор задания отображается в виде первого значения свойства во всех событиях DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-151">The job ID is displayed as the first property value in all DSC events.</span></span> <span data-ttu-id="64fc8-152">Далее описывается процесс сбора всех событий в структуре сгруппированного массива.</span><span class="sxs-lookup"><span data-stu-id="64fc8-152">The following steps explain how to accumulate all events in a grouped array structure.</span></span>

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>

wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true

<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>

Get-DscLocalConfigurationManager

<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>

$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)


<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}
```

<span data-ttu-id="64fc8-153">Здесь переменная `$SeparateDscOperations` содержит журналы, сгруппированные по идентификаторам заданий.</span><span class="sxs-lookup"><span data-stu-id="64fc8-153">Here, the variable `$SeparateDscOperations` contains logs grouped by the job IDs.</span></span> <span data-ttu-id="64fc8-154">Каждый элемент массива этой переменной представляет группу событий, записанных различными операциями DSC, что позволяет получить дополнительные сведения о журналах.</span><span class="sxs-lookup"><span data-stu-id="64fc8-154">Each array element of this variable represents a group of events logged by a different DSC operation, allowing access to more information about the logs.</span></span>

```
PS C:\> $SeparateDscOperations

Count Name                      Group
----- ----                      -----
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
PS C:\> $SeparateDscOperations[0].Group
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
```

<span data-ttu-id="64fc8-155">С помощью [Where-Object](https://technet.microsoft.com/library/ee177028.aspx) можно извлечь данные в переменную `$SeparateDscOperations`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-155">You can extract the data in the variable `$SeparateDscOperations` using [Where-Object](https://technet.microsoft.com/library/ee177028.aspx).</span></span> <span data-ttu-id="64fc8-156">Ниже приведены пять ситуаций, в которых может потребоваться извлечь данные для устранения неполадок DSC:</span><span class="sxs-lookup"><span data-stu-id="64fc8-156">Following are five scenarios in which you might want to extract data for troubleshooting DSC:</span></span>

### <a name="1-operations-failures"></a><span data-ttu-id="64fc8-157">1. Сбой при выполнении операции</span><span class="sxs-lookup"><span data-stu-id="64fc8-157">1: Operations failures</span></span>

<span data-ttu-id="64fc8-158">Все события имеют [уровни серьезности](https://msdn.microsoft.com/library/dd996917(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="64fc8-158">All events have [severity levels](https://msdn.microsoft.com/library/dd996917(v=vs.85)).</span></span> <span data-ttu-id="64fc8-159">С помощью этих сведений можно определить события с ошибкой:</span><span class="sxs-lookup"><span data-stu-id="64fc8-159">This information can be used to identify the error events:</span></span>

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a><span data-ttu-id="64fc8-160">2. Подробные сведения об операциях за последние полчаса</span><span class="sxs-lookup"><span data-stu-id="64fc8-160">2: Details of operations run in the last half hour</span></span>

<span data-ttu-id="64fc8-161">`TimeCreated`, свойство каждого события Windows, содержит время создания события.</span><span class="sxs-lookup"><span data-stu-id="64fc8-161">`TimeCreated`, a property of every Windows event, states the time the event was created.</span></span> <span data-ttu-id="64fc8-162">Для фильтрации событий можно сравнить это свойство с конкретным объектом даты и времени:</span><span class="sxs-lookup"><span data-stu-id="64fc8-162">Comparing this property with a particular date/time object can be used to filter all events:</span></span>

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a><span data-ttu-id="64fc8-163">3. Сообщения последней операции</span><span class="sxs-lookup"><span data-stu-id="64fc8-163">3: Messages from the latest operation</span></span>

<span data-ttu-id="64fc8-164">Последняя операция хранится по первому индексу в группе массива `$SeparateDscOperations`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-164">The latest operation is stored in the first index of the array group `$SeparateDscOperations`.</span></span> <span data-ttu-id="64fc8-165">При запросе сообщений группы для индекса 0 возвращаются всех сообщения для последней операции:</span><span class="sxs-lookup"><span data-stu-id="64fc8-165">Querying the group’s messages for index 0 returns all messages for the latest operation:</span></span>

```powershelll
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Consistency check completed.
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a><span data-ttu-id="64fc8-166">4. Сообщения об ошибках в журнале для последних неудачных операций</span><span class="sxs-lookup"><span data-stu-id="64fc8-166">4: Error messages logged for recent failed operations</span></span>

<span data-ttu-id="64fc8-167">`$SeparateDscOperations[0].Group` содержит набор событий для последней операции.</span><span class="sxs-lookup"><span data-stu-id="64fc8-167">`$SeparateDscOperations[0].Group` contains a set of events for the latest operation.</span></span> <span data-ttu-id="64fc8-168">Запустите командлет `Where-Object` для фильтрации событий в зависимости от их отображаемого уровня.</span><span class="sxs-lookup"><span data-stu-id="64fc8-168">Run the `Where-Object` cmdlet to filter the events based on their level display name.</span></span> <span data-ttu-id="64fc8-169">Результаты сохраняются в переменной `$myFailedEvent`, которую можно разделить на составные части для получения сообщения о событии:</span><span class="sxs-lookup"><span data-stu-id="64fc8-169">Results are stored in the `$myFailedEvent` variable, which can be further dissected to get the event message:</span></span>

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})

PS C:\> $myFailedEvent.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
DSC Engine Error :
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first.
Error Code : 1
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a><span data-ttu-id="64fc8-170">5. Все события, созданные для идентификатора конкретного задания</span><span class="sxs-lookup"><span data-stu-id="64fc8-170">5: All events generated for a particular job ID.</span></span>

<span data-ttu-id="64fc8-171">`$SeparateDscOperations` представляет собой массив групп, каждая из которых имеет имя, являющееся уникальным идентификатором задания.</span><span class="sxs-lookup"><span data-stu-id="64fc8-171">`$SeparateDscOperations` is an array of groups, each of which has the name as the unique job ID.</span></span> <span data-ttu-id="64fc8-172">Запустив командлет `Where-Object`, можно извлечь группы событий, которые имеют идентификатор конкретного задания:</span><span class="sxs-lookup"><span data-stu-id="64fc8-172">By running the `Where-Object` cmdlet, you can extract those groups of events that have a particular job ID:</span></span>

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a><span data-ttu-id="64fc8-173">Анализ журналов DSC с помощью xDscDiagnostics</span><span class="sxs-lookup"><span data-stu-id="64fc8-173">Using xDscDiagnostics to analyze DSC logs</span></span>

<span data-ttu-id="64fc8-174">**xDscDiagnostics** представляет собой модуль PowerShell, состоящий из нескольких простых функций, которые могут помочь в анализе сбоев DSC на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="64fc8-174">**xDscDiagnostics** is a PowerShell module that consists of several functions that can help analyze DSC failures on your machine.</span></span> <span data-ttu-id="64fc8-175">Эти функции помогают идентифицировать все локальные события для последних операций DSC или событий DSC на удаленных компьютерах (с действительными учетными данными).</span><span class="sxs-lookup"><span data-stu-id="64fc8-175">These functions can help you identify all local events from past DSC operations, or DSC events on remote computers (with valid credentials).</span></span> <span data-ttu-id="64fc8-176">В данном случае термин "операция DSC" используется для определения одного уникального выполнения DSC от начала до конца.</span><span class="sxs-lookup"><span data-stu-id="64fc8-176">Here, the term DSC operation is used to define a single unique DSC execution from its start to its end.</span></span> <span data-ttu-id="64fc8-177">Например, `Test-DscConfiguration` будет отдельной операцией DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-177">For example, `Test-DscConfiguration` would be a separate DSC operation.</span></span> <span data-ttu-id="64fc8-178">Аналогично все остальные командлеты в DSC (такие как `Get-DscConfiguration`, `Start-DscConfiguration` и т. д.) можно определить как отдельные операции DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-178">Similarly, every other cmdlet in DSC (such as `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) could each be identified as separate DSC operations.</span></span> <span data-ttu-id="64fc8-179">Эти функции описаны в разделе [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span><span class="sxs-lookup"><span data-stu-id="64fc8-179">The functions are explained at [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span></span>
<span data-ttu-id="64fc8-180">Чтобы получить справку, выполните команду `Get-Help <cmdlet name>`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-180">Help is available by running `Get-Help <cmdlet name>`.</span></span>

### <a name="getting-details-of-dsc-operations"></a><span data-ttu-id="64fc8-181">Получение сведений об операциях DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-181">Getting details of DSC operations</span></span>

<span data-ttu-id="64fc8-182">Функция `Get-xDscOperation` позволяет найти результаты операций DSC, выполняемых на одном или нескольких компьютерах, и возвращает объект, содержащий коллекцию событий, созданных при выполнении каждой операции DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-182">The `Get-xDscOperation` function lets you find the results of the DSC operations that run on one or multiple computers, and returns an object that contains the collection of events produced by each DSC operation.</span></span>
<span data-ttu-id="64fc8-183">Например, в следующем выводе были запущены три команды.</span><span class="sxs-lookup"><span data-stu-id="64fc8-183">For example, in the following output, three commands were run.</span></span> <span data-ttu-id="64fc8-184">Первая была выполнена успешно, две остальные — неудачно.</span><span class="sxs-lookup"><span data-stu-id="64fc8-184">The first one passed, and the other two failed.</span></span> <span data-ttu-id="64fc8-185">Эти результаты сводятся в выводе `Get-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-185">These results are summarized in the output of `Get-xDscOperation`.</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...

```

<span data-ttu-id="64fc8-186">С помощью параметра `Newest` можно также указать, что вам требуются только результаты по самой последней операции:</span><span class="sxs-lookup"><span data-stu-id="64fc8-186">You can also specify that you want only results for the most recent operations by using the `Newest` parameter:</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a><span data-ttu-id="64fc8-187">Получение сведений о событиях DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-187">Getting details of DSC events</span></span>

<span data-ttu-id="64fc8-188">Командлет `Trace-xDscOperation` возвращает объект, содержащий коллекцию событий, их типы и выводимые сообщения, созданные при выполнении определенной операции DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-188">The `Trace-xDscOperation` cmdlet returns an object containing a collection of events, their event types, and the message output generated from a particular DSC operation.</span></span> <span data-ttu-id="64fc8-189">Как правило, при обнаружении сбоя в любых операциях с помощью `Get-xDscOperation` необходимо выполнить трассировку этой операции, чтобы узнать, какое из событий вызвало сбой.</span><span class="sxs-lookup"><span data-stu-id="64fc8-189">Typically, when you find a failure in any of the operations using `Get-xDscOperation`, you would trace that operation to find out which of the events caused a failure.</span></span>

<span data-ttu-id="64fc8-190">Используйте параметр `SequenceID` для получения событий по конкретной операции на определенном компьютере.</span><span class="sxs-lookup"><span data-stu-id="64fc8-190">Use the  `SequenceID` parameter to get the events for a specific operation for a specific computer.</span></span> <span data-ttu-id="64fc8-191">Например, если указать `SequenceID` из 9, `Trace-xDscOperaion` получит трассировку для операции DSC, девятой по счету от последней операции:</span><span class="sxs-lookup"><span data-stu-id="64fc8-191">For example, if you specify a `SequenceID` of 9, `Trace-xDscOperaion` get the trace for the DSC operation that was 9th from the last operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully.
```

<span data-ttu-id="64fc8-192">Передайте идентификатор **GUID**, назначенный конкретной операции DSC (возвращенный командлетом `Get-xDscOperation`), для получения сведений о событии для этой операции DSC:</span><span class="sxs-lookup"><span data-stu-id="64fc8-192">Pass the **GUID** assigned to a specific DSC operation (as returned by the `Get-xDscOperation` cmldet) to get the event details for that DSC operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

<span data-ttu-id="64fc8-193">Обратите внимание, что поскольку `Trace-xDscOperation` объединяет события из аналитических, отладочных и операционных журналов, вам будет предложено включить эти журналы, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="64fc8-193">Note that, since `Trace-xDscOperation` aggregates events from the Analytic, Debug, and Operational logs, it will prompt you to enable these logs as described above.</span></span>

<span data-ttu-id="64fc8-194">Кроме того, можно собирать информацию о событиях, сохраняя результат в переменную `Trace-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-194">Alternately, you can gather information on the events by saving the output of `Trace-xDscOperation` into a variable.</span></span> <span data-ttu-id="64fc8-195">Чтобы отобразить все события для определенной операции DSC, можно использовать указанные далее команды.</span><span class="sxs-lookup"><span data-stu-id="64fc8-195">You can use the following commands to display all the events for a particular DSC operation.</span></span>

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

<span data-ttu-id="64fc8-196">Она отобразит те же результаты, что и командлет `Get-WinEvent`, как показано в выходных данных ниже:</span><span class="sxs-lookup"><span data-stu-id="64fc8-196">This will display the same results as the `Get-WinEvent` cmdlet, such as in the output below:</span></span>

```powershell
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

<span data-ttu-id="64fc8-197">В идеальном случае сначала нужно получить список последних конфигураций DSC, запущенных на ваших компьютерах, с помощью `Get-xDscOperation`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-197">Ideally, you would first use `Get-xDscOperation` to list out the last few DSC configuration runs on your machines.</span></span> <span data-ttu-id="64fc8-198">После этого можно исследовать отдельные операции (на основе идентификаторов SequenceID или JobID) при помощи команды `Trace-xDscOperation`, чтобы узнать, что именно сделала эта операция.</span><span class="sxs-lookup"><span data-stu-id="64fc8-198">Following this, you can examine any single operation (using its SequenceID or JobID) with `Trace-xDscOperation` to discover what it did behind the scenes.</span></span>

### <a name="getting-events-for-a-remote-computer"></a><span data-ttu-id="64fc8-199">Получение событий на удаленном компьютере</span><span class="sxs-lookup"><span data-stu-id="64fc8-199">Getting events for a remote computer</span></span>

<span data-ttu-id="64fc8-200">Используйте параметр `ComputerName` командлета `Trace-xDscOperation` для получения сведений о событиях на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="64fc8-200">Use the `ComputerName` parameter of the `Trace-xDscOperation` cmdlet to get the event details on a remote computer.</span></span> <span data-ttu-id="64fc8-201">Перед этим необходимо создать правило брандмауэра для разрешения удаленного администрирования на удаленном компьютере:</span><span class="sxs-lookup"><span data-stu-id="64fc8-201">Before you can do this, you have to create a firewall rule to allow remote administration on the remote computer:</span></span>

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
<span data-ttu-id="64fc8-202">Теперь можно указать этот компьютер при вызове `Trace-xDscOperation`:</span><span class="sxs-lookup"><span data-stu-id="64fc8-202">Now you can specify that computer in your call to `Trace-xDscOperation`:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a><span data-ttu-id="64fc8-203">Мои ресурсы не обновляются: как сбросить кэш</span><span class="sxs-lookup"><span data-stu-id="64fc8-203">My resources won’t update: How to reset the cache</span></span>

<span data-ttu-id="64fc8-204">Для повышения эффективности подсистема DSC кэширует ресурсы, которые реализованы в виде модулей PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64fc8-204">The DSC engine caches resources implemented as a PowerShell module for efficiency purposes.</span></span> <span data-ttu-id="64fc8-205">Однако это может вызвать проблемы при одновременной разработке и тестировании ресурса, так как DSC будет загружать кэшированную версию до тех пор, пока процесс не будет перезапущен.</span><span class="sxs-lookup"><span data-stu-id="64fc8-205">However, this can cause problems when you are authoring a resource and testing it simultaneously because DSC will load the cached version until the process is restarted.</span></span> <span data-ttu-id="64fc8-206">Единственный способ принудительной загрузки новой версии в DSC — явным образом завершить процесс подсистемы DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-206">The only way to make DSC load the newer version is to explicitly kill the process hosting the DSC engine.</span></span>

<span data-ttu-id="64fc8-207">Аналогично при запуске `Start-DscConfiguration` после добавления и изменения пользовательских ресурсов эти изменения могут вступить в силу только после перезагрузки компьютера.</span><span class="sxs-lookup"><span data-stu-id="64fc8-207">Similarly, when you run `Start-DscConfiguration`, after adding and modifying a custom resource, the modification may not execute unless, or until, the computer is rebooted.</span></span> <span data-ttu-id="64fc8-208">Это вызвано тем, что DSC выполняется в хост-процессе поставщика WMI (WmiPrvSE). Обычно существует несколько экземпляров WmiPrvSE, которые выполняются одновременно.</span><span class="sxs-lookup"><span data-stu-id="64fc8-208">This is because DSC runs in the WMI Provider Host Process (WmiPrvSE), and usually, there are many instances of WmiPrvSE running at once.</span></span> <span data-ttu-id="64fc8-209">После перезагрузки хост-процесс перезапускается и кэш очищается.</span><span class="sxs-lookup"><span data-stu-id="64fc8-209">When you reboot, the host process is restarted and the cache is cleared.</span></span>

<span data-ttu-id="64fc8-210">Для успешного обновления конфигурации и очистки кэша без перезагрузки необходимо остановить и перезапустить хост-процесс.</span><span class="sxs-lookup"><span data-stu-id="64fc8-210">To successfully recycle the configuration and clear the cache without rebooting, you must stop and then restart the host process.</span></span> <span data-ttu-id="64fc8-211">Это можно сделать отдельно для каждого экземпляра, определив процесс, остановив и перезапустив его.</span><span class="sxs-lookup"><span data-stu-id="64fc8-211">This can be done on a per instance basis, whereby you identify the process, stop it, and restart it.</span></span> <span data-ttu-id="64fc8-212">Кроме того, вы можете использовать `DebugMode` для перезагрузки ресурсов PowerShell DSC, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="64fc8-212">Or, you can use `DebugMode`, as demonstrated below, to reload the PowerShell DSC resource.</span></span>

<span data-ttu-id="64fc8-213">Для определения процесса, в котором размещается подсистема DSC, и остановки этого процесса для каждого экземпляра сначала получите идентификатор процесса WmiPrvSE, в котором размещена подсистема DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-213">To identify which process is hosting the DSC engine and stop it on a per instance basis, you can list the process ID of the WmiPrvSE which is hosting the DSC engine.</span></span> <span data-ttu-id="64fc8-214">Затем для обновления поставщика остановите процесс WmiPrvSE, используя приведенную ниже команду, а затем еще раз запустите командлет **Start-DscConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-214">Then, to update the provider, stop the WmiPrvSE process using the commands below, and then run **Start-DscConfiguration** again.</span></span>

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers |
Where-Object {$_.provider -like 'dsccore'} |
Select-Object -ExpandProperty HostProcessIdentifier

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a><span data-ttu-id="64fc8-215">Использование DebugMode</span><span class="sxs-lookup"><span data-stu-id="64fc8-215">Using DebugMode</span></span>

<span data-ttu-id="64fc8-216">Можно настроить локальный диспетчер конфигурации DSC, так чтобы он всегда очищал кэш с помощью `DebugMode` при перезапуске хост-процесса.</span><span class="sxs-lookup"><span data-stu-id="64fc8-216">You can configure the DSC Local Configuration Manager (LCM) to use `DebugMode` to always clear the cache when the host process is restarted.</span></span> <span data-ttu-id="64fc8-217">При установке значения **TRUE** ядро всегда перегружает ресурс PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="64fc8-217">When set to **TRUE**, it causes the engine to always reload the PowerShell DSC resource.</span></span> <span data-ttu-id="64fc8-218">После завершения записи ресурса можно снова установить свойство равным **FALSE**, и подсистема вернется к кэшированию модулей.</span><span class="sxs-lookup"><span data-stu-id="64fc8-218">Once you are done writing your resource, you can set it back to **FALSE** and the engine will revert to its behavior of caching the modules.</span></span>

<span data-ttu-id="64fc8-219">Ниже приведена демонстрация автоматического обновления кэша с помощью `DebugMode`.</span><span class="sxs-lookup"><span data-stu-id="64fc8-219">Following is a demonstration to show how `DebugMode` can automatically refresh the cache.</span></span> <span data-ttu-id="64fc8-220">Во-первых, давайте взглянем на конфигурацию по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="64fc8-220">First, let’s look at the default configuration:</span></span>

```
PS C:\> Get-DscLocalConfigurationManager


AllowModuleOverwrite           : False
CertificateID                  :
ConfigurationID                :
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     :
DebugMode                      : False
DownloadManagerCustomData      :
DownloadManagerName            :
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :
```

<span data-ttu-id="64fc8-221">Вы видите, что значение `DebugMode` установлено равным **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-221">You can see that `DebugMode` is set to **FALSE**.</span></span>

<span data-ttu-id="64fc8-222">Чтобы настроить демонстрацию `DebugMode`, используйте следующий ресурс PowerShell:</span><span class="sxs-lookup"><span data-stu-id="64fc8-222">To set up the `DebugMode` demonstration, use the following PowerShell resource:</span></span>

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
}
```

<span data-ttu-id="64fc8-223">Теперь создайте конфигурацию с именем `TestProviderDebugMode` с помощью этого ресурса:</span><span class="sxs-lookup"><span data-stu-id="64fc8-223">Now, author a configuration using the above resource called `TestProviderDebugMode`:</span></span>

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

<span data-ttu-id="64fc8-224">Вы увидите, что файл: **$env:SystemDrive\OutputFromTestProviderDebugMode.txt** содержит **1**.</span><span class="sxs-lookup"><span data-stu-id="64fc8-224">You will see that the contents of file: “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” is **1**.</span></span>

<span data-ttu-id="64fc8-225">Теперь обновите код поставщика с помощью следующего сценария:</span><span class="sxs-lookup"><span data-stu-id="64fc8-225">Now, update the provider code using the following script:</span></span>

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

<span data-ttu-id="64fc8-226">Этот сценарий создает случайное число и соответствующим образом обновляет код поставщика.</span><span class="sxs-lookup"><span data-stu-id="64fc8-226">This script generates a random number and updates the provider code accordingly.</span></span> <span data-ttu-id="64fc8-227">Если `DebugMode` установлено равным false, содержимое файла **$env:SystemDrive\OutputFromTestProviderDebugMode.txt** не изменяется.</span><span class="sxs-lookup"><span data-stu-id="64fc8-227">With `DebugMode` set to false, the contents of the file “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” are never changed.</span></span>

<span data-ttu-id="64fc8-228">Теперь установите `DebugMode` равным **TRUE** в сценарии настройки:</span><span class="sxs-lookup"><span data-stu-id="64fc8-228">Now, set `DebugMode` to **TRUE** in your configuration script:</span></span>

```powershell
LocalConfigurationManager
{
    DebugMode = $true
}
```

<span data-ttu-id="64fc8-229">При запуске приведенного выше сценария вы увидите, что содержимое файла каждый раз будет другим.</span><span class="sxs-lookup"><span data-stu-id="64fc8-229">When you run the above script again, you will see that the content of the file is different every time.</span></span> <span data-ttu-id="64fc8-230">(Проверить это можно с помощью `Get-DscConfiguration`.)</span><span class="sxs-lookup"><span data-stu-id="64fc8-230">(You can run `Get-DscConfiguration` to check it).</span></span> <span data-ttu-id="64fc8-231">Ниже приведен результат двух дополнительных запусков (у вас могут получиться другие результаты).</span><span class="sxs-lookup"><span data-stu-id="64fc8-231">Below is the result of two additional runs (your results may be different when you run the script):</span></span>

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
20                                      localhost

PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
14                                      localhost
```

## <a name="see-also"></a><span data-ttu-id="64fc8-232">См. также</span><span class="sxs-lookup"><span data-stu-id="64fc8-232">See Also</span></span>

### <a name="reference"></a><span data-ttu-id="64fc8-233">Ссылка</span><span class="sxs-lookup"><span data-stu-id="64fc8-233">Reference</span></span>
* [<span data-ttu-id="64fc8-234">Ресурс Log в DSC</span><span class="sxs-lookup"><span data-stu-id="64fc8-234">DSC Log Resource</span></span>](logResource.md)

### <a name="concepts"></a><span data-ttu-id="64fc8-235">Концепции</span><span class="sxs-lookup"><span data-stu-id="64fc8-235">Concepts</span></span>
* [<span data-ttu-id="64fc8-236">Создание пользовательских ресурсов DSC Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="64fc8-236">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

### <a name="other-resources"></a><span data-ttu-id="64fc8-237">Прочие ресурсы</span><span class="sxs-lookup"><span data-stu-id="64fc8-237">Other Resources</span></span>
* <span data-ttu-id="64fc8-238">[Конфигурация требуемого состояния Windows PowerShell (DSC)](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="64fc8-238">[Windows PowerShell Desired State Configuration Cmdlets](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)</span></span>