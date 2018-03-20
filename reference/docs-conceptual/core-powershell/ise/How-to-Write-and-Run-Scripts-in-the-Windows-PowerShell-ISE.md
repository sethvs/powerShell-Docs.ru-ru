---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Написание и запуск сценариев в интегрированной среде сценариев Windows PowerShell"
ms.assetid: 62f916d9-b3a1-484a-bdfb-41f57112c22b
ms.openlocfilehash: 77d8ae81cb03f03b3b5d044e6503bbb23cb5b771
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="how-to-write-and-run-scripts-in-the-windows-powershell-ise"></a><span data-ttu-id="6fe3e-103">Написание и запуск сценариев в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fe3e-103">How to Write and Run Scripts in the Windows PowerShell ISE</span></span>
<span data-ttu-id="6fe3e-104">Эта статья содержит инструкции по созданию, редактированию, выполнению и сохранению сценариев в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-104">This topic describes how to create, edit, run, and save scripts in the Script Pane.</span></span>

## <a name="how-to-create-and-run-scripts"></a><span data-ttu-id="6fe3e-105">Создание и выполнение сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-105">How to create and run scripts</span></span>
<span data-ttu-id="6fe3e-106">В области скриптов можно открывать и редактировать файлы Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-106">You can open and edit Windows PowerShell files in the Script Pane.</span></span> <span data-ttu-id="6fe3e-107">Сейчас нас интересуют следующие типы файлов Windows PowerShell: файлы скриптов (PS1), файлы данных скриптов (PSD1) и файлы модулей скриптов (PSM1).</span><span class="sxs-lookup"><span data-stu-id="6fe3e-107">Specific file types of interest in Windows PowerShell are script files (.ps1), script data files (.psd1), and script module files (.psm1).</span></span> <span data-ttu-id="6fe3e-108">Эти типы файлов имеют цветовую подсветку синтаксиса в редакторе области сценариев.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-108">These file types are syntax colored in the Script Pane editor.</span></span> <span data-ttu-id="6fe3e-109">Другие стандартные файлы, которые можно открыть в области сценариев, — это файлы конфигурации (PS1XML), XML-файлы и текстовые файлы.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-109">Other common file types you may open in the Script Pane are configuration files (.ps1xml), XML files, and text files.</span></span>

