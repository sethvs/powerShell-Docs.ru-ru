---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Выполнение задач по работе с сетями"
ms.assetid: a43cc55f-70c1-45c8-9467-eaad0d57e3b5
ms.openlocfilehash: 4d7a91595b9d9d637ce915be2c2be9c20879dd8b
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="performing-networking-tasks"></a><span data-ttu-id="5963f-103">Выполнение задач по работе с сетями</span><span class="sxs-lookup"><span data-stu-id="5963f-103">Performing Networking Tasks</span></span>
<span data-ttu-id="5963f-104">Большая часть задач администрирования низкоуровневых сетевых протоколов связана с протоколом TCP/IP, так как это наиболее распространенный сетевой протокол.</span><span class="sxs-lookup"><span data-stu-id="5963f-104">Because TCP/IP is the most commonly used network protocol, most low-level network protocol administration tasks involve TCP/IP.</span></span> <span data-ttu-id="5963f-105">В этом разделе описано использование Windows PowerShell и WMI для выполнения этих задач.</span><span class="sxs-lookup"><span data-stu-id="5963f-105">In this section, we use Windows PowerShell and WMI to do these tasks.</span></span>

### <a name="listing-ip-addresses-for-a-computer"></a><span data-ttu-id="5963f-106">Получение списка IP-адресов компьютера</span><span class="sxs-lookup"><span data-stu-id="5963f-106">Listing IP Addresses for a Computer</span></span>
<span data-ttu-id="5963f-107">Список всех IP-адресов, используемых локальным компьютером, возвращает следующая команда:</span><span class="sxs-lookup"><span data-stu-id="5963f-107">To get all IP addresses in use on the local computer, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Format-Table -Property IPAddress
```

<span data-ttu-id="5963f-108">Выходные данные этой команды отличаются от большинства списков свойств заключением значений в фигурные скобки:</span><span class="sxs-lookup"><span data-stu-id="5963f-108">The output of this command differs from most property lists, because values are enclosed in braces:</span></span>

<a name="preipaddress"></a><pre>IPAddress
---------
<span data-ttu-id="5963f-109">{192.168.1.80} {192.168.148.1} {192.168.171.1} {0.0.0.0}</span><span class="sxs-lookup"><span data-stu-id="5963f-109">{192.168.1.80} {192.168.148.1} {192.168.171.1} {0.0.0.0}</span></span></pre>

<span data-ttu-id="5963f-110">Чтобы понять причину появления скобок, используйте командлет Get-Member для изучения свойства **IPAddress**.</span><span class="sxs-lookup"><span data-stu-id="5963f-110">To understand why the braces appear, use the Get-Member cmdlet to examine the **IPAddress** property:</span></span>

<pre>PS> Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Get-Member -Name IPAddress
TypeName: System.Management.ManagementObject#root\cimv2\Win32_NetworkAdapter
Configuration
Name      MemberType Definition
----      ---------- ----------
IPAddress Property   System.String[] IPAddress {get;}</pre>

<span data-ttu-id="5963f-111">Свойство IPAddress каждого сетевого адаптера в действительности представляет собой массив.</span><span class="sxs-lookup"><span data-stu-id="5963f-111">The IPAddress property for each network adapter is actually an array.</span></span> <span data-ttu-id="5963f-112">Фигурные скобки в определении указывают на то, что свойство **IPAddress** содержит не значение типа **System.String**, а массив значений типа **System.String**.</span><span class="sxs-lookup"><span data-stu-id="5963f-112">The braces in the definition indicate that **IPAddress** is not a **System.String** value, but an array of **System.String** values.</span></span>

### <a name="listing-ip-configuration-data"></a><span data-ttu-id="5963f-113">Вывод данных IP-конфигурации</span><span class="sxs-lookup"><span data-stu-id="5963f-113">Listing IP Configuration Data</span></span>
<span data-ttu-id="5963f-114">Для отображения подробных данных IP-конфигурации каждого сетевого адаптера воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="5963f-114">To display detailed IP configuration data for each network adapter, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName .
```

