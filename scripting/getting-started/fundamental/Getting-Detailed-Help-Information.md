---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Получение подробной справки"
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 3260b5ec0a91749d3b7b126412137aa9d603ef0e
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="getting-detailed-help-information"></a><span data-ttu-id="58eef-103">Получение подробной справки</span><span class="sxs-lookup"><span data-stu-id="58eef-103">Getting Detailed Help Information</span></span>
<span data-ttu-id="58eef-104">В Windows PowerShell входят подробные разделы справки, объясняющие концепции Windows PowerShell и язык Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58eef-104">Windows PowerShell includes detailed Help topics that explain Windows PowerShell concepts and the Windows PowerShell language.</span></span> <span data-ttu-id="58eef-105">Разделы справки существуют для каждого командлета и поставщика, а также для многих функций и сценариев.</span><span class="sxs-lookup"><span data-stu-id="58eef-105">There are also Help topics for each cmdlet and provider and Help topics for many functions and scripts.</span></span>

<span data-ttu-id="58eef-106">Эти разделы можно отобразить в командной строке или просмотреть их последние обновленные версии в библиотеке Microsoft TechNet Library.</span><span class="sxs-lookup"><span data-stu-id="58eef-106">You can display these Help topics at the command prompt or view the most recently updated versions of these topics in the Microsoft TechNet Library.</span></span> <span data-ttu-id="58eef-107">Многие рабочие программы Windows PowerShell, например интегрированная среда сценариев Windows PowerShell, содержат дополнительные компоненты справки, например контекстную справку и скомпилированные файлы справки (CHM).</span><span class="sxs-lookup"><span data-stu-id="58eef-107">Many programs that host Windows PowerShell, such as Windows PowerShell Integrated Scripting Environment, provide additional Help features, such as context-sensitive Help and compiled Help file (.chm).</span></span>

