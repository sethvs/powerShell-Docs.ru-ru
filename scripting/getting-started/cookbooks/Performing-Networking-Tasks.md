---
title: "Выполнение задач по работе с сетями"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: 6d878b89a4cd49948cb465525e74e92db819c192

---

# Выполнение задач по работе с сетями
Большая часть задач администрирования низкоуровневых сетевых протоколов связана с протоколом TCP\/IP, поскольку это наиболее распространенный сетевой протокол. В этом разделе описано использование Windows PowerShell и WMI для выполнения этих задач.

### Получение списка IP-адресов компьютера
Список всех IP-адресов, используемых локальным компьютером, возвращает следующая команда:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Format-Table -Property IPAddress
```

Выходные данные этой команды отличаются от большинства списков свойств заключением значений в фигурные скобки:

<pre>IPAddress
---------
{192.168.1.80} {192.168.148.1} {192.168.171.1} {0.0.0.0}</pre>

Чтобы понять причину появления скобок, используйте командлет Get\-Member для изучения свойства **IPAddress**:

<pre>PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Get-Member -Name IPAddress TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapter Configuration Name      MemberType Definition ----      ---------- ---------- IPAddress Property   System.String[] IPAddress {get;}</pre>

Свойство IPAddress каждого сетевого адаптера в действительности представляет собой массив. Фигурные скобки в определении указывают на то, что свойство **IPAddress** содержит не значение типа **System.String**, а массив значений типа **System.String**.

### Вывод данных IP-конфигурации
Для отображения подробных данных IP-конфигурации каждого сетевого адаптера воспользуйтесь следующей командой:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName .
```

По умолчанию отображается очень небольшая часть доступных сведений об объекте конфигурации сетевого адаптера. Для более глубокого изучения и устранения неполадок воспользуйтесь командлетом Select\-Object или командлетом форматирования, например Format\-List, чтобы задать отображаемые свойства.

Если свойства IPX или WINS не представляют интереса (что характерно для современной сети TCP\/IP), можно использовать параметр ExcludeProperty командлета Select\-Object, чтобы скрыть свойства с именами, начинающимися на "WINS" или "IPX":

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

Эта команда выводит подробные сведения о DHCP, DNS, маршрутизации и других менее значительных свойствах IP-конфигурации.

### Проверка связи с компьютерами
Простую проверку связи с компьютером можно выполнить с помощью **Win32\_PingStatus**. Следующая команда производит проверку связи, но при этом выводит большой объем сведений:

```
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

Удобнее отображать сводные данные, содержащие свойства Address, ResponseTime и StatusCode, как это делает приведенная ниже команда. Параметр Autosize командлета Format\-Table изменяет размер столбцов таблицы для их правильного отображения в Windows PowerShell.

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
A status code of 0 indicates a successful ping.
```

Для проверки связи с несколькими компьютерами с помощью одной команды можно использовать массив. Поскольку адресов несколько, для проверки связи с каждым адресом по отдельности можно использовать **ForEach\-Object**:

```
"127.0.0.1","localhost","research.microsoft.com" | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Один и тот же формат команды можно использовать для проверки связи со всеми компьютерами подсети. Например, при проверке частной сети, использующей номер сети 192.168.1.0 и стандартную маску подсети класса C (255.255.255.0), допустимы только локальные адреса в диапазоне от 192.168.1.1 до 192.168.1.254 (0 всегда зарезервирован в качестве номера сети, а 255 используется в качестве широковещательного адреса подсети).

Чтобы представить массив чисел от 1 до 254 в Windows PowerShell, используйте оператор **1..254**. Таким образом, полную проверку связи с подсетью можно осуществить, сформировав этот массив и добавляя его элементы к частичному адресу в операторе проверки связи:

```
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

Такой метод формирования диапазона адресов может быть использован в любых подобных случаях. Полный набор адресов можно сформировать следующим образом:

`$ips = 1..254 | ForEach-Object -Process {"192.168.1." + $_}`

### Извлечение свойств сетевого адаптера
Ранее в данном руководстве пользователя упоминалось о возможности извлечения общих свойств конфигурации с помощью **Win32\_NetworkAdapterConfiguration**. Такие сведения о сетевом адаптере, как MAC-адреса и типы адаптеров, не относятся, строго говоря, к протоколу TCP\/IP, но могут оказаться полезными для понимания того, что происходит в компьютере. Сводные данные можно получить с помощью следующей команды:

```
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### Назначение домена DNS сетевому адаптеру
Чтобы назначить домен DNS для автоматического разрешения имен, нужно использовать метод **Win32\_NetworkAdapterConfiguration SetDNSDomain**. Поскольку назначение домена DNS для каждого сетевого адаптера производится независимо, необходимо воспользоваться оператором **ForEach\-Object**, чтобы назначить домен для каждого адаптера:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain("fabrikam.com") }
```

Здесь нужно использовать оператор фильтрации "IPEnabled\=true", поскольку даже в сети, использующей лишь протокол TCP\/IP, некоторые сетевые адаптеры компьютера не являются настоящими адаптерами TCP\/IP. Они представляют собой общие программные элементы, поддерживающие службы RAS, PPTP, QoS и т. п. для всех адаптеров, и не имеют собственного адреса.