<span data-ttu-id="5963f-115">По умолчанию отображается очень небольшая часть доступных сведений об объекте конфигурации сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="5963f-115">The default display for the network adapter configuration object is a very reduced set of the available information.</span></span> <span data-ttu-id="5963f-116">Для более глубокого изучения и устранения неполадок воспользуйтесь командлетом Select-Object или командлетом форматирования, например Format-List, чтобы задать отображаемые свойства.</span><span class="sxs-lookup"><span data-stu-id="5963f-116">For in-depth inspection and troubleshooting, use Select-Object or a formatting cmdlet, such as Format-List, to specify the properties to be displayed.</span></span>

<span data-ttu-id="5963f-117">Если свойства IPX или WINS не представляют интереса (что характерно для современной сети TCP/IP), можно использовать параметр ExcludeProperty командлета Select-Object, чтобы скрыть свойства с именами, начинающимися на WINS или IPX.</span><span class="sxs-lookup"><span data-stu-id="5963f-117">If you are not interested in IPX or WINS properties—probably the case in a modern TCP/IP network—you can use the ExcludeProperty parameter of Select-Object to hide properties with names that begin with "WINS" or "IPX:"</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=TRUE -ComputerName . | Select-Object -Property [a-z]* -ExcludeProperty IPX*,WINS*
```

<span data-ttu-id="5963f-118">Эта команда выводит подробные сведения о DHCP, DNS, маршрутизации и других менее значительных свойствах IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5963f-118">This command returns detailed information about DHCP, DNS, routing, and other minor IP configuration properties.</span></span>

### <a name="pinging-computers"></a><span data-ttu-id="5963f-119">Проверка связи с компьютерами</span><span class="sxs-lookup"><span data-stu-id="5963f-119">Pinging Computers</span></span>
<span data-ttu-id="5963f-120">Простую проверку связи с компьютером можно выполнить с помощью **Win32_PingStatus**.</span><span class="sxs-lookup"><span data-stu-id="5963f-120">You can perform a simple ping against a computer using by **Win32_PingStatus**.</span></span> <span data-ttu-id="5963f-121">Следующая команда производит проверку связи, но при этом выводит большой объем сведений:</span><span class="sxs-lookup"><span data-stu-id="5963f-121">The following command performs the ping, but returns lengthy output:</span></span>

```
Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName .
```

<span data-ttu-id="5963f-122">Удобнее отображать сводные данные, содержащие свойства Address, ResponseTime и StatusCode, как это делает приведенная ниже команда.</span><span class="sxs-lookup"><span data-stu-id="5963f-122">A more useful form for summary information a display of the Address, ResponseTime, and StatusCode properties, as generated by the following command.</span></span> <span data-ttu-id="5963f-123">Параметр Autosize командлета Format-Table изменяет размер столбцов таблицы для их правильного отображения в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5963f-123">The Autosize parameter of Format-Table resizes the table columns so that they display properly in Windows PowerShell.</span></span>

```
PS> Get-WmiObject -Class Win32_PingStatus -Filter "Address='127.0.0.1'" -ComputerName . | Format-Table -Property Address,ResponseTime,StatusCode -Autosize

