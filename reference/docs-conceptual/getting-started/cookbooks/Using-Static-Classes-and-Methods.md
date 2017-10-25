---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Использование статических классов и методов"
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: fe41c7d6b45564e7b5bc2b922a18587c9745e26d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="using-static-classes-and-methods"></a><span data-ttu-id="a3299-103">Использование статических классов и методов</span><span class="sxs-lookup"><span data-stu-id="a3299-103">Using Static Classes and Methods</span></span>
<span data-ttu-id="a3299-104">Не все классы .NET Framework можно создать с помощью **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="a3299-104">Not all .NET Framework classes can be created by using **New-Object**.</span></span> <span data-ttu-id="a3299-105">Например, при попытке создать объект **System.Environment** или **System.Math** с помощью **New-Object** вы получите следующие сообщения об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a3299-105">For example, if you try to create a **System.Environment** or a **System.Math** object with **New-Object**, you will get the following error messages:</span></span>

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

<span data-ttu-id="a3299-106">Эти ошибки вызваны тем, что из таких классов нельзя создать объект.</span><span class="sxs-lookup"><span data-stu-id="a3299-106">These errors occur because there is no way to create a new object from these classes.</span></span> <span data-ttu-id="a3299-107">Эти классы являются справочными библиотеками методов и свойств, которые не изменяют состояние.</span><span class="sxs-lookup"><span data-stu-id="a3299-107">These classes are reference libraries of methods and properties that do not change state.</span></span> <span data-ttu-id="a3299-108">Их не нужно создавать, а можно просто использовать.</span><span class="sxs-lookup"><span data-stu-id="a3299-108">You don't need to create them, you simply use them.</span></span> <span data-ttu-id="a3299-109">Такие классы и методы называются *статическими классами*, так как они не создаются, удаляются или изменяются.</span><span class="sxs-lookup"><span data-stu-id="a3299-109">Classes and methods such as these are called *static classes* because they are not created, destroyed, or changed.</span></span> <span data-ttu-id="a3299-110">В качестве пояснения мы представим примеры, использующие статические классы.</span><span class="sxs-lookup"><span data-stu-id="a3299-110">To make this clear we will provide examples that use static classes.</span></span>

### <a name="getting-environment-data-with-systemenvironment"></a><span data-ttu-id="a3299-111">Получение данных среды с помощью System.Environment</span><span class="sxs-lookup"><span data-stu-id="a3299-111">Getting Environment Data with System.Environment</span></span>
<span data-ttu-id="a3299-112">Обычно первый шаг при работе с объектом в Windows PowerShell — использовать Get-Member, чтобы выяснить, какие элементы он содержит.</span><span class="sxs-lookup"><span data-stu-id="a3299-112">Usually, the first step in working with an object in Windows PowerShell is to use Get-Member to find out what members it contains.</span></span> <span data-ttu-id="a3299-113">Работа со статическими классами несколько отличается, так как фактический класс не является объектом.</span><span class="sxs-lookup"><span data-stu-id="a3299-113">With static classes, the process is a little different because the actual class is not an object.</span></span>

#### <a name="referring-to-the-static-systemenvironment-class"></a><span data-ttu-id="a3299-114">Ссылка на статический класс System.Environment</span><span class="sxs-lookup"><span data-stu-id="a3299-114">Referring to the Static System.Environment Class</span></span>
<span data-ttu-id="a3299-115">Сослаться на статический класс можно, заключив его имя в квадратные скобки.</span><span class="sxs-lookup"><span data-stu-id="a3299-115">You can refer to a static class by surrounding the class name with square brackets.</span></span> <span data-ttu-id="a3299-116">Например, можно ссылаться на **System.Environment**, введя его имя в квадратные скобки.</span><span class="sxs-lookup"><span data-stu-id="a3299-116">For example, you can refer to **System.Environment** by typing the name within brackets.</span></span> <span data-ttu-id="a3299-117">При этом отображаются сведения об универсальном типе:</span><span class="sxs-lookup"><span data-stu-id="a3299-117">Doing so displays some generic type information:</span></span>

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> <span data-ttu-id="a3299-118">Как упоминалось ранее, Windows PowerShell автоматически добавляет "**System.**"</span><span class="sxs-lookup"><span data-stu-id="a3299-118">As we mentioned previously, Windows PowerShell automatically prepends '**System.**'</span></span> <span data-ttu-id="a3299-119">к именам типов при использовании **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="a3299-119">to type names when you use **New-Object**.</span></span> <span data-ttu-id="a3299-120">То же самое происходит и при использовании имени типа в квадратных скобках, поэтому можно указать **\[System.Environment]** как **\[Environment]**.</span><span class="sxs-lookup"><span data-stu-id="a3299-120">The same thing happens when using a bracketed type name, so you can specify **\[System.Environment]** as **\[Environment]**.</span></span>

