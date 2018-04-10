---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 85e9206ffef76fb4bd7714d847888e6e5bbcc4ec
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="new-language-features-in-powershell-50"></a><span data-ttu-id="7deb6-102">Новые возможности языка в PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7deb6-102">New language features in PowerShell 5.0</span></span>

<span data-ttu-id="7deb6-103">В PowerShell 5.0 появились следующие новые элементы языка для Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7deb6-103">PowerShell 5.0 introduces the following new language elements in Windows PowerShell:</span></span>

## <a name="class-keyword"></a><span data-ttu-id="7deb6-104">Ключевое слово Class</span><span class="sxs-lookup"><span data-stu-id="7deb6-104">Class keyword</span></span>

<span data-ttu-id="7deb6-105">Ключевое слово **class** определяет новый класс.</span><span class="sxs-lookup"><span data-stu-id="7deb6-105">The **class** keyword defines a new class.</span></span> <span data-ttu-id="7deb6-106">Это подлинный тип .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7deb6-106">This is a true .NET Framework type.</span></span>
<span data-ttu-id="7deb6-107">Члены класса являются открытыми, но только в рамках области модуля.</span><span class="sxs-lookup"><span data-stu-id="7deb6-107">Class members are public, but only public within the module scope.</span></span>
<span data-ttu-id="7deb6-108">Вы не можете ссылаться на имя типа в виде строки (например, `New-Object` не работает), а также использовать литерал типа (например, `[MyClass]`) за пределами файла сценария или модуля, где определен этот класс.</span><span class="sxs-lookup"><span data-stu-id="7deb6-108">You can't refer to the type name as a string (for example, `New-Object` doesn't work), and in this release, you can't use a type literal (for example, `[MyClass]`) outside the script/module file in which the class is defined.</span></span>

```powershell
class MyClass
{
    ...
}
```

## <a name="enum-keyword-and-enumerations"></a><span data-ttu-id="7deb6-109">Ключевое слово Enum и перечисления</span><span class="sxs-lookup"><span data-stu-id="7deb6-109">Enum keyword and enumerations</span></span>

<span data-ttu-id="7deb6-110">Добавлена поддержка ключевого слова **enum**, где символ новой строки используется в качестве разделителя.</span><span class="sxs-lookup"><span data-stu-id="7deb6-110">Support for the **enum** keyword has been added, which uses newline as the delimiter.</span></span>
<span data-ttu-id="7deb6-111">Текущие ограничения: перечислитель нельзя определить относительно самого себя, но можно инициализировать перечисление относительно другого перечисления, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="7deb6-111">Current limitations: you cannot define an enumerator in terms of itself, but you can initialize an enum in terms of another enum, as shown in the following example.</span></span>
<span data-ttu-id="7deb6-112">Кроме того, в настоящее время нельзя задать базовый тип (всегда [int]).</span><span class="sxs-lookup"><span data-stu-id="7deb6-112">Also, the base type cannot currently be specified; it is always [int].</span></span>

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

<span data-ttu-id="7deb6-113">Значение перечислителя должно быть константой времени анализа. Для него нельзя задать результат вызванной команды.</span><span class="sxs-lookup"><span data-stu-id="7deb6-113">An enumerator value must be a parse time constant; you cannot set it to the result of an invoked command.</span></span>

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

<span data-ttu-id="7deb6-114">Перечисления поддерживают арифметические операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="7deb6-114">Enums support arithmetic operations, as shown in the following example.</span></span>

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## <a name="import-dscresource"></a><span data-ttu-id="7deb6-115">Import-DscResource</span><span class="sxs-lookup"><span data-stu-id="7deb6-115">Import-DscResource</span></span>

<span data-ttu-id="7deb6-116">**Import-DscResource** теперь является подлинным динамическим ключевым словом.</span><span class="sxs-lookup"><span data-stu-id="7deb6-116">**Import-DscResource** is now a true dynamic keyword.</span></span>
<span data-ttu-id="7deb6-117">PowerShell анализирует корневой модуль указанного модуля, выполняя поиск классов, которые содержат атрибут **DscResource**.</span><span class="sxs-lookup"><span data-stu-id="7deb6-117">PowerShell parses the specified module’s root module, searching for classes that contain the **DscResource** attribute.</span></span>

## <a name="implementingassembly"></a><span data-ttu-id="7deb6-118">ImplementingAssembly</span><span class="sxs-lookup"><span data-stu-id="7deb6-118">ImplementingAssembly</span></span>

