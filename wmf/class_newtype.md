# Новые возможности языка в PowerShell 5.0 

В PowerShell 5.0 появились следующие новые элементы языка для Windows PowerShell:

## Ключевое слово Class

Ключевое слово **class** определяет новый класс. Это подлинный тип .NET Framework. 
Члены класса являются открытыми, но только в рамках области модуля.
Вы не можете ссылаться на имя типа в виде строки (например, `New-Object` не работает), а также использовать литерал типа (например, `[MyClass]`) за пределами файла сценария или модуля, где определен этот класс.

```powershell
class MyClass
{
    ...
}
```

## Ключевое слово Enum и перечисления

Добавлена поддержка ключевого слова **enum**, где символ новой строки используется в качестве разделителя.
Текущие ограничения: перечислитель нельзя определить относительно самого себя, но можно инициализировать перечисление относительно другого перечисления, как показано в приведенном ниже примере.
Кроме того, в настоящее время нельзя задать базовый тип (всегда [int]).

```powershell
enum Color2
{
    Yellow = [Color]::Blue
}
```

Значение перечислителя должно быть константой времени анализа. Для него нельзя задать результат вызванной команды.

```powershell
enum MyEnum
{
    Enum1
    Enum2
    Enum3 = 42
    Enum4 = [int]::MaxValue
}
```

Перечисления поддерживают арифметические операции, как показано в следующем примере:

```powershell
enum SomeEnum { Max = 42 }
enum OtherEnum { Max = [SomeEnum]::Max + 1 }
```

## Import-DscResource

**Import-DscResource** теперь является подлинным динамическим ключевым словом.
PowerShell анализирует корневой модуль указанного модуля, выполняя поиск классов, которые содержат атрибут **DscResource**.

## ImplementingAssembly

В ModuleInfo добавлено новое поле **ImplementingAssembly**. Ему присваивается динамическая сборка, созданная для модуля сценариев, если скрипт определяет классы, или загруженная сборка для двоичных модулей. Оно не задано, когда ModuleType = Manifest. 

Отражение поля **ImplementingAssembly** обнаруживает ресурсы в модуле. Это означает, что можно обнаруживать ресурсы, созданные в PowerShell или в любых других управляемых языках.

Поля с инициализаторами:      

```powershell
[int] $i = 5
```

Поддерживается Static, который выступает в качестве атрибута, как и ограничения типов, и поэтому может быть указан в любом порядке.

```powershell
static [int] $count = 0
```

Тип не является обязательным.

```powershell
$s = "hello"
```

Все члены являются открытыми. 

## Конструкторы и создание экземпляров

Классы Windows PowerShell могут иметь конструкторы, имя которых совпадает с именем их класса. Конструкторы могут быть перегружены. Поддерживаются статические конструкторы. Свойства с выражениями инициализации инициализируются перед выполнением любого кода в конструкторе. Статические свойства инициализируются до основной части статического конструктора, а свойства экземпляра инициализируются до основной части нестатического конструктора. В настоящее время не существует синтаксис для вызова конструктора из другого конструктора (такой как синтаксис C\# ": this()"). Обходной путь заключается в определении общего метода Init. 

Ниже приведены способы создания экземпляров классов в этом выпуске.

Создание экземпляров с помощью конструктора по умолчанию. Обратите внимание, что New-Object не поддерживается в этом выпуске.

```powershell
$a = [MyClass]::new()
```

Вызов конструктора с параметром:

```powershell
$b = [MyClass]::new(42)
```

Передача массива в конструктор с несколькими параметрами:
```powershell
$c = [MyClass]::new(@(42,43,44), "Hello")
```

В этом выпуске New-Object не работает с классами, определенными в Windows PowerShell. Кроме того, в нем имя типа отображается только лексически, то есть оно не отображается за пределами модуля или сценария, определяющего класс. Функции могут возвращать экземпляры класса, определенного в Windows PowerShell, и они прекрасно работают за пределами модуля или сценария.

`Get-Member -Static` выводит список конструкторов, чтобы перегрузки можно было просматривать как и любой другой метод. Производительность этого синтаксиса значительно выше по сравнению с New-Object.

Псевдостатический метод с именем **new** работает с типами .NET, как показано в следующем примере:

```powershell
[hashtable]::new()
```

Теперь можно просмотреть перегрузки конструктора с помощью Get-Member или так, как показано в этом примере:

```powershell
PS> [hashtable]::new
OverloadDefinitions
-------------------
hashtable new()
hashtable new(int capacity)
hashtable new(int capacity, float loadFactor)
```

## Методы

Метод класса Windows PowerShell реализуется как ScriptBlock, имеющий только конечный блок. Все методы являются открытыми. Ниже приведен пример определения метода с именем **DoSomething**.

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

Вызов метода:

```powershell
$b = [MyClass]::new()
$b.DoSomething(42) 
```

Поддерживаются и перегруженные методы, которые называются так же, как и существующий метод, но отличаются от него заданными значениями.

## Свойства 

Все свойства являются открытыми. Для свойств требуется точка с запятой или новая строка. Если тип объекта не указан, тип свойства является объектом.

Свойства, использующие атрибуты проверки или атрибуты преобразования аргументов (например, `[ValidateSet("aaa")]`) работают должным образом.

## Hidden

Было добавлено новое ключевое слово **Hidden**. Оно **** может применяться к свойствам и методам (включая конструкторы).

Члены Hidden являются открытыми, но отображаются в выходных данных Get-Member только при использовании параметра -Force.

Элементы Hidden не учитываются при заполнении нажатием клавиши TAB или использовании Intellisense, если только такая операция не выполняется в классе, определяющем элемент Hidden.

Добавлен новый атрибут **System.Management.Automation.HiddenAttribute**, чтобы код C# мог иметь ту же семантику в Windows PowerShell.

## Типы возвращаемых значений

Тип возвращаемого значения является контрактом; возвращаемое значение преобразуется к ожидаемому типу. Если тип возвращаемого значения не указан, ему присваивается значение void. Потоковая передача объектов отсутствует; записать объекты в конвейер специально или случайно невозможно.

## Атрибуты

Добавлены четыре новых атрибута **DscResource**, **DscResourceKey**, **DscResourceMandatory** и **DscResourceOut**.

## Лексическая область переменных

Ниже приведен пример того, как работает лексическая область в этом выпуске.

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

## Комплексный пример

Следующий пример создает несколько новых пользовательских классов для реализации языка динамических таблиц стилей (DSL) HTML. 
Затем пример добавляет вспомогательные функции для создания определенных типов элементов в рамках класса элементов, таких как стили заголовков и таблицы, так как типы нельзя использовать за пределами области действия модуля.

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
```<!--HONumber=Mar16_HO2-->