## <a name="getting-help-for-cmdlets"></a><span data-ttu-id="58eef-108">Получение справки для командлетов</span><span class="sxs-lookup"><span data-stu-id="58eef-108">Getting Help for Cmdlets</span></span>
<span data-ttu-id="58eef-109">Для получения справки о командлетах Windows PowerShell используйте командлет [Get-Help [m2]](https://technet.microsoft.com/en-us/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2).</span><span class="sxs-lookup"><span data-stu-id="58eef-109">To get Help about Windows PowerShell cmdlets, use the [Get-Help [m2]](https://technet.microsoft.com/en-us/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) cmdlet.</span></span> <span data-ttu-id="58eef-110">Например, для получения справки о командлете [Get-ChildItem [m2]](https://technet.microsoft.com/en-us/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc), введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-110">For example, to get Help for the [Get-ChildItem [m2]](https://technet.microsoft.com/en-us/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) cmdlet, type:</span></span>

```
get-help get-childitem
```

<span data-ttu-id="58eef-111">или</span><span class="sxs-lookup"><span data-stu-id="58eef-111">or</span></span>

```
get-childitem -?
```

<span data-ttu-id="58eef-112">Справку можно получить и по самому командлету Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-112">You can even get Help about the Get-Help cmdlet.</span></span> <span data-ttu-id="58eef-113">Например:</span><span class="sxs-lookup"><span data-stu-id="58eef-113">For example:</span></span>

```
get-help get-help
```

<span data-ttu-id="58eef-114">Чтобы отобразить список всех разделов справки для текущего сеанса, введите:</span><span class="sxs-lookup"><span data-stu-id="58eef-114">To get a list of all the cmdlet Help topics in your session, type:</span></span>

```
get-help -category cmdlet
```

<span data-ttu-id="58eef-115">Чтобы отображать каждый раздел справки постранично, используйте функцию **help** или ее псевдоним **man**.</span><span class="sxs-lookup"><span data-stu-id="58eef-115">To display one page of each Help topic at a time, use the **help** function or its alias **man**.</span></span> <span data-ttu-id="58eef-116">Например, чтобы вывести справку по командлету Get-ChildItem, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-116">For example, to display Help for the Get-ChildItem cmdlet, type</span></span>

```
man get-childitem
```

<span data-ttu-id="58eef-117">или</span><span class="sxs-lookup"><span data-stu-id="58eef-117">or</span></span>

```
help get-childitem
```

<span data-ttu-id="58eef-118">Чтобы вывести подробную информацию о командлете, функции или сценарии, включающую описания параметров и примеры использования, используйте параметр *Detailed* командлета Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-118">To display detailed information about a cmdlet, function, or script, including descriptions of its parameters and examples of its use, use the *Detailed* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="58eef-119">Например, чтобы получить подробные справочные сведения о командлете Get-ChildItem, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-119">For example, to get detailed information about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -detailed
```

<span data-ttu-id="58eef-120">Чтобы показать все содержимое раздела справки, используйте параметр *Full* командлета Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-120">To display all content in the Help topic, use the *Full* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="58eef-121">Например, чтобы вывести все содержимое раздела справки для командлета Get-ChildItem, введите:</span><span class="sxs-lookup"><span data-stu-id="58eef-121">For example, to display all content in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -full
```

<span data-ttu-id="58eef-122">Чтобы получить подробную справку по параметрам командлета, используйте параметр *Parameter* командлета Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-122">To get detailed Help about the parameters of a cmdlet, use the *Parameter* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="58eef-123">Например, для получения подробной справки по всем параметрам командлета Get-ChildItem введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-123">For example, to get detailed Help for all of the parameters of the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -parameter *
```

<span data-ttu-id="58eef-124">Чтобы вывести только примеры из раздела справки, используйте параметр *Example* командлета Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-124">To display only the examples in a Help topic, use the *Example* parameter of the Get-Help.</span></span> <span data-ttu-id="58eef-125">Например, чтобы получить примеры из раздела справки для командлета Get-ChildItem, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-125">For example, to display only the examples in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -examples
```

<span data-ttu-id="58eef-126">Дополнительные сведения о написании разделов справки для командлетов см. в статье "How to Write Cmdlet Help" (Как писать справку для командлетов) в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="58eef-126">For information about how to write Help topics for the cmdlets that you write, see the "How to Write Cmdlet Help" topic in MSDN.</span></span>

## <a name="getting-conceptual-help"></a><span data-ttu-id="58eef-127">Получение справки по концепциям</span><span class="sxs-lookup"><span data-stu-id="58eef-127">Getting Conceptual Help</span></span>
<span data-ttu-id="58eef-128">Командлет Get-Help также можно использовать для вывода разделов справки, посвященных концепциям Windows PowerShell, в том числе разделов о языке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58eef-128">The Get-Help cmdlet also displays information about conceptual topics in Windows PowerShell, including topics about the Windows PowerShell language.</span></span> <span data-ttu-id="58eef-129">Посвященные концепциям разделы справки начинаются с префикса about_, например about_line_editing.</span><span class="sxs-lookup"><span data-stu-id="58eef-129">Conceptual Help topics begin with the "about_" prefix, such as about_line_editing.</span></span> <span data-ttu-id="58eef-130">(Название концепции нужно вводить на английском языке, даже если используется локализованная версия Windows PowerShell.)</span><span class="sxs-lookup"><span data-stu-id="58eef-130">(The name of the conceptual topic must be entered in English even on non-English versions of Windows PowerShell.)</span></span>

<span data-ttu-id="58eef-131">Для отображения списка концептуальных разделов введите:</span><span class="sxs-lookup"><span data-stu-id="58eef-131">To display a list of conceptual topics, type:</span></span>

```
get-help about_*
```

<span data-ttu-id="58eef-132">Для отображения определенного раздела справки введите его имя, например:</span><span class="sxs-lookup"><span data-stu-id="58eef-132">To display a particular Help topic, type the topic name, for example:</span></span>

```
get-help about_command_syntax
```

<span data-ttu-id="58eef-133">Параметры командлета Get-Help, например *Detailed*, *Parameter* и *Examples*, не влияют на отображение концептуальных разделов справки.</span><span class="sxs-lookup"><span data-stu-id="58eef-133">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of conceptual Help topics.</span></span>

## <a name="getting-help-about-providers"></a><span data-ttu-id="58eef-134">Получение справки о поставщиках</span><span class="sxs-lookup"><span data-stu-id="58eef-134">Getting Help About Providers</span></span>
<span data-ttu-id="58eef-135">Командлет Get-Help позволяет получить информацию о поставщиках Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58eef-135">The Get-Help cmdlet displays information about Windows PowerShell providers.</span></span> <span data-ttu-id="58eef-136">Чтобы получить справку для поставщика, введите команду Get-Help и имя поставщика.</span><span class="sxs-lookup"><span data-stu-id="58eef-136">To get Help for a provider, type "Get-Help" followed by the provider name.</span></span> <span data-ttu-id="58eef-137">Например, чтобы получить справку для поставщика Registry, введите:</span><span class="sxs-lookup"><span data-stu-id="58eef-137">For example, to get Help for the Registry provider, type:</span></span>

```
get-help registry
```

<span data-ttu-id="58eef-138">Чтобы отобразить список всех разделов справки по поставщикам для текущего сеанса, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-138">To get a list of all the provider Help topics in your session, type</span></span>

```
get-help -category provider
```

<span data-ttu-id="58eef-139">Параметры командлета Get-Help, например *Detailed*, *Parameter* и *Examples*, не влияют на отображение разделов справки о поставщиках.</span><span class="sxs-lookup"><span data-stu-id="58eef-139">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of provider Help topics.</span></span>

## <a name="getting-help-about-scripts-and-functions"></a><span data-ttu-id="58eef-140">Получение справки по сценариям и функциям</span><span class="sxs-lookup"><span data-stu-id="58eef-140">Getting Help About Scripts and Functions</span></span>
<span data-ttu-id="58eef-141">Многим сценариям и функциям Windows PowerShell посвящены разделы справки.</span><span class="sxs-lookup"><span data-stu-id="58eef-141">Many scripts and functions in Windows PowerShell have Help topics.</span></span> <span data-ttu-id="58eef-142">Для их просмотра можно использовать командлет Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-142">Use the Get-Help cmdlet to display the Help topics for scripts and functions.</span></span>

<span data-ttu-id="58eef-143">Чтобы получить справку для функции, введите команду get-help и имя функции.</span><span class="sxs-lookup"><span data-stu-id="58eef-143">To display the Help for a function, type "get-help" followed by the function name.</span></span> <span data-ttu-id="58eef-144">Например, для получения справки по функции Disable-PSRemoting введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-144">For example, to get Help for the Disable-PSRemoting function, type:</span></span>

```
get-help disable-psremoting
```

<span data-ttu-id="58eef-145">Для вывода справки по сценарию введите полный путь к файлу сценария.</span><span class="sxs-lookup"><span data-stu-id="58eef-145">To display the Help for a script, type the fully qualified path to the script file.</span></span> <span data-ttu-id="58eef-146">Если путь к сценарию указан в переменной среды Path, его можно не указывать в команде.</span><span class="sxs-lookup"><span data-stu-id="58eef-146">If the script is in a path that is listed in the Path environment variable, you can omit the path from the command.</span></span>

<span data-ttu-id="58eef-147">Например, если сценарий TestScript.ps1 находится в каталоге C:\\PS-Test, для вывода раздела справки по этому сценарию введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-147">For example, if you have a script called "TestScript.ps1" in your C:\\PS-Test directory, to display the Help topic for the script, type:</span></span>

```
get-help c:\ps-test\TestScript.ps1
```

<span data-ttu-id="58eef-148">Параметры вывода справки по командлетам, в том числе *Detailed*, *Full*, *Examples* и *Parameter*, работают для вывода справки по сценариям и функциям.</span><span class="sxs-lookup"><span data-stu-id="58eef-148">The parameters that were designed for displaying cmdlet Help, such as *Detailed*, *Full*, *Examples*, and *Parameter*, work for script Help and function Help, too.</span></span> <span data-ttu-id="58eef-149">Однако при выводе всех разделов справки с помощью команды "get-help \*" справка по функциям и сценариям не выводится.</span><span class="sxs-lookup"><span data-stu-id="58eef-149">However, when you display all Help, by typing "get-help \*", Help for functions and scripts does not appear.</span></span>

<span data-ttu-id="58eef-150">Сведения о написании разделов справки для функций и сценариев см. в статьях [about_Functions [m2]](https://technet.microsoft.com/en-us/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/en-us/library/7dc08334-dcfe-450b-b949-0554855623af) и [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span><span class="sxs-lookup"><span data-stu-id="58eef-150">For information about writing Help topics for your functions and scripts, see [about_Functions [m2]](https://technet.microsoft.com/en-us/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/en-us/library/7dc08334-dcfe-450b-b949-0554855623af), and [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span></span>

## <a name="getting-help-online"></a><span data-ttu-id="58eef-151">Получение справки в Интернете</span><span class="sxs-lookup"><span data-stu-id="58eef-151">Getting Help Online</span></span>
<span data-ttu-id="58eef-152">Если локальный компьютер подключен к Интернету, лучше всего использовать разделы справки в Интернете.</span><span class="sxs-lookup"><span data-stu-id="58eef-152">If you are connected to the Internet, one of the best ways to get Help is to view the Help topics online.</span></span> <span data-ttu-id="58eef-153">Поскольку разделы справки в Интернете легко обновлять, в них обычно содержится самая актуальная информация.</span><span class="sxs-lookup"><span data-stu-id="58eef-153">Because online topics are easy to update, they are likely to provide the most current content.</span></span>

<span data-ttu-id="58eef-154">Для получения справки в Интернете используйте параметр *Online* командлета Get-Help.</span><span class="sxs-lookup"><span data-stu-id="58eef-154">To get Help online, try the *Online* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="58eef-155">Параметр *Online* командлета Get-Help подходит только для справки по командлетам, функциям и сценариям.</span><span class="sxs-lookup"><span data-stu-id="58eef-155">The *Online* parameter of the Get-Help cmdlet works only for cmdlet Help, function Help, and script Help.</span></span> <span data-ttu-id="58eef-156">Параметр *Online* нельзя использовать для вывода разделов справки о концепциях (About) и поставщиках.</span><span class="sxs-lookup"><span data-stu-id="58eef-156">You cannot use the *Online* parameter with conceptual (About) topics or provider Help topics.</span></span> <span data-ttu-id="58eef-157">Поскольку эта возможность необязательна, она может не работать для некоторых разделов справки по командлетам, функциям и сценариям.</span><span class="sxs-lookup"><span data-stu-id="58eef-157">Also, because this feature is optional, it does not work for every cmdlet, function, or script Help topic.</span></span>

<span data-ttu-id="58eef-158">Однако все разделы справки, входящие в комплект Windows PowerShell, в том числе разделы справки по поставщикам и концептуальные (About) разделы справки, можно найти в Интернете в разделе [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) библиотеки Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="58eef-158">However, all the Help topics that come with Windows PowerShell, including provider Help and conceptual (About) Help topics, are available online in the [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) section of the Microsoft TechNet Library.</span></span>

<span data-ttu-id="58eef-159">Для использования параметра *Online* командлета Get-Help нужно применять следующий формат:</span><span class="sxs-lookup"><span data-stu-id="58eef-159">To use the *Online* parameter of the Get-Help cmdlet, use the following command format.</span></span>

```
get-help <command-name> -online
```

<span data-ttu-id="58eef-160">Например, чтобы открыть интернет-версию раздела справки о командлете Get-ChildItem, введите:</span><span class="sxs-lookup"><span data-stu-id="58eef-160">For example, to get the online version of the Help topic about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -online
```

<span data-ttu-id="58eef-161">Если интернет-версия раздела справки доступна, она откроется в установленном по умолчанию браузере.</span><span class="sxs-lookup"><span data-stu-id="58eef-161">If an online version of the Help topic is available, it will open in your default browser.</span></span>

<span data-ttu-id="58eef-162">Если для раздела справки имеется интернет-версия, можно просмотреть и интернет-адрес (URL) раздела справки.</span><span class="sxs-lookup"><span data-stu-id="58eef-162">If online Help is supported for a Help topic, you can also view the Internet address (URL) of the Help topic.</span></span> <span data-ttu-id="58eef-163">Интернет-адрес отображается в разделе "Связанные ссылки" раздела справки.</span><span class="sxs-lookup"><span data-stu-id="58eef-163">The Internet address appears in the Related Links section of a Help topic.</span></span>

<span data-ttu-id="58eef-164">Например, чтобы посмотреть адрес интернет-версии командлета Add-Computer, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="58eef-164">For example, to see the URL for the online version of the Add-Computer cmdlet, type:</span></span>

```
get-help add-computer
```

<span data-ttu-id="58eef-165">Первая строка в разделе "Связанные ссылки" показана ниже.</span><span class="sxs-lookup"><span data-stu-id="58eef-165">The first line in the Related Links section of the topic is shown below.</span></span>

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

<span data-ttu-id="58eef-166">Сведения об организации интернет-поддержки собственных разделов справки см. в статьях [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), и "How to Write Cmdlet Help" (Как писать справку для командлетов) ([http://go.microsoft.com/fwlink/?LinkID=123415](http://go.microsoft.com/fwlink/?LinkID=123415)) — в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="58eef-166">For information about how to provide online support for your Help topics, see [about_Comment_Based_Help](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), and see "How to Write Cmdlet Help" ([http://go.microsoft.com/fwlink/?LinkID=123415](http://go.microsoft.com/fwlink/?LinkID=123415)) in the MSDN (Microsoft Developer Network) library.</span></span>

## <a name="see-also"></a><span data-ttu-id="58eef-167">См. также</span><span class="sxs-lookup"><span data-stu-id="58eef-167">See Also</span></span>
- [<span data-ttu-id="58eef-168">about_Functions [m2]</span><span class="sxs-lookup"><span data-stu-id="58eef-168">about_Functions [m2]</span></span>](https://technet.microsoft.com/en-us/library/61d40692-5300-4de9-a9b5-bae31815e105)
- [<span data-ttu-id="58eef-169">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="58eef-169">about_Scripts</span></span>](https://technet.microsoft.com/en-us/library/7dc08334-dcfe-450b-b949-0554855623af)
- [<span data-ttu-id="58eef-170">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="58eef-170">about_Comment_Based_Help</span></span>](https://technet.microsoft.com/en-us/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
- [<span data-ttu-id="58eef-171">Get-Help [m2]</span><span class="sxs-lookup"><span data-stu-id="58eef-171">Get-Help [m2]</span></span>](https://technet.microsoft.com/en-us/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)

