---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Получение объектов WMI (Get-WmiObject)"
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: e7b10648e91d1c0dc1424944e55177dc7407fe36
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="08787-103">Получение объектов WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="08787-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="08787-104">Получение объектов WMI (Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="08787-104">Getting WMI Objects (Get-WmiObject)</span></span>
<span data-ttu-id="08787-105">Инструментарий управления Windows (WMI) является ключевой технологией системного администрирования Windows, поскольку предоставляет широкий спектр сведений в унифицированном виде.</span><span class="sxs-lookup"><span data-stu-id="08787-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="08787-106">Так как спектр возможностей инструментария WMI достаточно широк, командлет **Get-WmiObject** Windows PowerShell, служащий для доступа к объектам WMI, — один из наиболее полезных.</span><span class="sxs-lookup"><span data-stu-id="08787-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="08787-107">Мы рассмотрим, как командлет Get-WmiObject обращается к объектам WMI и как использовать объекты WMI для выполнения определенных задач.</span><span class="sxs-lookup"><span data-stu-id="08787-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="08787-108">Вывод списка классов WMI</span><span class="sxs-lookup"><span data-stu-id="08787-108">Listing WMI Classes</span></span>
<span data-ttu-id="08787-109">Первая проблема, с которой сталкивается большинство пользователей WMI, — это выяснение того, что можно сделать с помощью инструментария WMI.</span><span class="sxs-lookup"><span data-stu-id="08787-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="08787-110">Классы WMI описывают ресурсы, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="08787-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="08787-111">Имеются сотни классов WMI, некоторые из которых содержат множество свойств.</span><span class="sxs-lookup"><span data-stu-id="08787-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="08787-112">Командлет **Get-WmiObject** решает эту проблему, предоставляя сведения об инструментарии WMI.</span><span class="sxs-lookup"><span data-stu-id="08787-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="08787-113">Список классов WMI, доступных на локальном компьютере, можно получить, введя команду:</span><span class="sxs-lookup"><span data-stu-id="08787-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="08787-114">Можно извлечь те же сведения на удаленном компьютере, указав в параметре ComputerName имя компьютера или его IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="08787-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="08787-115">Список классов, возвращаемый удаленным компьютером, может различаться в зависимости от операционной системы компьютера и определенных расширений WMI, добавленных установленными приложениями.</span><span class="sxs-lookup"><span data-stu-id="08787-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="08787-116">При использовании командлета Get-WmiObject для подключения к удаленному компьютеру на последнем должен быть запущен инструментарий WMI, а используемая учетная запись должна входить в группу локальных администраторов на удаленном компьютере (конфигурация по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="08787-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="08787-117">На удаленной системе может быть не установлена оболочка Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08787-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="08787-118">Это позволяет администрировать операционные системы, на которых не запущена оболочка Windows PowerShell, но имеется инструментарий WMI.</span><span class="sxs-lookup"><span data-stu-id="08787-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="08787-119">При подключении к локальной системе можно указать и параметр ComputerName.</span><span class="sxs-lookup"><span data-stu-id="08787-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="08787-120">Можно использовать имя локального компьютера, его IP-адрес (или петлевой адрес 127.0.0.1) либо "." (в стиле инструментария WMI) в качестве имени компьютера.</span><span class="sxs-lookup"><span data-stu-id="08787-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="08787-121">Если на компьютере с именем "Admin01" и IP-адресом 192.168.1.90 запущена оболочка Windows PowerShell, следующие команды возвратят список классов WMI для этого компьютера:</span><span class="sxs-lookup"><span data-stu-id="08787-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="08787-122">Командлет Get-WmiObject использует по умолчанию пространство имен root/cimv2.</span><span class="sxs-lookup"><span data-stu-id="08787-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="08787-123">Чтобы задать другое пространство имен WMI, воспользуйтесь параметром **Namespace** и укажите путь к соответствующему пространству имен:</span><span class="sxs-lookup"><span data-stu-id="08787-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="08787-124">Вывод сведений о классе WMI</span><span class="sxs-lookup"><span data-stu-id="08787-124">Displaying WMI Class Details</span></span>
<span data-ttu-id="08787-125">Если имя класса WMI уже известно, можно немедленно получить сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="08787-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="08787-126">Например, одним из классов WMI, используемых для получения сведений о компьютере, является **Win32_OperatingSystem**.</span><span class="sxs-lookup"><span data-stu-id="08787-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="08787-127">Хотя показаны все параметры, команда может быть представлена в более короткой форме.</span><span class="sxs-lookup"><span data-stu-id="08787-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="08787-128">Параметр **ComputerName** не является обязательным при подключении к локальной системе.</span><span class="sxs-lookup"><span data-stu-id="08787-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="08787-129">Мы покажем это, чтобы продемонстрировать наиболее общий случай и напомнить об этом параметре.</span><span class="sxs-lookup"><span data-stu-id="08787-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="08787-130">По умолчанию параметр **Namespace** получает значение root/cimv2 и может быть опущен.</span><span class="sxs-lookup"><span data-stu-id="08787-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="08787-131">В конце концов, большинство командлетов позволяет опускать имя типовых параметров.</span><span class="sxs-lookup"><span data-stu-id="08787-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="08787-132">Если в командлете Get-WmiObject не указано имя для первого параметра, Windows PowerShell считает его параметром **Class**.</span><span class="sxs-lookup"><span data-stu-id="08787-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="08787-133">Это значит, что последнюю команду можно было ввести в таком виде:</span><span class="sxs-lookup"><span data-stu-id="08787-133">This means the last command could have been issued by typing:</span></span>

