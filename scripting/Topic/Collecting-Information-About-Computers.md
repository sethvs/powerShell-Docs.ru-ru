---
title: Сбор информации о компьютерах
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e7b6a2d-34f7-4731-a92c-8b3382eb51bb
---
# Сбор информации о компьютерах
**Get-WmiObject** — самый важный командлет для общих задач управления системой. Все ключевые параметры подсистемы доступны через инструментарий WMI. Более того, инструментарий WMI обрабатывает данные как объекты, сгруппированные в коллекции из одного или нескольких элементов. Поскольку Windows PowerShell также работает с объектами и имеет конвейер, позволяющий одинаково обрабатывать отдельный объект или несколько объектов, общий доступ к инструментарию WMI предоставляет возможность выполнять некоторые сложные задачи с небольшими затратами усилий.

В следующих примерах показано, как собрать определенные сведения, применяя командлет **Get-WmiObject** к произвольному компьютеру. Значение параметра **ComputerName** задается точкой **.**, представляющей локальный компьютер. Здесь можно указать имя или IP-адрес, связанные с любым компьютером, к которому требуется получить доступ через инструментарий WMI. Чтобы получить сведения о локальном компьютере, параметр **-ComputerName** можно опустить.

### Вывод параметров рабочего стола
Для начала рассмотрим команду, собирающую сведения о рабочих столах локального компьютера.

```
Get-WmiObject -Class Win32_Desktop -ComputerName .
```

Эта команда возвращает сведения обо всех рабочих столах, вне зависимости от их использования.

> [!NOTE]
> Сведения, возвращаемые некоторыми классами WMI, могут быть очень подробными и часто содержат метаданные о классе WMI. Поскольку имена большинства этих свойств метаданных начинаются двойным знаком подчеркивания, эти свойства можно отфильтровать с помощью командлета Select-Object. Чтобы выбрать свойства, начинающиеся с буквы, для параметра Property следует указать **[a-z]&#42;**. Например:

```
Get-WmiObject -Class Win32_Desktop -ComputerName . | Select-Object -Property [a-z]*
```

Чтобы отфильтровать метаданные, направьте результаты команды Get-WmiObject в **Select-Object -Property [a-z]&#42;** с помощью оператора конвейера (|).

### Вывод сведений о BIOS
Класс WMI Win32_BIOS возвращает довольно компактные и полные сведения о системной BIOS локального компьютера:

```
Get-WmiObject -Class Win32_BIOS -ComputerName .
```

### Вывод сведений о процессоре
Общие сведения о процессоре можно получить с помощью класса **Win32_Processor** инструментария WMI, однако пользователю наверняка потребуется отфильтровать полученные данные:

```
Get-WmiObject -Class Win32_Processor -ComputerName . | Select-Object -Property [a-z]*
```

Чтобы получить общую строку описания семейства процессора, достаточно вернуть свойство **Win32_ComputerSystemSystemType**:

```
PS> Get-WmiObject -Class Win32_ComputerSystem -ComputerName . | Select-Object -Property SystemType
SystemType
----------
X86-based PC
```

### Вывод производителя и модели компьютера
Сведения о модели компьютера также доступны в **Win32_ComputerSystem**. Чтобы получить данные поставщика вычислительной техники (OEM), стандартные отображаемые выходные данные фильтровать не нужно:

```
PS> Get-WmiObject -Class Win32_ComputerSystem
Domain              : WORKGROUP
Manufacturer        : Compaq Presario 06
Model               : DA243A-ABA 6415cl NA910
Name                : MyPC
PrimaryOwnerName    : Jane Doe
TotalPhysicalMemory : 804765696
```

Выходные данные из команд, подобных показанной выше и возвращающих сведения напрямую от аппаратного обеспечения, не могут быть дополнены. Иногда сведения неверно сконфигурированы производителем оборудования и недоступны для запроса.

### Вывод установленных исправлений
Список всех установленных исправлений можно получить с помощью **Win32_QuickFixEngineering**:

```
Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName .
```

Этот класс возвращает список исправлений в следующем виде:

```
Description         : Update for Windows XP (KB910437)
FixComments         : Update
HotFixID            : KB910437
Install Date        :
InstalledBy         : Administrator
InstalledOn         : 12/16/2005
Name                :
ServicePackInEffect : SP3
Status              :
```