Address   ResponseTime StatusCode
-------   ------------ ----------
127.0.0.1            0          0
A status code of 0 indicates a successful ping.
```

<span data-ttu-id="5963f-124">Для проверки связи с несколькими компьютерами с помощью одной команды можно использовать массив.</span><span class="sxs-lookup"><span data-stu-id="5963f-124">You can use an array to ping multiple computers with a single command.</span></span> <span data-ttu-id="5963f-125">Так как адресов несколько, для проверки связи с каждым адресом по отдельности можно использовать **ForEach-Object**.</span><span class="sxs-lookup"><span data-stu-id="5963f-125">Because there is more than one address, use the **ForEach-Object** to ping each address separately:</span></span>

```
"127.0.0.1","localhost","research.microsoft.com" | ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='" + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="5963f-126">Один и тот же формат команды можно использовать для проверки связи со всеми компьютерами подсети. Например, при проверке частной сети, использующей номер сети 192.168.1.0 и стандартную маску подсети класса C (255.255.255.0), допустимы только локальные адреса в диапазоне от 192.168.1.1 до 192.168.1.254 (0 всегда зарезервирован в качестве номера сети, а 255 используется в качестве широковещательного адреса подсети).</span><span class="sxs-lookup"><span data-stu-id="5963f-126">You can use the same command format to ping all of the computers on a subnet, such as a private network that uses network number 192.168.1.0 and a standard Class C subnet mask (255.255.255.0)., Only addresses in the range of 192.168.1.1 through 192.168.1.254 are legitimate local addresses (0 is always reserved for the network number and 255 is a subnet broadcast address).</span></span>

<span data-ttu-id="5963f-127">Чтобы представить массив чисел от 1 до 254 в Windows PowerShell, используйте оператор **1..254**.</span><span class="sxs-lookup"><span data-stu-id="5963f-127">To represent an array of the numbers from 1 through 254 in Windows PowerShell, use the statement **1..254.**</span></span> <span data-ttu-id="5963f-128">Таким образом, полную проверку связи с подсетью можно осуществить, сформировав этот массив и добавляя его элементы к частичному адресу в операторе проверки связи:</span><span class="sxs-lookup"><span data-stu-id="5963f-128">A complete subnet ping can be performed by generating the array and then adding the values onto a partial address in the ping statement:</span></span>

```
1..254| ForEach-Object -Process {Get-WmiObject -Class Win32_PingStatus -Filter ("Address='192.168.1." + $_ + "'") -ComputerName .} | Select-Object -Property Address,ResponseTime,StatusCode
```

<span data-ttu-id="5963f-129">Такой метод формирования диапазона адресов может быть использован в любых подобных случаях.</span><span class="sxs-lookup"><span data-stu-id="5963f-129">Note that this technique for generating a range of addresses can be used elsewhere as well.</span></span> <span data-ttu-id="5963f-130">Полный набор адресов можно сформировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5963f-130">You can generate a complete set of addresses in this way:</span></span>

`$ips = 1..254 | ForEach-Object -Process {"192.168.1." + $_}`

### <a name="retrieving-network-adapter-properties"></a><span data-ttu-id="5963f-131">Извлечение свойств сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="5963f-131">Retrieving Network Adapter Properties</span></span>
<span data-ttu-id="5963f-132">Ранее в данном руководстве пользователя упоминалось о возможности извлечения общих свойств конфигурации с помощью **Win32_NetworkAdapterConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="5963f-132">Earlier in this user's guide, we mentioned that you could retrieve general configuration properties by using **Win32_NetworkAdapterConfiguration**.</span></span> <span data-ttu-id="5963f-133">Такие сведения о сетевом адаптере, как MAC-адреса и типы адаптеров, не относятся, строго говоря, к протоколу TCP/IP, но могут оказаться полезными для понимания того, что происходит в компьютере.</span><span class="sxs-lookup"><span data-stu-id="5963f-133">Although not strictly TCP/IP information, network adapter information such as MAC addresses and adapter types can be useful for understanding what is going on with a computer.</span></span> <span data-ttu-id="5963f-134">Сводные данные можно получить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5963f-134">To get a summary of this information, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapter -ComputerName .
```

### <a name="assigning-the-dns-domain-for-a-network-adapter"></a><span data-ttu-id="5963f-135">Назначение домена DNS сетевому адаптеру</span><span class="sxs-lookup"><span data-stu-id="5963f-135">Assigning the DNS Domain for a Network Adapter</span></span>
<span data-ttu-id="5963f-136">Чтобы назначить домен DNS для автоматического разрешения имен, нужно использовать метод **Win32_NetworkAdapterConfiguration SetDNSDomain**.</span><span class="sxs-lookup"><span data-stu-id="5963f-136">To assign the DNS domain for automatic name resolution, use the **Win32_NetworkAdapterConfiguration SetDNSDomain** method.</span></span> <span data-ttu-id="5963f-137">Так как назначение домена DNS для каждого сетевого адаптера производится независимо, чтобы назначить домен для каждого адаптера, необходимо воспользоваться оператором **ForEach-Object**.</span><span class="sxs-lookup"><span data-stu-id="5963f-137">Because you assign the DNS domain for each network adapter configuration independently, you need to use a **ForEach-Object** statement to assign the domain to each adapter:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process { $_. SetDNSDomain("fabrikam.com") }
```

