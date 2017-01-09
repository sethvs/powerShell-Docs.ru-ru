---
title: "Выполнение второго прыжка при удаленном взаимодействии PowerShell"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: eslesar
manager: carmonmills
ms.prod: powershell
ms.openlocfilehash: da4cf4f1274f5b0108c1c48ecb44d478cb409165
ms.sourcegitcommit: b88151841dd44c8ee9296d0855d8b322cbf16076
translationtype: HT
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>Выполнение второго прыжка при удаленном взаимодействии PowerShell

"Проблема второго прыжка" относится к ситуации, аналогичной следующей:

1. Вы вошли на сервер _ServerA_.
2. С сервера _ServerA_ вы запускаете удаленный сеанс PowerShell для подключения к серверу _ServerB_.
3. Команда, запущенная вами на сервере _ServerB_ через сеанс удаленного взаимодействия PowerShell, пытается получить доступ к ресурсу на сервере _ServerC_.
4. Доступ к ресурсу на _ServerC_ запрещен, так как учетные данные, используемые вами для создания сеанса удаленного взаимодействия PowerShell, не передаются с сервера _ServerB_ на сервер _ServerC_.

Существует несколько способов для решения этой проблемы. В этом разделе мы рассмотрим некоторые из наиболее популярных решений для проблемы второго прыжка.

## <a name="credssp"></a>CredSSP

Для проверки подлинности можно использовать [протокол CredSSP](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx). Протокол CredSSP кэширует учетные данные на удаленном сервере (_ServerB_), что делает их уязвимыми для атак, направленных на кражу учетных данных. Если безопасность удаленного компьютера нарушена, злоумышленник получает доступ к учетным данным пользователя. Протокол CredSSP по умолчанию отключен на компьютерах клиента и сервера. Включать протокол CredSSP следует только в самых надежных средах. Например, при подключении администратора домена к контроллеру домена, так как контроллер домена является высоконадежным.

Дополнительные сведения о вопросах безопасности при использовании протокола CredSSP для удаленного взаимодействия PowerShell см. в статье [Accidental Sabotage: Beware of CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp) (Непреднамеренный саботаж: берегитесь CredSSP).

