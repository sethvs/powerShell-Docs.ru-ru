---
title: "Использование статических классов и методов"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: 50ebc8a737b50aba5a5af49716b59905da74669a

---

# Использование статических классов и методов
Не все классы .NET Framework можно создать с помощью **New\-Object**. Например, при попытке создать объект **System.Environment** или **System.Math** с помощью **New\-Object** вы получите следующие сообщения об ошибке:

```
PS> New-Object System.Environment
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Environment.
At line:1 char:11
+ New-Object  <<<< System.Environment
PS> New-Object System.Math
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Math.
At line:1 char:11
+ New-Object  <<<< System.Math
```

Эти ошибки вызваны тем, что из таких классов нельзя создать объект. Эти классы являются справочными библиотеками методов и свойств, которые не изменяют состояние. Их не нужно создавать, а можно просто использовать. Такие классы и методы называются *статическими классами*, так как они не создаются, удаляются или изменяются. В качестве пояснения мы представим примеры, использующие статические классы.

### Получение данных среды с помощью System.Environment
Обычно первый шаг при работе с объектом в Windows PowerShell заключается в использовании Get\-Member, чтобы выяснить, какие элементы он содержит. Работа со статическими классами несколько отличается, так как фактический класс не является объектом.

#### Ссылка на статический класс System.Environment
Сослаться на статический класс можно, заключив его имя в квадратные скобки. Например, можно ссылаться на **System.Environment**, введя его имя в квадратные скобки. При этом отображаются сведения об универсальном типе:

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> Как упоминалось ранее, Windows PowerShell автоматически добавляет "**System.**" к именам типов при использовании **New\-Object**. То же самое происходит и при использовании имени типа в квадратных скобках, поэтому можно указать **\[System.Environment]** как **\[Environment]**.

Класс **System.Environment** содержит общие сведения о рабочей среде для текущего процесса, которой при работе в Windows PowerShell является powershell.exe.

Если попытаться просмотреть описание этого класса, введя **\[System.Environment] | Get\-Member**, тип объекта указывается как **System.RuntimeType**, а не **System.Environment**:

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

Чтобы просмотреть статические элементы с помощью Get\-Member, укажите параметр **Static**:

```
PS> [System.Environment] | Get-Member -Static

   TypeName: System.Environment

Name                       MemberType Definition
----                       ---------- ----------
Equals                     Method     static System.Boolean Equals(Object ob...
Exit                       Method     static System.Void Exit(Int32 exitCode)
...
CommandLine                Property   static System.String CommandLine {get;}
CurrentDirectory           Property   static System.String CurrentDirectory ...
ExitCode                   Property   static System.Int32 ExitCode {get;set;}
HasShutdownStarted         Property   static System.Boolean HasShutdownStart...
MachineName                Property   static System.String MachineName {get;}
NewLine                    Property   static System.String NewLine {get;}
OSVersion                  Property   static System.OperatingSystem OSVersio...
ProcessorCount             Property   static System.Int32 ProcessorCount {get;}
StackTrace                 Property   static System.String StackTrace {get;}
SystemDirectory            Property   static System.String SystemDirectory {...
TickCount                  Property   static System.Int32 TickCount {get;}
UserDomainName             Property   static System.String UserDomainName {g...
UserInteractive            Property   static System.Boolean UserInteractive ...
UserName                   Property   static System.String UserName {get;}
Version                    Property   static System.Version Version {get;}
WorkingSet                 Property   static System.Int64 WorkingSet {get;}
TickCount                               ExitCode
```

Теперь можно выбрать свойства для просмотра из System.Environment.

#### Отображение статических свойств System.Environment
Свойства System.Environment также являются статическими и должны быть указаны иначе, чем обычные свойства. Мы используем **::**, чтобы сообщить Windows PowerShell, что требуется использовать статический метод или статическое свойство. Чтобы просмотреть команду, которая использовалась для запуска Windows PowerShell, мы проверяем свойство **CommandLine**, введя следующее:

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

Чтобы проверить версию операционной системы, отобразите свойство OSVersion, введя следующее:

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

Можно проверить, находится ли компьютер в процессе завершения работы, отобразив свойство **HasShutdownStarted**:

```
PS> [System.Environment]::HasShutdownStarted
False
```

### Математические операции с помощью System.Math
Статический класс System.Math полезен для выполнения некоторых математических операций. Важными элементами **System.Math** являются главным образом методы, которые можно отобразить с помощью **Get\-Member**.

> [!NOTE]
> System.Math имеет несколько методов с одинаковым именем, но они различаются по типу параметров.

Введите следующую команду, чтобы получить список методов для класса **System.Math**.

```
PS> [System.Math] | Get-Member -Static -MemberType Methods

   TypeName: System.Math

Name            MemberType Definition
----            ---------- ----------
Abs             Method     static System.Single Abs(Single value), static Sy...
Acos            Method     static System.Double Acos(Double d)
Asin            Method     static System.Double Asin(Double d)
Atan            Method     static System.Double Atan(Double d)
Atan2           Method     static System.Double Atan2(Double y, Double x)
BigMul          Method     static System.Int64 BigMul(Int32 a, Int32 b)
Ceiling         Method     static System.Double Ceiling(Double a), static Sy...
Cos             Method     static System.Double Cos(Double d)
Cosh            Method     static System.Double Cosh(Double value)
DivRem          Method     static System.Int32 DivRem(Int32 a, Int32 b, Int3...
Equals          Method     static System.Boolean Equals(Object objA, Object ...
Exp             Method     static System.Double Exp(Double d)
Floor           Method     static System.Double Floor(Double d), static Syst...
IEEERemainder   Method     static System.Double IEEERemainder(Double x, Doub...
Log             Method     static System.Double Log(Double d), static System...
Log10           Method     static System.Double Log10(Double d)
Max             Method     static System.SByte Max(SByte val1, SByte val2), ...
Min             Method     static System.SByte Min(SByte val1, SByte val2), ...
Pow             Method     static System.Double Pow(Double x, Double y)
ReferenceEquals Method     static System.Boolean ReferenceEquals(Object objA...
Round           Method     static System.Double Round(Double a), static Syst...
Sign            Method     static System.Int32 Sign(SByte value), static Sys...
Sin             Method     static System.Double Sin(Double a)
Sinh            Method     static System.Double Sinh(Double value)
Sqrt            Method     static System.Double Sqrt(Double d)
Tan             Method     static System.Double Tan(Double a)
Tanh            Method     static System.Double Tanh(Double value)
Truncate        Method     static System.Decimal Truncate(Decimal d), static...
```

При этом отображается несколько математических методов. Ниже приведен список команд, которые демонстрируют работу некоторых распространенных методов:

```
PS> [System.Math]::Sqrt(9)
3
PS> [System.Math]::Pow(2,3)
8
PS> [System.Math]::Floor(3.3)
3
PS> [System.Math]::Floor(-3.3)
-4
PS> [System.Math]::Ceiling(3.3)
4
PS> [System.Math]::Ceiling(-3.3)
-3
PS> [System.Math]::Max(2,7)
7
PS> [System.Math]::Min(2,7)
2
PS> [System.Math]::Truncate(9.3)
9
PS> [System.Math]::Truncate(-9.3)
-9
```




<!--HONumber=Jun16_HO4-->