<span data-ttu-id="7deb6-119">В ModuleInfo добавлено новое поле **ImplementingAssembly**.</span><span class="sxs-lookup"><span data-stu-id="7deb6-119">A new field, **ImplementingAssembly**, has been added to ModuleInfo.</span></span> <span data-ttu-id="7deb6-120">Ему присваивается динамическая сборка, созданная для модуля сценариев, если скрипт определяет классы, или загруженная сборка для двоичных модулей.</span><span class="sxs-lookup"><span data-stu-id="7deb6-120">It is set to the dynamic assembly created for a script module if the script defines classes, or the loaded assembly for binary modules.</span></span> <span data-ttu-id="7deb6-121">Оно не задано, когда ModuleType = Manifest.</span><span class="sxs-lookup"><span data-stu-id="7deb6-121">It is not set when ModuleType = Manifest.</span></span>

<span data-ttu-id="7deb6-122">Отражение поля **ImplementingAssembly** обнаруживает ресурсы в модуле.</span><span class="sxs-lookup"><span data-stu-id="7deb6-122">Reflection on the **ImplementingAssembly** field discovers resources in a module.</span></span> <span data-ttu-id="7deb6-123">Это означает, что можно обнаруживать ресурсы, созданные в PowerShell или в любых других управляемых языках.</span><span class="sxs-lookup"><span data-stu-id="7deb6-123">This means you can discover resources written in either PowerShell or other managed languages.</span></span>

<span data-ttu-id="7deb6-124">Поля с инициализаторами:</span><span class="sxs-lookup"><span data-stu-id="7deb6-124">Fields with initializers:</span></span>

```powershell
[int] $i = 5
```

<span data-ttu-id="7deb6-125">Поддерживается Static, который выступает в качестве атрибута, как и ограничения типов, и поэтому может быть указан в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="7deb6-125">Static is supported; it works like an attribute, as do the type constraints, so it can be specified in any order.</span></span>

```powershell
static [int] $count = 0
```

<span data-ttu-id="7deb6-126">Тип не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="7deb6-126">A type is optional.</span></span>

```powershell
$s = "hello"
```

<span data-ttu-id="7deb6-127">Все члены являются открытыми.</span><span class="sxs-lookup"><span data-stu-id="7deb6-127">All members are public.</span></span>

## <a name="constructors-and-instantiation"></a><span data-ttu-id="7deb6-128">Конструкторы и создание экземпляров</span><span class="sxs-lookup"><span data-stu-id="7deb6-128">Constructors and instantiation</span></span>

