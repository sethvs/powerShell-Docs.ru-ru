---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "от начала до конца — Active Directory"
ms.technology: powershell
ms.sourcegitcommit: 7504fe496a8913718847e45115d126caf4049bef
ms.openlocfilehash: 0a262e2c83174db7041d3cf35d97542b1cac4386

---

# От начала до конца — Active Directory
Допустим, область применения вашей программы расширилась.
Теперь вы отвечаете за добавление JEA на контроллеры доменов для выполнения действий Active Directory.
Сотрудники службы поддержки будут использовать JEA для разблокировки учетных записей, сброса паролей и других подобных действий.

Вам необходимо предоставить доступ к совершенно иному набору команд другой группе людей.
Кроме того, у вас есть ряд уже существующих сценариев Active Directory, доступ к которым нужно предоставить.
В этом разделе вы узнаете, как создать конфигурацию сеанса и возможности роли для этой задачи.

## Необходимые компоненты
Для выполнения пошаговых инструкций в этом разделе необходимо работать на контроллере домена.
Если у вас нет доступа к контроллеру домена, не волнуйтесь.
Попробуйте сделать то же самое, работая по другому сценарию или в другой роли, которые вам знакомы.
Инструкции по быстрой настройке нового контроллера домена см. в приложении [Создание контроллера домена](#creating-a-domain-controller).

## Процедура создания возможностей роли и конфигурации сеанса

На первый взгляд создание возможностей роли может показаться сложным, но мы разделим эту процедуру на несколько простых шагов:

1.  Определить включаемые задачи.
2.  Ограничить эти задачи при необходимости.
3.  Убедиться, что они работают с JEA.
4.  Поместить их в файл возможностей роли.
5.  Зарегистрировать конфигурацию сеанса, предоставляющую возможности роли.

## Шаг 1. Определение необходимых задач
Прежде чем создавать возможности роли или конфигурацию сеанса, необходимо определить все задачи, которые пользователи должны будут выполнять через конечную точку JEA, а также порядок их выполнения с помощью PowerShell.
Для этого необходимо провести большую работу по сбору и изучению требований.
То, как вы будете это делать, зависит от вашей организации и целей.
Важно понимать, что на практике сбор и анализ требований составляют критически важную часть работы.
Это, вероятно, самый сложный этап в процессе внедрения JEA.

### Поиск ресурсов
Во время исследовательской работы при создании конечной точки управления Active Directory вам могут пригодиться следующие интернет-ресурсы:
-   [Обзор Active Directory PowerShell](http://blogs.msdn.com/b/adpowershell/archive/2009/03/05/active-directory-powershell-overview.aspx)
-   [Руководство по Windows PowerShell для Active Directory](http://blogs.technet.com/b/ashleymcglone/archive/2013/01/02/free-download-cmd-to-powershell-guide-for-ad.aspx)

### Составление списка
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

## Шаг 2. Ограничение задач при необходимости

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

### Шаг в сторону: добавление функции в модуль
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

## Шаг 4. Изменение файла с возможностями роли
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

## Шаг 5. Регистрация новой конфигурации сеанса
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
## Тестирование
Получите учетные данные пользователя без прав администратора:
```PowerShell
$HelpDeskCred = Get-Credential
```
Если вы выполнили указания из раздела [Настройка пользователей и групп](creating-a-domain-controller.md#set-up-users-and-groups), это будут следующие учетные данные:
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
## Основные понятия
**Режим без языка**: когда PowerShell работает в режиме без языка (NoLanguage), пользователи могут выполнять только команды, но не могут использовать какие-либо элементы языка.
Чтобы получить дополнительные сведения, запустите `Get-Help about_Language_Modes`.

**Функции PowerShell**: функции PowerShell — это элементы кода PowerShell, которые можно вызывать по имени.
Чтобы получить дополнительные сведения, запустите `Get-Help about_Functions`.

**ValidateSet или ValidatePattern**: предоставляя доступ к команде, вы можете ограничить действительные аргументы для определенных параметров.
ValidateSet — это конкретный список допустимых команд.
ValidatePattern — это регулярное выражение, которому должны соответствовать аргументы для этого параметра.




<!--HONumber=Jun16_HO4-->