<span data-ttu-id="5963f-138">Здесь нужно использовать оператор фильтрации IPEnabled=true, так как даже в сети, использующей лишь протокол TCP/IP, некоторые сетевые адаптеры компьютера не являются настоящими адаптерами TCP/IP. Они представляют собой общие программные элементы, поддерживающие службы RAS, PPTP, QoS и т. п. для всех адаптеров, и не имеют собственного адреса.</span><span class="sxs-lookup"><span data-stu-id="5963f-138">The filtering statement "IPEnabled=true" is necessary, because even on a network that uses only TCP/IP, several of the network adapter configurations on a computer are not true TCP/IP adapters; they are general software elements supporting RAS, PPTP, QoS, and other services for all adapters and thus do not have an address of their own.</span></span>

<span data-ttu-id="5963f-139">Фильтрацию в команде можно осуществить с помощью командлета **Where-Object** вместо фильтра **Get-WmiObject**.</span><span class="sxs-lookup"><span data-stu-id="5963f-139">You can filter the command by using the **Where-Object** cmdlet, instead of using the **Get-WmiObject** filter.</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -ComputerName . | Where-Object -FilterScript {$_.IPEnabled} | ForEach-Object -Process {$_.SetDNSDomain("fabrikam.com")}
```

### <a name="performing-dhcp-configuration-tasks"></a><span data-ttu-id="5963f-140">Выполнение задач настройки DHCP</span><span class="sxs-lookup"><span data-stu-id="5963f-140">Performing DHCP Configuration Tasks</span></span>
<span data-ttu-id="5963f-141">Изменение сведений DHCP, так же как и настройка DNS, включает работу с набором сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="5963f-141">Modifying DHCP details involves working with a set of network adapters, just as the DNS configuration does.</span></span> <span data-ttu-id="5963f-142">Существует несколько отдельных действий, выполняемых с помощью инструментария WMI. Мы рассмотрим несколько наиболее типичных.</span><span class="sxs-lookup"><span data-stu-id="5963f-142">There are several distinct actions you can perform by using WMI, and we will step through a few of the common ones.</span></span>

#### <a name="determining-dhcp-enabled-adapters"></a><span data-ttu-id="5963f-143">Определение адаптеров, поддерживающих DHCP</span><span class="sxs-lookup"><span data-stu-id="5963f-143">Determining DHCP-Enabled Adapters</span></span>
<span data-ttu-id="5963f-144">Найти на компьютере адаптеры, поддерживающие DHCP, можно с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5963f-144">To find the DHCP-enabled adapters on a computer, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName .
```

<span data-ttu-id="5963f-145">Чтобы исключить из поиска адаптеры, имеющие проблемы в IP-конфигурации, можно добавить требование поддержки протокола IP:</span><span class="sxs-lookup"><span data-stu-id="5963f-145">To exclude adapters with IP configuration problems, you can retrieve only IP-enabled adapters:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName .
```

#### <a name="retrieving-dhcp-properties"></a><span data-ttu-id="5963f-146">Извлечение свойств DHCP</span><span class="sxs-lookup"><span data-stu-id="5963f-146">Retrieving DHCP Properties</span></span>
<span data-ttu-id="5963f-147">Свойства адаптера, относящиеся к протоколу DHCP, обычно начинаются с DHCP, поэтому для отображения только этих свойств можно использовать параметр Property командлета Format-Table:</span><span class="sxs-lookup"><span data-stu-id="5963f-147">Because DHCP-related properties for an adapter generally begin with "DHCP," you can use the Property parameter of Format-Table to display only those properties:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "DHCPEnabled=true" -ComputerName . | Format-Table -Property DHCP*
```

