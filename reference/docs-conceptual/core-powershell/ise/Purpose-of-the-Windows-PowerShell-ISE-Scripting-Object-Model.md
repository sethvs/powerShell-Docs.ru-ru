---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Назначение объектной модели сценариев интегрированной среды сценариев Windows PowerShell"
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: 65535948d681ec63c6cc36583c6d145cfa19b937
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a><span data-ttu-id="98172-103">Назначение объектной модели сценариев интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-103">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>
  <span data-ttu-id="98172-104">Объекты определяют внешний вид и функции интегрированной среды сценариев Windows PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="98172-104">Objects are associated with the form and function of Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="98172-105">В справочнике по объектной модели содержатся сведения о свойствах- и методах-членах, предоставляемых этими объектами.</span><span class="sxs-lookup"><span data-stu-id="98172-105">The object model reference provides details about the member properties and methods that these objects expose.</span></span> <span data-ttu-id="98172-106">Примеры показывают, как использовать сценарии для прямого доступа к этим методам и свойствам.</span><span class="sxs-lookup"><span data-stu-id="98172-106">Examples are provided to show how you can use scripts to directly access these methods and properties.</span></span> <span data-ttu-id="98172-107">Объектная модель сценариев упрощает выполнение следующих задач.</span><span class="sxs-lookup"><span data-stu-id="98172-107">The scripting object model makes the following range of tasks easier.</span></span>

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a><span data-ttu-id="98172-108">Настройка внешнего вида интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-108">Customizing the appearance of Windows PowerShell ISE</span></span>
 <span data-ttu-id="98172-109">Объектную модель можно использовать для изменения параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="98172-109">You can use the object model to modify the application settings and options.</span></span> <span data-ttu-id="98172-110">Например, их можно изменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98172-110">For example, you can modify them as follows:</span></span>

-   <span data-ttu-id="98172-111">можно изменить цвет текста и фона в сообщениях об ошибках, предупреждениях, подробных сообщениях и выходных данных отладки;</span><span class="sxs-lookup"><span data-stu-id="98172-111">You can change the color of errors, warnings, verbose outputs, and debug outputs.</span></span>

-   <span data-ttu-id="98172-112">можно получить или задать цвета фона для области команд, области вывода и области сценариев;</span><span class="sxs-lookup"><span data-stu-id="98172-112">You can get or set the background colors for the Command pane, the Output pane, and the Script pane.</span></span>

-   <span data-ttu-id="98172-113">можно задать цвет переднего плана для области вывода;</span><span class="sxs-lookup"><span data-stu-id="98172-113">You can set the foreground color for the Output pane.</span></span>

-   <span data-ttu-id="98172-114">можно задать название и размер шрифта для интегрированной среды сценариев Windows PowerShell;</span><span class="sxs-lookup"><span data-stu-id="98172-114">You can set the font name and font size for Windows PowerShell ISE.</span></span>

-   <span data-ttu-id="98172-115">можно настроить предупреждения</span><span class="sxs-lookup"><span data-stu-id="98172-115">You can configure warnings.</span></span> <span data-ttu-id="98172-116">(к ним относятся предупреждения, которые выдаются при открытии файла на нескольких вкладках PowerShell или при запуске сценария в файле до сохранения файла);</span><span class="sxs-lookup"><span data-stu-id="98172-116">This setting includes warnings that are issued when a file is opened in multiple PowerShell tabs or when a script in the file is run before the file has been saved.</span></span>

-   <span data-ttu-id="98172-117">можно переключиться в представление, где область сценариев и область вывода отображаются рядом или область сценариев отображается над областью вывода.</span><span class="sxs-lookup"><span data-stu-id="98172-117">You can switch between a view where the Script pane and the Output pane are side-by-side and a view where the Script pane is on top of the Output pane.</span></span> <span data-ttu-id="98172-118">Область команд можно закрепить под или над областью вывода.</span><span class="sxs-lookup"><span data-stu-id="98172-118">You can dock the Command pane to the bottom or the top of the Output pane.</span></span>

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a><span data-ttu-id="98172-119">Расширение функций интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-119">Enhancing the functionality of Windows PowerShell ISE</span></span>
 <span data-ttu-id="98172-120">Объектную модель можно использовать для расширения возможностей интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98172-120">You can use the object model to enhance the functionality of Windows PowerShell ISE.</span></span> <span data-ttu-id="98172-121">Например, администратор может сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="98172-121">For example, you can:</span></span>

-   <span data-ttu-id="98172-122">добавить или изменить экземпляр интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-122">Add and modify the instance of Windows PowerShell ISE itself.</span></span> <span data-ttu-id="98172-123">(например, можно добавить новые пункты меню, чтобы изменить меню, и сопоставить новые пункты меню со сценариями);</span><span class="sxs-lookup"><span data-stu-id="98172-123">For example, to change the menus, you can add new menu items and map the new menu items to scripts.</span></span>

