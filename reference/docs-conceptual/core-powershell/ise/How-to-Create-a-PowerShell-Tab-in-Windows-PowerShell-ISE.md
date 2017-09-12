---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Создание вкладки PowerShell в интегрированной среде сценариев Windows PowerShell"
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 3cfeb18babe6b63f0e02da8cf0fd460950f1afce
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a><span data-ttu-id="ecdb7-103">Создание вкладки PowerShell в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-103">How to Create a PowerShell Tab in Windows PowerShell ISE</span></span>
<span data-ttu-id="ecdb7-104">Вкладки в интегрированной среде сценариев (ISE) Windows PowerShell позволяют одновременно создавать и использовать несколько сред выполнения внутри одного приложения.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-104">Tabs in the Windows PowerShell Integrated Scripting Environment (ISE) allow you to simultaneously create and use several execution environments within the same application.</span></span>
<span data-ttu-id="ecdb7-105">Каждая вкладка PowerShell соответствует отдельной среде выполнения или отдельному сеансу.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-105">Each PowerShell tab corresponds to a separate execution environment or session.</span></span>

> <span data-ttu-id="ecdb7-106">**Примечание.**</span><span class="sxs-lookup"><span data-stu-id="ecdb7-106">**NOTE**:</span></span>
>
> <span data-ttu-id="ecdb7-107">Переменные, функции и псевдонимы, созданные на одной вкладке, на другую не переносятся.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-107">Variables, functions, and aliases that you create in one tab do not carry over to another.</span></span> <span data-ttu-id="ecdb7-108">Это разные сеансы Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-108">They are different Windows PowerShell sessions.</span></span>

<span data-ttu-id="ecdb7-109">Выполните следующие действия, чтобы открыть или закрыть вкладку в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-109">Use the following steps to open or close a tab in Windows PowerShell.</span></span>
<span data-ttu-id="ecdb7-110">Чтобы переименовать вкладку, задайте свойство [DisplayName](The-PowerShellTab-Object.md#displayname) для объекта сценария на вкладке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-110">To rename a tab, set the [DisplayName](The-PowerShellTab-Object.md#displayname) property on the Windows PowerShell Tab scripting object.</span></span>

## <a name="to-create-and-use-a-new-powershell-tab"></a><span data-ttu-id="ecdb7-111">Создание и использование вкладки PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-111">To create and use a new PowerShell Tab</span></span>

<span data-ttu-id="ecdb7-112">В меню **Файл** щелкните элемент **Создать вкладку PowerShell**. Новая вкладка PowerShell всегда открывается в виде активного окна.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-112">On the **File** menu, click **New PowerShell Tab**. The new PowerShell tab always opens as the active window.</span></span>
<span data-ttu-id="ecdb7-113">Вкладки PowerShell нумеруются последовательно в порядке их открытия.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-113">PowerShell tabs are incrementally numbered in the order that they are opened.</span></span>
<span data-ttu-id="ecdb7-114">Каждая вкладка связана с собственным окном консоли Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-114">Each tab is associated with its own Windows PowerShell console window.</span></span>
<span data-ttu-id="ecdb7-115">Одновременно можно открыть до 32 вкладок PowerShell со своим сеансом (в интегрированной среде сценариев Windows PowerShell 2.0 это ограничение равно 8).</span><span class="sxs-lookup"><span data-stu-id="ecdb7-115">You can have up to 32 PowerShell tabs with their own session open at a time (this is limited to 8 on Windows PowerShell ISE 2.0.)</span></span>

<span data-ttu-id="ecdb7-116">Обратите внимание, что нажатие значка **Создать** или **Открыть** не приводит к созданию вкладки с отдельным сеансом.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-116">Note that clicking the **New** or **Open** icons on the toolbar does not create a new tab with a separate session.</span></span>
<span data-ttu-id="ecdb7-117">Эти кнопки открывают новый или существующий файл сценария на активной вкладке с сеансом.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-117">Instead, those buttons open a new or existing script file on the currently active tab with a session.</span></span>
<span data-ttu-id="ecdb7-118">Для каждой вкладки и сеанса можно открыть несколько файлов сценариев.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-118">You can have multiple script files open with each tab and session.</span></span>
<span data-ttu-id="ecdb7-119">Вкладки сценариев для сеанса отображаются под вкладками сеанса, только когда соответствующий сеанс активен.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-119">The script tabs for a session only appear below the session tabs when the associated session is active.</span></span>

<span data-ttu-id="ecdb7-120">Чтобы сделать вкладку PowerShell активной, щелкните ее. Чтобы выбрать одну из всех открытых вкладок PowerShell, щелкните ее в меню **Вид**.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-120">To make a PowerShell tab active, click the tab. To select from all PowerShell tabs that are open, on the **View** menu, click the PowerShell tab you want to use.</span></span>

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a><span data-ttu-id="ecdb7-121">Создание и использование вкладки удаленного использования PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-121">To create and use a new Remote PowerShell tab</span></span>

<span data-ttu-id="ecdb7-122">В меню **Файл** щелкните **Создание вкладки удаленного использования PowerShell** для создания сеанса на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-122">On the **File** menu, click **New Remote PowerShell Tab** to establish a session on a remote computer.</span></span>
<span data-ttu-id="ecdb7-123">Отображается диалоговое окно, предлагающее ввести сведения для установки удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-123">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>
<span data-ttu-id="ecdb7-124">Удаленная вкладка PowerShell работает так же, как и локальная, только команды и сценарии выполняются на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-124">The remote tab functions just like a local PowerShell tab, but the commands and scripts are run on the remote computer.</span></span>

## <a name="to-close-a-powershell-tab"></a><span data-ttu-id="ecdb7-125">Закрытие вкладки PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-125">To close a PowerShell Tab</span></span>

<span data-ttu-id="ecdb7-126">Чтобы закрыть вкладку, можно использовать любой из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="ecdb7-126">To close a tab, you can use any of the following techniques:</span></span>

- <span data-ttu-id="ecdb7-127">Щелкните вкладку, которую требуется закрыть.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-127">Click the tab that you want to close.</span></span>

- <span data-ttu-id="ecdb7-128">В меню **Файл** щелкните **Закрыть вкладку PowerShell** или нажмите кнопку "Закрыть" (**X**) на активной вкладке для ее закрытия.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-128">On the **File** menu, click **Close PowerShell Tab**, or click  the Close button  (**X**) on an active tab to close the tab.</span></span>

<span data-ttu-id="ecdb7-129">Если на закрываемой вкладке PowerShell имеются несохраненные файлы, вам будет предложено сохранить их или отменить изменения.</span><span class="sxs-lookup"><span data-stu-id="ecdb7-129">If you have unsaved files open in the PowerShell tab that you are closing, you are prompted to save or discard them.</span></span>
<span data-ttu-id="ecdb7-130">Дополнительные сведения о сохранении сценария см. в статье [Сохранение скрипта](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span><span class="sxs-lookup"><span data-stu-id="ecdb7-130">For more information about how to save a script, see [How to Save a Script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span></span>

## <a name="see-also"></a><span data-ttu-id="ecdb7-131">См. также</span><span class="sxs-lookup"><span data-stu-id="ecdb7-131">See Also</span></span>

- [<span data-ttu-id="ecdb7-132">Использование интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-132">Using the Windows PowerShell ISE</span></span>](Using-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="ecdb7-133">Использование области консоли в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecdb7-133">How to Use the Console Pane in the Windows PowerShell ISE</span></span>](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)