<span data-ttu-id="7deb6-129">Классы Windows PowerShell могут иметь конструкторы, имя которых совпадает с именем их класса.</span><span class="sxs-lookup"><span data-stu-id="7deb6-129">Windows PowerShell classes can have constructors; they have the same name as their class.</span></span> <span data-ttu-id="7deb6-130">Конструкторы могут быть перегружены.</span><span class="sxs-lookup"><span data-stu-id="7deb6-130">Constructors can be overloaded.</span></span> <span data-ttu-id="7deb6-131">Поддерживаются статические конструкторы.</span><span class="sxs-lookup"><span data-stu-id="7deb6-131">Static constructors are supported.</span></span> <span data-ttu-id="7deb6-132">Свойства с выражениями инициализации инициализируются перед выполнением любого кода в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="7deb6-132">Properties with initialization expressions are initialized before running any code in a constructor.</span></span> <span data-ttu-id="7deb6-133">Статические свойства инициализируются до основной части статического конструктора, а свойства экземпляра инициализируются до основной части нестатического конструктора.</span><span class="sxs-lookup"><span data-stu-id="7deb6-133">Static properties are initialized before the body of a static constructor, and instance properties are initialized before the body of the non-static constructor.</span></span> <span data-ttu-id="7deb6-134">В настоящее время не существует синтаксис для вызова конструктора из другого конструктора (такой как синтаксис C\# ": this()").</span><span class="sxs-lookup"><span data-stu-id="7deb6-134">Currently, there is no syntax for calling a constructor from another constructor (like the C\# syntax ": this()").</span></span> <span data-ttu-id="7deb6-135">Обходной путь заключается в определении общего метода Init.</span><span class="sxs-lookup"><span data-stu-id="7deb6-135">The workaround is to define a common Init method.</span></span>

<span data-ttu-id="7deb6-136">Ниже приведены способы создания экземпляров классов в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="7deb6-136">The following are ways of instantiating classes in this release.</span></span>

<span data-ttu-id="7deb6-137">Создание экземпляров с помощью конструктора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7deb6-137">Instantiating by using the default constructor.</span></span> <span data-ttu-id="7deb6-138">Обратите внимание, что New-Object не поддерживается в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="7deb6-138">Note that New-Object is not supported in this release.</span></span>

```powershell
$a = [MyClass]::new()
```

<span data-ttu-id="7deb6-139">Вызов конструктора с параметром:</span><span class="sxs-lookup"><span data-stu-id="7deb6-139">Calling a constructor with a parameter</span></span>

```powershell
$b = [MyClass]::new(42)
```

<span data-ttu-id="7deb6-140">Передача массива в конструктор с несколькими параметрами:</span><span class="sxs-lookup"><span data-stu-id="7deb6-140">Passing an array to a constructor with multiple parameters</span></span>
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

<span data-ttu-id="7deb6-141">В этом выпуске New-Object не работает с классами, определенными в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7deb6-141">In this release, New-Object does not work with classes defined in Windows PowerShell.</span></span> <span data-ttu-id="7deb6-142">Кроме того, в нем имя типа отображается только лексически, то есть оно не отображается за пределами модуля или сценария, определяющего класс.</span><span class="sxs-lookup"><span data-stu-id="7deb6-142">Also for this release, the type name is only visible lexically, meaning it is not visible outside of the module or script that defines the class.</span></span> <span data-ttu-id="7deb6-143">Функции могут возвращать экземпляры класса, определенного в Windows PowerShell, и они прекрасно работают за пределами модуля или сценария.</span><span class="sxs-lookup"><span data-stu-id="7deb6-143">Functions can return instances of a class defined in Windows PowerShell, and instances work well outside of the module or script.</span></span>

<span data-ttu-id="7deb6-144">`Get-Member -Static` выводит список конструкторов, чтобы перегрузки можно было просматривать как и любой другой метод.</span><span class="sxs-lookup"><span data-stu-id="7deb6-144">`Get-Member -Static` lists constructors, so you can view overloads like any other method.</span></span> <span data-ttu-id="7deb6-145">Производительность этого синтаксиса значительно выше по сравнению с New-Object.</span><span class="sxs-lookup"><span data-stu-id="7deb6-145">The performance of this syntax is also considerably faster than New-Object.</span></span>

<span data-ttu-id="7deb6-146">Псевдостатический метод с именем **new** работает с типами .NET, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="7deb6-146">The pseudo-static method named **new** works with .NET types, as shown in the following example.</span></span>

```powershell
[hashtable]::new()
```

<span data-ttu-id="7deb6-147">Теперь можно просмотреть перегрузки конструктора с помощью Get-Member или так, как показано в этом примере:</span><span class="sxs-lookup"><span data-stu-id="7deb6-147">You can now see constructor overloads with Get-Member, or as shown in this example:</span></span>

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## <a name="methods"></a><span data-ttu-id="7deb6-148">Методы</span><span class="sxs-lookup"><span data-stu-id="7deb6-148">Methods</span></span>

<span data-ttu-id="7deb6-149">Метод класса Windows PowerShell реализуется как ScriptBlock, имеющий только конечный блок.</span><span class="sxs-lookup"><span data-stu-id="7deb6-149">A Windows PowerShell class method is implemented as a ScriptBlock that has only an end block.</span></span> <span data-ttu-id="7deb6-150">Все методы являются открытыми.</span><span class="sxs-lookup"><span data-stu-id="7deb6-150">All methods are public.</span></span> <span data-ttu-id="7deb6-151">Ниже приведен пример определения метода с именем **DoSomething**.</span><span class="sxs-lookup"><span data-stu-id="7deb6-151">The following shows an example of defining a method named **DoSomething**.</span></span>

```powershell
class MyClass
{
    DoSomething($x)
    {
        $this._doSomething($x) # method syntax
    }
    private _doSomething($a) {}
}
```

<span data-ttu-id="7deb6-152">Вызов метода:</span><span class="sxs-lookup"><span data-stu-id="7deb6-152">Method invocation:</span></span>

```powershell
$b = [MyClass]::new()
$b.DoSomething(42)
```

<span data-ttu-id="7deb6-153">Поддерживаются и перегруженные методы, которые называются так же, как и существующий метод, но отличаются от него заданными значениями.</span><span class="sxs-lookup"><span data-stu-id="7deb6-153">Overloaded methods--that is, those that are named the same as an existing method, but differentiated by their specified values--are also supported.</span></span>

## <a name="properties"></a><span data-ttu-id="7deb6-154">Свойства</span><span class="sxs-lookup"><span data-stu-id="7deb6-154">Properties</span></span>

<span data-ttu-id="7deb6-155">Все свойства являются открытыми.</span><span class="sxs-lookup"><span data-stu-id="7deb6-155">All properties are public.</span></span> <span data-ttu-id="7deb6-156">Для свойств требуется точка с запятой или новая строка.</span><span class="sxs-lookup"><span data-stu-id="7deb6-156">Properties require either a newline or semicolon.</span></span> <span data-ttu-id="7deb6-157">Если тип объекта не указан, тип свойства является объектом.</span><span class="sxs-lookup"><span data-stu-id="7deb6-157">If no object type is specified, the property type is object.</span></span>

<span data-ttu-id="7deb6-158">Свойства, использующие атрибуты проверки или атрибуты преобразования аргументов (например, `[ValidateSet("aaa")]`) работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="7deb6-158">Properties that use validation attributes or argument transformation attributes (e.g. `[ValidateSet("aaa")]`) work as expected.</span></span>

## <a name="hidden"></a><span data-ttu-id="7deb6-159">Hidden</span><span class="sxs-lookup"><span data-stu-id="7deb6-159">Hidden</span></span>

<span data-ttu-id="7deb6-160">Было добавлено новое ключевое слово **Hidden**.</span><span class="sxs-lookup"><span data-stu-id="7deb6-160">A new keyword, **Hidden**, has been added.</span></span> <span data-ttu-id="7deb6-161">**Оно** может применяться к свойствам и методам (включая конструкторы).</span><span class="sxs-lookup"><span data-stu-id="7deb6-161">**Hidden** can be applied to properties and methods (including constructors).</span></span>

<span data-ttu-id="7deb6-162">Члены Hidden являются открытыми, но отображаются в выходных данных Get-Member только при использовании параметра -Force.</span><span class="sxs-lookup"><span data-stu-id="7deb6-162">Hidden members are public, but do not appear in the output of Get-Member unless the -Force parameter is added.</span></span>

<span data-ttu-id="7deb6-163">Элементы Hidden не учитываются при заполнении нажатием клавиши TAB или использовании Intellisense, если только такая операция не выполняется в классе, определяющем элемент Hidden.</span><span class="sxs-lookup"><span data-stu-id="7deb6-163">Hidden members are not included when tab completing or using Intellisense unless the completion occurs in the class defining the hidden member.</span></span>

<span data-ttu-id="7deb6-164">Добавлен новый атрибут **System.Management.Automation.HiddenAttribute**, чтобы код C# мог иметь ту же семантику в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7deb6-164">A new attribute, **System.Management.Automation.HiddenAttribute** has been added so that C# code can have the same semantics within Windows PowerShell.</span></span>

## <a name="return-types"></a><span data-ttu-id="7deb6-165">Типы возвращаемых значений</span><span class="sxs-lookup"><span data-stu-id="7deb6-165">Return types</span></span>

<span data-ttu-id="7deb6-166">Тип возвращаемого значения является контрактом; возвращаемое значение преобразуется к ожидаемому типу.</span><span class="sxs-lookup"><span data-stu-id="7deb6-166">Return type is a contract; the return value is converted to the expected type.</span></span> <span data-ttu-id="7deb6-167">Если тип возвращаемого значения не указан, ему присваивается значение void.</span><span class="sxs-lookup"><span data-stu-id="7deb6-167">If no return type is specified, the return type is void.</span></span> <span data-ttu-id="7deb6-168">Потоковая передача объектов отсутствует; записать объекты в конвейер специально или случайно невозможно.</span><span class="sxs-lookup"><span data-stu-id="7deb6-168">There is no streaming of objects; objects cannot be written to the pipeline either intentionally or by accident.</span></span>

## <a name="attributes"></a><span data-ttu-id="7deb6-169">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="7deb6-169">Attributes</span></span>

<span data-ttu-id="7deb6-170">Добавлены два новых атрибута — **DscResource** и **DscProperty**.</span><span class="sxs-lookup"><span data-stu-id="7deb6-170">Two new attributes, **DscResource** and **DscProperty** have been added.</span></span>

## <a name="lexical-scoping-of-variables"></a><span data-ttu-id="7deb6-171">Лексическая область переменных</span><span class="sxs-lookup"><span data-stu-id="7deb6-171">Lexical scoping of variables</span></span>

<span data-ttu-id="7deb6-172">Ниже приведен пример того, как работает лексическая область в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="7deb6-172">The following shows an example of how lexical scoping works in this release.</span></span>

```powershell
$d = 42 # Script scope

function bar
{
    $d = 0 # Function scope
    [MyClass]::DoSomething()
}

class MyClass
{
    static [object] DoSomething()
    {
        return $d # error, not found dynamically
        return $script:d # no error
        $d = $script:d
        return $d # no error, found lexically
    }
}

$v = bar
$v -eq $d # true
```

## <a name="end-to-end-example"></a><span data-ttu-id="7deb6-173">Комплексный пример</span><span class="sxs-lookup"><span data-stu-id="7deb6-173">End-to-End Example</span></span>

<span data-ttu-id="7deb6-174">Следующий пример создает несколько новых пользовательских классов для реализации языка динамических таблиц стилей (DSL) HTML.</span><span class="sxs-lookup"><span data-stu-id="7deb6-174">The following example creates several new, custom classes to implement an HTML dynamic style sheet language (DSL).</span></span>
<span data-ttu-id="7deb6-175">Затем пример добавляет вспомогательные функции для создания определенных типов элементов в рамках класса элементов, таких как стили заголовков и таблицы, так как типы нельзя использовать за пределами области действия модуля.</span><span class="sxs-lookup"><span data-stu-id="7deb6-175">Then, the example adds helper functions to create specific element types as part of the element class, such as heading styles and tables, because types cannot be used outside the scope of a module.</span></span>

```powershell
# Classes that define the structure of the document
#
class Html
{
    [string] $docType
    [HtmlHead] $Head
    [Element[]] $Body

    [string] Render()
    {
        $text = "<html>`n<head>`n"
        $text += $this.Head
        $text += "`n</head>`n<body>`n"
        $text += $this.Body -join "`n" # Render all of the body elements
        $text += "</body>`n</html>"
        return $text
    }
    [string] ToString() { return $this.Render() }
}