Для получения более кратких сведений нужно исключить некоторые свойства. Параметр **Get-WmiObject Property** позволяет выбрать только идентификаторы **HotFixID**, однако на самом деле возвращается больше данных, поскольку по умолчанию отображаются все метаданные:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property HotFixId
HotFixID         : KB910437
__GENUS          : 2
__CLASS          : Win32_QuickFixEngineering
__SUPERCLASS     :
__DYNASTY        :
__RELPATH        :
__PROPERTY_COUNT : 1
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
```

Дополнительные данные выводятся, поскольку параметр Property командлета **Get-WmiObject** ограничивает свойства, возвращаемые из экземпляров класса, но не объекты, возвращаемые оболочке Windows PowerShell. Командлет **Select-Object** позволяет сократить возвращаемые выходные данные:

```
PS> Get-WmiObject -Class Win32_QuickFixEngineering -ComputerName . -Property Hot
FixId | Select-Object -Property HotFixId
HotFixId
--------
KB910437
```

### Вывод сведений о версии операционной среды
Свойства класса **Win32_OperatingSystem** включают сведения о версии операционной среды и пакета обновлений. Эти свойства можно выбрать явным образом, чтобы получить сводные данные о версиях из **Win32_OperatingSystem**:

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property BuildNumber,BuildType,OSType,ServicePackMajorVersion,ServicePackMinorVersion
```

С параметром **Select-Object Property** можно использовать подстановочные символы. Поскольку в рассматриваемом случае важны все свойства, имена которых начинаются с **Build** либо с **ServicePack**, указанную строку можно сократить:

```
PS> Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property Build*,OSType,ServicePack*

BuildNumber             : 2600
BuildType               : Uniprocessor Free
OSType                  : 18
ServicePackMajorVersion : 2
ServicePackMinorVersion : 0
```

### Вывод локальных пользователей и владельца
Общие сведения о локальных пользователях — количество лицензированных пользователей, текущее число пользователей и имя владельца — можно получить, выбрав соответствующие свойства **Win32_OperatingSystem**. Отображаемые свойства можно указать явным образом:

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property NumberOfLicensedUsers,NumberOfUsers,RegisteredUser
```

В более сжатом варианте используются подстановочные символы:

```
Get-WmiObject -Class Win32_OperatingSystem -ComputerName . | Select-Object -Property *user*
```

### Получение сведений о доступном месте на диске
Чтобы получить сведения о дисковом пространстве и свободном месте на всех локальных дисках, можно воспользоваться классом Win32_LogicalDisk инструментария WMI. Для просмотра следует выбрать только те экземпляры, у которых свойство DriveType принимает значение 3, — именно оно используется инструментарием WMI для постоянных жестких дисков.

```
Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName .

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 65541357568
Size         : 203912880128
VolumeName   : Local Disk

DeviceID     : Q:
DriveType    : 3
ProviderName :
FreeSpace    : 44298250240
Size         : 122934034432
VolumeName   : New Volume

PS> Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum

Get-WmiObject -Class Win32_LogicalDisk -Filter "DriveType=3" -ComputerName . | Measure-Object -Property FreeSpace,Size -Sum | Select-Object -Property Property,Sum
```

### Получение сведений о сеансах входа в систему
Общие сведения о сеансах входа в систему, связанных с пользователями, можно получить через класс Win32_LogonSession инструментария WMI:

```
Get-WmiObject -Class Win32_LogonSession -ComputerName .
```

### Получение сведений о пользователе, выполнившем вход на компьютер
Имя пользователя, выполнившего вход на определенный компьютер, можно отобразить с помощью Win32_ComputerSystem. Приведенная ниже команда возвращает только пользователей, выполнивших вход на рабочий стол системы:

```
Get-WmiObject -Class Win32_ComputerSystem -Property UserName -ComputerName .
```

### Получение сведений о местном времени компьютера
Данные о текущем местном времени определенного компьютера можно получить с помощью класса Win32_LocalTime инструментария WMI. Поскольку этот класс по умолчанию отображает все метаданные, пользователю может потребоваться фильтрация с помощью командлета **Select-Object**:

```
PS> Get-WmiObject -Class Win32_LocalTime -ComputerName . | Select-Object -Property [a-z]*

Day          : 15
DayOfWeek    : 4
Hour         : 12
Milliseconds :
Minute       : 11
Month        : 6
Quarter      : 2
Second       : 52
WeekInMonth  : 3
Year         : 2006
```

### Отображение состояния службы
Для просмотра состояния всех служб на определенном компьютере можно локально воспользоваться командлетом **Get-Service**, как было показано ранее. Для удаленных систем можно использовать класс Win32_Service инструментария WMI. Если использовать **Select-Object** для получения результатов **Status**, **Name** и **DisplayName**, формат вывода будет идентичен формату вывода командлета **Get-Service**:

```
Get-WmiObject -Class Win32_Service -ComputerName . | Select-Object -Property Status,Name,DisplayName
```

Чтобы полностью отобразить службы с очень длинными именами, может потребоваться использование командлета **Format-Table** с параметрами **AutoSize** и **Wrap**, позволяющими оптимизировать ширину столбцов и переносить длинные имена на следующие строки вместо их усечения:

```
Get-WmiObject -Class Win32_Service -ComputerName . | Format-Table -Property Status,Name,DisplayName -AutoSize -Wrap
```



<!--HONumber=Apr16_HO1-->