-   <span data-ttu-id="98172-124">создавать сценарии, выполняющие некоторые задачи, которые можно выполнять с помощью команд и кнопок меню в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-124">Create scripts that perform some of the tasks that you can perform by using the menu commands and buttons in Windows PowerShell ISE.</span></span> <span data-ttu-id="98172-125">(например, можно добавить, удалить или выбрать вкладку PowerShell);</span><span class="sxs-lookup"><span data-stu-id="98172-125">For example, you can add, remove, or select a PowerShell tab.</span></span>

-   <span data-ttu-id="98172-126">дополнять задачи, которые можно выполнить с помощью команд и кнопок меню</span><span class="sxs-lookup"><span data-stu-id="98172-126">Complement tasks that can be performed by using menu commands and buttons.</span></span> <span data-ttu-id="98172-127">(например, можно переименовать вкладку PowerShell);</span><span class="sxs-lookup"><span data-stu-id="98172-127">For example, you can rename a PowerShell tab.</span></span>

-   <span data-ttu-id="98172-128">управлять текстовыми буферами для области команд, области вывода и области сценариев, связанными с файлом.</span><span class="sxs-lookup"><span data-stu-id="98172-128">Manipulate text buffers for the Command pane, the Output pane, and the Script pane that are associated with a file.</span></span> <span data-ttu-id="98172-129">Например, администратор может сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="98172-129">For example, you can:</span></span>

    -   <span data-ttu-id="98172-130">получить или задать весь текст,</span><span class="sxs-lookup"><span data-stu-id="98172-130">Get or set all text.</span></span>

    -   <span data-ttu-id="98172-131">получить или задать выделенный текст,</span><span class="sxs-lookup"><span data-stu-id="98172-131">Get or set a text selection.</span></span>

    -   <span data-ttu-id="98172-132">запустить сценарий или выбранный фрагмент сценария,</span><span class="sxs-lookup"><span data-stu-id="98172-132">Run a script or run a selected portion of a script.</span></span>

    -   <span data-ttu-id="98172-133">прокрутить строку в представлении,</span><span class="sxs-lookup"><span data-stu-id="98172-133">Scroll a line into view.</span></span>

    -   <span data-ttu-id="98172-134">вставить текст в позиции курсора,</span><span class="sxs-lookup"><span data-stu-id="98172-134">Insert text at a caret position.</span></span>

    -   <span data-ttu-id="98172-135">выбрать блок текста,</span><span class="sxs-lookup"><span data-stu-id="98172-135">Select a block of text.</span></span>

    -   <span data-ttu-id="98172-136">получить номер последней строки,</span><span class="sxs-lookup"><span data-stu-id="98172-136">Get the last line number.</span></span>

-   <span data-ttu-id="98172-137">выполнить операции с файлами.</span><span class="sxs-lookup"><span data-stu-id="98172-137">Perform file operations.</span></span> <span data-ttu-id="98172-138">Например, администратор может сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="98172-138">For example, you can:</span></span>

    -   <span data-ttu-id="98172-139">открыть файл, сохранить файл или сохранить файл, используя другое имя,</span><span class="sxs-lookup"><span data-stu-id="98172-139">Open a file, save a file, or save a file by using a different name.</span></span>

    -   <span data-ttu-id="98172-140">определить, был ли файл изменен с момента последнего сохранения,</span><span class="sxs-lookup"><span data-stu-id="98172-140">Determine whether a file has been changed after it was last saved.</span></span>

    -   <span data-ttu-id="98172-141">получить имя файла,</span><span class="sxs-lookup"><span data-stu-id="98172-141">Get the file name.</span></span>

    -   <span data-ttu-id="98172-142">выбрать файл.</span><span class="sxs-lookup"><span data-stu-id="98172-142">Select a file.</span></span>

## <a name="automating-tasks"></a><span data-ttu-id="98172-143">Автоматизация задач</span><span class="sxs-lookup"><span data-stu-id="98172-143">Automating tasks</span></span>
 <span data-ttu-id="98172-144">Объектную модель сценариев можно использовать для создания сочетаний клавиш для часто выполняемых операций.</span><span class="sxs-lookup"><span data-stu-id="98172-144">You can use the scripting object model to create keyboard shortcuts for frequent operations.</span></span>

## <a name="see-also"></a><span data-ttu-id="98172-145">См. также</span><span class="sxs-lookup"><span data-stu-id="98172-145">See Also</span></span>
- [<span data-ttu-id="98172-146">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="98172-146">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md) 
- [<span data-ttu-id="98172-147">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-147">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="98172-148">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="98172-148">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