class HtmlHead
{
    $Title
    $Base
    $Link
    $Style
    $Meta
    $Script
    [string] Render() { return "<title>$($this.Title)</title>" }
    [string] ToString() { return $this.Render() }
}

class Element
{
    [string] $Tag
    [string] $Text
    [hashtable] $Attributes
    [string] Render() {
        $attributesText= ""
        if ($this.Attributes)
        {
            foreach ($attr in $this.Attributes.Keys)
            {
                #BUGBUG - need to validate keys against attribute
                $attributesText += " $attr=`"$($this.Attributes[$attr])\`""
            }
        }
        return "<$($this.tag)${attributesText}>$($this.text)</$($this.tag)>`n"
    }
[string] ToString() { return $this.Render() }
}

#
# Helper functions for creating specific element types on top of the classes.
# These are required because types aren’t visible outside of the module.
#

function H1 { [Element] @{ Tag = "H1" ; Text = $args.foreach{$_} -join " " }}
function H2 { [Element] @{ Tag = "H2" ; Text = $args.foreach{$_} -join " " }}
function H3 { [Element] @{ Tag = "H3" ; Text = $args.foreach{$_} -join " " }}
function P { [Element] @{ Tag = "P" ; Text = $args.foreach{$_} -join " " }}
function B { [Element] @{ Tag = "B" ; Text = $args.foreach{$_} -join " " }}
function I { [Element] @{ Tag = "I" ; Text = $args.foreach{$_} -join " " }}
function HREF
{
    param (
        $Name,
        $Link
    )
    return [Element] @{
        Tag = "A"
        Attributes = @{ HREF = $link }
        Text = $name
    }
}
function Table
{
    param (
    [Parameter(Mandatory)]
    [object[]]
        $Data,
    [Parameter()]
    [string[]]
        $Properties = "*",
    [Parameter()]
    [hashtable]
        $Attributes = @{ border=2; cellpadding=2; cellspacing=2 }
    )
$bodyText = ""
# Add the header tags
$bodyText += $Properties.foreach{TH $_}
# Add the rows
$bodyText += foreach ($row in $Data)
    {
        TR (-join $Properties.Foreach{ TD ($row.$\_) } )
    }

    $table = [Element] @{
        Tag = "Table"
        Attributes = $Attributes
        Text = $bodyText
    }
$table
}
function TH { ([Element] @{ Tag = "TH" ; Text = $args.foreach{$_} -join " " }) }
function TR { ([Element] @{ Tag = "TR" ; Text = $args.foreach{$_} -join " " }) }
function TD { ([Element] @{ Tag = "TD" ; Text = $args.foreach{$_} -join " " }) }
function Style

{
    return [Element] @{
        Tag = "style"
        Text = "$args"
    }
}

# Takes a hash table, casts it to and HTML document
# and then returns the resulting type.
#
function Html ([HTML] $doc) { return $doc }
```