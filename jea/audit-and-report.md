---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea,powershell,безопасность"
title: "Аудит и отчеты для JEA"
ms.openlocfilehash: 60bc7a4213c75735628207bb21078bf90f7b1ca3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="3cf7e-103">Аудит и отчеты для JEA</span><span class="sxs-lookup"><span data-stu-id="3cf7e-103">Auditing and Reporting on JEA</span></span>

> <span data-ttu-id="3cf7e-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3cf7e-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="3cf7e-105">После развертывания JEA потребуется регулярно проводить аудит конфигурации JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-105">After you've deployed JEA, you will want to regularly audit the JEA configuration.</span></span>
<span data-ttu-id="3cf7e-106">Это поможет вам убедиться, что доступ к конечной точке JEA получают уполномоченные для этого люди и что назначенные им роли по-прежнему являются допустимыми.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-106">This will help you assess if the correct people have access to the JEA endpoint and if their assigned roles are still appropriate.</span></span>

<span data-ttu-id="3cf7e-107">В этом разделе описываются различные способы проведения аудита для конечной точки JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-107">This topic describes the various ways you can audit a JEA endpoint.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="3cf7e-108">Поиск зарегистрированных сеансов JEA на компьютере</span><span class="sxs-lookup"><span data-stu-id="3cf7e-108">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="3cf7e-109">Чтобы узнать, какие сеансы JEA зарегистрированы на компьютере, используйте командлет [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration).</span><span class="sxs-lookup"><span data-stu-id="3cf7e-109">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="3cf7e-110">Действующие права для конечной точки перечислены в свойстве "Permission".</span><span class="sxs-lookup"><span data-stu-id="3cf7e-110">The effective rights for the endpoint are listed in the "Permission" property.</span></span>
<span data-ttu-id="3cf7e-111">Эти пользователи имеют право подключаться к конечной точке JEA, однако доступные им роли (а значит и команды) определяются в поле "RoleDefinitions" [файла конфигурации сеанса](session-configurations.md), который использовался для регистрации конечной точки.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-111">These users have the right to connect to the JEA endpoint, but which roles (and, by extension, commands) they have access to is determined by the "RoleDefinitions" field in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span>

<span data-ttu-id="3cf7e-112">Вы можете оценить сопоставления ролей в зарегистрированной конечной точке JEA, развернув данные в свойстве "RoleDefinitions".</span><span class="sxs-lookup"><span data-stu-id="3cf7e-112">You can evaluate the role mappings in a registered JEA endpoint by expanding the data in the "RoleDefinitions" property.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="3cf7e-113">Поиск доступных возможностей ролей на компьютере</span><span class="sxs-lookup"><span data-stu-id="3cf7e-113">Find available role capabilities on the machine</span></span>

