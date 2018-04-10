---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Использование команд Format для изменения представления вывода
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-format-commands-to-change-output-view"></a><span data-ttu-id="0fc39-103">Использование команд Format для изменения представления вывода</span><span class="sxs-lookup"><span data-stu-id="0fc39-103">Using Format Commands to Change Output View</span></span>

<span data-ttu-id="0fc39-104">Windows PowerShell содержит набор командлетов, позволяющих пользователю контролировать, какие свойства должны отображаться для определенных объектов.</span><span class="sxs-lookup"><span data-stu-id="0fc39-104">Windows PowerShell has a set of cmdlets that allow you to control which properties are displayed for particular objects.</span></span> <span data-ttu-id="0fc39-105">Имена всех этих командлетов начинаются глаголом **Format**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-105">The names of all the cmdlets begin with the verb **Format**.</span></span> <span data-ttu-id="0fc39-106">Они позволяют выбрать для отображения одно или несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="0fc39-106">They let you select one or more properties to show.</span></span>

<span data-ttu-id="0fc39-107">С глагола **Format** начинаются командлеты **Format-Wide**, **Format-List**, **Format-Table** и **Format-Custom**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-107">The **Format** cmdlets are **Format-Wide**, **Format-List**, **Format-Table**, and **Format-Custom**.</span></span> <span data-ttu-id="0fc39-108">В этом руководстве пользователя рассматриваются только командлеты **Format-Wide**, **Format-List** и **Format-Table**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-108">We will only describe the **Format-Wide**, **Format-List**, and **Format-Table** cmdlets in this user's guide.</span></span>

<span data-ttu-id="0fc39-109">Каждый командлет форматирования имеет свойства по умолчанию, которые используются, если не задается отображение каких-либо определенных свойств.</span><span class="sxs-lookup"><span data-stu-id="0fc39-109">Each format cmdlet has default properties that will be used if you do not specify specific properties to display.</span></span> <span data-ttu-id="0fc39-110">Для указания свойств, которые нужно отобразить, каждый командлет использует одно и то же имя параметра **Property**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-110">Each cmdlet also uses the same parameter name, **Property**, to specify which properties you want to display.</span></span> <span data-ttu-id="0fc39-111">Так как командлет **Format-Wide** отображает только одно свойство, для его параметра **Property** задается только одно значение, но в качестве значений параметров свойств у командлетов **Format-List** и **Format-Table** задается список имен свойств.</span><span class="sxs-lookup"><span data-stu-id="0fc39-111">Because **Format-Wide** only shows a single property, its **Property** parameter only takes a single value, but the property parameters of **Format-List** and **Format-Table** will accept a list of property names.</span></span>

<span data-ttu-id="0fc39-112">Если команда **Get-Process -Name powershell** используется во время работы двух экземпляров Windows PowerShell, формируются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0fc39-112">If you use the command **Get-Process -Name powershell** with two instances of Windows PowerShell running, you get output that looks like this:</span></span>

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

<span data-ttu-id="0fc39-113">Оставшаяся часть этого раздела посвящена ознакомлению с тем, как использовать командлеты **Format** для изменения способа отображения выходных данных команды.</span><span class="sxs-lookup"><span data-stu-id="0fc39-113">In the rest of this section, we will explore how to use **Format** cmdlets to change the way the output of this command is displayed.</span></span>

### <a name="using-format-wide-for-single-item-output"></a><span data-ttu-id="0fc39-114">Применение командлета Format-Wide для вывода с одним элементом</span><span class="sxs-lookup"><span data-stu-id="0fc39-114">Using Format-Wide for Single-Item Output</span></span>

<span data-ttu-id="0fc39-115">По умолчанию командлет **Format-Wide** отображает только свойство по умолчанию для объекта.</span><span class="sxs-lookup"><span data-stu-id="0fc39-115">The **Format-Wide** cmdlet, by default, displays only the default property of an object.</span></span> <span data-ttu-id="0fc39-116">Данные, связанные с каждым объектом, отображаются в одном столбце:</span><span class="sxs-lookup"><span data-stu-id="0fc39-116">The information associated with each object is displayed in a single column:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

<span data-ttu-id="0fc39-117">Можно также задать свойство, отличное от используемого по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="0fc39-117">You can also specify a non-default property:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a><span data-ttu-id="0fc39-118">Настройка отображения командлета Format-Wide с помощью параметра Column</span><span class="sxs-lookup"><span data-stu-id="0fc39-118">Controlling Format-Wide Display with Column</span></span>