#### <a name="enabling-dhcp-on-each-adapter"></a><span data-ttu-id="5963f-148">Включение поддержки DHCP на каждом адаптере</span><span class="sxs-lookup"><span data-stu-id="5963f-148">Enabling DHCP on Each Adapter</span></span>
<span data-ttu-id="5963f-149">Чтобы включить поддержку DHCP на всех адаптерах, используйте команду:</span><span class="sxs-lookup"><span data-stu-id="5963f-149">To enable DHCP on all adapters, use the following command:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter IPEnabled=true -ComputerName . | ForEach-Object -Process {$_.EnableDHCP()}
```

<span data-ttu-id="5963f-150">Можно воспользоваться оператором **Filter** "IPEnabled=true and DHCPEnabled=false" во избежание включения поддержки DHCP для адаптеров, у которых она уже включена, но пропуск этого шага не приведет к появлению ошибок.</span><span class="sxs-lookup"><span data-stu-id="5963f-150">You can use the **Filter** statement "IPEnabled=true and DHCPEnabled=false" to avoid enabling DHCP where it is already enabled, but omitting this step will not cause errors.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-specific-adapters"></a><span data-ttu-id="5963f-151">Отмена и обновление аренды адреса DHCP для отдельных адаптеров</span><span class="sxs-lookup"><span data-stu-id="5963f-151">Releasing and Renewing DHCP Leases on Specific Adapters</span></span>
<span data-ttu-id="5963f-152">Класс **Win32_NetworkAdapterConfiguration** использует методы **ReleaseDHCPLease** и **RenewDHCPLease**.</span><span class="sxs-lookup"><span data-stu-id="5963f-152">The **Win32_NetworkAdapterConfiguration** class has **ReleaseDHCPLease** and **RenewDHCPLease** methods.</span></span> <span data-ttu-id="5963f-153">Оба метода используются одинаково.</span><span class="sxs-lookup"><span data-stu-id="5963f-153">Both are used in the same way.</span></span> <span data-ttu-id="5963f-154">Обычно их применяют лишь при необходимости отмены или обновления аренды адресов для адаптера в отдельной подсети.</span><span class="sxs-lookup"><span data-stu-id="5963f-154">In general, use these methods if you only need to release or renew addresses for an adapter on a specific subnet.</span></span> <span data-ttu-id="5963f-155">Простейшим способом фильтрации адаптеров в подсети является выбор лишь тех адаптеров, которые используют шлюз для этой подсети.</span><span class="sxs-lookup"><span data-stu-id="5963f-155">The easiest way to filter adapters on a subnet is to choose only the adapter configurations that use the gateway for that subnet.</span></span> <span data-ttu-id="5963f-156">Например, следующая команда отменяет все аренды адресов DHCP для адаптеров на локальном компьютере, которые арендуют адреса DHCP с 192.168.1.254:</span><span class="sxs-lookup"><span data-stu-id="5963f-156">For example, the following command releases all DHCP leases on adapters on the local computer that are obtaining DHCP leases from 192.168.1.254:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

<span data-ttu-id="5963f-157">Единственное отличие при обновлении аренды адреса DHCP состоит в вызове метода **RenewDHCPLease** вместо метода **ReleaseDHCPLease**:</span><span class="sxs-lookup"><span data-stu-id="5963f-157">The only change for renewing a DHCP lease is to use the **RenewDHCPLease** method instead of the **ReleaseDHCPLease** method:</span></span>

```
Get-WmiObject -Class Win32_NetworkAdapterConfiguration -Filter "IPEnabled=true and DHCPEnabled=true" -ComputerName . | Where-Object -FilterScript {$_.DHCPServer -contains "192.168.1.254"} | ForEach-Object -Process {$_.ReleaseDHCPLease()}
```

> [!NOTE]
> <span data-ttu-id="5963f-158">Если эти методы применяются на удаленном компьютере, возможна потеря доступа к удаленной системе, которая подключена через адаптер с отмененной или обновленной арендой.</span><span class="sxs-lookup"><span data-stu-id="5963f-158">When using these methods on a remote computer, be aware that you can lose access to the remote system if you are connected to it through the adapter with the released or renewed lease.</span></span>

#### <a name="releasing-and-renewing-dhcp-leases-on-all-adapters"></a><span data-ttu-id="5963f-159">Отмена и обновление аренды адресов DHCP для всех адаптеров</span><span class="sxs-lookup"><span data-stu-id="5963f-159">Releasing and Renewing DHCP Leases on All Adapters</span></span>
<span data-ttu-id="5963f-160">Отменить или обновить аренду адресов DHCP сразу для всех адаптеров можно с помощью методов **Win32_NetworkAdapterConfiguration** — **ReleaseDHCPLeaseAll** и **RenewDHCPLeaseAll**.</span><span class="sxs-lookup"><span data-stu-id="5963f-160">You can perform global DHCP address releases or renewals on all adapters by using the **Win32_NetworkAdapterConfiguration** methods, **ReleaseDHCPLeaseAll** and **RenewDHCPLeaseAll**.</span></span> <span data-ttu-id="5963f-161">Однако эту команду следует применять к классу WMI, а не к отдельному адаптеру, поскольку глобальная отмена и обновление аренды осуществляется на уровне класса, а не отдельного адаптера.</span><span class="sxs-lookup"><span data-stu-id="5963f-161">However, the command must apply to the WMI class, rather than a particular adapter, because releasing and renewing leases globally is performed on the class, not on a specific adapter.</span></span>

<span data-ttu-id="5963f-162">Ссылку на класс WMI вместо ссылки на экземпляры класса можно получить путем перечисления всех классов WMI и выбора нужного класса по имени.</span><span class="sxs-lookup"><span data-stu-id="5963f-162">You can get a reference to a WMI class, instead of class instances, by listing all WMI classes and then selecting only the desired class by name.</span></span> <span data-ttu-id="5963f-163">Например, следующая команда возвращает класс Win32_NetworkAdapterConfiguration:</span><span class="sxs-lookup"><span data-stu-id="5963f-163">For example, the following command returns the Win32_NetworkAdapterConfiguration class:</span></span>

```
Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"}
```

<span data-ttu-id="5963f-164">Эту команду можно рассматривать как класс и использовать ее при вызове метода **ReleaseDHCPAdapterLease**.</span><span class="sxs-lookup"><span data-stu-id="5963f-164">You can treat the entire command as the class and then invoke the **ReleaseDHCPAdapterLease** method on it.</span></span> <span data-ttu-id="5963f-165">В следующей команде элементы конвейера **Get-WmiObject** и **Where-Object** ограничены круглыми скобками, поэтому Windows PowerShell обрабатывает их первыми:</span><span class="sxs-lookup"><span data-stu-id="5963f-165">In the following command, the parentheses surrounding the **Get-WmiObject** and **Where-Object** pipeline elements direct Windows PowerShell to evaluate them first:</span></span>

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).ReleaseDHCPLeaseAll()
```

