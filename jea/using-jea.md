---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "JEA,Powershell,безопасность"
title: "Использование JEA"
ms.openlocfilehash: 9996a432bca27240e0f08adf932126ced116985d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="using-jea" class="xliff"></a>
# Использование JEA

> Область применения: Windows PowerShell 5.0

В этом разделе описываются различные способы использования конечной точки JEA и подключения к ней.

<a id="using-jea-interactively" class="xliff"></a>
## Интерактивное использование JEA

Если вы тестируете конфигурацию JEA или предлагаете пользователям выполнять лишь простые задачи, JEA можно использовать аналогично обычному сеансу удаленного взаимодействия PowerShell.
Для выполнения более сложных задач рекомендуется использовать [неявное удаленное взаимодействие](#using-jea-with-implicit-remoting), чтобы позволить пользователям работать с объектами данных локально.

Для интерактивного использования JEA потребуется следующее:
- имя компьютера, к которому вы подключаетесь (это может быть локальный компьютер);
- имя конечной точки JEA, зарегистрированной на этом компьютере;
- учетные данные для компьютера, предоставляющие доступ к конечной точке JEA.

Располагая этой информацией, можно запустить сеанс JEA с помощью командлета [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) или [Enter-PSSession](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Если учетная запись, с помощью которой вы вошли в систему, имеет доступ к конечной точке JEA, параметр `-Credential` можно опустить.

Когда командная строка PowerShell изменяется на `[localhost]: PS>`, это означает, что теперь вы взаимодействуете с удаленным сеансом JEA.
Чтобы ознакомиться со списком доступных команд, запустите `Get-Command`.
Вам потребуется узнать у администратора, налагаются ли какие-либо ограничения на доступные параметры и допустимые значения параметров.

Напомним, что сеансы JEA работают в режиме NoLanguage, поэтому некоторые из способов использования PowerShell могут быть недоступны.
Например, нельзя использовать переменные для хранения данных или проверки свойств для объектов, возвращаемых из командлетов.
Ниже показан пример возможного использования PowerShell и приведены два способа работы с аналогичной командой в режиме NoLanguage.

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

Для более сложных вызовов команд, которые затрудняют применение такой методики, рекомендуется использовать [неявное удаленное взаимодействие](#using-jea-with-implicit-remoting) или [создание пользовательских функций](role-capabilities.md#creating-custom-functions), включающих в себя нужную вам функциональность.

<a id="using-jea-with-implicit-remoting" class="xliff"></a>
## Использование JEA с помощью неявного удаленного взаимодействия

PowerShell поддерживает альтернативную модель удаленного взаимодействия, где можно импортировать командлеты прокси-сервера с удаленного компьютера на локальный и работать с ними, как если бы они были локальными командами.
Это называется неявным удаленным взаимодействием и описано в [этой записи блога: *Hey, Scripting Guy!*](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).
Неявное удаленное взаимодействие особенно полезно при работе с JEA, так как оно позволяет работать с командлетами JEA в полноязыковом режиме.
Это означает, что можно использовать заполнение нажатием клавиши TAB, переменные, работать с объектами и даже использовать локальные сценарии для упрощения автоматизации взаимодействия с конечной точкой JEA.
При каждом выполнении команды прокси-сервера данные отправляются в конечную точку JEA на удаленном компьютере и выполняются там.

Неявное удаленное взаимодействие работает путем импорта командлетов из существующего сеанса PowerShell.
При необходимости можно присваивать существительным каждого командлета прокси-сервера префикс в виде строки по своему выбору, чтобы отличать команды, предназначенные для удаленной системы.
Создается временный модуль сценария, содержащий все команды прокси-сервера, который можно использовать в течение локального сеанса PowerShell.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> В некоторых системах импорт всего сеанса JEA может быть невозможен из-за ограничений в командлетах JEA по умолчанию.
> Чтобы обойти эту проблему, импортируйте из сеанса JEA только необходимые команды, явно указав их имена в параметре `-CommandName`.
> Данная проблема с импортом целых сеансов JEA на таких системах будет исправлена в будущем обновлении.

Если вам не удается импортировать сеанс JEA из-за ограничений для параметров JEA по умолчанию, можно выполнить указанные ниже шаги, чтобы отфильтровать стандартные команды из импортированного набора.
Вы по-прежнему сможете использовать такие команды, как `Select-Object`. Просто во время сеанса JEA вы будете использовать локальную версию, установленную на компьютере, вместо удаленной.

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

Можно также сохранить командлеты, выполненные через прокси-сервер, из неявного удаленного взаимодействия с помощью [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).
Дополнительные сведения о неявном удаленном взаимодействии см. в справочной документации по [Import-PSSession](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) и [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).

<a id="using-jea-programatically" class="xliff"></a>
## Программное использование JEA

JEA можно также использовать в системах автоматизации и приложениях пользователей, таких как приложения и веб-сайты собственной службы поддержки.
Этот подход аналогичен созданию приложений, взаимодействующих с не имеющими ограничений конечными точками PowerShell. Однако при этом программе должно быть известно, что JEA ограничивает набор команд, который можно выполнять в удаленном сеансе.

Для простых одноразовых задач можно использовать [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command), чтобы запустить набор команд с помощью JEA.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Чтобы узнать, какие команды доступны для использования при подключении к сеансу JEA, запустите `Get-Command` и просмотрите результаты для поиска допустимых параметров.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

При разработке приложения C# можно создать пространство выполнения PowerShell, которое подключается к сеансу JEA путем указания имени конфигурации в объекте [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx).

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

<a id="using-jea-with-powershell-direct" class="xliff"></a>
## Использование JEA с помощью PowerShell Direct

Hyper-V в Windows 10 и Windows Server 2016 предоставляет функцию [PowerShell Direct](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), позволяющую администраторам Hyper-V управлять виртуальными машинами с помощью PowerShell независимо от конфигурации сети и параметров удаленного управления на виртуальной машине.

Используя PowerShell Direct с JEA, вы можете предоставить администратору Hyper-V ограниченный доступ к виртуальной машине, что может оказаться полезным, если была потеряна связь с виртуальной машиной и администратору центра обработки данных требуется исправить параметры сети.

Никакая дополнительная настройка для использования JEA с PowerShell Direct не требуется, однако на виртуальной машине должна выполняться операционная система Windows 10 или Windows Server 2016.
Администратор Hyper-V может подключиться к конечной точке JEA с помощью параметров `-VMName` или `-VMId` в командлетах PSRemoting:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Настоятельно рекомендуется создать выделенного локального пользователя без каких-либо других прав на управление системой, которыми смогут воспользоваться администраторы Hyper-V.
Помните, что по умолчанию даже непривилегированный пользователь может войти на компьютер Windows, в том числе с использованием не имеющей ограничений системы PowerShell.
Это позволит ему просмотреть (часть) файловой системы и подробнее узнать о среде операционной системы.
Чтобы разрешить администратору Hyper-V доступ к виртуальной машине только с помощью PowerShell Direct с JEA, удалите права на локальный вход в систему из учетной записи JEA администратора Hyper-V.