<span data-ttu-id="0fc39-119">С помощью командлета **Format-Wide** одновременно можно отобразить только одно свойство.</span><span class="sxs-lookup"><span data-stu-id="0fc39-119">With the **Format-Wide** cmdlet, you can only display a single property at a time.</span></span> <span data-ttu-id="0fc39-120">Это может быть полезным при отображении простых списков, у которых в каждой строке отображается только один элемент.</span><span class="sxs-lookup"><span data-stu-id="0fc39-120">This makes it useful for displaying simple lists that show only one element per line.</span></span> <span data-ttu-id="0fc39-121">Для получения простого списка нужно установить для параметра **Column** значение 1, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="0fc39-121">To get a simple listing, set the value of the **Column** parameter to 1 by typing:</span></span>

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a><span data-ttu-id="0fc39-122">Использование командлета Format-List для представления в виде списка</span><span class="sxs-lookup"><span data-stu-id="0fc39-122">Using Format-List for a List View</span></span>

<span data-ttu-id="0fc39-123">Командлет **Format-List** показывает объект в виде списка, в котором каждое свойство имеет метку и отображается в отдельной строке:</span><span class="sxs-lookup"><span data-stu-id="0fc39-123">The **Format-List** cmdlet displays an object in the form of a listing, with each property labeled and displayed on a separate line:</span></span>

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

<span data-ttu-id="0fc39-124">Можно указать произвольное число свойств:</span><span class="sxs-lookup"><span data-stu-id="0fc39-124">You can specify as many properties as you want:</span></span>

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a><span data-ttu-id="0fc39-125">Получение подробных сведений с помощью подстановочных знаков в командлете Format-List</span><span class="sxs-lookup"><span data-stu-id="0fc39-125">Getting Detailed Information by Using Format-List with Wildcards</span></span>

<span data-ttu-id="0fc39-126">Командлет **Format-List** позволяет использовать подстановочные знаки в качестве значения параметра **Property**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-126">The **Format-List** cmdlet lets you use a wildcard as the value of its **Property** parameter.</span></span> <span data-ttu-id="0fc39-127">Это дает возможность отображать подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="0fc39-127">This lets you display detailed information.</span></span> <span data-ttu-id="0fc39-128">Часто объекты содержат больше информации, чем необходимо. Поэтому Windows PowerShell по умолчанию выводит значения не всех свойств.</span><span class="sxs-lookup"><span data-stu-id="0fc39-128">Often, objects include more information than you need, which is why Windows PowerShell does not show all property values by default.</span></span> <span data-ttu-id="0fc39-129">Чтобы вывести список всех свойств объекта, используйте команду **Format-List -Property \&#42;**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-129">To show all of properties of an object, use the **Format-List -Property \&#42;** command.</span></span> <span data-ttu-id="0fc39-130">Следующая команда формирует более 60 строк выходных данных для одного процесса:</span><span class="sxs-lookup"><span data-stu-id="0fc39-130">The following command generates over 60 lines of output for a single process:</span></span>

```powershell
Get-Process -Name powershell | Format-List -Property *
```

<span data-ttu-id="0fc39-131">Хотя команда **Format-List** и полезна для вывода подробных сведений, для получения сведений, содержащих много элементов, обычно удобнее использовать упрощенное табличное представление.</span><span class="sxs-lookup"><span data-stu-id="0fc39-131">Although the **Format-List** command is useful for showing detail, if you want an overview of output that includes many items, a simpler tabular view is often more useful.</span></span>

### <a name="using-format-table-for-tabular-output"></a><span data-ttu-id="0fc39-132">Применение командлета Format-Table для табличного вывода</span><span class="sxs-lookup"><span data-stu-id="0fc39-132">Using Format-Table for Tabular Output</span></span>

<span data-ttu-id="0fc39-133">Если использовать командлет **Format-Table** без указания имен свойств для форматирования вывода команды **Get-Process**, будут получены точно такие же выходные данные, что и без использования форматирования.</span><span class="sxs-lookup"><span data-stu-id="0fc39-133">If you use the **Format-Table** cmdlet with no property names specified to format the output of the **Get-Process** command, you get exactly the same output as you do without performing any formatting.</span></span> <span data-ttu-id="0fc39-134">Это вызвано тем, что процессы обычно показываются в виде таблицы, как и большинство объектов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fc39-134">The reason is that processes are usually displayed in a tabular format, as are most Windows PowerShell objects.</span></span>

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a><span data-ttu-id="0fc39-135">Улучшение вывода командлета Format-Table (параметр AutoSize)</span><span class="sxs-lookup"><span data-stu-id="0fc39-135">Improving Format-Table Output (AutoSize)</span></span>