<span data-ttu-id="5963f-166">Такой же формат команды используется при вызове метода **RenewDHCPLeaseAll**:</span><span class="sxs-lookup"><span data-stu-id="5963f-166">You can use the same command format to invoke the **RenewDHCPLeaseAll** method:</span></span>

```
( Get-WmiObject -List | Where-Object -FilterScript {$_.Name -eq "Win32_NetworkAdapterConfiguration"} ).RenewDHCPLeaseAll()
```

### <a name="creating-a-network-share"></a><span data-ttu-id="5963f-167">Создание сетевой папки</span><span class="sxs-lookup"><span data-stu-id="5963f-167">Creating a Network Share</span></span>
<span data-ttu-id="5963f-168">Создать сетевую папку можно с помощью метода **Win32_Share Create**:</span><span class="sxs-lookup"><span data-stu-id="5963f-168">To create a network share, use the **Win32_Share Create** method:</span></span>

```
(Get-WmiObject -List -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Win32_Share"}).Create("C:\temp","TempShare",0,25,"test share of the temp folder")
```

<span data-ttu-id="5963f-169">Для этой же цели в Windows PowerShell можно использовать команду **net share**:</span><span class="sxs-lookup"><span data-stu-id="5963f-169">You can also create the share by using **net share** in Windows PowerShell:</span></span>