```
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="08787-134">Класс **Win32_OperatingSystem** имеет больше свойств, чем показано здесь.</span><span class="sxs-lookup"><span data-stu-id="08787-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="08787-135">Можно воспользоваться командлетом Get-Member, чтобы показать все свойства.</span><span class="sxs-lookup"><span data-stu-id="08787-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="08787-136">Свойства класса WMI автоматически доступны, как и другие свойства объекта:</span><span class="sxs-lookup"><span data-stu-id="08787-136">The properties of a WMI class are automatically available like other object properties:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Get-Member -MemberType Property

   TypeName: System.Management.ManagementObject#root\cimv2\Win32_OperatingSyste
m

Name                                      MemberType Definition
----                                      ---------- ----------
__CLASS                                   Property   System.String __CLASS {...
...
BootDevice                                Property   System.String BootDevic...
BuildNumber                               Property   System.String BuildNumb...
...
```

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="08787-137">Вывод свойств, отличных от используемых по умолчанию, с помощью командлетов Format</span><span class="sxs-lookup"><span data-stu-id="08787-137">Displaying Non-Default Properties with Format Cmdlets</span></span>
<span data-ttu-id="08787-138">Если необходимо показать сведения, содержащиеся в классе **Win32_OperatingSystem**, которые не выводятся по умолчанию, можно воспользоваться командлетом **Format**.</span><span class="sxs-lookup"><span data-stu-id="08787-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="08787-139">Например, если нужно показать сведения о количестве доступной памяти, введите:</span><span class="sxs-lookup"><span data-stu-id="08787-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMem FreePhysicalMem FreeVirtualMemo FreeSpaceInPagi
                              ory              ry         ngFiles
--------------- --------------- --------------- --------------- ---------------
        2097024          785904          305808         2056724         1558232
```

> [!NOTE]
> <span data-ttu-id="08787-140">Подстановочные знаки допускаются в именах свойств в командлете **Format-Table**, поэтому последний элемент конвейера может быть сокращен до **Format-Table -Property TotalV\&#42;,Free\&#42;**.</span><span class="sxs-lookup"><span data-stu-id="08787-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to **Format-Table -Property TotalV\&#42;,Free\&#42;**</span></span>

<span data-ttu-id="08787-141">Сведения о памяти можно представить в более понятном виде, отформатировав список с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="08787-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```