<span data-ttu-id="0fc39-136">Хотя табличное представление и полезно при выводе большого количества сведений для сравнения, интерпретация данных может вызвать затруднения, если экран слишком узок и не вмещает все данные.</span><span class="sxs-lookup"><span data-stu-id="0fc39-136">Although a tabular view is useful for displaying a lot of comparable information, it may be difficult to interpret if the display is too narrow for the data.</span></span> <span data-ttu-id="0fc39-137">Например, если отобразить путь процесса, идентификатор, имя и организацию, данные в столбцах пути процесса и организации окажутся обрезанными:</span><span class="sxs-lookup"><span data-stu-id="0fc39-137">For example, if you try to display process path, ID, name, and company, you get truncated output for the process path and the company column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

<span data-ttu-id="0fc39-138">Если указать параметр **AutoSize** при выполнении команды **Format-Table**, Windows PowerShell вычислит ширину столбцов по ширине реально отображаемых данных.</span><span class="sxs-lookup"><span data-stu-id="0fc39-138">If you specify the **AutoSize** parameter when you run the **Format-Table** command, Windows PowerShell will calculate column widths based on the actual data you are going to display.</span></span> <span data-ttu-id="0fc39-139">Это улучшит внешний вид столбца **Path**, но значение столбца с названием организации останется обрезанным:</span><span class="sxs-lookup"><span data-stu-id="0fc39-139">This makes the **Path** column readable, but the company column remains truncated:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

<span data-ttu-id="0fc39-140">Командлет **Format-Table** может обрезать данные, но это происходит только на правой границе экрана.</span><span class="sxs-lookup"><span data-stu-id="0fc39-140">The **Format-Table** cmdlet might still truncate data, but it will only do so at the end of the screen.</span></span> <span data-ttu-id="0fc39-141">Свойствам, за исключением последнего отображаемого, выделяется столько места, сколько нужно для корректного вывода самого длинного элемента данных.</span><span class="sxs-lookup"><span data-stu-id="0fc39-141">Properties, other than the last one displayed, are given as much size as they need for their longest data element to display correctly.</span></span> <span data-ttu-id="0fc39-142">Если поменять местами элементы **Path** и **Company** в списке значений **Property**, название организации отображается полностью, но путь обрезан:</span><span class="sxs-lookup"><span data-stu-id="0fc39-142">You can see that company name is visible but path is truncated if you swap the locations of **Path** and **Company** in the **Property** value list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

<span data-ttu-id="0fc39-143">Команда **Format-Table** предполагает, что чем ближе свойство к началу списка свойств, тем оно важнее.</span><span class="sxs-lookup"><span data-stu-id="0fc39-143">The **Format-Table** command assumes that the nearer a property is to the beginning of the property list, the more important it is.</span></span> <span data-ttu-id="0fc39-144">В связи с этим предпринимается попытка отобразить полностью свойства, находящиеся ближе всего к началу.</span><span class="sxs-lookup"><span data-stu-id="0fc39-144">So it attempts to display the properties nearest the beginning completely.</span></span> <span data-ttu-id="0fc39-145">Если команда **Format-Table** не может отобразить все свойства, она удаляет некоторые столбцы из выходных данных и выдает предупреждение.</span><span class="sxs-lookup"><span data-stu-id="0fc39-145">If the **Format-Table** command cannot display all the properties, it will remove some columns from the display and provide a warning.</span></span> <span data-ttu-id="0fc39-146">Такое поведение можно наблюдать, если поместить свойство **Name** в конец списка:</span><span class="sxs-lookup"><span data-stu-id="0fc39-146">You can see this behavior if you make **Name** the last property in the list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

<span data-ttu-id="0fc39-147">В приведенных выше входных данных столбец идентификатора обрезан, чтобы его значение уместилось в списке, а заголовки столбцов расположены вертикально.</span><span class="sxs-lookup"><span data-stu-id="0fc39-147">In the output above, the ID column is truncated to make it fit into the listing, and the column headings are stacked up.</span></span> <span data-ttu-id="0fc39-148">Автоматическое изменение размера столбцов не всегда дает желаемый результат.</span><span class="sxs-lookup"><span data-stu-id="0fc39-148">Automatically resizing the columns does not always do what you want.</span></span>