```
net share tempshare=c:\temp /users:25 /remark:"test share of the temp folder"
```

### <a name="removing-a-network-share"></a><span data-ttu-id="5963f-170">Удаление сетевой папки</span><span class="sxs-lookup"><span data-stu-id="5963f-170">Removing a Network Share</span></span>
<span data-ttu-id="5963f-171">Сетевую папку можно удалить с помощью **Win32_Share**, но этот процесс немного отличается от создания, так как требует получения именно удаляемой сетевой папки, а не класса **Win32_Share**.</span><span class="sxs-lookup"><span data-stu-id="5963f-171">You can remove a network share with **Win32_Share**, but the process is slightly different from creating a share, because you need to retrieve the specific share to be removed, rather than the **Win32_Share** class.</span></span> <span data-ttu-id="5963f-172">Следующий оператор удаляет сетевую папку TempShare:</span><span class="sxs-lookup"><span data-stu-id="5963f-172">The following statement deletes the share "TempShare":</span></span>

```
(Get-WmiObject -Class Win32_Share -ComputerName . -Filter "Name='TempShare'").Delete()
```

<span data-ttu-id="5963f-173">В этом случае подойдет и **Net share**:</span><span class="sxs-lookup"><span data-stu-id="5963f-173">**Net share** works as well:</span></span>

```
PS> net share tempshare /delete
tempshare was deleted successfully.
```

### <a name="connecting-a-windows-accessible-network-drive"></a><span data-ttu-id="5963f-174">Подключение сетевого диска, доступного в Windows</span><span class="sxs-lookup"><span data-stu-id="5963f-174">Connecting a Windows Accessible Network Drive</span></span>
<span data-ttu-id="5963f-175">Командлет **New-PSDrive** позволяет создавать диски Windows PowerShell, но они доступны только в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5963f-175">The **New-PSDrive** cmdlets creates a Windows PowerShell drive, but drives created this way are available only to Windows PowerShell.</span></span> <span data-ttu-id="5963f-176">Для создания сетевого диска можно воспользоваться COM-объектом **WScript.Network**.</span><span class="sxs-lookup"><span data-stu-id="5963f-176">To create a new networked drive, you can use the **WScript.Network** COM object.</span></span> <span data-ttu-id="5963f-177">Следующая команда сопоставляет сетевую папку \\\\FPS01\\users с локальным диском B:</span><span class="sxs-lookup"><span data-stu-id="5963f-177">The following command maps the share \\\\FPS01\\users to local drive B:</span></span>

```
(New-Object -ComObject WScript.Network).MapNetworkDrive("B:", "\\FPS01\users")
```

<span data-ttu-id="5963f-178">Так же работает и команда **net use**:</span><span class="sxs-lookup"><span data-stu-id="5963f-178">The **net use** command works as well:</span></span>

```
net use B: \\FPS01\users
```

<span data-ttu-id="5963f-179">Диски, сопоставленные с помощью **WScript.Network** или команды net use, мгновенно становятся доступными в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5963f-179">Drives mapped with either **WScript.Network** or net use are immediately available to Windows PowerShell.</span></span>

