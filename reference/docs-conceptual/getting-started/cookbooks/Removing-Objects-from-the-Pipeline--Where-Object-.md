---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Удаление объектов из конвейера (Where-Object)"
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 4140c4c3ebb26223d03ca139992fedf6e184a38b
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="c63cd-103">Удаление объектов из конвейера (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="c63cd-103">Removing Objects from the Pipeline (Where-Object)</span></span>
<span data-ttu-id="c63cd-104">В Windows PowerShell часто создается и передается в конвейер большее количество объектов, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="c63cd-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="c63cd-105">Чтобы указать свойства конкретного объекта, которые требуется отобразить, можно воспользоваться командлетом **Format**, но это не позволяет решить проблему удаления с экрана всех объектов.</span><span class="sxs-lookup"><span data-stu-id="c63cd-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="c63cd-106">Может потребоваться отфильтровать объекты до достижения конца конвейера, чтобы выполнить те или иные действия только с подмножеством объектов, созданных изначально.</span><span class="sxs-lookup"><span data-stu-id="c63cd-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="c63cd-107">В Windows PowerShell есть командлет **Where-Object**, позволяющий проверить каждый объект в конвейере и передать его дальше, только если он удовлетворяет условию теста.</span><span class="sxs-lookup"><span data-stu-id="c63cd-107">Windows PowerShell includes a **Where-Object** cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="c63cd-108">Объекты, не прошедшие проверку, удаляются из конвейера.</span><span class="sxs-lookup"><span data-stu-id="c63cd-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="c63cd-109">Условие теста передается в виде значения параметра **Where-ObjectFilterScript**.</span><span class="sxs-lookup"><span data-stu-id="c63cd-109">You supply the test condition as the value of the **Where-ObjectFilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="c63cd-110">Выполнение простых проверок с использованием командлета Where-Object</span><span class="sxs-lookup"><span data-stu-id="c63cd-110">Performing Simple Tests with Where-Object</span></span>
<span data-ttu-id="c63cd-111">Значение **FilterScript** представляет собой *блок сценария* — одну или несколько команд Windows PowerShell, заключенных в фигурные скобки {}, — результатом которого могут быть значения True или False.</span><span class="sxs-lookup"><span data-stu-id="c63cd-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="c63cd-112">Такие блоки сценариев могут быть очень простыми, но для их создания требуется понимание другой концепции Windows PowerShell, а именно операторов сравнения.</span><span class="sxs-lookup"><span data-stu-id="c63cd-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="c63cd-113">Оператор сравнения сравнивает элементы, расположенные с обеих сторон оператора.</span><span class="sxs-lookup"><span data-stu-id="c63cd-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="c63cd-114">Запись операторов сравнения начинается знаком "-", после которого следует имя оператора.</span><span class="sxs-lookup"><span data-stu-id="c63cd-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="c63cd-115">Основные операторы сравнения работают, как правило, с любыми видами объектов.</span><span class="sxs-lookup"><span data-stu-id="c63cd-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="c63cd-116">Более сложные операторы сравнения работают только с текстом или массивами.</span><span class="sxs-lookup"><span data-stu-id="c63cd-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="c63cd-117">По умолчанию при работе с текстом в Windows PowerShell операторы сравнения нечувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="c63cd-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="c63cd-118">Исходя из соображений синтаксического анализа, такие знаки, как "<", ">" и "=", не используются в качестве операторов сравнения.</span><span data-stu-id="c63cd-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="c63cd-119">Вместо этого операторы сравнения записываются в буквенной форме. <span data-ttu-id="c63cd-120">Основные операторы сравнения перечислены в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="c63cd-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="c63cd-121">Оператор сравнения</span><span class="sxs-lookup"><span data-stu-id="c63cd-121">Comparison Operator</span></span>|<span data-ttu-id="c63cd-122">Значение</span><span class="sxs-lookup"><span data-stu-id="c63cd-122">Meaning</span></span>|<span data-ttu-id="c63cd-123">Пример (возвращает значение True)</span><span class="sxs-lookup"><span data-stu-id="c63cd-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="c63cd-124">-eq</span><span class="sxs-lookup"><span data-stu-id="c63cd-124">-eq</span></span>|<span data-ttu-id="c63cd-125">равно</span><span class="sxs-lookup"><span data-stu-id="c63cd-125">is equal to</span></span>|<span data-ttu-id="c63cd-126">1 -eq 1</span><span class="sxs-lookup"><span data-stu-id="c63cd-126">1 -eq 1</span></span>|
|<span data-ttu-id="c63cd-127">-ne</span><span class="sxs-lookup"><span data-stu-id="c63cd-127">-ne</span></span>|<span data-ttu-id="c63cd-128">не равно</span><span class="sxs-lookup"><span data-stu-id="c63cd-128">Is not equal to</span></span>|<span data-ttu-id="c63cd-129">1 -ne 2</span><span class="sxs-lookup"><span data-stu-id="c63cd-129">1 -ne 2</span></span>|
|<span data-ttu-id="c63cd-130">-lt</span><span class="sxs-lookup"><span data-stu-id="c63cd-130">-lt</span></span>|<span data-ttu-id="c63cd-131">меньше</span><span class="sxs-lookup"><span data-stu-id="c63cd-131">Is less than</span></span>|<span data-ttu-id="c63cd-132">1 -lt 2</span><span class="sxs-lookup"><span data-stu-id="c63cd-132">1 -lt 2</span></span>|
|<span data-ttu-id="c63cd-133">-le</span><span class="sxs-lookup"><span data-stu-id="c63cd-133">-le</span></span>|<span data-ttu-id="c63cd-134">меньше или равно</span><span class="sxs-lookup"><span data-stu-id="c63cd-134">Is less than or equal to</span></span>|<span data-ttu-id="c63cd-135">1 -le 2</span><span class="sxs-lookup"><span data-stu-id="c63cd-135">1 -le 2</span></span>|
|<span data-ttu-id="c63cd-136">-gt</span><span class="sxs-lookup"><span data-stu-id="c63cd-136">-gt</span></span>|<span data-ttu-id="c63cd-137">больше</span><span class="sxs-lookup"><span data-stu-id="c63cd-137">Is greater than</span></span>|<span data-ttu-id="c63cd-138">2 -gt 1</span><span class="sxs-lookup"><span data-stu-id="c63cd-138">2 -gt 1</span></span>|
|<span data-ttu-id="c63cd-139">-ge</span><span class="sxs-lookup"><span data-stu-id="c63cd-139">-ge</span></span>|<span data-ttu-id="c63cd-140">больше или равно</span><span class="sxs-lookup"><span data-stu-id="c63cd-140">Is greater than or equal to</span></span>|<span data-ttu-id="c63cd-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="c63cd-141">2 -ge 1</span></span>|
|<span data-ttu-id="c63cd-142">-like</span><span class="sxs-lookup"><span data-stu-id="c63cd-142">-like</span></span>|<span data-ttu-id="c63cd-143">сравнение на совпадение с учетом подстановочного знака в тексте</span><span class="sxs-lookup"><span data-stu-id="c63cd-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="c63cd-144">"file.doc" -like "f\*.do?"</span><span class="sxs-lookup"><span data-stu-id="c63cd-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="c63cd-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="c63cd-145">-notlike</span></span>|<span data-ttu-id="c63cd-146">сравнение на несовпадение с учетом подстановочного знака в тексте</span><span class="sxs-lookup"><span data-stu-id="c63cd-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="c63cd-147">"file.doc" -notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="c63cd-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="c63cd-148">-contains</span><span class="sxs-lookup"><span data-stu-id="c63cd-148">-contains</span></span>|<span data-ttu-id="c63cd-149">Содержит</span><span class="sxs-lookup"><span data-stu-id="c63cd-149">Contains</span></span>|<span data-ttu-id="c63cd-150">1,2,3 -contains 1</span><span class="sxs-lookup"><span data-stu-id="c63cd-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="c63cd-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="c63cd-151">-notcontains</span></span>|<span data-ttu-id="c63cd-152">не содержит</span><span class="sxs-lookup"><span data-stu-id="c63cd-152">Does not contain</span></span>|<span data-ttu-id="c63cd-153">1,2,3 -notcontains 4</span><span class="sxs-lookup"><span data-stu-id="c63cd-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="c63cd-154">В блоках сценариев командлета Where-Object для обращения к текущему объекту конвейера используется специальная переменная $_.</span><span class="sxs-lookup"><span data-stu-id="c63cd-154">Where-Object script blocks use the special variable '$_' to refer to the current object in the pipeline.</span></span> <span data-ttu-id="c63cd-155">Ниже приведен пример использования этой переменной.</span><span class="sxs-lookup"><span data-stu-id="c63cd-155">Here is an example of how it works.</span></span> <span data-ttu-id="c63cd-156">Если в списке содержатся числа и требуется вернуть только те, которые меньше 3, в командлете Where-Object можно настроить фильтр чисел.</span><span class="sxs-lookup"><span data-stu-id="c63cd-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="c63cd-157">Фильтрация, основанная на свойствах объектов</span><span class="sxs-lookup"><span data-stu-id="c63cd-157">Filtering Based on Object Properties</span></span>
<span data-ttu-id="c63cd-158">Так как переменная $_ ссылается на текущий объект конвейера, для выполнения проверок можно обратиться к ее свойствам.</span><span class="sxs-lookup"><span data-stu-id="c63cd-158">Since $_ refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="c63cd-159">Например, в инструментарии WMI можно просмотреть класс Win32_SystemDriver.</span><span class="sxs-lookup"><span data-stu-id="c63cd-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="c63cd-160">В какой-то конкретной системе могут содержаться сотни системных драйверов, но для проверки необходим определенный набор системных драйверов — таких, которые запущены в данный момент.</span><span class="sxs-lookup"><span data-stu-id="c63cd-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="c63cd-161">Если для просмотра объектов класса Win32_SystemDriver использовать командлет Get-Member (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**), можно увидеть, что соответствующее свойство State принимает значение Running, когда драйвер запущен.</span><span class="sxs-lookup"><span data-stu-id="c63cd-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="c63cd-162">Таким образом, фильтровать системные драйверы и выбирать только запущенные можно с помощью строки:</span><span class="sxs-lookup"><span data-stu-id="c63cd-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"}
```

<span data-ttu-id="c63cd-163">В результате будет получен длинный список.</span><span class="sxs-lookup"><span data-stu-id="c63cd-163">This still produces a long list.</span></span> <span data-ttu-id="c63cd-164">Отфильтровать эти драйверы и выбирать только такие, запуск которых выполняется автоматически, можно проверкой значения StartMode:</span><span class="sxs-lookup"><span data-stu-id="c63cd-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

<span data-ttu-id="c63cd-165">Результат выполнения этой команды содержит много ненужных сведений, поскольку драйверы, запущенные в данный момент, уже известны.</span><span class="sxs-lookup"><span data-stu-id="c63cd-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="c63cd-166">В действительности, из всех сведений на данном этапе требуется только имя и отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="c63cd-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="c63cd-167">Следующая команда включает только эти два свойства, что дает более простые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c63cd-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

<span data-ttu-id="c63cd-168">Приведенная выше команда содержит два элемента Where-Object, но их можно объединить, используя знак "-" и логический оператор.</span><span class="sxs-lookup"><span data-stu-id="c63cd-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq "Running") -and ($_.StartMode -eq "Manual") } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="c63cd-169">Стандартные логические операторы перечислены в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="c63cd-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="c63cd-170">Логический оператор</span><span class="sxs-lookup"><span data-stu-id="c63cd-170">Logical Operator</span></span>|<span data-ttu-id="c63cd-171">Значение</span><span class="sxs-lookup"><span data-stu-id="c63cd-171">Meaning</span></span>|<span data-ttu-id="c63cd-172">Пример (возвращает значение True)</span><span class="sxs-lookup"><span data-stu-id="c63cd-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="c63cd-173">-and</span><span class="sxs-lookup"><span data-stu-id="c63cd-173">-and</span></span>|<span data-ttu-id="c63cd-174">Логическое И; возвращает значение True, если оба операнда принимают значение True</span><span class="sxs-lookup"><span data-stu-id="c63cd-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="c63cd-175">(1 -eq 1) -and (2 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="c63cd-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="c63cd-176">-or</span><span class="sxs-lookup"><span data-stu-id="c63cd-176">-or</span></span>|<span data-ttu-id="c63cd-177">Логическое ИЛИ; возвращает значение True, если один из операндов принимает значение True</span><span class="sxs-lookup"><span data-stu-id="c63cd-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="c63cd-178">(1 -eq 1) -or (1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="c63cd-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="c63cd-179">-not</span><span class="sxs-lookup"><span data-stu-id="c63cd-179">-not</span></span>|<span data-ttu-id="c63cd-180">Логическое НЕ; изменяет значение (True или False) на противоположное</span><span class="sxs-lookup"><span data-stu-id="c63cd-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="c63cd-181">-not (1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="c63cd-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="c63cd-182">Логическое НЕ; изменяет значение (True или False) на противоположное</span><span class="sxs-lookup"><span data-stu-id="c63cd-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="c63cd-183">\! (1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="c63cd-183">\!(1 -eq 2)</span></span>|