#### <a name="wrapping-format-table-output-in-columns-wrap"></a><span data-ttu-id="0fc39-149">Перенос на следующую строку вывода командлета Format-Table в столбцах (параметр Wrap)</span><span class="sxs-lookup"><span data-stu-id="0fc39-149">Wrapping Format-Table Output in Columns (Wrap)</span></span>

<span data-ttu-id="0fc39-150">Длинные данные командлета **Format-Table** можно принудительно перенести на следующую строку в пределах столбца с помощью параметра **Wrap**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-150">You can force lengthy **Format-Table** data to wrap within its display column by using the **Wrap** parameter.</span></span> <span data-ttu-id="0fc39-151">Использование параметра **Wrap** в отдельности не всегда приводит к ожидаемому результату, так как если не указан еще и параметр **AutoSize**, применяются параметры по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="0fc39-151">Using the **Wrap** parameter alone will not necessarily do what you expect, since it uses default settings if you do not also specify **AutoSize**:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

<span data-ttu-id="0fc39-152">Преимущество использования параметра **Wrap** без других параметров заключается в отсутствии существенного замедления обработки.</span><span class="sxs-lookup"><span data-stu-id="0fc39-152">An advantage of using the **Wrap** parameter by itself is that it does not slow down processing very much.</span></span> <span data-ttu-id="0fc39-153">Использование параметра **AutoSize** во время выполнения рекурсивного вывода списка файлов в большом каталоге может потребовать значительного объема памяти и времени перед отображением первых выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0fc39-153">If you perform a recursive file listing of a large directory system, it might take a very long time and use a lot of memory before displaying the first output items if you use **AutoSize**.</span></span>

<span data-ttu-id="0fc39-154">Если загрузка системы не имеет решающего значения, параметр **AutoSize** хорошо работает в сочетании с параметром **Wrap**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-154">If you are not concerned about system load, then **AutoSize** works well with the **Wrap** parameter.</span></span> <span data-ttu-id="0fc39-155">Начальным столбцам всегда выделяется необходимый размер для вывода элементов в одной строке, как и при указании параметра **AutoSize** без параметра **Wrap**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-155">The initial columns are always allotted as much width as they need to display items on one line, just as when you specify **AutoSize** without the **Wrap** parameter.</span></span> <span data-ttu-id="0fc39-156">Единственное отличие состоит в том, что последний столбец будет при необходимости перенесен на следующую строку:</span><span class="sxs-lookup"><span data-stu-id="0fc39-156">The only difference is that the final column will be wrapped if necessary:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

<span data-ttu-id="0fc39-157">Некоторые столбцы могут не быть показаны, если первым указать самый широкий столбец, поэтому безопаснее указывать первыми самые маленькие элементы данных.</span><span class="sxs-lookup"><span data-stu-id="0fc39-157">Some columns might not be displayed if you specify the widest columns first, so it is safest to specify the smallest data elements first.</span></span> <span data-ttu-id="0fc39-158">В следующем примере первым указан чрезвычайно большой элемент — путь. Даже при переносе на следующую строку последний столбец **Name** теряется:</span><span class="sxs-lookup"><span data-stu-id="0fc39-158">In the following example, we specify the extremely wide path element first, and even with wrapping, we still lose the final **Name** column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a><span data-ttu-id="0fc39-159">Организация табличного вывода (параметр -GroupBy)</span><span class="sxs-lookup"><span data-stu-id="0fc39-159">Organizing Table Output (-GroupBy)</span></span>

<span data-ttu-id="0fc39-160">Другим полезным параметром управления табличным выводом является **GroupBy**.</span><span class="sxs-lookup"><span data-stu-id="0fc39-160">Another useful parameter for tabular output control is **GroupBy**.</span></span> <span data-ttu-id="0fc39-161">Длинные табличные списки особенно тяжелы для сравнения.</span><span class="sxs-lookup"><span data-stu-id="0fc39-161">Longer tabular listings in particular may be hard to compare.</span></span> <span data-ttu-id="0fc39-162">Параметр **GroupBy** группирует выходные данные в соответствии со значением свойства.</span><span class="sxs-lookup"><span data-stu-id="0fc39-162">The **GroupBy** parameter groups output based on a property value.</span></span> <span data-ttu-id="0fc39-163">Например, можно сгруппировать процессы по организации для упрощения проверки, исключая название организации из списка свойства:</span><span class="sxs-lookup"><span data-stu-id="0fc39-163">For example, we can group processes by company for easier inspection, omitting the company value from the property listing:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```