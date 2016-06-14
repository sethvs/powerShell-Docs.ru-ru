# Just Enough Administration (JEA): введение

## Содержание
Изучив этот документ, вы сможете создавать, развертывать, использовать и обслуживать развертывание Just Enough Administration (JEA), а также вести его аудит.
Это вводное руководство включает следующие разделы:

1.  [Введение](#introduction): вкратце рассмотрим, почему JEA — это важно

2.  [Предварительные требования](#prerequisites): настроим среду

3.  [Использование JEA](#using-jea): начнем с изучения работы оператора с JEA

4.  [Переделка демоверсии](#remake-the-demo-endpoint): создадим конфигурацию сеанса JEA с нуля

5.  [Возможности ролей](#role-capabilities): узнаем, как настраивать возможности JEA, используя файлы возможностей ролей

6.  [От начала до конца: Active Directory](#end-to-end---active-directory): создадим новую конечную точку для управления Active Directory

7.  [Развертывание и обслуживание на нескольких компьютерах](#multi-machine-deployment-and-maintenance): узнаем, как меняется процесс развертывания и создания при изменении масштаба

8.  [Отчеты о JEA](#reporting-on-jea): узнаем, как вести аудит и формировать отчеты по всем действиям и инфраструктуре JEA

9.  [Приложение](#appendix): важные навыки и темы для обсуждения

## Введение

### Причины для использования
Предоставляя кому-либо привилегированный доступ к своим системам, вы полагаетесь на этого человека.
Это риск, и администраторы всегда находятся под угрозой.
Внутренние атаки и кража учетных данных реальны и распространены.

Эта проблема не нова.
Вероятно, вы уже знакомы с принципом минимальных полномочий или использовали ту или иную форму управления доступом на основе ролей в приложениях, предоставляющих такую возможность.
В то же время эффективность и управляемость таких решений часто ограничены из-за широкой области их применения и неточности.
Кроме того, в RBAC есть пробелы.
Например, в Windows привилегированный доступ — это по сути двухпозиционный переключатель, вынуждающий предоставлять ненужные разрешения при добавлении пользователей в группу администраторов.

Функция Just Enough Administration (JEA) позволяет использовать платформу RBAC через удаленное взаимодействие PowerShell.
*С ее помощью отдельные пользователи могут выполнять определенные задачи администрирования на серверах, не получая права администраторов.*
Это позволяет заполнять пробелы между существующими решениями RBAC и упрощает управление соответствующими параметрами.

## Необходимые компоненты

### Начальное состояние
Прежде чем приступать к этому разделу, убедитесь в следующем.

1. В вашей системе доступна функция JEA. Проверьте список поддерживаемых операционных систем и необходимые скачиваемые компоненты в файле [README](./README.md).
2. У вас есть права администратора на компьютере, где используется JEA.
3. Компьютер присоединен к домену.
Инструкции по быстрой настройке нового домена на сервере см. в статье [Создание контроллера домена](#creating-a-domain-controller).

### Включение удаленного взаимодействия PowerShell
Управление с помощью функции JEA осуществляется через удаленное взаимодействие PowerShell.
Чтобы убедиться, что оно включено и правильно настроено, выполните в окне администратора PowerShell следующую команду:

```PowerShell
Enable-PSRemoting 
```

Если вы не знакомы с работой удаленного взаимодействия PowerShell, запустите `Get-Help about_Remote` и ознакомьтесь с этой важной фундаментальной концепцией.

### Идентификация пользователей или групп
Чтобы показать JEA в действии, необходимо определить пользователей и группы без прав администратора, которые будут использоваться в этом руководстве.
  
Если используется существующий домен, определите или создайте учетные записи непривилегированных пользователей и группы.
Им будет предоставлен доступ к JEA без прав администратора.
Каждый раз, когда вы видите переменную `$NonAdministrator` в верхней части сценария, необходимо записать в нее выбранных пользователей или группы без прав администратора. 

При создании нового домена с нуля все происходит гораздо проще.
Для создания учетных записей пользователей и групп без прав администратора воспользуйтесь разделом [Настройка пользователей и групп](#set-up-users-and-groups).
Значениями переменной `$NonAdministrator` по умолчанию будут группы, созданные в указанном разделе.

### Настройка файла возможности для роли обслуживания
Чтобы создать демонстрационный файл возможностей роли, который понадобится нам в следующем разделе, выполните в PowerShell следующие команды:
Для чего нужен этот файл, вы узнаете далее в этом разделе.

```PowerShell
# Fields in the role capability
$MaintenanceRoleCapabilityCreationParams = @{
    Author = 'Contoso Admin'
    CompanyName = 'Contoso'
    VisibleCmdlets = 'Restart-Service'
    FunctionDefinitions = 
            @{ Name = 'Get-UserInfo'; ScriptBlock = { $PSSenderInfo } }
}

# Create the demo module, which will contain the maintenance Role Capability File
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module" -ItemType Directory
New-ModuleManifest -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\Demo_Module.psd1"
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities" -ItemType Directory 

# Create the Role Capability file
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc" @MaintenanceRoleCapabilityCreationParams 
```
  
### Создание и регистрация демонстрационного файла конфигурации сеанса
Чтобы создать и зарегистрировать демонстрационный файл конфигурации сеанса, который понадобится нам в следующем разделе, выполните следующие команды:
Для чего нужен этот файл, вы узнаете далее в этом разделе.

```PowerShell
# Determine domain
$domain = (Get-CimInstance -ClassName Win32_ComputerSystem).Domain

# Replace with your non-admin group name
$NonAdministrator = "$domain\JEA_NonAdmin_Operator"

# Specify the settings for this JEA endpoint
# Note: You will not be able to use a virtual account if you are using WMF 5.0 on Windows 7 or Windows Server 2008 R2
$JEAConfigParams = @{
    SessionType = 'RestrictedRemoteServer'
    RunAsVirtualAccount = $true
    RoleDefinitions = @{
        $NonAdministrator = @{ RoleCapabilities = 'Maintenance' }
    }
    TranscriptDirectory = "$env:ProgramData\JEAConfiguration\Transcripts"
}

# Set up a folder for the Session Configuration files
if (-not (Test-Path "$env:ProgramData\JEAConfiguration"))
{
    New-Item -Path "$env:ProgramData\JEAConfiguration" -ItemType Directory
}

# Specify the name of the JEA endpoint
$sessionName = 'JEA_Demo'

if (Get-PSSessionConfiguration -Name $sessionName -ErrorAction SilentlyContinue)
{
    Unregister-PSSessionConfiguration -Name $sessionName -ErrorAction Stop
}

New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc" @JEAConfigParams

# Register the session configuration
Register-PSSessionConfiguration -Name $sessionName -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc"
```
 
### Включение ведения журнала модуля PowerShell (необязательно)
Указанные ниже действия позволят включить ведение журнала действий PowerShell в вашей системе.
Это не обязательно для работы с JEA, но пригодится при работе с разделом [Отчеты о JEA](#reporting-on-jea).

1. Откройте редактор локальных групповых политик
2. Откройте папку "Конфигурация компьютера\Административные шаблоны\Компоненты Windows\Windows PowerShell".
3. Дважды щелкните пункт "Включить модуль ведения журнала".
4. Нажмите кнопку "Включено".
5. В разделе "Параметры" нажмите кнопку "Показать" рядом с именами модулей.
6. Введите "*" во всплывающем окне. Это означает, что PowerShell будет регистрировать в журнале команды из всех модулей.
7. Нажмите кнопку "ОК" и примените политику.

Примечание. Вы можете также включить при помощи групповой политики запись действий PowerShell в масштабе всей системы.

**Итак, вы настроили на компьютере демонстрационную конечную точку и готовы приступить к работе с JEA.**

## Использование JEA
Этот раздел посвящен *взаимодействию* конечных пользователей с JEA.
В разделе предварительных требований вы создали демонстрационную конечную точку JEA.
На ее примере мы покажем вам JEA в действии.
В последующих разделах руководство будет работать в обратном направлении — вы познакомитесь с действиями и файлами, обеспечивающими взаимодействие с конечным пользователем.

### Использование JEA без прав администратора
Чтобы увидеть, как работает JEA, потребуется работать с удаленным взаимодействием PowerShell как пользователь, не имеющий прав администратора.
В новом окне PowerShell выполните следующую команду:   

```PowerShell
$NonAdminCred = Get-Credential
```

По запросу введите учетные данные пользователя без прав администратора.
Если вы выполнили указания из раздела [Настройка пользователей и групп](#set-up-users-and-groups), это будут следующие учетные данные:
-   Имя пользователя: OperatorUser
-   Пароль: pa$$w0rd

Затем выполните следующую команду, чтобы подключиться к демонстрационной конечной точке, используя указанные учетные данные:

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEA_Demo -Credential $NonAdminCred 
```

Вы вошли в интерактивный удаленный сеанс PowerShell на локальном компьютере. С помощью параметра "Credential" вы подключились *как* OperatorUser (или по другой указанной вами учетной записи).
Изменение командной строки на `[localhost]: PS>` означает, чтобы вы работаете в удаленном сеансе.  

В удаленной командной строке выполните следующую команду, чтобы отобразить список доступных команд:

```PowerShell
Get-Command 
```

Как вы видите, это весьма ограниченный набор команд по сравнению с теми, которые доступны в обычном окне PowerShell (нередко в него входит несколько тысяч команд).
В частности, он включает только семь командлетов JEA по умолчанию (Clear-Host, Exit-PSSession, Get-Command, Get-FormatData, Get-Help, Measure-Object, Out-Default, Select-Object) и две команды, отдельно добавленные в файл возможностей для роли обслуживания.

Теперь посмотрим, в каком пользовательском контексте осуществляется этот сеанс, вызвав пользовательскую функцию, включенную в файл возможностей для роли обслуживания:

```PowerShell
Get-UserInfo
```
 
Выходные данные этой функции содержат пользователей ConnectedUser и RunAsUser.
Подключенный пользователь (ConnectedUser) — это учетная запись, подключенная к удаленному сеансу (например, ваша учетная запись).
Подключенному пользователю права администратора не требуются.
Учетная запись RunAsUser — это учетная запись, которая фактически выполняет привилегированные действия.
За счет подключения в качестве одного пользователя и выполнения действий от имени привилегированного пользователя обычным пользователям дается возможность выполнять определенные административные задачи без предоставления прав администратора.

Чтобы увидеть, как это работает, выполните следующую команду:

```PowerShell
Restart-Service -Name Spooler -Verbose
```

Обычно для выполнения командлета Restart-Service требуются права администратора.
Но с виртуальной учетной записью JEA его можно выполнять по учетным данным непривилегированных пользователей.

Таким образом, JEA позволяет работать, используя уже знакомые вам команды.
Но что насчет команд, которые должны быть вам *недоступны*?
Попробуйте выполнить в сеансе JEA другую команду, например `Restart-Computer`, и вы увидите, что JEA не позволяет выполнять такие команды.

```PowerShell
[localhost]: PS> Restart-Computer
The term 'Restart-Computer' is not recognized as the name of a cmdlet, function, script file, or
operable program. Check the spelling of the name, or if a path was included, verify that the path
is correct and try again.
    + CategoryInfo          : ObjectNotFound: (Restart-Computer:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException 
```

Наконец, чтобы покинуть ограниченную конечную точку JEA, выполните следующую команду:

```PowerShell
Exit-PSSession
```

Она отключит вас от удаленного сеанса PowerShell.

## Повторное создание демонстрационной конечной точки
В этом разделе вы узнаете, как создать точную копию демонстрационной конечной точки, которая использовалась в предыдущем разделе.
Здесь представлены основные понятия, необходимые для понимания JEA, включая конфигурации сеансов и возможности ролей PowerShell. 

### Конфигурации сеансов PowerShell
При работе JEA в предыдущем разделе вы начали со следующей команды:

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEA_Demo -Credential $NonAdminCred
```

Хотя большинство параметров говорят сами за себя, параметр *ConfigurationName* сначала может показаться противоречивым.
Этот параметр задается в конфигурации сеанса PowerShell, к которому вы подключаетесь. 

*Конфигурация сеанса PowerShell* — еще один термин для обозначения конечной точки PowerShell.
Это то "место", где пользователи могут подключаться и получать доступ к функциональным возможностям PowerShell.
В зависимости от настройки конфигурация сеанса может предоставлять подключающимся пользователям различные функциональные возможности.
В JEA конфигурации сеансов используются для того, чтобы ограничить PowerShell определенным набором функциональных возможностей и вести работу от имени привилегированной виртуальной учетной записи.

На вашем компьютере уже есть несколько зарегистрированных конфигураций сеансов PowerShell, каждая из которых настроена несколько иначе, чем остальные.
Большинство из них входят в состав Windows, но конфигурация сеанса "JEA_Demo" была настроена в разделе [предварительных требований](#prerequisites).
Чтобы увидеть все зарегистрированные конфигурации сеансов, выполните в командной строке администратора PowerShell следующую команду:

```PowerShell
Get-PSSessionConfiguration
```

### Файлы конфигурации сеансов PowerShell
Новые конфигурации сеансов PowerShell создаются путем регистрации новых *файлов конфигурации сеансов PowerShell*.
Файлы конфигурации сеансов имеют расширение PSSC.
Файл конфигурации сеанса можно создать с помощью командлета New-PSSessionConfigurationFile.

Теперь создадим и зарегистрируем новую конфигурацию сеанса для JEA. 

### Создание и изменение конфигурации сеанса PowerShell
Для создания "каркасного" файла конфигурации сеанса PowerShell выполните следующую команду:

```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

> **Совет.** По умолчанию каркасный файл включает только основные настройки конфигурации.
> Чтобы включить в создаваемый PSSC-файл все применимые настройки, используйте параметр `-Full`.

Откройте файл в интегрированной среде сценариев PowerShell или в любом удобном текстовом редакторе.

```PowerShell
ise "$env:ProgramData\JEAConfiguration\JEADemo2.pssc" 
```

Измените в нем следующие поля, указав приведенные ниже значения (не забудьте указать собственную группу безопасности без прав администратора). 

```PowerShell
# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: # RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{'CONTOSO\JEA_NonAdmin_Operator' = @{ RoleCapabilities =  'Maintenance' }}
```

Вот что означает каждая из этих записей:

1.  Поле *SessionType* определяет предустановленные параметры по умолчанию для конечной точки.
*RestrictedRemoteServer* определяет минимальный набор параметров, необходимых для удаленного управления. По умолчанию конечная точка *RestrictedRemoteServer* имеет параметры Get-Command, Get-FormatData, Select-Object, Get-Help, Measure-Object, Exit-PSSession, Clear-Host и Out-Default.
Она устанавливает для параметра *ExecutionPolicy* значение *RemoteSigned*, а для параметра *LanguageMode* значение *NoLanguage*.
По итогам применения этих параметров создается минимальная безопасная основа для настройки конечной точки.

2.  Поле *RoleDefinitions* назначает возможности ролей для отдельных групп.
Оно определяет, какие действия разрешает выполнять привилегированная учетная запись.
В этом поле можно указать функциональные возможности, которые будут предоставлены подключившемуся пользователю в зависимости от членства в группах.
Это основные функциональные возможности элемента RBAC в JEA.
В этом примере членам группы "Contoso\JEA_NonAdmin_Operator" предоставляются возможности роли "Demo".

3.  Поле *RunAsVirtualAccount* означает, что PowerShell следует запустить от имени виртуальной учетной записи в этой конечной точке.
По умолчанию виртуальная учетная запись входит во встроенную группу администраторов.
На контроллере домена она также по умолчанию входит в группу администраторов домена.
Далее в этом руководстве вы узнаете, как настроить права доступа для виртуальной учетной записи.

4.  Поле *TranscriptDirectory* определяет, где будут сохраняться созданные детализированные записи PowerShell с "подсматриванием" после каждого удаленного сеанса.
Эти записи позволяют отслеживать, какие действия были выполнены в каждом сеансе.
Дополнительные сведения о записях PowerShell см. в этой [записи в блоге](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).
Примечание. В обычные журналы событий Windows также записываются данные о том, какие команды каждый пользователь выполнил в PowerShell.
При этом записи, создаваемые здесь, более удобны для чтения.

Наконец, сохраните изменения в *JEADemo2.pssc*.

### Применение конфигурации сеанса PowerShell 

Для создания конечной точки из файла конфигурации сеанса необходимо зарегистрировать файл.
При этом требуется несколько фрагментов данных:

1. Путь к файлу конфигурации сеанса.
2. Имя зарегистрированной конфигурации сеанса. Это то же имя, которое пользователи указывают как значение параметра "ConfigurationName" при подключении конечной точки к `Enter-PSSession` или `New-PSSession`.

Чтобы зарегистрировать конфигурацию сеанса на локальном компьютере, выполните следующую команду:

```PowerShell
Register-PSSessionConfiguration -Name 'JEADemo2' -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

Все готово. Вы настроили конечную точку JEA.

### Тестирование конечной точки
Повторите шаги, указанные в разделе [Использование JEA](#using-jea), с новой конечной точкой, чтобы убедиться в том, что она работает, как предполагалось.
Задавая имя конфигурации в команде Enter-PSSession, используйте имя новой конечной точки (JEADemo2).

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
```

### Основные понятия
**Конфигурация сеанса PowerShell**: иногда называется *конечной точкой PowerShell*; это то "место", где пользователи могут подключаться к PowerShell и получать доступ к его функциональным возможностям.
Чтобы получить список конфигураций сеансов, зарегистрированных в системе, выполните команду `Get-PSSessionConfiguration`.
При определенной настройке конфигурацию сеанса PowerShell можно назвать *конечной точкой JEA*.

**Файл конфигурации сеанса PowerShell (PSSC)**: файл, который, будучи зарегистрированным, определяет параметры конфигурации сеанса PowerShell.
Он содержит спецификации для ролей пользователей, которые могут подключаться к конечной точке, виртуальную запись, с использованием которой он запускается, и многое другое.     

**Определения ролей**: поле в файле конфигурации сеанса, задающее возможности ролей, предоставляемые подключающимся пользователям.
Оно определяет, *кому* и *какие* действия разрешает выполнять привилегированная учетная запись.
Это основные функциональные возможности RBAC в JEA.

**SessionType**: поле в файле конфигурации сеанса, представляющее параметры по умолчанию для конфигурации сеанса.
У конечных точек JEA оно должно иметь значение RestrictedRemoteServer.

**PowerShell Transcript**: файл, содержащий представление сеанса PowerShell с "подсматриванием".
В PowerShell можно настроить создание записей сеансов JEA с помощью поля TranscriptDirectory.
Дополнительные сведения о записях см. в этой [записи в блоге](https://technet.microsoft.com/en-us/magazine/ff687007.aspx).

## Возможности ролей

### Обзор
В предыдущем разделе вы узнали, что поле RoleDefinitions определяет, какие группы имеют доступ к отдельным возможностям ролей.
Вероятно, вы задумались о том, что такое возможности ролей?
Ответ находится в этом разделе.  

## Введение в возможности ролей PowerShell
Возможности ролей PowerShell определяют, что именно сможет делать пользователь в конечной точке JEA.
Они содержат подробный список таких вещей, как видимые команды, видимые приложения и многое другое.
Возможности ролей определяются файлами с расширением PSRC.

## Содержимое возможностей роли
Начнем с изучения и изменения демонстрационного файла возможностей роли, который мы использовали раньше.
Допустим, вы развернули конфигурацию сеанса в своей среде, но получили указание изменить предоставляемые пользователям возможности.
У операторов должна быть возможность перезапускать компьютеры, а также получать информацию о параметрах их сетей.
Кроме того, группа, отвечающая за безопасность, сообщила вам, что разрешать пользователям выполнять команду Restart-Service без ограничений недопустимо.
Список служб, которые может перезапускать оператор, необходимо ограничить.

Для внесения этих изменений запустите интегрированную среду сценариев PowerShell и откройте следующий файл:

```
C:\Program Files\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc
```

Теперь найдите и измените в этом файле следующие строки: 

```PowerShell
# OLD: VisibleCmdlets = 'Restart-Service'
VisibleCmdlets = 'Restart-Computer',
                 @{
                     Name = 'Restart-Service'
                     Parameters = @{ Name = 'Name'; ValidateSet = 'Spooler' }
                 },
                 'NetTCPIP\Get-*'

# OLD: VisibleExternalCommands = 'Item1', 'Item2'
VisibleExternalCommands = 'C:\Windows\system32\ipconfig.exe'
```

Здесь есть несколько интересных примеров:

1.  Вы ограничили выполнение команды Restart-Service таким образом, что операторы могут выполнять ее только с параметром -Name и использовать для этого параметра только аргумент "Spooler".
При желании доступные аргументы можно ограничить с помощью регулярного выражения, указав "ValidatePattern" вместо "ValidateSet".

2.  Вы предоставили доступ ко всем командам с глаголом "Get" из модуля NetTCPIP.
Так как команды "Get" обычно не изменяют системные данные, это относительно безопасное действие.
С другой стороны, настоятельно рекомендуется тщательно изучать все команды, предоставляемые через JEA.

3.  Вы предоставили доступ к исполняемому файлу (ipconfig), используя VisibleExternalCommands.
С помощью этого поля можно также предоставить доступ ко всем сценариям PowerShell.
Очень важно всегда указывать полный путь ко внешним командам, чтобы вместо нужной программы не была выполнена одноименная (и, возможно, вредоносная) программа, указанная в пути пользователя.

Сохраните файл, а затем еще раз подключитесь к демонстрационной конечной точке, чтобы убедиться в том, что изменения сработали.

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
Get-Command
```
Так как вы изменили только файл возможностей роли, регистрировать конфигурацию сеанса заново не нужно.
При подключении пользователя PowerShell автоматически находит обновленные возможности роли.
Так как возможности роли загружаются при запуске сеанса, изменения в файлах возможностей ролей не влияют на существующие сеансы.

Теперь убедитесь, что вы можете перезапустить компьютер, выполнив команду Restart-Computer с параметром -WhatIf (если только перезагрузка компьютера не требуется вам на самом деле).

```PowerShell
Restart-Computer -WhatIf 
```

Убедитесь, что вы можете выполнить команду "ipconfig".

```PowerShell
ipconfig
```

Наконец, убедитесь, что команда Restart-Service работает только со службой Spooler.

```PowerShell
Restart-Service Spooler # This should work
Restart-Service WSearch # This should fail 
```

Закончив, выйдите из сеанса.

```PowerShell
Exit-PSSession 
```

### Создание возможностей роли
В следующем разделе мы создадим конечную точку JEA для пользователей службы поддержки AD.
Для подготовки создадим пустой файл возможностей роли, который заполним в этом разделе.
Возможности роли должны создаваться в папке "RoleCapabilities" в допустимом модуле PowerShell, чтобы их можно было использовать при запуске сеанса.

По сути модули PowerShell — это пакеты функциональных возможностей PowerShell.
Они могут содержать функции PowerShell, командлеты, ресурсы DSC, возможности ролей и многое другое.
Чтобы получить сведения о модулях, выполните команду `Get-Help about_Modules` в консоли PowerShell.

Чтобы создать новый модуль PowerShell с пустым файлом возможностей роли, выполните следующие команды:  

```PowerShell
# Create a new folder for the module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module' -ItemType Directory

# Add a module manifest to contain metadata for this module.
New-ModuleManifest -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psd1' -RootModule Contoso_AD_Module.psm1

# Create a blank script module. You'll use this for custom functions in the next section.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1' -ItemType File 

# Create a RoleCapabilities folder in the AD_Module folder. PowerShell expects Role Capabilities to be located in a "RoleCapabilities" folder within a module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities' -ItemType Directory

# Create a blank Role Capability in your RoleCapabilities folder. Running this command without any additional parameters just creates a blank template.
New-PSRoleCapabilityFile -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc' 
```

Поздравляем, вы создали пустой файл возможностей роли.
Он будет использоваться в следующем разделе.

### Основные понятия
**Возможности роли PowerShell (PSRC)**: файл, определяющий, что именно может делать пользователь в конечной точке JEA.
Он содержит подробный список таких вещей, как видимые команды, видимые приложения консоли и многое другое.
Чтобы среда PowerShell обнаруживала возможности ролей, необходимо поместить их в папку RoleCapabilities в допустимом модуле PowerShell.

**Модуль PowerShell**: пакет функциональных возможностей PowerShell.
Может содержать функции PowerShell, командлеты, ресурсы DSC, возможности ролей и многое другое.
Для автоматической загрузки модули PowerShell должны находиться в папке `$env:PSModulePath`. 

## От начала до конца — Active Directory
Допустим, область применения вашей программы расширилась.
Теперь вы отвечаете за добавление JEA на контроллеры доменов для выполнения действий Active Directory.
Сотрудники службы поддержки будут использовать JEA для разблокировки учетных записей, сброса паролей и других подобных действий.

Вам необходимо предоставить доступ к совершенно иному набору команд другой группе людей.
Кроме того, у вас есть ряд уже существующих сценариев Active Directory, доступ к которым нужно предоставить.
В этом разделе вы узнаете, как создать конфигурацию сеанса и возможности роли для этой задачи.

### Необходимые компоненты
Для выполнения пошаговых инструкций в этом разделе необходимо работать на контроллере домена.
Если у вас нет доступа к контроллеру домена, не волнуйтесь.
Попробуйте сделать то же самое, работая по другому сценарию или в другой роли, которые вам знакомы.
Инструкции по быстрой настройке нового контроллера домена см. в приложении [Создание контроллера домена](#creating-a-domain-controller).

### Процедура создания возможностей роли и конфигурации сеанса

На первый взгляд создание возможностей роли может показаться сложным, но мы разделим эту процедуру на несколько простых шагов:

1.  Определить включаемые задачи.
2.  Ограничить эти задачи при необходимости.
3.  Убедиться, что они работают с JEA.
4.  Поместить их в файл возможностей роли.
5.  Зарегистрировать конфигурацию сеанса, предоставляющую возможности роли.

### Шаг 1. Определение необходимых задач
Прежде чем создавать возможности роли или конфигурацию сеанса, необходимо определить все задачи, которые пользователи должны будут выполнять через конечную точку JEA, а также порядок их выполнения с помощью PowerShell.
Для этого необходимо провести большую работу по сбору и изучению требований.
То, как вы будете это делать, зависит от вашей организации и целей.
Важно понимать, что на практике сбор и анализ требований составляют критически важную часть работы.
Это, вероятно, самый сложный этап в процессе внедрения JEA.

#### Поиск ресурсов
Во время исследовательской работы при создании конечной точки управления Active Directory вам могут пригодиться следующие интернет-ресурсы:
-   [Обзор Active Directory PowerShell](http://blogs.msdn.com/b/adpowershell/archive/2009/03/05/active-directory-powershell-overview.aspx) 
-   [Руководство по Windows PowerShell для Active Directory](http://blogs.technet.com/b/ashleymcglone/archive/2013/01/02/free-download-cmd-to-powershell-guide-for-ad.aspx)

#### Составление списка
В остальной части этого раздела вы будете работать с указанными ниже десятью действиями.
Помните, что это просто пример, и требования вашей организации могут отличаться:

|Действие                                                         |Команда PowerShell                                             |
|---------------------------------------------------------------|---------------------------------------------------------------|
|Разблокирование учетной записи                                                 |`Unlock-ADAccount`                                             |
|Сброс пароля                                                 |`Set-ADAccountPassword` и `Set-ADUser -ChangePasswordAtLogon`|
|Изменение должности пользователя                                          |`Set-ADUser -Title`                                            |  
|Поиск заблокированных, отключенных, неактивных и других учетных записей AD |`Search-ADAccount`                                             | 
|Добавление пользователя в группу                                              |`Add-ADGroupMember -Identity (with whitelist) -Members`        | 
|Удаление пользователя из группы                                         |`Remove-ADGroupMember -Identity (with whitelist) -Members`     | 
|Включение учетной записи пользователя                                          |`Enable-ADAccount`                                             |
|Удаление учетной записи пользователя                                         |`Disable-ADAccount`                                            |

### Шаг 2. Ограничение задач при необходимости

Теперь, когда у вас есть список действий, продумайте возможности каждой команды.
Это нужно сделать по двум причинам.

1.  Пользователям очень легко предоставить больше возможностей, чем планировалось.
Например, `Set-ADUser` — невероятно мощная и гибкая команда.
Не все ее возможности стоит предоставлять пользователям службы поддержки.  

2.  Хуже того, существует возможность предоставлять доступ к командам, позволяющим пользователям обходить ограничения JEA.
В этом случае JEA перестает служить рубежом безопасности.
Будьте внимательны при выборе команд.
Например, команда Invoke-Expression позволит пользователям выполнять код без ограничений.
Дополнительное обсуждение этой темы см. в разделе "Рекомендации по ограничению команд".

Просмотрев все команды, вы можете добавить следующие ограничения:

1.  `Set-ADUser` может выполняться только с параметром "-Title"; 

2.  `Add-ADGroupMember` `Remove-ADGroupMember` может работать только с определенными группами.

### Шаг 3. Контроль работы задач с JEA
Фактически в ограниченной среде JEA эти командлеты можно оптимизировать.
JEA выполняется в режиме *без языка*, что, кроме прочего, не дает пользователям использовать переменные.
Для удобства конечных пользователей необходимо проверить несколько моментов.

Возьмем, например, команду `Set-ADAccountPassword`.
Параметр "-NewPassword" требует защищенной строки.
Часто пользователи создают защищенную строку и передают ее как переменную (как показано ниже):

```PowerShell
$newPassword = (Read-Host -Prompt "Specify a new password" -AsSecureString)
Set-ADAccountPassword -Identity mollyd -NewPassword $newPassword -Reset
```

Но режим без языка не позволяет использовать переменные.
Это ограничение можно обойти двумя способами.

1.  Вы можете потребовать, чтобы пользователи выполняли команду без назначения переменных.
Сделать это легко, но операторам будет крайне затруднительно работать с конечной точкой.
Кто захочет вводить эти данные каждый раз при сбросе пароля?
```PowerShell
Set-ADAccountPassword -Identity mollyd -NewPassword (Read-Host -Prompt "Specify a new password" -AsSecureString) -Reset
```

2.  Сложный код можно заключить в сценарий или функцию, которые будут предоставлены конечным пользователям.
Предоставленные сценарии и функции будут выполняться в неограниченном контексте; вы можете написать функции, которые будут использовать переменные и вызывать другие команды без каких-либо трудностей.
Такой подход упрощает работу пользователя, предотвращает ошибки, сокращает необходимую степень понимания PowerShell и препятствует непреднамеренному предоставлению доступа к лишним функциям.
Единственный недостаток — стоимость разработки и обслуживания функции.

#### Шаг в сторону: добавление функции в модуль
Выберем второй подход и напишем функцию PowerShell `Reset-ContosoUserPassword`.
Эта функция будет делать все, что должно происходить при сбросе пароля пользователя.
В вашей организации она может включать сложные, замысловатые действия.
Так как это лишь пример, ваша команда сбросит пароль и потребует, чтобы пользователь изменил пароль при входе в систему.
Мы добавим ее в модуль Contoso_AD_Module, который вы создали в предыдущем разделе.

1. В интегрированной среде сценариев PowerShell откройте файл Contoso_AD_Module.psm1.
```PowerShell
ISE 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1' 
```

2. Нажмите клавиши CTRL+J, чтобы открыть меню фрагментов кода.

3. Найдите в списке слово "функция" и нажмите клавишу ВВОД.
Будет создан каркас для функции.

4. Измените имя функции на Reset-ContosoUserPassword.  

5. Измените имя одного из параметров на Identity и удалите второй.

6. Скопируйте следующий код в тело функции.
```PowerShell
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
```

7. Сохраните файл.
Должен получиться код следующего вида:
```PowerShell
function Reset-ContosoUserPassword ($Identity)
{
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
} 
```
Теперь пользователи смогут просто вызвать команду `Reset-ContosoUserPassword` — им не придется запоминать синтаксис для создания безопасной строки.

### Шаг 4. Изменение файла с возможностями роли
В разделе [Создание возможностей роли](#role-capability-creation) вы создали пустой файл возможностей роли.
В этом разделе мы заполним его значениями.

Сначала откройте файл возможностей роли в интегрированной среде сценариев.
```PowerShell
ise 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc' 
```
Внесите в файл следующие изменения:
```PowerShell
# OLD: VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }
VisibleCmdlets =
    'Unlock-ADAccount',
    'Search-ADAccount',
    'Enable-ADAccount',
    'Disable-ADAccount',
    @{ Name = 'Set-ADUser'; Parameters = @{ Name = 'Title'; ValidateSet = 'Manager', 'Engineer' }},
    @{ Name = 'Add-ADGroupMember'; Parameters = 
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}},
    @{ Name = 'Remove-ADGroupMember'; Parameters = 
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}}
  
# OLD: VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }   
VisibleFunctions = 'Reset-ContosoUserPassword'
```

При этом необходимо обратить внимание на следующее.
1.  PowerShell попытается автоматически загрузить модули, необходимые для ваших возможностей роли.
Если этого не происходит, явно перечислите имена модулей в поле "ModulesToImport".

2.  Если вы не уверены, является команда командлетом или функцией, выполните `Get-Command` и проверьте параметр "CommandType".

3.  ValidatePattern позволяет ограничить аргументы параметра с помощью регулярного выражения, если определить набор допустимых значений непросто.
Определить ValidatePattern и ValidateSet для отдельного параметра одновременно невозможно.

### Шаг 5. Регистрация новой конфигурации сеанса
Далее создадим новый файл конфигурации сеанса, который будет предоставлять возможности роли членам группы AD "JEA_NonAdmin_HelpDesk". 

Для начала создайте и откройте пустой файл конфигурации сеанса в интегрированной среде сценариев PowerShell.
```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc" 
ise "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
```
Измените значения следующих полей в PSSC-файле.
Если вы работаете в собственной среде, замените "CONTOSO\JEA_NonAdmins_Helpdesk" на имя собственного пользователя или группы без прав администратора.
```PowerShell
# OLD: Description = ''
Description = 'An endpoint for active directory tasks.' 

# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{ 'CONTOSO\JEA_NonAdmin_HelpDesk' = @{ RoleCapabilities =  'ADHelpDesk' }} 
```
Сохранение и регистрация конфигурации сеанса
```PowerShell
Register-PSSessionConfiguration -Name ADHelpDesk -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc" 
```
### Тестирование
Получите учетные данные пользователя без прав администратора:
```PowerShell
$HelpDeskCred = Get-Credential
```
Если вы выполнили указания из раздела "Настройка пользователей и групп", это будут следующие учетные данные:
-   Имя пользователя: HelpDeskUser
-   Пароль: pa$$w0rd

Установите удаленное подключение к конечной точке службы поддержки AD, используя учетные данные без прав администратора:
```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName ADHelpDesk -Credential $HelpDeskCred 
```
Используйте команду Set-ADUser для сброса должности пользователя.
```PowerShell
Set-ADUser -Identity OperatorUser -Title Engineer 
```
Убедитесь, что должность изменилась.
```PowerShell
Get-ADUser -Identity OperatorUser -Property Title 
```
Теперь используйте команду Add-ADGroupMember, чтобы добавить пользователя в TestGroup.
Примечание. Группа TestGroup должна быть создана заранее.
```PowerShell
Add-ADGroupMember TestGroup -Member OperatorUser -Verbose 
```
Завершите сеанс:
```PowerShell
Exit-PSSession
```
### Основные понятия
**Режим без языка**: когда PowerShell работает в режиме без языка (NoLanguage), пользователи могут выполнять только команды, но не могут использовать какие-либо элементы языка.
Чтобы получить дополнительные сведения, запустите `Get-Help about_Language_Modes`.

**Функции PowerShell**: функции PowerShell — это элементы кода PowerShell, которые можно вызывать по имени.
Чтобы получить дополнительные сведения, запустите `Get-Help about_Functions`.

**ValidateSet или ValidatePattern**: предоставляя доступ к команде, вы можете ограничить действительные аргументы для определенных параметров.
ValidateSet — это конкретный список допустимых команд.
ValidatePattern — это регулярное выражение, которому должны соответствовать аргументы для этого параметра.

## Обслуживание и развертывание на нескольких компьютерах
К этому моменту вы уже неоднократно развертывали JEA в локальных системах.
Так как ваша рабочая среда может включать не один компьютер, а несколько, нужно выполнить критически важные шаги в процессе развертывания и повторить их на каждом компьютере.

### Шаги на высоком уровне.
1.  Скопируйте модули (с возможностями ролей) в каждый узел.
2.  Скопируйте файлы конфигурации сеансов на каждый узел.
3.  Выполните `Register-PSSessionConfiguration` с конфигурацией сеанса.
4.  Сохраните копию конфигурации сеанса и наборы инструментов в безопасном месте.
Внося изменения, хорошо иметь исходный эталонный образец.

### Пример сценария
Рассмотрим пример сценария развертывания.
Чтобы использовать его в среде, необходимо вставить имена и пути реальных общих папок и модулей.
```PowerShell
# First, copy the session configuration and modules (containing role capability files) onto a file share you have access to.
Copy-Item -Path 'C:\Demo\Demo.pssc' -Destination '\\FileShare\JEA\Demo.pssc'
Copy-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\SomeModule\' -Recurse -Destination '\\FileShare\JEA\SomeModule'

# Next, author a setup script (C:\JEA\Deploy.ps1) to run on each individual node
    # Contents of C:\JEA\Deploy.ps1
    New-Item -ItemType Directory -Path C:\JEADeploy
    Copy-Item -Path '\\FileShare\JEA\Demo.pssc' -Destination 'C:\JEADeploy\'
    Copy-Item -Path '\\FileShare\JEA\SomeModule' -Recurse -Destination 'C:\Program Files\WindowsPowerShell\Modules' # Remember, Role Capability Files are found in modules
    if (Get-PSSessionConfiguration -Name JEADemo -ErrorAction SilentlyContinue)
    {
        Unregister-PSSessionConfiguration -Name JEADemo -ErrorAction Stop
    }

    Register-PSSessionConfiguration -Name JEADemo -Path 'C:\JEADeploy\Demo.pssc'
    Remove-Item -Path 'C:\JEADeploy' # Don't forget to clean up!

# Now, invoke the script on all of the target machines.
# Note: this requires PowerShell Remoting be enabled on each machine. Enabling PowerShell remoting is a requirement to use JEA as well.
# You may need to provide the "-Credential" parameter if your current user account does not have admin permissions on these machines.
Invoke-Command –ComputerName 'Node1', 'Node2', 'Node3', 'NodeN' -FilePath 'C:\JEA\Deploy.ps1'

# Finally, delete the session configuration and role capability files from the file share.
Remove-Item -Path '\\FileShare\JEA\Demo.pssc'
Remove-Item -Path '\\FileShare\JEA\SomeModule' -Recurse
```
### Изменение возможностей
При работе с несколькими компьютерами важно вносить изменения согласованно.
Когда у JEA появится ресурс DSC, это позволит обеспечить синхронизацию среды.
Пока же настоятельно рекомендуем сохранять мастер-копии конфигураций сеансов и обращаться к ним при каждом изменении.

### Удаление возможностей
Чтобы удалить конфигурацию JEA из системы, выполните на каждом компьютере следующую команду:
```PowerShell
Unregister-PSSessionConfiguration -Name JEADemo 
```
## Отчеты о JEA
Так как JEA позволяет непривилегированным пользователям работать в привилегированном контексте, ведение журнала и аудит получают особое значение.
В этом разделе мы рассмотрим инструменты, которые помогут вам вести журналы и отчетность.

### Отчеты о действиях JEA
#### Запись с "подсматриванием"
Один из самых быстрых способов понять, что происходит в сеансе PowerShell, — просто подсмотреть за пользователем.
Вы увидите команды, результаты выполнения этих команд и убедитесь, что все в порядке.
Если что-то не так, вы по меньшей мере об этом узнаете.
Запись PowerShell позволяет получить похожее представление постфактум.

При использовании поля "TranscriptDirectory" в конфигурации сеанса PowerShell автоматически запишет все действия пользователя, предпринятые в течение данного сеанса.
Записи сеансов см. в документе, который находится в папке "$env:ProgramData\JEAConfiguration\Transcripts".

Как можно видеть, запись содержит сведения о подключенном пользователе, пользователе, от имени которого ведется работа, выполняемые в ходе сеанса команды и многое другое.
Дополнительные сведения о записях PowerShell см. в этой [записи в блоге](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).

#### Журналы событий PowerShell
После того как вы включите запись журнала модуля, все действия PowerShell будут также записываться в обычные журналы событий Windows.
Работать с ними сложнее, чем с записями, но журналы обеспечивают более глубокий уровень детализации.

Если ведение журнала модулей включено, по идентификатору события 4104 в журнале операций PowerShell можно видеть запись всех вызванных команд.

#### Другие журналы событий
В отличие от журналов и записей PowerShell, другие механизмы ведения журнала не записывают действия подключенного пользователя.
Для сопоставления предпринятых действий потребуется соотнести журналы PowerShell и другие журналы.

По идентификатору события 193 в журнале операций "Служба удаленного управления Windows" будут записаны SID и имя подключенного пользователя, а также SID виртуальной учетной записи запуска от имени для подобного соотнесения.
Как вы могли заметить, имя виртуальной учетной записи запуска от имени заканчивается именем домена и именем подключенного пользователя.

### Отчеты о конфигурации JEA
#### Get-PSSessionConfiguration
Для получения точных отчетов о состоянии среды важно знать, сколько конечных точек JEA настроено на вашем компьютере.
`Get-PSSessionConfiguration` делает именно это.
 
#### Get-PSSessionCapability
Создавать отчеты по возможностям того или иного пользователя через конечную точку JEA может быть непросто.
Для этого иногда придется проверить несколько отдельных возможностей ролей.
К счастью, с этой задачей справляется командлет "Get-PSSessionCapability".

Чтобы убедиться, выполните следующую команду в командной строке администратора PowerShell:
```PowerShell
Get-PSSessionCapability -Username 'CONTOSO\OperatorUser' -ConfigurationName JEADemo
```
## Заключение 
Изучив это руководство, вы получили средства и знания, позволяющие создать собственную конечную точку JEA. Спасибо за участие!

## Приложение

## Основные понятия, используемые в этом руководстве
**Удаленное взаимодействие PowerShell**: удаленное взаимодействие PowerShell позволяет выполнять команды PowerShell с удаленных компьютеров.
Можно работать с одного или нескольких компьютеров и использовать временные или постоянные подключения.
В этой демонстрации вы устанавливаете удаленное подключение к локальному компьютеру через интерактивный сеанс.
JEA ограничивает функциональные возможности, доступные через службу удаленного взаимодействия PowerShell.
Чтобы получить дополнительные сведения об удаленном взаимодействии PowerShell, выполните `Get-Help about_Remote`.

**Пользователь запуска от имени**: при использовании JEA пользователь без прав администратора работает от имени привилегированной виртуальной учетной записи.
Виртуальная учетная запись действует только во время удаленного сеанса.
Иными словами, она создается при подключении пользователя к конечной точке и удаляется, когда пользователь завершает сеанс.
По умолчанию виртуальная учетная запись входит в локальную группу администраторов.
На контроллере домена он входит в группу администраторов домена.
Виртуальные учетные записи являются локальными для компьютера, на котором они были созданы, и не имеют разрешений за его пределами.
Это означает, что они не зарегистрированы в Active Directory (им не назначен RID).
Кроме того, если разрешенная команда или сценарий пытаются получить доступ к ресурсам за пределами локального компьютера, они будут обращаться к этим ресурсам, используя удостоверение компьютера, а не виртуальной учетной записи.

**Подключенный пользователь**: пользователь без прав администратора, который подключается к конечной точке JEA и которому назначаются роли.
Все команды этого пользователя выполняются в контексте пользователя запуска от имени или виртуальной учетной записи.


### Создание контроллера домена

В этом документе предполагается, что компьютер уже присоединен к домену.
Если сейчас у вас нет домена для присоединения, этот раздел поможет вам быстро настроить контроллер домена с помощью DSC.

#### Необходимые компоненты

1.  Компьютер находится во внутренней сети.
2.  Компьютер не присоединен к существующему домену.
3.  Компьютер работает под управлением Windows Server 2016 или на нем установлена платформа WMF 5.0.

#### Установка xActiveDirectory
Если компьютер имеет активное подключение к Интернету, выполните следующую команду в окне PowerShell с повышенными привилегиями:
```PowerShell
Install-Module xActiveDirectory -Force 
```
Если подключения к Интернету нет, установите xActiveDirectory на другой компьютер и скопируйте папку xActiveDirectory в папку "C:\Program Files\WindowsPowerShell\Modules" на вашем компьютере.

Чтобы проверить успешность установки, выполните следующую команду:
```PowerShell
Get-Module xActiveDirectory -ListAvailable
``` 

#### Настройка имени домена
Скопируйте приведенный ниже сценарий в PowerShell, чтобы сделать компьютер контроллером нового домена.
**ПРИМЕЧАНИЕ АВТОРА: ИЗВЕСТНО, ЧТО СУЩЕСТВУЕТ ПРОБЛЕМА, ПРИ КОТОРОЙ УКАЗАННЫЕ УЧЕТНЫЕ ДАННЫЕ НЕ ИСПОЛЬЗУЮТСЯ.  В ЦЕЛЯХ БЕЗОПАСНОСТИ НЕ ЗАБЫВАЙТЕ СВОЙ ПАРОЛЬ ЛОКАЛЬНОГО АДМИНИСТРАТОРА.**

```PowerShell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value $env:COMPUTERNAME -Force 

# This "MetaConfiguration" sets the DSC Engine to automatically reboot if required
[DscLocalConfigurationManager()]
Configuration MetaConfiguration
{
    Node $env:Computername
    {
        Settings
        {
            RebootNodeIfNeeded = $true
        }
    }
    
}

MetaConfiguration
# Apply the MetaConfiguration
Set-DscLocalConfigurationManager .\MetaConfiguration

# Configure a domain controller of a new "Contoso" domain
configuration DomainController
{
    param
    (
        $node,
        $cred
    )
    Import-DscResource -ModuleName xActiveDirectory

    Node $node
    {
        WindowsFeature ADDS
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain Contoso
        {
            DomainName = 'contoso.com'
            DomainAdministratorCredential = $cred
            SafemodeAdministratorPassword = $cred
            DependsOn = '[WindowsFeature]ADDS'
        }

        file temp
        {
            DestinationPath = 'C:\temp.txt'
            Contents = 'Domain has been created'
            DependsOn = '[xADDomain]Contoso'
        }
    }
}

$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = $env:Computername
            PSDscAllowPlainTextPassword = $true
        }
    )
}

# Enter your desired password for the domain administrator (note, this will be stored as plain text)
DomainController -cred (Get-Credential -Message "Enter desired credential for domain administrator") -node $env:Computername -configurationData $ConfigData

# Apply the configuration to create the domain controller
Start-DSCConfiguration -path .\DomainController -ComputerName $env:Computername -Wait -Force -Verbose
```
Компьютер перезагрузится несколько раз.
Вы узнаете, что процесс завершен, как только будет создан файл с именем "C:\temp.txt", содержащий текст "Domain has been created" (Домен создан). 

#### Настройка пользователей и групп
Следующие команды настроят группы операторов и службы поддержки в вашем домене и учетную запись соответствующего пользователя без прав администратора, входящего в эту группу.
```PowerShell
# Make Groups
$NonAdminOperatorGroup = New-ADGroup -Name "JEA_NonAdmin_Operator" -GroupScope DomainLocal -PassThru
$NonAdminHelpDeskGroup = New-ADGroup -Name "JEA_NonAdmin_HelpDesk" -GroupScope DomainLocal -PassThru
$TestGroup = New-ADGroup -Name "Test_Group" -GroupScope DomainLocal -PassThru

# Make Users
$OperatorUser = New-ADUser -Name "OperatorUser" -AccountPassword (ConvertTo-SecureString "pa`$`$w0rd" -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $OperatorUser

$HelpDeskUser = New-ADUser -name "HelpDeskUser" -AccountPassword (ConvertTo-SecureString "pa`$`$w0rd" -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $HelpDeskUser

# Add Users to Groups
Add-ADGroupMember -Identity $NonAdminOperatorGroup -Members $OperatorUser
Add-ADGroupMember -Identity $NonAdminHelpDeskGroup -Members $HelpDeskUser
```

### О запрещенных списках
Познакомившись с JEA, вы можете задуматься о том, можно ли добавлять команды в запрещенный список.
Эта потребность понятна, но сейчас ее реализация в JEA не планируется по следующим причинам.

1.  Мы разработали JEA для того, чтобы операторы получали доступ только к тем действиям, которые им необходимы.
Запрещенный список имеет противоположное назначение.

2.  Авторы команд PowerShell не разрабатывали свои команды для JEA.
Сразу после установки Windows Server 2016 предоставляет около 1520 команд.
Модели угроз для этих команд не учитывают вероятность того, что пользователь будет вести работу от имени более привилегированной учетной записи.
Например, некоторые команды по своему назначению позволяют внедрять код (например, Add-Type и Invoke-Command в основном модуле PowerShell).
JEA может предупредить вас при предоставлении доступа к некоторым известным нам командам, но мы не проверяли остальные команды в Windows в соответствии с новой моделью угрозы.
Необходимо понимать возможности команд, к которым вы предоставляете доступ через JEA.  

3.  Кроме того, даже если бы среда JEA блокировала все команды, уязвимые для внедрения кода, нет никаких гарантий того, что злоумышленник не сможет выполнить действие из запрещенного списка с помощью другой аналогичной команды.
Если вы не понимаете, к каким командам предоставляете доступ, то не сможете гарантировать невозможность того или иного действия.
Именно вы должны понимать, к каким командам предоставляете доступ, независимо от того, используется ли в них запрещенный или разрешенный список.
Состав команд, которые остались бы доступны при использовании запрещенного списка, контролировать нельзя, поэтому вместо этого в JEA применяются разрешенные списки.

### Рекомендации по ограничениям команд
На этом этапе необходимо обратить внимание на один важный момент.
Все возможности, предоставляемые через JEA, находятся в областях, ограниченных правами администратора.
Пользователи без прав не должны иметь возможность изменять используемые сценарии через конечные точки JEA.

Кроме того, ни в коем случае нельзя предоставлять пользователям JEA возможность перезаписывать конфигурации JEA и сценарии из разрешенного списка во время сеансов JEA.
Будьте особенно внимательны, предоставляя доступ к таким командам, как `Copy-Item`.

### Распространенные проблемы возможностей ролей
При самостоятельной работе вы можете столкнуться с несколькими распространенными проблемами.
Вот краткое руководство по тому, как выявлять и устранять такие проблемы при изменении или создании новой конечной точки.

#### Функции. Командлеты
Команды PowerShell, написанные в PowerShell, являются функциями PowerShell.
Команды PowerShell, написанные как специализированные классы .NET, являются командлетами PowerShell.
Тип команды можно проверить, выполнив `Get-Command`.

#### VisibleProviders 
Вам потребуется предоставить доступ ко всем поставщикам, необходимым для ваших команд.
Чаще всего используется поставщик FileSystem, но может потребоваться доступ и к другим поставщикам, таким как Registry.
Вводные сведения о поставщиках см. в записи в блоге [Эй, сценарист](http://blogs.technet.com/b/heyscriptingguy/archive/2015/04/20/find-and-use-windows-powershell-providers.aspx).
Будьте внимательны, предоставляя доступ к поставщикам: зачастую лучше определить собственную функцию, которая будет работать с соответствующими базовыми поставщиками, чем напрямую предоставлять доступ к поставщику в сеансе JEA.
Таким образом вы можете дать пользователям возможность работать с файлами, разделами реестра и т. д., но при этом сохраните контроль над тем, с **какими* из них они могут работать, используя настраиваемую логику проверки.

<!--HONumber=Jun16_HO1-->