> [!NOTE]
> <span data-ttu-id="6fe3e-110">Политика выполнения Windows PowerShell определяет, можно ли выполнять сценарии, загружать профили Windows PowerShell и файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-110">The Windows PowerShell execution policy determines whether you can run scripts and load Windows PowerShell profiles and configuration files.</span></span> <span data-ttu-id="6fe3e-111">Политика выполнения по умолчанию, Restricted, запрещает выполнение сценариев и блокирует загрузку профилей.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-111">The default execution policy, Restricted, prevents all scripts from running, and prevents loading profiles.</span></span> <span data-ttu-id="6fe3e-112">Чтобы изменить эту политику выполнения и разрешить загрузку и использование профилей, изучите статьи [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) и [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span><span class="sxs-lookup"><span data-stu-id="6fe3e-112">To change the execution policy to allow profiles to load and be used, see [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) and [about_Signing [v4]](https://technet.microsoft.com/library/fcbdd3b9-0b9f-4734-b5c7-e0dcc304fa1d).</span></span>

### <a name="to-create-a-new-script-file"></a><span data-ttu-id="6fe3e-113">Создание файла сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-113">To create a new script file</span></span>
<span data-ttu-id="6fe3e-114">Нажмите кнопку **Создать** на панели инструментов или откройте меню **Файл** и выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-114">On the toolbar, click **New** , or on the **File** menu, click **New**.</span></span> <span data-ttu-id="6fe3e-115">Созданный файл появится в новой вкладке, расположенной под текущей вкладкой PowerShell. Помните, что вкладки PowerShell отображаются, только если их несколько.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-115">The created file appears in a new file tab under the current PowerShell tab. Remember that the PowerShell tabs are only visible when there are more than one.</span></span> <span data-ttu-id="6fe3e-116">По умолчанию создается файл сценария (PS1), но его можно сохранить с новым именем и расширением.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-116">By default a file of type script (.ps1) is created, but it can be saved with a new name and extension.</span></span> <span data-ttu-id="6fe3e-117">На одной вкладке PowerShell может быть создано несколько файлов сценариев.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-117">Multiple script files can be created in the same PowerShell tab.</span></span>

### <a name="to-open-an-existing-script"></a><span data-ttu-id="6fe3e-118">Открытие существующего сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-118">To open an existing script</span></span>
<span data-ttu-id="6fe3e-119">Нажмите кнопку **Открыть...** на панели инструментов или откройте меню **Файл** и выберите пункт **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-119">On the toolbar, click **Open**, or on the **File** menu, click **Open**.</span></span> <span data-ttu-id="6fe3e-120">В диалоговом окне **Открыть** выберите файл, который требуется открыть.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-120">In the **Open** dialog box, select the file you want to open.</span></span> <span data-ttu-id="6fe3e-121">Открытый файл появится в новой вкладке.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-121">The opened file appears in a new tab.</span></span>

### <a name="to-close-a-script-tab"></a><span data-ttu-id="6fe3e-122">Закрытие вкладки сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-122">To close a script tab</span></span>
<span data-ttu-id="6fe3e-123">Щелкните вкладку того сценария, который нужно закрыть, а затем выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="6fe3e-123">Click the script tab of the script you want to close, then do one of the following:</span></span>

1. <span data-ttu-id="6fe3e-124">щелкните значок **Закрыть** (X) на вкладке сценария;</span><span class="sxs-lookup"><span data-stu-id="6fe3e-124">Click the **Close** icon (X) on the script tab.</span></span>

2. <span data-ttu-id="6fe3e-125">выберите пункт **Закрыть** в меню **Файл**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-125">On the **File** menu, click **Close**.</span></span>

<span data-ttu-id="6fe3e-126">Если файл был изменен с момента последнего сохранения, будет предложено сохранить или отменить изменения.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-126">If the file has been altered since it was last saved, you are prompted to save or discard it.</span></span>

### <a name="to-display-the-file-path"></a><span data-ttu-id="6fe3e-127">Отображение пути к файлу</span><span class="sxs-lookup"><span data-stu-id="6fe3e-127">To display the file path</span></span>
<span data-ttu-id="6fe3e-128">На вкладке файла наведите курсор на его имя.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-128">On the file tab, point to the file name.</span></span> <span data-ttu-id="6fe3e-129">Появится подсказка с полным путем к файлу сценария.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-129">The fully qualified path to the script file appears in a tooltip.</span></span>

### <a name="to-run-a-script"></a><span data-ttu-id="6fe3e-130">Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-130">To run a script</span></span>
<span data-ttu-id="6fe3e-131">Нажмите кнопку **Выполнить сценарий** на панели инструментов или откройте меню **Файл** и выберите пункт **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-131">On the toolbar, click **Run Script**, or on the **File** menu, click **Run**.</span></span>

### <a name="to-run-a-portion-of-a-script"></a><span data-ttu-id="6fe3e-132">Выполнение части сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-132">To run a portion of a script</span></span>

1. <span data-ttu-id="6fe3e-133">Выберите часть сценария в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-133">In the Script Pane, select a portion of a script.</span></span>

2. <span data-ttu-id="6fe3e-134">Нажмите кнопку **Выполнить выделенный фрагмент** на панели инструментов или откройте меню **Файл** и выберите пункт **Выполнить выделенный фрагмент**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-134">On the **File** menu, click **Run Selection**, or on the toolbar, click **Run Selection**.</span></span>

### <a name="to-stop-a-running-script"></a><span data-ttu-id="6fe3e-135">Остановка выполняемого сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-135">To stop a running script</span></span>
<span data-ttu-id="6fe3e-136">Нажмите кнопку **Остановить операцию** на панели инструментов, нажмите клавиши CTRL+BREAK или выберите пункт **Остановить операцию** в меню **Файл**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-136">On the toolbar, click **Stop Operation**, press CTRL+BREAK, or on the **File** menu, click **Stop Operation**.</span></span> <span data-ttu-id="6fe3e-137">Нажатие клавиш **CTRL+C** также сработает, если нет выделенного текста. В противном случае нажатие клавиш **CTRL+C** приведет к копированию выделенного текста.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-137">Pressing **CTRL+C** also works unless some text is currently selected, in which case **CTRL+C** maps to the copy function for the selected text.</span></span>

## <a name="how-to-write-and-edit-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-138">Написание и редактирование текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-138">How to write and edit text in the Script Pane</span></span>
<span data-ttu-id="6fe3e-139">Для редактирования текста в области сценариев выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-139">Use the following steps to edit text in the Script Pane.</span></span> <span data-ttu-id="6fe3e-140">Текст можно копировать, вырезать, вставлять, искать и заменять.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-140">You can copy, cut, paste, find, and replace text.</span></span> <span data-ttu-id="6fe3e-141">Также можно отменить и повторить последнее выполненное действие.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-141">You can also undo and redo the last action you just performed.</span></span> <span data-ttu-id="6fe3e-142">Для этого используются такие же сочетания клавиш, как и во всех других приложениях Windows.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-142">The keyboard shortcuts for performing these actions are the same as those used for all Windows applications.</span></span>

### <a name="to-enter-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-143">Ввод текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-143">To enter text in the Script Pane</span></span>

1. <span data-ttu-id="6fe3e-144">Установите курсор в область сценариев, щелкнув кнопкой мыши любую ее часть или выбрав пункт **Перейти в область сценариев** в меню **Вид**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-144">Move the cursor to the Script Pane by clicking anywhere in the Script Pane, or by clicking **Go to Script Pane** in the **View** menu.</span></span>

2. <span data-ttu-id="6fe3e-145">Создайте сценарий.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-145">Create a script.</span></span> <span data-ttu-id="6fe3e-146">Цветовая подсветка синтаксиса и заполнение нажатием клавиши TAB делают эту задачу гораздо проще в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-146">Syntax coloring and tab completion make this a richer experience in Windows PowerShell ISE.</span></span>

3. <span data-ttu-id="6fe3e-147">Подробную информацию о заполнении нажатием клавиши TAB, помогающем при вводе кода, см. в статье [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) (Использование заполнения нажатием клавиши TAB в областях сценариев и консоли).</span><span class="sxs-lookup"><span data-stu-id="6fe3e-147">See [How to Use Tab Completion in the Script Pane and Console Pane](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) for details about using the tab completion feature to help in typing.</span></span>

### <a name="to-find-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-148">Поиск текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-148">To find text in the Script Pane</span></span>

1. <span data-ttu-id="6fe3e-149">Чтобы найти текст в любой части сценария, нажмите клавиши **CTRL+F** или выберите **Найти в сценарии** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-149">To find text anywhere, press **CTRL+F** or, on the **Edit** menu, click **Find in Script**.</span></span>

2. <span data-ttu-id="6fe3e-150">Чтобы найти текст после курсора, нажмите клавишу **F3** или выберите **Найти следующее в сценарии** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-150">To find text after the cursor, press **F3** or, on the **Edit** menu, click **Find Next in Script**.</span></span>

3. <span data-ttu-id="6fe3e-151">Чтобы найти текст до курсора, нажмите клавиши **SHIFT+F3** или выберите **Find Previous in Script** (Найти предыдущее в сценарии) в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-151">To find text before the cursor, press **SHIFT+F3** or, on the **Edit** menu, click **Find Previous in Script**.</span></span>

### <a name="to-find-and-replace-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-152">Поиск и замена текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-152">To find and replace text in the Script Pane</span></span>
<span data-ttu-id="6fe3e-153">Нажмите клавиши **CRTL+H** или выберите **Replace in Script** (Заменить в сценарии) в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-153">Press **CRTL+H** or, on the **Edit** menu, click **Replace in Script**.</span></span> <span data-ttu-id="6fe3e-154">Введите искомый текст и текст, которым его нужно заменить, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-154">Enter both the text you want to find and the text with which you want to replace it, and then press **ENTER**.</span></span>

### <a name="to-go-to-a-particular-line-of-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-155">Переход к определенной строке текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-155">To go to a particular line of text in the Script Pane</span></span>

1. <span data-ttu-id="6fe3e-156">В области сценариев нажмите клавиши **CTRL+G** или выберите **Перейти к строке** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-156">In the Script Pane, press **CTRL+G** or, on the **Edit** menu, click **Go to Line**.</span></span>

2. <span data-ttu-id="6fe3e-157">Введите номер строки.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-157">Enter a line number.</span></span>

### <a name="to-copy-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-158">Копирование текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-158">To copy text in the Script Pane</span></span>

1. <span data-ttu-id="6fe3e-159">В области сценариев выделите текст, который требуется скопировать.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-159">In the Script Pane, select the text that you want to copy.</span></span>

2. <span data-ttu-id="6fe3e-160">Нажмите клавиши **CTRL+C**, щелкните значок **Копировать** на панели инструментов или выберите **Копировать** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-160">Press **CTRL+C** or, on the toolbar, click the **Copy** icon, or on the **Edit** menu, click **Copy**.</span></span>

### <a name="to-cut-text-in-the-script-pane"></a><span data-ttu-id="6fe3e-161">Вырезание текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-161">To cut text in the Script Pane</span></span>

1. <span data-ttu-id="6fe3e-162">В области сценариев выделите текст, который требуется вырезать.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-162">In the Script Pane, select the text that you want to cut.</span></span>

2. <span data-ttu-id="6fe3e-163">Нажмите клавиши **CTRL+X**, щелкните значок **Вырезать** на панели инструментов или выберите **Вырезать** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-163">Press **CTRL+X** or, on the toolbar, click the **Cut** icon, or on the **Edit** menu, click **Cut**.</span></span>

### <a name="to-paste-text-into-the-script-pane"></a><span data-ttu-id="6fe3e-164">Вставка текста в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-164">To paste text into the Script Pane</span></span>
<span data-ttu-id="6fe3e-165">Нажмите клавиши **CTRL+V**, щелкните значок **Вставить** на панели инструментов или выберите **Вставить** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-165">Press **CTRL+V** or, on the toolbar, click the **Paste** icon, or on the **Edit** menu, click **Paste**.</span></span>

### <a name="to-undo-an-action-in-the-script-pane"></a><span data-ttu-id="6fe3e-166">Отмена действия в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-166">To undo an action in the Script Pane</span></span>
<span data-ttu-id="6fe3e-167">Нажмите клавиши **CTRL+Z**, щелкните значок **Отменить** на панели инструментов или выберите **Отменить** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-167">Press **CTRL+Z** or, on the toolbar, click the **Undo** icon, or on the **Edit** menu, click **Undo**.</span></span>

### <a name="to-redo-an-action-in-the-script-pane"></a><span data-ttu-id="6fe3e-168">Повторное выполнение действия в области сценариев</span><span class="sxs-lookup"><span data-stu-id="6fe3e-168">To redo an action in the Script Pane</span></span>
<span data-ttu-id="6fe3e-169">Нажмите клавиши **CTRL+Y**, щелкните значок **Повторить** на панели инструментов или выберите **Повторить** в меню **Правка**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-169">Press **CTRL+Y** or, on the toolbar, click the **Redo** icon, or on the **Edit** menu, click **Redo**.</span></span>

## <a name="how-to-save-a-script"></a><span data-ttu-id="6fe3e-170">Сохранение сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-170">How to save a script</span></span>
<span data-ttu-id="6fe3e-171">Используйте следующую процедуру, чтобы сохранить и назвать сценарий.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-171">Use the following steps to save and name a script.</span></span> <span data-ttu-id="6fe3e-172">Звездочка рядом с именем сценария обозначает, что файл не был сохранен после изменения.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-172">An asterisk appears next to the script name to mark a file that has not been saved since it was altered.</span></span> <span data-ttu-id="6fe3e-173">После сохранения звездочка исчезает.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-173">The asterisk disappears when the file is saved.</span></span>

### <a name="to-save-a-script"></a><span data-ttu-id="6fe3e-174">Сохранение сценария</span><span class="sxs-lookup"><span data-stu-id="6fe3e-174">To save a script</span></span>
<span data-ttu-id="6fe3e-175">Нажмите клавиши **CTRL+S**, щелкните значок **Сохранить** на панели инструментов или выберите **Сохранить** в меню **Файл**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-175">Press **CTRL+S** or, on the toolbar, click the **Save** icon, or on the **File** menu, click **Save**.</span></span>

### <a name="to-save-and-name-a-script"></a><span data-ttu-id="6fe3e-176">Сохранение сценария с определенным именем</span><span class="sxs-lookup"><span data-stu-id="6fe3e-176">To save and name a script</span></span>

1. <span data-ttu-id="6fe3e-177">В меню **Файл** выберите команду **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-177">On the **File** menu, click **Save As**.</span></span> <span data-ttu-id="6fe3e-178">Появится диалоговое окно **Сохранить как**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-178">The **Save As** dialog box will appear.</span></span>

2. <span data-ttu-id="6fe3e-179">В поле **Имя файла** введите имя файла.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-179">In the **File name** box, enter a name for the file.</span></span>

3. <span data-ttu-id="6fe3e-180">В поле **Тип файла** выберите тип файла.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-180">In the **Save as type** box, select a file type.</span></span> <span data-ttu-id="6fe3e-181">Например, в поле **Тип файла** выберите "Сценарии PowerShell (\* .ps1)".</span><span class="sxs-lookup"><span data-stu-id="6fe3e-181">For example, in the **Save as type** box, select 'œPowerShell Scripts (\* .ps1)'.</span></span>

4. <span data-ttu-id="6fe3e-182">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-182">Click **Save**.</span></span>

### <a name="to-save-a-script-in-ascii-encoding"></a><span data-ttu-id="6fe3e-183">Сохранение сценария в кодировке ASCII</span><span class="sxs-lookup"><span data-stu-id="6fe3e-183">To save a script in ASCII encoding</span></span>
<span data-ttu-id="6fe3e-184">По умолчанию интегрированная среда сценариев Windows PowerShell сохраняет новые файлы сценариев (PS1), файлы данных сценариев (PSD1) и файлы модулей сценариев (PSM1) в кодировке Юникод (BigEndianUnicode). Чтобы сохранить сценарий в другой кодировке, например ASCII (ANSI), используйте методы **Сохранить** или **Сохранить как** объекта [$psISE.CurrentFile](https://technet.microsoft.com/en-us/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile).</span><span class="sxs-lookup"><span data-stu-id="6fe3e-184">By default, Windows PowerShell ISE saves new script files (.ps1), script data files (.psd1), and script module files (.psm1) as Unicode (BigEndianUnicode) by default.Â To save a script in another encoding, such as ASCII (ANSI), use the **Save** or **SaveAs** methods on the [$psISE.CurrentFile](https://technet.microsoft.com/en-us/library/bc3300e4-9c17-4f00-a621-c8867126e3b3#CurrentFile) object.</span></span>

<span data-ttu-id="6fe3e-185">Следующая команда сохраняет новый сценарий в кодировке ASCII и с именем MyScript.ps1:</span><span class="sxs-lookup"><span data-stu-id="6fe3e-185">The following command saves a new script as MyScript.ps1 with ASCII encoding.</span></span>

```
$psise.CurrentFile.SaveAs("MyScript.ps1", [System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6fe3e-186">Следующая команда заменяет текущий файл сценария на файл с таким же именем, но в кодировке ASCII:</span><span class="sxs-lookup"><span data-stu-id="6fe3e-186">The following command replaces the current script file with a file with the same name, but with ASCII encoding.</span></span>

```
$psise.CurrentFile.Save([System.Text.Encoding]::ASCII)
```

<span data-ttu-id="6fe3e-187">Следующая команда возвращает кодировку текущего файла:</span><span class="sxs-lookup"><span data-stu-id="6fe3e-187">The following command gets the encoding of the current file.</span></span>

```
$psise.CurrentFile.encoding
```

<span data-ttu-id="6fe3e-188">Интегрированная среда сценариев Windows PowerShell поддерживает следующие параметры кодировки: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 и Default.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-188">Windows PowerShell ISE supports the following encoding options: ASCII, BigEndianUnicode, Unicode, UTF32, UTF7, UTF8 and Default.</span></span> <span data-ttu-id="6fe3e-189">Значение параметра Default зависит от системы.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-189">The value of the Default option varies with the system.</span></span>

<span data-ttu-id="6fe3e-190">Интегрированная среда сценариев Windows PowerShell не изменяет кодировку сценариев, созданных в других редакторах, даже при использовании команд "Сохранить" или "Сохранить как" в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fe3e-190">Windows PowerShell ISE does not change the encoding of scripts that were created by in other editors, even when you use the Save or Save As commands in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="6fe3e-191">См. также</span><span class="sxs-lookup"><span data-stu-id="6fe3e-191">See Also</span></span>
- [<span data-ttu-id="6fe3e-192">Обзор интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fe3e-192">Exploring the Windows PowerShell ISE</span></span>](../../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
