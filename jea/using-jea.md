---
ms.date: 06/12/2017
author: rpsqrd
ms.topic: conceptual
keywords: JEA,Powershell,безопасность
title: Использование JEA
ms.openlocfilehash: 8a6fb2682cf82de8dd20a8699178d4abde4954c2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-jea"></a><span data-ttu-id="a1cbd-103">Использование JEA</span><span class="sxs-lookup"><span data-stu-id="a1cbd-103">Using JEA</span></span>

> <span data-ttu-id="a1cbd-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a1cbd-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="a1cbd-105">В этом разделе описываются различные способы использования конечной точки JEA и подключения к ней.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-105">This topic describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="a1cbd-106">Интерактивное использование JEA</span><span class="sxs-lookup"><span data-stu-id="a1cbd-106">Using JEA interactively</span></span>

<span data-ttu-id="a1cbd-107">Если вы тестируете конфигурацию JEA или предлагаете пользователям выполнять лишь простые задачи, JEA можно использовать аналогично обычному сеансу удаленного взаимодействия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-107">If you are testing your JEA configuration or have simple tasks for users to perform, you can use JEA the same way you would a regular PowerShell remoting session.</span></span>
<span data-ttu-id="a1cbd-108">Для выполнения более сложных задач рекомендуется использовать [неявное удаленное взаимодействие](#using-jea-with-implicit-remoting), чтобы позволить пользователям работать с объектами данных локально.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-108">For complex remoting tasks, it is recommended to use [implicit remoting](#using-jea-with-implicit-remoting) instead to make it easier for your users by allowing users to operate with the data objects locally.</span></span>

<span data-ttu-id="a1cbd-109">Для интерактивного использования JEA потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="a1cbd-109">To use JEA interactively, you will need:</span></span>
- <span data-ttu-id="a1cbd-110">имя компьютера, к которому вы подключаетесь (это может быть локальный компьютер);</span><span class="sxs-lookup"><span data-stu-id="a1cbd-110">The name of the computer you are connecting to (can be the local machine)</span></span>
- <span data-ttu-id="a1cbd-111">имя конечной точки JEA, зарегистрированной на этом компьютере;</span><span class="sxs-lookup"><span data-stu-id="a1cbd-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="a1cbd-112">учетные данные для компьютера, предоставляющие доступ к конечной точке JEA.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-112">Credentials for the computer that have access to the JEA endpoint</span></span>

<span data-ttu-id="a1cbd-113">Располагая этой информацией, можно запустить сеанс JEA с помощью командлета [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) или [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="a1cbd-113">With that information in hand, you can start a JEA session using [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="a1cbd-114">Если учетная запись, с помощью которой вы вошли в систему, имеет доступ к конечной точке JEA, параметр `-Credential` можно опустить.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-114">If the account you're currently logged in as has access to the JEA endpoint, you can omit the `-Credential` parameter.</span></span>

<span data-ttu-id="a1cbd-115">Когда командная строка PowerShell изменяется на `[localhost]: PS>`, это означает, что теперь вы взаимодействуете с удаленным сеансом JEA.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-115">When the PowerShell prompt changes to `[localhost]: PS>` you will know that you are now interacting with the remote JEA session.</span></span>
<span data-ttu-id="a1cbd-116">Чтобы ознакомиться со списком доступных команд, запустите `Get-Command`.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-116">You can run `Get-Command` to check which commands are available.</span></span>
<span data-ttu-id="a1cbd-117">Вам потребуется узнать у администратора, налагаются ли какие-либо ограничения на доступные параметры и допустимые значения параметров.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-117">You will need to consult with your administrator to learn if there are any restrictions on the available parameters or allowable parameter values.</span></span>

<span data-ttu-id="a1cbd-118">Напомним, что сеансы JEA работают в режиме NoLanguage, поэтому некоторые из способов использования PowerShell могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-118">As a reminder, JEA sessions operate in NoLanguage mode, so some of the ways you typically use PowerShell may not be available.</span></span>
<span data-ttu-id="a1cbd-119">Например, нельзя использовать переменные для хранения данных или проверки свойств для объектов, возвращаемых из командлетов.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-119">For instance, you cannot use variables to store data or inspect the properties on objects returned from cmdlets.</span></span>
<span data-ttu-id="a1cbd-120">Ниже показан пример возможного использования PowerShell и приведены два способа работы с аналогичной командой в режиме NoLanguage.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-120">The below example shows an example of how you may be using PowerShell today, and two approaches to get the same command working in NoLanguage mode.</span></span>

```powershell
# Using variables in NoLanguage mode is disallowed, so the following will not work
# $vm = Get-VM -Name 'SQL01'
# Start-VM -VM $vm

# You can use pipes to pass data through to commands that accept input from the pipeline
Get-VM -Name 'SQL01' | Start-VM

# You can also wrap subcommands in parentheses and enter them inline as arguments
Start-VM -VM (Get-VM -Name 'SQL01')

# Better yet, use parameter sets that don't require extra data to be passed in when possible
Start-VM -VMName 'SQL01'
```

<span data-ttu-id="a1cbd-121">Для более сложных вызовов команд, которые затрудняют применение такой методики, рекомендуется использовать [неявное удаленное взаимодействие](#using-jea-with-implicit-remoting) или [создание пользовательских функций](role-capabilities.md#creating-custom-functions), включающих в себя нужную вам функциональность.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-121">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you desire.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="a1cbd-122">Использование JEA с помощью неявного удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="a1cbd-122">Using JEA with implicit remoting</span></span>

<span data-ttu-id="a1cbd-123">PowerShell поддерживает альтернативную модель удаленного взаимодействия, где можно импортировать командлеты прокси-сервера с удаленного компьютера на локальный и работать с ними, как если бы они были локальными командами.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-123">PowerShell supports an alternative remoting model where you can import proxy cmdlets from a remote machine on your local computer and interact with them as if they were local commands.</span></span>
<span data-ttu-id="a1cbd-124">Это называется неявным удаленным взаимодействием и описано в [этой записи блога: *Hey, Scripting Guy!*](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="a1cbd-124">This is called implicit remoting, and is explained well in [this *Hey, Scripting Guy!* blog post](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="a1cbd-125">Неявное удаленное взаимодействие особенно полезно при работе с JEA, так как оно позволяет работать с командлетами JEA в полноязыковом режиме.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-125">Implicit remoting is particularly useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span>
<span data-ttu-id="a1cbd-126">Это означает, что можно использовать заполнение нажатием клавиши TAB, переменные, работать с объектами и даже использовать локальные сценарии для упрощения автоматизации взаимодействия с конечной точкой JEA.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-126">This means you can use tab completion, variables, manipulate objects, and even use local scripts to more easily automate against a JEA endpoint.</span></span>
<span data-ttu-id="a1cbd-127">При каждом выполнении команды прокси-сервера данные отправляются в конечную точку JEA на удаленном компьютере и выполняются там.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-127">Anytime you invoke a proxy command, the data will be sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="a1cbd-128">Неявное удаленное взаимодействие работает путем импорта командлетов из существующего сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-128">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span>
<span data-ttu-id="a1cbd-129">При необходимости можно присваивать существительным каждого командлета прокси-сервера префикс в виде строки по своему выбору, чтобы отличать команды, предназначенные для удаленной системы.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-129">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing to distinguish which commands are for the remote system.</span></span>
<span data-ttu-id="a1cbd-130">Создается временный модуль сценария, содержащий все команды прокси-сервера, который можно использовать в течение локального сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-130">A temporary script module containing all of the proxy commands will be created and can be used for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="a1cbd-131">В некоторых системах импорт всего сеанса JEA может быть невозможен из-за ограничений в командлетах JEA по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-131">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span>
> <span data-ttu-id="a1cbd-132">Чтобы обойти эту проблему, импортируйте из сеанса JEA только необходимые команды, явно указав их имена в параметре `-CommandName`.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-132">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span>
> <span data-ttu-id="a1cbd-133">Данная проблема с импортом целых сеансов JEA на таких системах будет исправлена в будущем обновлении.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-133">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="a1cbd-134">Если вам не удается импортировать сеанс JEA из-за ограничений для параметров JEA по умолчанию, можно выполнить указанные ниже шаги, чтобы отфильтровать стандартные команды из импортированного набора.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-134">If you are unable to import a JEA session due to constraints on the default JEA parameters, you can follow the steps below to filter out the default commands from the imported set.</span></span>
<span data-ttu-id="a1cbd-135">Вы по-прежнему сможете использовать такие команды, как `Select-Object`. Просто во время сеанса JEA вы будете использовать локальную версию, установленную на компьютере, вместо удаленной.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-135">You will still be able to use commands like `Select-Object` -- you'll just use the local version installed on your computer instead of the remote one in the JEA session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Get a list of all the commands on the JEA endpoint
$commands = Invoke-Command -Session $jeasession -ScriptBlock { Get-Command }

# Filter out the default cmdlets
$jeaDefaultCmdlets = 'Clear-Host', 'Exit-PSSession', 'Get-Command', 'Get-FormatData', 'Get-Help', 'Measure-Object', 'Out-Default', 'Select-Object'
$filteredCommands = $commands.Name | Where-Object { $jeaDefaultCmdlets -notcontains $_ }

# Import only commands explicitly added in role capabilities and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA' -CommandName $filteredCommands
```

<span data-ttu-id="a1cbd-136">Можно также сохранить командлеты, выполненные через прокси-сервер, из неявного удаленного взаимодействия с помощью [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="a1cbd-136">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="a1cbd-137">Дополнительные сведения о неявном удаленном взаимодействии см. в справочной документации по [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) и [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="a1cbd-137">For more information about implicit remoting, check out the help documentation for [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) and [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programatically"></a><span data-ttu-id="a1cbd-138">Программное использование JEA</span><span class="sxs-lookup"><span data-stu-id="a1cbd-138">Using JEA programatically</span></span>

<span data-ttu-id="a1cbd-139">JEA можно также использовать в системах автоматизации и приложениях пользователей, таких как приложения и веб-сайты собственной службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-139">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and web sites.</span></span>
<span data-ttu-id="a1cbd-140">Этот подход аналогичен созданию приложений, взаимодействующих с не имеющими ограничений конечными точками PowerShell. Однако при этом программе должно быть известно, что JEA ограничивает набор команд, который можно выполнять в удаленном сеансе.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-140">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints, with the caveat that the program should be aware that JEA is limiting the commands that can be run in the remote session.</span></span>

<span data-ttu-id="a1cbd-141">Для простых одноразовых задач можно использовать [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command), чтобы запустить набор команд с помощью JEA.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-141">For simple, one-off tasks, you can use [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) to run a set of commands using JEA.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="a1cbd-142">Чтобы узнать, какие команды доступны для использования при подключении к сеансу JEA, запустите `Get-Command` и просмотрите результаты для поиска допустимых параметров.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-142">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="a1cbd-143">При разработке приложения C# можно создать пространство выполнения PowerShell, которое подключается к сеансу JEA путем указания имени конфигурации в объекте [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a1cbd-143">If you are building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) object.</span></span>

```csharp

// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
var creds        = // create a PSCredential object here (https://msdn.microsoft.com/en-us/library/system.management.automation.pscredential(v=vs.85).aspx)

WSManConnectionInfo connectionInfo = new WSManConnectionInfo(
                    false,                 // Use SSL
                    computerName,          // Computer name
                    5985,                  // WSMan Port
                    "/wsman",              // WSMan Path
                    string.Format(CultureInfo.InvariantCulture, "http://schemas.microsoft.com/powershell/{0}", configName),  // Connection URI with config name
                    creds);                // Credentials
// Now, use the connection info to create a runspace where you can run the commands
using (Runspace runspace = RunspaceFactory.CreateRunspace(connectionInfo))
{
    // Open the runspace
    runspace.Open();

    using (PowerShell ps = PowerShell.Create())
    {
        // Set the PowerShell object to use the JEA runspace
        ps.Runspace = runspace;

        // Now you can add and invoke commands
        ps.AddCommand("Get-Command");
        foreach (var result in ps.Invoke())
        {
            Console.WriteLine(result);
        }
    }

    // Close the runspace
    runspace.Close();
}
```

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="a1cbd-144">Использование JEA с помощью PowerShell Direct</span><span class="sxs-lookup"><span data-stu-id="a1cbd-144">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="a1cbd-145">Hyper-V в Windows 10 и Windows Server 2016 предоставляет функцию [PowerShell Direct](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), позволяющую администраторам Hyper-V управлять виртуальными машинами с помощью PowerShell независимо от конфигурации сети и параметров удаленного управления на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-145">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), a feature which allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="a1cbd-146">Используя PowerShell Direct с JEA, вы можете предоставить администратору Hyper-V ограниченный доступ к виртуальной машине, что может оказаться полезным, если была потеряна связь с виртуальной машиной и администратору центра обработки данных требуется исправить параметры сети.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-146">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM, which can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="a1cbd-147">Никакая дополнительная настройка для использования JEA с PowerShell Direct не требуется, однако на виртуальной машине должна выполняться операционная система Windows 10 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-147">No additional configuration is required to use JEA over PowerShell Direct, however the operating system running inside the virtual machine must be Windows 10 or Windows Server 2016.</span></span>
<span data-ttu-id="a1cbd-148">Администратор Hyper-V может подключиться к конечной точке JEA с помощью параметров `-VMName` или `-VMId` в командлетах PSRemoting:</span><span class="sxs-lookup"><span data-stu-id="a1cbd-148">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="a1cbd-149">Настоятельно рекомендуется создать выделенного локального пользователя без каких-либо других прав на управление системой, которыми смогут воспользоваться администраторы Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-149">It is strongly recommended that you create a dedicated local user with no other rights to manage the system for your Hyper-V administrators to use.</span></span>
<span data-ttu-id="a1cbd-150">Помните, что по умолчанию даже непривилегированный пользователь может войти на компьютер Windows, в том числе с использованием не имеющей ограничений системы PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-150">Remember that even an unprivileged user can still log into a Windows machine by default, including using unconstrained PowerShell.</span></span>
<span data-ttu-id="a1cbd-151">Это позволит ему просмотреть (часть) файловой системы и подробнее узнать о среде операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-151">That will allow them to browse (some of) the file system and learn more about your OS environment.</span></span>
<span data-ttu-id="a1cbd-152">Чтобы разрешить администратору Hyper-V доступ к виртуальной машине только с помощью PowerShell Direct с JEA, удалите права на локальный вход в систему из учетной записи JEA администратора Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="a1cbd-152">To lock down a Hyper-V administrator to only access a VM using PowerShell Direct with JEA, you will need to deny local logon rights to the Hyper-V admin's JEA account.</span></span>