<span data-ttu-id="a3299-121">Класс **System.Environment** содержит общие сведения о рабочей среде для текущего процесса, которой при работе в Windows PowerShell является powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="a3299-121">The **System.Environment** class contains general information about the working environment for the current process, which is powershell.exe when working within Windows PowerShell.</span></span>

<span data-ttu-id="a3299-122">Если попытаться просмотреть описание этого класса, введя **\[System.Environment] | Get-Member**, тип объекта указывается как **System.RuntimeType**, а не **System.Environment**:</span><span class="sxs-lookup"><span data-stu-id="a3299-122">If you try to view details of this class by typing **\[System.Environment] | Get-Member**, the object type is reported as being **System.RuntimeType** , not **System.Environment**:</span></span>

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

<span data-ttu-id="a3299-123">Чтобы просмотреть статические элементы с помощью Get-Member, укажите параметр **Static**.</span><span class="sxs-lookup"><span data-stu-id="a3299-123">To view static members with Get-Member, specify the **Static** parameter:</span></span>

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

<span data-ttu-id="a3299-124">Теперь можно выбрать свойства для просмотра из System.Environment.</span><span class="sxs-lookup"><span data-stu-id="a3299-124">We can now select properties to view from System.Environment.</span></span>

#### <a name="displaying-static-properties-of-systemenvironment"></a><span data-ttu-id="a3299-125">Отображение статических свойств System.Environment</span><span class="sxs-lookup"><span data-stu-id="a3299-125">Displaying Static Properties of System.Environment</span></span>
<span data-ttu-id="a3299-126">Свойства System.Environment также являются статическими и должны быть указаны иначе, чем обычные свойства.</span><span class="sxs-lookup"><span data-stu-id="a3299-126">The properties of System.Environment are also static, and must be specified in a different way than normal properties.</span></span> <span data-ttu-id="a3299-127">Мы используем **::**, чтобы сообщить Windows PowerShell, что требуется использовать статический метод или статическое свойство.</span><span class="sxs-lookup"><span data-stu-id="a3299-127">We use **::** to indicate to Windows PowerShell that we want to work with a static method or property.</span></span> <span data-ttu-id="a3299-128">Чтобы просмотреть команду, которая использовалась для запуска Windows PowerShell, мы проверяем свойство **CommandLine**, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="a3299-128">To see the command that was used to launch Windows PowerShell, we check the **CommandLine** property by typing:</span></span>

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

<span data-ttu-id="a3299-129">Чтобы проверить версию операционной системы, отобразите свойство OSVersion, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="a3299-129">To check the operating system version, display the OSVersion property by typing:</span></span>

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

<span data-ttu-id="a3299-130">Можно проверить, находится ли компьютер в процессе завершения работы, отобразив свойство **HasShutdownStarted**:</span><span class="sxs-lookup"><span data-stu-id="a3299-130">We can check whether the computer is in the process of shutting down by displaying the **HasShutdownStarted** property:</span></span>

```
PS> [System.Environment]::HasShutdownStarted
False
```

### <a name="doing-math-with-systemmath"></a><span data-ttu-id="a3299-131">Математические операции с помощью System.Math</span><span class="sxs-lookup"><span data-stu-id="a3299-131">Doing Math with System.Math</span></span>
<span data-ttu-id="a3299-132">Статический класс System.Math полезен для выполнения некоторых математических операций.</span><span class="sxs-lookup"><span data-stu-id="a3299-132">The System.Math static class is useful for performing some mathematical operations.</span></span> <span data-ttu-id="a3299-133">Важные элементы **System.Math** — главным образом методы, которые можно отобразить с помощью **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="a3299-133">The important members of **System.Math** are mostly methods, which we can display by using **Get-Member**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3299-134">System.Math имеет несколько методов с одинаковым именем, но они различаются по типу параметров.</span><span class="sxs-lookup"><span data-stu-id="a3299-134">System.Math has several methods with the same name, but they are distinguished by the type of their parameters.</span></span>

<span data-ttu-id="a3299-135">Введите следующую команду, чтобы получить список методов для класса **System.Math**.</span><span class="sxs-lookup"><span data-stu-id="a3299-135">Type the following command to list the methods of the **System.Math** class.</span></span>

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

<span data-ttu-id="a3299-136">При этом отображается несколько математических методов.</span><span class="sxs-lookup"><span data-stu-id="a3299-136">This displays several mathematical methods.</span></span> <span data-ttu-id="a3299-137">Ниже приведен список команд, которые демонстрируют работу некоторых распространенных методов:</span><span class="sxs-lookup"><span data-stu-id="a3299-137">Here is a list of commands that demonstrate how some of the common methods work:</span></span>

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