<span data-ttu-id="3cf7e-114">Файлы возможностей ролей будут использоваться JEA, только если они хранятся в папке "RoleCapabilities" внутри допустимого модуля PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-114">Role capability files will only be used by JEA if they are stored in a "RoleCapabilities" folder inside a valid PowerShell module.</span></span>
<span data-ttu-id="3cf7e-115">Все возможности ролей, доступные на компьютере, можно найти путем поиска по списку доступных модулей.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-115">You can find all role capabilities available on a computer by searching the list of available modules.</span></span>

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{ Name = 'Path'; Expression = { $_.FullName }} | Sort-Object Name
}
```

> [!NOTE]
> <span data-ttu-id="3cf7e-116">Порядок результатов, получаемых из этой функции, необязательно соответствует порядку, в котором будут выбираться возможности ролей, когда несколько возможностей ролей имеют одинаковые имена.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-116">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="3cf7e-117">Проверка действующих прав для конкретного пользователя</span><span class="sxs-lookup"><span data-stu-id="3cf7e-117">Check effective rights for a specific user</span></span>

<span data-ttu-id="3cf7e-118">После настройки конечной точки JEA вам может потребоваться проверить, какие команды доступны определенному пользователю в сеансе JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-118">Once you have set up a JEA endpoint, you may want to check which commands are available to a specific user in a JEA session.</span></span>
<span data-ttu-id="3cf7e-119">Вы можете использовать [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability), чтобы перечислить все команды, применимые для пользователя, если тот решит запустить сеанс JEA с имеющимся членством в группах.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-119">You can use [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) to enumerate all of the commands applicable to a user if they were to start a JEA session with their current group memberships.</span></span>
<span data-ttu-id="3cf7e-120">Выходные данные `Get-PSSessionCapability` идентичны данным для указанного пользователя, запустившего `Get-Command -CommandType All` в сеансе JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-120">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="3cf7e-121">Если пользователи не являются постоянными членами групп, предоставляющих им дополнительные права JEA, этот командлет может не отражать такие дополнительные разрешения.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-121">If your users are not permanent members of groups which would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span>
<span data-ttu-id="3cf7e-122">Обычно это происходит, когда с помощью систем управления привилегированным доступом JIT реализуется временная принадлежность пользователей к группе безопасности.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-122">This is typically the case when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span>
<span data-ttu-id="3cf7e-123">Всегда тщательно оценивайте сопоставление пользователей с ролями, а также содержимое каждой роли, чтобы убедиться, что пользователи получают доступ к минимальному набору команд, необходимых для успешного выполнения порученной им работы.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-123">Always carefully evaluate the mapping of users to roles and the contents of each role to ensure users are only getting access to the least amount of commands needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="3cf7e-124">Журналы событий PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cf7e-124">PowerShell event logs</span></span>

<span data-ttu-id="3cf7e-125">Если в системе включено ведение журнала для модуля или блока сценария, в журнале событий Windows можно найти события для каждой команды, которую пользователь выполнял в своих сеансах JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-125">If you enabled module and/or script block logging on the system, you will be able to find events in the Windows event logs for each command a user ran in their JEA sessions.</span></span>
<span data-ttu-id="3cf7e-126">Чтобы найти эти события, откройте средство просмотра событий Windows, перейдите к журналу событий **Microsoft-Windows-PowerShell/Operational** и найдите событие с идентификатором **4104**.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-126">To find these events, open the Windows Event Viewer, navigate to the **Microsoft-Windows-PowerShell/Operational** event log, and look for events with event ID **4104**.</span></span>

<span data-ttu-id="3cf7e-127">Каждая запись журнала событий содержит сведения о сеансе, в котором была запущена команда.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-127">Each event log entry will include information about the session in which the command was run.</span></span>
<span data-ttu-id="3cf7e-128">Для сеансов JEA приводятся важные сведения о **ConnectedUser** — фактическом пользователе, создавшем сеанс JEA, а также о **RunAsUser** — учетной записи, используемой JEA для выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-128">For JEA sessions, this includes important information about the **ConnectedUser**, which is the actual user who created the JEA session, as well as the **RunAsUser** which identifies the account JEA used to execute the command.</span></span>
<span data-ttu-id="3cf7e-129">Журналы событий приложений показывают изменения, внесенные RunAsUser, поэтому крайне важно включить ведение записей или журналов для модулей или сценариев, чтобы отследить вызов определенной команды до конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-129">Application event logs will show changes being made by the RunAsUser, so having transcripts or module/script logging enabled is crucial to be able to trace a specific command invocation back to a user.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="3cf7e-130">Журналы событий приложений</span><span class="sxs-lookup"><span data-stu-id="3cf7e-130">Application event logs</span></span>

<span data-ttu-id="3cf7e-131">При выполнении команды в сеансе JEA, который взаимодействует с внешним приложением или внешней службой, эти приложения могут записывать события в собственные журналы.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-131">When you run a command in a JEA session that interacts with an external application or service, those applications may log events to their own event logs.</span></span>
<span data-ttu-id="3cf7e-132">В отличие от записей и журналов PowerShell, другие механизмы ведения журнала не фиксируют подключенного пользователя сеанса JEA, а лишь регистрируют виртуальную учетную запись запуска от имени или групповую управляемую учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-132">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the connected user of the JEA session, and will instead only log the virtual run-as user or group managed service account.</span></span>
<span data-ttu-id="3cf7e-133">Чтобы определить, кем выполнена команда, требуется просмотреть [запись сеанса](#session-transcripts) или сопоставлять журналы событий PowerShell с временем и пользователем, указанными в журнале событий приложений.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-133">In order to determine who ran the command, you will need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="3cf7e-134">Журнал WinRM может помочь сопоставить пользователей, от имени которых выполняется запуск, в журнале событий приложения с подключающимся пользователем.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-134">The WinRM log can also help you correlate run as users in an application event log with the connecting user.</span></span>
<span data-ttu-id="3cf7e-135">Событие с идентификатором **193** в журнале **Microsoft-Windows-Windows Remote Management/Operational** регистрирует идентификатор безопасности (SID) и имя учетной записи как для подключающегося пользователя, так и для пользователя, от имени которого выполняется запуск, при каждом создании сеанса JEA.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-135">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user every time a JEA session is created.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="3cf7e-136">Записи сеансов</span><span class="sxs-lookup"><span data-stu-id="3cf7e-136">Session transcripts</span></span>

<span data-ttu-id="3cf7e-137">Если вы настроили JEA для создания записи для каждого сеанса пользователя, в указанной папке будет храниться текстовая копия перечня всех действий каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-137">If you configured JEA to create a transcript for each user session, a text copy of every user's actions will be stored in the specified folder.</span></span>

<span data-ttu-id="3cf7e-138">Чтобы найти все каталоги записей, выполните следующую команду с правами администратора на компьютере, где настроена JEA:</span><span class="sxs-lookup"><span data-stu-id="3cf7e-138">To find all transcript directories, run the following command as an administrator on the computer configured with JEA:</span></span>

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="3cf7e-139">Каждая запись начинается со сведений о том, когда запущен сеанс, какой пользователь подключился к нему и какое удостоверение JEA было им присвоено.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-139">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="3cf7e-140">В основной части записи регистрируются сведения о каждой из вызванных пользователем команд.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-140">In the body of the transcript, information is logged about each command the user invoked.</span></span>
<span data-ttu-id="3cf7e-141">Точный синтаксис команды, запущенной пользователем, в сеансах JEA недоступен из-за способа преобразования команд для удаленного взаимодействия PowerShell. Однако вы по-прежнему можете определить действительную выполненную команду.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-141">The exact syntax of the command the user ran is unavailable in JEA sessions due to the way commands are transformed for PowerShell remoting, however you can still determine the effective command that was executed.</span></span>
<span data-ttu-id="3cf7e-142">Ниже приведен пример фрагмента записи для пользователя, запускающего `Get-Service Dns` в сеансе JEA:</span><span class="sxs-lookup"><span data-stu-id="3cf7e-142">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="3cf7e-143">Для каждой выполняемой пользователем команды записывается строка "CommandInvocation", которая описывает командлет или функцию, вызванные пользователем.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-143">For each command a user runs, a "CommandInvocation" line will be written, describing the cmdlet or function the user invoked.</span></span>
<span data-ttu-id="3cf7e-144">За каждым CommandInvocation следует элемент ParameterBindings, сообщающий о каждом параметре и значении, переданном с помощью команды.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-144">ParameterBindings follow each CommandInvocation to tell you about each parameter and value that was supplied with the command.</span></span>
<span data-ttu-id="3cf7e-145">В приведенном выше примере можно заметить, что параметр "Name" передал значение "Dns" для командлета "Get-Service".</span><span class="sxs-lookup"><span data-stu-id="3cf7e-145">In the above example, you can see that the parameter "Name" was supplied the value "Dns" for the "Get-Service" cmdlet.</span></span>

<span data-ttu-id="3cf7e-146">Выходные данные каждой команды также вызывают CommandInvocation, обычно Out-Default.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-146">The output of each command will also trigger a CommandInvocation, usually to Out-Default.</span></span> <span data-ttu-id="3cf7e-147">InputObject в Out-Default представляет собой объект PowerShell, возвращаемый из команды.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-147">The InputObject of Out-Default is the PowerShell object returned from the command.</span></span>
<span data-ttu-id="3cf7e-148">Сведения об этом объекте выводятся несколькими строчками ниже, в точности имитируя то, что увидел бы пользователь.</span><span class="sxs-lookup"><span data-stu-id="3cf7e-148">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="3cf7e-149">См. также:</span><span class="sxs-lookup"><span data-stu-id="3cf7e-149">See also</span></span>

- [<span data-ttu-id="3cf7e-150">Аудит действий пользователей в сеансе JEA</span><span class="sxs-lookup"><span data-stu-id="3cf7e-150">Audit user actions in a JEA session</span></span>](audit-and-report.md)
- [<span data-ttu-id="3cf7e-151">Запись блога *PowerShell ♥ the Blue Team* по безопасности</span><span class="sxs-lookup"><span data-stu-id="3cf7e-151">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

