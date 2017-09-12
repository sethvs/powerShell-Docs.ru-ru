---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Получение объектов WMI (Get-WmiObject)"
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: fbaac2797dd62eb03a2be581b3b5f8be6dafc0ad
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="getting-wmi-objects-get-wmiobject"></a>Получение объектов WMI (Get-WmiObject)

## <a name="getting-wmi-objects-get-wmiobject"></a>Получение объектов WMI (Get-WmiObject)
Инструментарий управления Windows (WMI) является ключевой технологией системного администрирования Windows, поскольку предоставляет широкий спектр сведений в унифицированном виде. Так как спектр возможностей инструментария WMI достаточно широк, командлет **Get-WmiObject** Windows PowerShell, служащий для доступа к объектам WMI, — один из наиболее полезных. Мы рассмотрим, как командлет Get-WmiObject обращается к объектам WMI и как использовать объекты WMI для выполнения определенных задач.

### <a name="listing-wmi-classes"></a>Вывод списка классов WMI
Первая проблема, с которой сталкивается большинство пользователей WMI, — это выяснение того, что можно сделать с помощью инструментария WMI. Классы WMI описывают ресурсы, которыми можно управлять. Имеются сотни классов WMI, некоторые из которых содержат множество свойств.

Командлет **Get-WmiObject** решает эту проблему, предоставляя сведения об инструментарии WMI. Список классов WMI, доступных на локальном компьютере, можно получить, введя команду:

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

Можно извлечь те же сведения на удаленном компьютере, указав в параметре ComputerName имя компьютера или его IP-адрес:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

Список классов, возвращаемый удаленным компьютером, может различаться в зависимости от операционной системы компьютера и определенных расширений WMI, добавленных установленными приложениями.

> [!NOTE]
> При использовании командлета Get-WmiObject для подключения к удаленному компьютеру на последнем должен быть запущен инструментарий WMI, а используемая учетная запись должна входить в группу локальных администраторов на удаленном компьютере (конфигурация по умолчанию). На удаленной системе может быть не установлена оболочка Windows PowerShell. Это позволяет администрировать операционные системы, на которых не запущена оболочка Windows PowerShell, но имеется инструментарий WMI.

При подключении к локальной системе можно указать и параметр ComputerName. Можно использовать имя локального компьютера, его IP-адрес (или петлевой адрес 127.0.0.1) либо "." (в стиле инструментария WMI) в качестве имени компьютера. Если на компьютере с именем "Admin01" и IP-адресом 192.168.1.90 запущена оболочка Windows PowerShell, следующие команды возвратят список классов WMI для этого компьютера:

```
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

Командлет Get-WmiObject использует по умолчанию пространство имен root/cimv2. Чтобы задать другое пространство имен WMI, воспользуйтесь параметром **Namespace** и укажите путь к соответствующему пространству имен:

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a>Вывод сведений о классе WMI
Если имя класса WMI уже известно, можно немедленно получить сведения о нем. Например, одним из классов WMI, используемых для получения сведений о компьютере, является **Win32_OperatingSystem**.

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

Хотя показаны все параметры, команда может быть представлена в более короткой форме. Параметр **ComputerName** не является обязательным при подключении к локальной системе. Мы покажем это, чтобы продемонстрировать наиболее общий случай и напомнить об этом параметре. По умолчанию параметр **Namespace** получает значение root/cimv2 и может быть опущен. В конце концов, большинство командлетов позволяет опускать имя типовых параметров. Если в командлете Get-WmiObject не указано имя для первого параметра, Windows PowerShell считает его параметром **Class**. Это значит, что последнюю команду можно было ввести в таком виде:

```
Get-WmiObject Win32_OperatingSystem
```

Класс **Win32_OperatingSystem** имеет больше свойств, чем показано здесь. Можно воспользоваться командлетом Get-Member, чтобы показать все свойства. Свойства класса WMI автоматически доступны, как и другие свойства объекта:

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

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a>Вывод свойств, отличных от используемых по умолчанию, с помощью командлетов Format
Если необходимо показать сведения, содержащиеся в классе **Win32_OperatingSystem**, которые не выводятся по умолчанию, можно воспользоваться командлетом **Format**. Например, если нужно показать сведения о количестве доступной памяти, введите:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMemory FreePhysicalMemory FreeVirtualMemory FreeSpaceInPagingFiles
---------------------- ---------------    ------------------ -==--------------------- ---------------
               2097024          785904                305808           2056724                1558232
```

> [!NOTE]
> Подстановочные знаки допускаются в именах свойств в командлете **Format-Table**, поэтому последний элемент конвейера может быть сокращен до **Format-Table - Property Total*, Free*.

Сведения о памяти можно представить в более понятном виде, отформатировав список с помощью следующей команды:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```