Дополнительные сведения об атаках, направленных на хищение учетных данных, см. в техническом документе [Mitigating Pass-the-Hash (PtH) Attacks and Other Credential Theft](https://www.microsoft.com/en-us/download/details.aspx?id=36036).

Пример того, как включить и использовать CredSSP для удаленного взаимодействия PowerShell, см. в разделе [Использование CredSSP для решения проблемы второго прыжка](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).

### <a name="pros"></a>Плюсы

- Это работает для всех серверов с Windows Server 2008 или более поздней версии.

### <a name="cons"></a>Минусы

- Имеет уязвимости.
- Требует настройки как клиентских, так и серверных ролей.

## <a name="kerberos-delegation-unconstrained"></a>Делегирование Kerberos (без ограничений)

Для выполнения второго прыжка можно также использовать делегирование Kerberos без ограничений. Однако этот метод не позволяет управлять тем, где именно используются делегированные учетные данные.

>**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы. Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Плюсы

- Не требует специального кода.

### <a name="cons"></a>Минусы

- Не поддерживает второй прыжок для WinRM.
- Не позволяет управлять тем, где именно используются делегированные учетные данные.

## <a name="kerberos-constrained-delegation"></a>Ограниченное делегирование Kerberos

Для выполнения второго прыжка можно использовать устаревшее ограниченное делегирование (не на основе ресурсов). 

>**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы. Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Плюсы

- Не требует специального кода.

### <a name="cons"></a>Минусы

- Не поддерживает второй прыжок для WinRM.
- Требует настройки для объекта Active Directory удаленного сервера (_ServerB_).
- Ограничен одним доменом. Не может использоваться между доменами или лесами.
- Требует права на обновление объектов и имен субъектов-служб (SPN).

## <a name="resource-based-kerberos-constrained-delegation"></a>Ограниченное делегирование Kerberos на основе ресурсов

С помощью ограниченного делегирования Kerberos на основе ресурсов (которое впервые появилось в Windows Server 2012) можно настроить делегирование учетных данных на объект сервера, где находятся ресурсы.
В описанном выше сценарии второго прыжка вы настраиваете сервер _ServerC_, чтобы указать, откуда он будет принимать делегированные учетные данные.

>**Примечание.** Учетные записи Active Directory, которые имеют набор свойств **Учетная запись важна и не может быть делегирована**, не могут быть делегированы. Дополнительные сведения см. в разделе [Фокус безопасности: анализ свойств "Учетная запись важна и не может быть делегирована" для привилегированных учетных записей](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) и [Средства и параметры проверки подлинности Kerberos](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Плюсы

- Учетные данные не сохраняются.
- Относительно легок в настройке с помощью командлетов PowerShell — специальный код не требуется.
- Не требуется доступ к специальному домену.
- Работает между доменами и лесами.
- Код PowerShell.

### <a name="cons"></a>Минусы

- Требует Windows Server 2012 или более поздней версии.
- Не поддерживает второй прыжок для WinRM.
- Требует права на обновление объектов и имен субъектов-служб (SPN). 

### <a name="example"></a>Пример

Рассмотрим пример, в котором ограниченное делегирование на основе ресурсов PowerShell настраивается на сервере _ServerC_, чтобы разрешить использование делегированных учетных данных с сервера _ServerB_.
В этом примере предполагается, что все серверы работают под управлением Windows Server 2012 или более поздней версии и существует по меньшей мере один контроллер домена Windows Server 2012 в каждом домене, к которому относятся какие-либо из серверов.

Перед настройкой ограниченного делегирования следует добавить компонент `RSAT-AD-PowerShell`, чтобы установить модуль Active Directory PowerShell, а затем импортировать этот модуль в сеанс:

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirector
```
Сейчас параметр несколько доступных командлетов имеют параметр **PrincipalsAllowedToDelegateToAccount**:

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName     
----------- ----                 ----------     
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

Параметр **PrincipalsAllowedToDelegateToAccount** задает атрибут объекта Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, содержащий список управления доступом (ACL), который указывает, какие учетные записи имеют разрешение на делегирование учетных данных для связанной учетной записи (в нашем примере это будет учетная запись компьютера для _сервера_).

Теперь давайте настроим переменные, которые будем использовать для представления серверов:

```powershell
# Set up variables for reuse            
$ServerA = $env:COMPUTERNAME            
$ServerB = Get-ADComputer -Identity ServerB            
$ServerC = Get-ADComputer -Identity ServerC            
```

WinRM (и поэтому удаленное взаимодействие PowerShell) по умолчанию выполняется как учетная запись компьютера. Это можно проверить, просмотрев свойство **StartName** службы `winrm`:

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

Чтобы сервер _ServerC_ разрешал делегирование из сеанса удаленного взаимодействия PowerShell на сервер _ServerB_, мы предоставим доступ, задав для параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ значение в виде объекта-компьютера сервера _ServerB_:

```powershell
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB            
            
# Check the value of the attribute directly            
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity            
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access            
            
# Check the value of the attribute indirectly            
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

[Центр распространения ключей (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) Kerberos кэширует отклоненные попытки доступа (негативный кэш) в течение 15 минут. Если сервер _ServerB_ ранее пытался получить доступ к серверу _ServerC_, потребуется очистить кэш на сервере _ServerB_, вызвав следующую команду:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    klist purge -li 0x3e7            
}
```

Можно также перезагрузить компьютер или подождать не менее 15 минут для очистки кэша.

После очистки кэша можно запустить код с _ServerA_ через _ServerB_ и до _ServerC_:

```powershell
# Capture a credential            
$cred = Get-Credential Contoso\Alice            
            
# Test kerberos double hop            
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    Test-Path \\$($using:ServerC.Name)\C$            
    Get-Process lsass -ComputerName $($using:ServerC.Name)            
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)            
}
```

В этом примере переменная `$using` используется, чтобы сделать переменную `$ServerC` видимой для сервера _ServerB_. Дополнительные сведения о переменной `$using` см. в разделе [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).

Чтобы разрешить нескольким серверам делегировать учетные данные серверу _ServerC_, задайте в качестве значения параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ в массив:

```powershell
# Set up variables for each server            
$ServerB1 = Get-ADComputer -Identity ServerB1            
$ServerB2 = Get-ADComputer -Identity ServerB2            
$ServerB3 = Get-ADComputer -Identity ServerB3            
$ServerC  = Get-ADComputer -Identity ServerC            
            
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

