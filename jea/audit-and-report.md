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
<a id="auditing-and-reporting-on-jea" class="xliff"></a>
# Аудит и отчеты для JEA

> Область применения: Windows PowerShell 5.0

После развертывания JEA потребуется регулярно проводить аудит конфигурации JEA.
Это поможет вам убедиться, что доступ к конечной точке JEA получают уполномоченные для этого люди и что назначенные им роли по-прежнему являются допустимыми.

В этом разделе описываются различные способы проведения аудита для конечной точки JEA.

<a id="find-registered-jea-sessions-on-a-machine" class="xliff"></a>
## Поиск зарегистрированных сеансов JEA на компьютере

Чтобы узнать, какие сеансы JEA зарегистрированы на компьютере, используйте командлет [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration).

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

Действующие права для конечной точки перечислены в свойстве "Permission".
Эти пользователи имеют право подключаться к конечной точке JEA, однако доступные им роли (а значит и команды) определяются в поле "RoleDefinitions" [файла конфигурации сеанса](session-configurations.md), который использовался для регистрации конечной точки.

Вы можете оценить сопоставления ролей в зарегистрированной конечной точке JEA, развернув данные в свойстве "RoleDefinitions".

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

<a id="find-available-role-capabilities-on-the-machine" class="xliff"></a>
## Поиск доступных возможностей ролей на компьютере

Файлы возможностей ролей будут использоваться JEA, только если они хранятся в папке "RoleCapabilities" внутри допустимого модуля PowerShell.
Все возможности ролей, доступные на компьютере, можно найти путем поиска по списку доступных модулей.

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
> Порядок результатов, получаемых из этой функции, необязательно соответствует порядку, в котором будут выбираться возможности ролей, когда несколько возможностей ролей имеют одинаковые имена.

<a id="check-effective-rights-for-a-specific-user" class="xliff"></a>
## Проверка действующих прав для конкретного пользователя

После настройки конечной точки JEA вам может потребоваться проверить, какие команды доступны определенному пользователю в сеансе JEA.
Вы можете использовать [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability), чтобы перечислить все команды, применимые для пользователя, если тот решит запустить сеанс JEA с имеющимся членством в группах.
Выходные данные `Get-PSSessionCapability` идентичны данным для указанного пользователя, запустившего `Get-Command -CommandType All` в сеансе JEA.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Если пользователи не являются постоянными членами групп, предоставляющих им дополнительные права JEA, этот командлет может не отражать такие дополнительные разрешения.
Обычно это происходит, когда с помощью систем управления привилегированным доступом JIT реализуется временная принадлежность пользователей к группе безопасности.
Всегда тщательно оценивайте сопоставление пользователей с ролями, а также содержимое каждой роли, чтобы убедиться, что пользователи получают доступ к минимальному набору команд, необходимых для успешного выполнения порученной им работы.

<a id="powershell-event-logs" class="xliff"></a>
## Журналы событий PowerShell

Если в системе включено ведение журнала для модуля или блока сценария, в журнале событий Windows можно найти события для каждой команды, которую пользователь выполнял в своих сеансах JEA.
Чтобы найти эти события, откройте средство просмотра событий Windows, перейдите к журналу событий **Microsoft-Windows-PowerShell/Operational** и найдите событие с идентификатором **4104**.

Каждая запись журнала событий содержит сведения о сеансе, в котором была запущена команда.
Для сеансов JEA приводятся важные сведения о **ConnectedUser** — фактическом пользователе, создавшем сеанс JEA, а также о **RunAsUser** — учетной записи, используемой JEA для выполнения команды.
Журналы событий приложений показывают изменения, внесенные RunAsUser, поэтому крайне важно включить ведение записей или журналов для модулей или сценариев, чтобы отследить вызов определенной команды до конкретного пользователя.

<a id="application-event-logs" class="xliff"></a>
## Журналы событий приложений

При выполнении команды в сеансе JEA, который взаимодействует с внешним приложением или внешней службой, эти приложения могут записывать события в собственные журналы.
В отличие от записей и журналов PowerShell, другие механизмы ведения журнала не фиксируют подключенного пользователя сеанса JEA, а лишь регистрируют виртуальную учетную запись запуска от имени или групповую управляемую учетную запись службы.
Чтобы определить, кем выполнена команда, требуется просмотреть [запись сеанса](#session-transcripts) или сопоставлять журналы событий PowerShell с временем и пользователем, указанными в журнале событий приложений.

Журнал WinRM может помочь сопоставить пользователей, от имени которых выполняется запуск, в журнале событий приложения с подключающимся пользователем.
Событие с идентификатором **193** в журнале **Microsoft-Windows-Windows Remote Management/Operational** регистрирует идентификатор безопасности (SID) и имя учетной записи как для подключающегося пользователя, так и для пользователя, от имени которого выполняется запуск, при каждом создании сеанса JEA.

<a id="session-transcripts" class="xliff"></a>
## Записи сеансов

Если вы настроили JEA для создания записи для каждого сеанса пользователя, в указанной папке будет храниться текстовая копия перечня всех действий каждого пользователя.

Чтобы найти все каталоги записей, выполните следующую команду с правами администратора на компьютере, где настроена JEA:

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

Каждая запись начинается со сведений о том, когда запущен сеанс, какой пользователь подключился к нему и какое удостоверение JEA было им присвоено.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

В основной части записи регистрируются сведения о каждой из вызванных пользователем команд.
Точный синтаксис команды, запущенной пользователем, в сеансах JEA недоступен из-за способа преобразования команд для удаленного взаимодействия PowerShell. Однако вы по-прежнему можете определить действительную выполненную команду.
Ниже приведен пример фрагмента записи для пользователя, запускающего `Get-Service Dns` в сеансе JEA:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

Для каждой выполняемой пользователем команды записывается строка "CommandInvocation", которая описывает командлет или функцию, вызванные пользователем.
За каждым CommandInvocation следует элемент ParameterBindings, сообщающий о каждом параметре и значении, переданном с помощью команды.
В приведенном выше примере можно заметить, что параметр "Name" передал значение "Dns" для командлета "Get-Service".

Выходные данные каждой команды также вызывают CommandInvocation, обычно Out-Default. InputObject в Out-Default представляет собой объект PowerShell, возвращаемый из команды.
Сведения об этом объекте выводятся несколькими строчками ниже, в точности имитируя то, что увидел бы пользователь.

<a id="see-also" class="xliff"></a>
## См. также:

- [Аудит действий пользователей в сеансе JEA](audit-and-report.md)
- [Запись блога *PowerShell ♥ the Blue Team* по безопасности](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