Фильтрацию в команде можно осуществить с помощью командлета **Where\-Object** вместо фильтра **Get\-WmiObject**.

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain("fabrikam.com")}
```

### Выполнение задач настройки DHCP
Изменение сведений DHCP, так же как и настройка DNS, включает работу с набором сетевых адаптеров. Существует несколько отдельных действий, выполняемых с помощью инструментария WMI. Мы рассмотрим несколько наиболее типичных.

#### Определение адаптеров, поддерживающих DHCP
Найти на компьютере адаптеры, поддерживающие DHCP, можно с помощью следующей команды:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName .
```

Чтобы исключить из поиска адаптеры, имеющие проблемы в IP-конфигурации, можно добавить требование поддержки протокола IP:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName .
```

#### Извлечение свойств DHCP
Свойства адаптера, относящиеся к протоколу DHCP, обычно начинаются с "DHCP", поэтому для отображения только этих свойств можно использовать параметр Property командлета Format\-Table:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName . | Format-Table -Property DHCP*
```

#### Включение поддержки DHCP на каждом адаптере
Чтобы включить поддержку DHCP на всех адаптерах, используйте команду:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

Можно воспользоваться оператором **Filter** "IPEnabled\=true and DHCPEnabled\=false" во избежание включения поддержки DHCP для адаптеров, у которых она уже включена, но пропуск этого шага не приведет к появлению ошибок.

#### Отмена и обновление аренды адреса DHCP для отдельных адаптеров
Класс **Win32\_NetworkAdapterConfiguration** использует методы **ReleaseDHCPLease** и **RenewDHCPLease**. Оба метода используются одинаково. Обычно их применяют лишь при необходимости отмены или обновления аренды адресов для адаптера в отдельной подсети. Простейшим способом фильтрации адаптеров в подсети является выбор лишь тех адаптеров, которые используют шлюз для этой подсети. Например, следующая команда отменяет все аренды адресов DHCP для адаптеров на локальном компьютере, которые арендуют адреса DHCP с 192.168.1.254:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

Единственное отличие при обновлении аренды адреса DHCP состоит в вызове метода **RenewDHCPLease** вместо метода **ReleaseDHCPLease**:

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> Если эти методы применяются на удаленном компьютере, возможна потеря доступа к удаленной системе, которая подключена через адаптер с отмененной или обновленной арендой.

#### Отмена и обновление аренды адресов DHCP для всех адаптеров
Отменить или обновить аренду адресов DHCP сразу для всех адаптеров можно с помощью методов **Win32\_NetworkAdapterConfiguration** — **ReleaseDHCPLeaseAll** и **RenewDHCPLeaseAll**. Однако эту команду следует применять к классу WMI, а не к отдельному адаптеру, поскольку глобальная отмена и обновление аренды осуществляется на уровне класса, а не отдельного адаптера.

Ссылку на класс WMI вместо ссылки на экземпляры класса можно получить путем перечисления всех классов WMI и выбора нужного класса по имени. Например, следующая команда возвращает класс Win32\_NetworkAdapterConfiguration:

```
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"}
```

Эту команду можно рассматривать как класс и использовать ее при вызове метода **ReleaseDHCPAdapterLease**. В следующей команде элементы конвейера **Get\-WmiObject** и **Where\-Object** ограничены круглыми скобками, в результате чего Windows PowerShell обрабатывает их первыми:

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).ReleaseDHCPLeaseAll()
```

Такой же формат команды используется при вызове метода **RenewDHCPLeaseAll**:

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).RenewDHCPLeaseAll()
```

### Создание сетевой папки
Создать сетевую папку можно с помощью метода **Win32\_Share Create**:

```
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Win32_Share"}).Create("C:\temp","TempShare",0,25,"test share of the temp folder")
```

Для этой же цели в Windows PowerShell можно использовать команду **net share**:

```
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### Удаление сетевой папки
Сетевую папку можно удалить с помощью **Win32\_Share**, но этот процесс немного отличается от создания, поскольку требует получения именно удаляемой сетевой папки, а не класса **Win32\_Share**. Следующий оператор удаляет сетевую папку TempShare:

```
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

В этом случае подойдет и **Net share**:

```
PS> net share tempshare /delete
tempshare was deleted successfully.
```

### Подключение сетевого диска, доступного в Windows
Командлет **New\-PSDrive** позволяет создавать диски Windows PowerShell, но они доступны только в Windows PowerShell. Для создания сетевого диска можно воспользоваться COM-объектом **WScript.Network**. Следующая команда сопоставляет сетевую папку \\\\FPS01\\users с локальным диском B:

```
(New-Object -ComObject WScript.Network).MapNetworkDrive("B:", "\\FPS01\users")
```

Так же работает и команда **net use**:

```
net use B: \\FPS01\users
```

Диски, сопоставленные с помощью **WScript.Network** или команды net use, мгновенно становятся доступными в Windows PowerShell.




<!--HONumber=Jun16_HO4-->