Если вы хотите сделать второй прыжок между доменами, добавьте полное доменное имя (FQDN) контроллера домена для того домена, к которому принадлежит _ServerB_:

```powershell
# For ServerC in Contoso domain and ServerB in other domain            
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com            
$ServerC = Get-ADComputer -Identity ServerC            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

Чтобы запретить нескольким серверам делегировать учетные данные серверу ServerC, задайте для параметра **PrincipalsAllowedToDelegateToAccount** на сервере _ServerC_ значение `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Информация об ограниченном делегировании Kerberos на основе ресурсов

- [Новые возможности проверки подлинности Kerberos](https://technet.microsoft.com/library/hh831747.aspx)
- [Как Windows Server 2012 упрощает работу с ограниченным делегированием Kerberos, часть 1](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [Как Windows Server 2012 упрощает работу с ограниченным делегированием Kerberos, часть 2](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [Основные сведения об ограниченном делегировании Kerberos для развертывания прокси приложения Azure Active Directory со встроенной проверкой подлинности Windows](http://aka.ms/kcdpaper)
- [[MS-ADA2]. Атрибуты M2.210 схемы Active Directory msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)
- [[MS-SFU]. Расширения протокола Kerberos: S4U и протокола ограниченного делегирования 1.3.2 S4U2proxy](https://msdn.microsoft.com/en-us/library/cc246079.aspx)
- [Ограниченное делегирование Kerberos на основе ресурсов](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [Удаленное администрирование без ограниченного делегирования с помощью PrincipalsAllowedToDelegateToAccount](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration с использованием RunAs

Можно создать конфигурацию сеанса на сервере _ServerB_ и задать ее параметр **RunAsCredential**.

Сведения об использовании PSSessionConfiguration и RunAs для решения проблемы второго прыжка см. в разделе [Другое решение для удаленного взаимодействия PowerShell с несколькими прыжками](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).

### <a name="pros"></a>Плюсы

- Работает для любого сервера с WMF 3.0 или более поздней версии.

### <a name="cons"></a>Минусы

- Требует настройки **PSSessionConfiguration** и **RunAs** на каждом промежуточном сервере (_ServerB_).
- Требуется обслуживание паролей при использовании учетной записи **запуска от имени** домена.

## <a name="just-enough-administration-jea"></a>Just Enough Administration (JEA)

JEA позволяет ограничить команды, доступные администратору во время сеанса PowerShell. Это позволяет решить проблему второго прыжка.

Сведения о JEA см. в разделе [Just Enough Administration](https://msdn.microsoft.com/powershell/jea/readme).

### <a name="pros"></a>Плюсы

- При использовании виртуальной учетной записи обслуживание паролей не требуется.

### <a name="cons"></a>Минусы

- Требуется WMF 5.0 или более поздней версии.
- Требует настройки на каждом промежуточном сервере (_ServerB_).

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Передача учетных данных внутри блока сценария Invoke-Command

Можно передать учетные данные внутри параметра **ScriptBlock** вызова командлета [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command).

### <a name="pros"></a>Плюсы

- Не требуется специальной настройки серверов.
- Работает на любом сервере с WMF 2.0 или более поздней версии.

## <a name="cons"></a>Минусы

- Требует внимательного составления кода.
- При использовании WMF 2.0 требуется использовать иной синтаксис для передачи аргументов в удаленный сеанс.

## <a name="example"></a>Пример

Следующий пример показывает, как передать учетные данные внутри блока сценария **Invoke-Command**:

```powershell
# This works without delegation, passing fresh creds            
# Note $Using:Cred in nested request            
$cred = Get-Credential Contoso\Administrator            
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {            
    hostname            
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}            
}
```

## <a name="see-also"></a>См. также:

[Вопросы обеспечения безопасности для удаленного взаимодействия PowerShell](WinRMSecurity.md)








 
