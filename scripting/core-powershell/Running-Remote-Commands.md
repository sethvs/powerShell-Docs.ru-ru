---
title: "Выполнение удаленных команд"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
translationtype: Human Translation
ms.sourcegitcommit: 0f77e2d13a26c58d2a4813e57a76ba54dbcaac46
ms.openlocfilehash: 48385de53964217b2f7d263d85bfb99b1dbf6507

---

# Выполнение удаленных команд
Вы можете запускать команды на одном или сотнях компьютеров одной командой Windows PowerShell. Windows PowerShell поддерживает удаленное вычисление с помощью разных технологий, включая WMI, RPC и WS \- Management.

## Удаленное взаимодействие без настройки
Многие командлеты Windows PowerShell имеют параметр ComputerName, который позволяет собирать данные и изменять параметры одного или нескольких удаленных компьютеров. Они используют различные способы связи, многие из которых работают во всех операционных системах Windows, которые Windows PowerShell поддерживает без необходимости какой-либо настройки.

В эти командлеты входят следующие:

-   [Restart-Computer](https://technet.microsoft.com/en-us/library/dd315301.aspx)

-   [Test-Connection](https://technet.microsoft.com/en-us/library/dd315259.aspx)

-   [Clear-EventLog](https://technet.microsoft.com/en-us/library/dd347552.aspx)

-   [Get-EventLog](https://technet.microsoft.com/en-us/library/dd315250.aspx)

-   [Get-HotFix](https://technet.microsoft.com/en-us/library/e1ef636f-5170-4675-b564-199d9ef6f101)

-   [Get-Process](https://technet.microsoft.com/en-us/library/dd347630.aspx)

-   [Get-Service](https://technet.microsoft.com/en-us/library/dd347591.aspx)

-   [Set-Service](https://technet.microsoft.com/en-us/library/dd315324.aspx)

-   [Get-WinEvent](https://technet.microsoft.com/en-us/library/dd315358.aspx)

-   [Get-WmiObject](https://technet.microsoft.com/en-us/library/dd315295.aspx)

Обычно командлеты, которые поддерживают удаленное взаимодействие без специальной настройки, имеют параметр ComputerName, но не имеют параметра Session. Чтобы найти эти командлеты в сеансе, введите:

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## Служба удаленного взаимодействия Windows PowerShell
Служба удаленного взаимодействия Windows PowerShell, использующая протокол WS \- Management, позволяет запустить любую команду Windows PowerShell на одном или нескольких удаленных компьютерах. С ее помощью можно устанавливать постоянные подключения, запускать интерактивные сеансы 1:1 и сценарии на нескольких компьютерах.

Чтобы использовать службу удаленного взаимодействия Windows PowerShell, удаленный компьютер должен быть настроен для удаленного управления. Дополнительные сведения, в том числе инструкции, см. в разделе [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/dd315349.aspx).

После настройки службы удаленного взаимодействия Windows PowerShell вам станут доступны многие стратегии удаленного взаимодействия. В остальной части этого документа перечислены только некоторые из них. Дополнительные сведения см. в разделах [about_Remote](https://technet.microsoft.com/en-us/library/dd347744.aspx) и [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/dd347744.aspx).

### Запуск интерактивного сеанса
Чтобы запустить интерактивный сеанс с одним удаленным компьютером, используйте командлет [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx). Например, чтобы запустить интерактивный сеанс с удаленным компьютером Server01, введите:

```
Enter-PSSession Server01
```

В командной строке отобразится имя компьютера, к которому вы подключены. В дальнейшем все команды, введенные в командной строке, будут запускаться на удаленном компьютере, а результаты отобразятся на локальном компьютере.

Чтобы завершить интерактивный сеанс, введите:

```
Exit-PSSession
```

Дополнительные сведения о командлетах Enter \-PSSession и Exit\- PSSession см. в статьях [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx) и [Exit-PSSession](https://technet.microsoft.com/en-us/library/dd315322.aspx).

### Выполнение удаленной команды
Чтобы выполнить любую команду на одном или нескольких удаленных компьютеров, используйте командлет [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx).
Например, чтобы выполнить команду [Get-UICulture](https://technet.microsoft.com/en-us/library/dd347742.aspx) на удаленных компьютерах Server01 и Server02, введите:

```
Invoke-Command -ComputerName Server01, Server02 {Get-UICulture}
```

Выходные данные будут возвращены на ваш компьютер.

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

Дополнительные сведения о командлете Invoke \- Command см. в статье [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462).

### Запуск сценария
Чтобы запустить сценарий на одном или нескольких удаленных компьютерах, используйте параметр FilePath командлета Invoke \- Command. Сценарий должен быть включен или доступен для локального компьютера. Результаты будут возвращены на локальный компьютер.

Например, следующая команда выполняет сценарий DiskCollect.ps1 на удаленных компьютерах Server01 и Server02.

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

Дополнительные сведения о командлете Invoke \- Command см. в статье [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx).

### Установка постоянного подключения
Чтобы выполнить ряд связанных команд с общими данными, создайте сеанс на удаленном компьютере, а затем используйте командлет Invoke \- Command для выполнения команд в созданном сеансе. Чтобы создать удаленный сеанс, используйте командлет New \- PSSession.

Например, следующая команда создает удаленный сеанс на компьютере Server01 и другой удаленный сеанс на компьютере Server02. Она сохраняет объекты сеанса в переменной $s.

```
$s = New-PSSession -ComputerName Server01, Server02
```

После установки сеансов в них можно выполнить любую команду. Так как сеансы являются постоянными, вы можете собирать данные в одной команде и использовать их в последующей.

Например, следующая команда выполняет команду Get\-HotFix в сеансах в переменной $s и сохраняет результаты в переменной $h. Переменная $h создается в каждом сеансе в $s, но она не существует в локальном сеансе.

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

Теперь данные в переменной $h можно использовать в последующих командах, таких как следующая. Результаты отобразятся на локальном компьютере.

```
Invoke-Command -Session $s {$h | where {$_.installedby -ne "NTAUTHORITY\SYSTEM"}}
```

### Расширенная служба удаленного взаимодействия
Это и есть служба удаленного взаимодействия Windows PowerShell. Используя командлеты, установленные с Windows PowerShell, можно установить и настроить удаленные сеансы с локальных и удаленных компьютеров, создать настраиваемые и ограниченные сеансы, разрешить пользователям импортировать команды из удаленного сеанса, которые могут неявно выполняться в удаленном сеансе, настроить безопасность удаленного сеанса и многое другое.

Для упрощения настройки в PowerShell включен поставщик WSMan. Диск WSMAN:, созданный поставщиком, позволяет перемещаться по иерархии параметров конфигурации на локальном и удаленном компьютерах.
Дополнительные сведения о поставщике WSMan см. в разделах [Поставщик WSMan](https://technet.microsoft.com/en-us/library/dd819476.aspx) и   [Сведения о командлетах WS-Management](https://technet.microsoft.com/en-us/library/dd819481.aspx) или введите команду "Get\-Help wsman" в консоли Windows PowerShell.

Дополнительная информация:
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/dd819496.aspx)
- [Import-PSSession](https://technet.microsoft.com/en-us/library/dd347575.aspx) 

Справку по ошибкам службы удаленного взаимодействия см. в статье [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).

## См. также
- [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [Сведения об удаленной диагностике](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
- [Import-PSSession](https://technet.microsoft.com/en-us/library/048c115e-a6fb-4e0d-8cea-c5ca24630c9d)
- [New-PSSession](https://technet.microsoft.com/en-us/library/59452f12-a11d-4558-99ea-e6ca6ad5ffd3)
- [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/af68867a-d201-4b19-a1de-594015ed8a25)
- [WSMan Provider](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)




<!--HONumber=Jul16_HO1-->


