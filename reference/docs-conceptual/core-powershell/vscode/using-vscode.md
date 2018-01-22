# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="c32e0-101">Использование Visual Studio Code для разработки в PowerShell</span><span class="sxs-lookup"><span data-stu-id="c32e0-101">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="c32e0-102">В дополнение к [интегрированной среде сценариев PowerShell][ise] продукт PowerShell также хорошо поддерживается в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c32e0-102">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="c32e0-103">Кроме того, интегрированная среда сценариев не поддерживается в PowerShell Core, хотя Visual Studio Code поддерживается для PowerShell Core на всех платформах (Windows, macOS и Linux)</span><span class="sxs-lookup"><span data-stu-id="c32e0-103">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="c32e0-104">Вы можете использовать Visual Studio Code для Windows вместе с PowerShell версии 5 в Windows 10 или установить [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для более низких версий Windows (например, Windows 8.1 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c32e0-104">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="c32e0-105">Перед запуском убедитесь, что PowerShell установлен в системе.</span><span class="sxs-lookup"><span data-stu-id="c32e0-105">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="c32e0-106">Сведения о современных рабочих нагрузках для Windows, macOS и Linux см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="c32e0-106">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="c32e0-107">[Установка PowerShell Core в macOS и Linux][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="c32e0-107">[Installing PowerShell Core on macOS and Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="c32e0-108">[Установка PowerShell Core в Windows][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="c32e0-108">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="c32e0-109">Сведения о традиционных рабочих нагрузках Windows PowerShell см. в разделе [Установка Windows PowerShell][install-winps].</span><span class="sxs-lookup"><span data-stu-id="c32e0-109">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="c32e0-110">Редактирование с помощью Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c32e0-110">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="c32e0-111">1. Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c32e0-111">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="c32e0-112">**Linux**: следуйте инструкциям по установке на странице [Запуск VS Code в Linux](https://code.visualstudio.com/docs/setup/linux).</span><span class="sxs-lookup"><span data-stu-id="c32e0-112">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="c32e0-113">**macOS**: следуйте инструкциям по установке на странице [Запуск VS Code в macOS](https://code.visualstudio.com/docs/setup/mac).</span><span class="sxs-lookup"><span data-stu-id="c32e0-113">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c32e0-114">В macOS нужно установить OpenSSL для правильной работы расширения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c32e0-114">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
> <span data-ttu-id="c32e0-115">Для этого проще всего установить [Homebrew](http://brew.sh/), а затем запустить `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="c32e0-115">The easiest way to accomplish this is to install [Homebrew](http://brew.sh/) and then run `brew install openssl`.</span></span>
> <span data-ttu-id="c32e0-116">После этого расширение PowerShell будет загружено правильно.</span><span class="sxs-lookup"><span data-stu-id="c32e0-116">The PowerShell extension will now be able to load successfully.</span></span>

- <span data-ttu-id="c32e0-117">**Windows**: следуйте инструкциям по установке на странице [Запуск VS Code в Windows](https://code.visualstudio.com/docs/setup/windows).</span><span class="sxs-lookup"><span data-stu-id="c32e0-117">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="c32e0-118">2. Установка расширения PowerShell</span><span class="sxs-lookup"><span data-stu-id="c32e0-118">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="c32e0-119">Запустите Visual Studio Code следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c32e0-119">Launch the Visual Studio Code app by:</span></span>
    - <span data-ttu-id="c32e0-120">**Windows**: введите `code` в сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c32e0-120">**Windows**: typing `code` in your PowerShell session</span></span>
    - <span data-ttu-id="c32e0-121">**Linux**: введите `code` в терминале.</span><span class="sxs-lookup"><span data-stu-id="c32e0-121">**Linux**: typing `code` in your terminal</span></span>
    - <span data-ttu-id="c32e0-122">**macOS**: введите `code` в терминале.</span><span class="sxs-lookup"><span data-stu-id="c32e0-122">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="c32e0-123">Запустите **Quick Open**, нажав клавиши **CTRL+P** (**CMD+P** на Mac).</span><span class="sxs-lookup"><span data-stu-id="c32e0-123">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="c32e0-124">В Quick Open введите `ext install powershell` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-124">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="c32e0-125">На боковой панели открывается представление **Расширения**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-125">The **Extensions** view will open on the Side Bar.</span></span> <span data-ttu-id="c32e0-126">Выберите расширение PowerShell корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c32e0-126">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="c32e0-127">Вы увидите примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="c32e0-127">You will see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="c32e0-129">Нажмите кнопку **Установить** для расширения PowerShell корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c32e0-129">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="c32e0-130">После установки кнопка **Установить** изменится на **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-130">After the install, you will see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="c32e0-131">Нажмите кнопку **Перезагрузить**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-131">Click on **Reload**.</span></span>
- <span data-ttu-id="c32e0-132">После перезагрузки Visual Studio Code можно приступать к редактированию.</span><span class="sxs-lookup"><span data-stu-id="c32e0-132">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="c32e0-133">Например, чтобы создать файл, выберите **Файл -> Создать**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-133">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="c32e0-134">Чтобы сохранить его, выберите **Файл -> Сохранить** и укажите имя файла, например `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c32e0-134">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="c32e0-135">Чтобы закрыть файл, щелкните "x" рядом с его именем.</span><span class="sxs-lookup"><span data-stu-id="c32e0-135">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="c32e0-136">Чтобы завершить работу Visual Studio Code, выберите **Файл -> Выйти**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-136">To exit Visual Studio Code, **File->Exit**.</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="c32e0-137">Использование определенной установленной версии PowerShell</span><span class="sxs-lookup"><span data-stu-id="c32e0-137">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="c32e0-138">Если вы хотите использовать с Visual Studio Code определенную установку PowerShell, нужно добавить в файл параметров пользователя новую переменную.</span><span class="sxs-lookup"><span data-stu-id="c32e0-138">If you wish to use a specific installation of PowerShell with Visual Studio Code, you will need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="c32e0-139">Щелкните **Файл -> Параметры -> Параметры**</span><span class="sxs-lookup"><span data-stu-id="c32e0-139">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="c32e0-140">Отображаются две панели редактора.</span><span class="sxs-lookup"><span data-stu-id="c32e0-140">Two editor panes will appear.</span></span>
   <span data-ttu-id="c32e0-141">На панели справа (`settings.json`) вставьте параметр в разделе соответствующей операционной системы между двумя фигурными скобками (`{` и `}`) и замените *<version>* на установленную версию PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c32e0-141">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace *<version>* with the installed PowerShell version:</span></span>

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. <span data-ttu-id="c32e0-142">Замените параметр на путь к требуемому исполняемому файлу PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c32e0-142">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="c32e0-143">Сохраните файл параметров и перезапустите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c32e0-143">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="c32e0-144">Параметры конфигурации для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c32e0-144">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="c32e0-145">Следуя инструкциям в предыдущем абзаце, вы можете добавить параметры конфигурации в `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="c32e0-145">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="c32e0-146">Мы рекомендуем использовать следующие параметры конфигурации для Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c32e0-146">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="c32e0-147">Отладка с помощью Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c32e0-147">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="c32e0-148">Отладка без рабочей области</span><span class="sxs-lookup"><span data-stu-id="c32e0-148">No-workspace debugging</span></span>

<span data-ttu-id="c32e0-149">Начиная с Visual Studio Code версии 1.9, вы можете отлаживать сценарии PowerShell, не открывая папку со сценарием PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c32e0-149">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span>
<span data-ttu-id="c32e0-150">Просто откройте файл сценария PowerShell с помощью команды **Файл -> Открыть файл...** , установите точку останова на строке (нажав клавишу F9) и нажмите клавишу F5 для запуска отладки.</span><span class="sxs-lookup"><span data-stu-id="c32e0-150">Simply open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span>
<span data-ttu-id="c32e0-151">Отображается панель действий отладки, позволяющая прервать работу отладчика, возобновить отладку, выполнить ее пошагово или остановить.</span><span class="sxs-lookup"><span data-stu-id="c32e0-151">You will see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="c32e0-152">Отладка с рабочей областью</span><span class="sxs-lookup"><span data-stu-id="c32e0-152">Workspace debugging</span></span>

<span data-ttu-id="c32e0-153">Отладка с рабочей областью обозначает отладку в контексте папки, которую вы открыли в Visual Studio Code с помощью команды **Открыть папку...** из меню **Файл**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-153">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="c32e0-154">Обычно открытая папка является папкой проекта PowerShell и (или) корнем репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="c32e0-154">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="c32e0-155">Даже в этом режиме вы можете начать отладку выбранного сценария PowerShell, просто нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="c32e0-155">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="c32e0-156">Однако отладка с рабочей областью позволяет задать несколько конфигураций отладки, отличных от простой отладки открытого файла.</span><span class="sxs-lookup"><span data-stu-id="c32e0-156">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="c32e0-157">Например, можно добавить конфигурации следующего характера:</span><span class="sxs-lookup"><span data-stu-id="c32e0-157">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="c32e0-158">Запуск тестов Pester в отладчике</span><span class="sxs-lookup"><span data-stu-id="c32e0-158">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="c32e0-159">Запуск определенного файла с аргументами в отладчике</span><span class="sxs-lookup"><span data-stu-id="c32e0-159">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="c32e0-160">Запуск интерактивного сеанса в отладчике</span><span class="sxs-lookup"><span data-stu-id="c32e0-160">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="c32e0-161">Подключение отладчика к хост-процессу PowerShell</span><span class="sxs-lookup"><span data-stu-id="c32e0-161">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="c32e0-162">Выполните следующие действия, чтобы создать файл конфигурации отладки:</span><span class="sxs-lookup"><span data-stu-id="c32e0-162">Follow these steps to create your debug configuration file:</span></span>

1. <span data-ttu-id="c32e0-163">Откройте представление **Отладка**, нажав клавиши **CTRL+SHIFT+D** (**CMD+SHIFT+D** на Mac).</span><span class="sxs-lookup"><span data-stu-id="c32e0-163">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
1. <span data-ttu-id="c32e0-164">Щелкните значок с шестеренкой **Настройка** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="c32e0-164">Press the **Configure** gear icon in the toolbar.</span></span>
1. <span data-ttu-id="c32e0-165">Visual Studio Code предлагает вам **выбрать среду**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-165">Visual Studio Code will prompt you to **Select Environment**.</span></span>
   <span data-ttu-id="c32e0-166">Выберите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-166">Choose **PowerShell**.</span></span>

   <span data-ttu-id="c32e0-167">При этом Visual Studio Code создает каталог и файл ".vscode\launch.json" в корневой папке рабочей области.</span><span class="sxs-lookup"><span data-stu-id="c32e0-167">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
   <span data-ttu-id="c32e0-168">Именно там хранится ваша конфигурация отладки.</span><span class="sxs-lookup"><span data-stu-id="c32e0-168">This is where your debug configuration is stored.</span></span> <span data-ttu-id="c32e0-169">Если ваши файлы хранятся в репозитории Git, скорее всего, вы захотите зафиксировать файл launch.json.</span><span class="sxs-lookup"><span data-stu-id="c32e0-169">If your files are in a Git repository, you will typically want to commit the launch.json file.</span></span>
   <span data-ttu-id="c32e0-170">Файла launch.json содержит следующее:</span><span class="sxs-lookup"><span data-stu-id="c32e0-170">The contents of the launch.json file are:</span></span>

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Launch (current file)",
            "script": "${file}",
            "args": [],
            "cwd": "${file}"
        },
        {
            "type": "PowerShell",
            "request": "attach",
            "name": "PowerShell Attach to Host Process",
            "processId": "${command.PickPSHostProcess}",
            "runspaceId": 1
        },
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Interactive Session",
            "cwd": "${workspaceRoot}"
        }
    ]
}
```

<span data-ttu-id="c32e0-171">Это представляет типичные сценарии отладки.</span><span class="sxs-lookup"><span data-stu-id="c32e0-171">This represents the common debug scenarios.</span></span>
<span data-ttu-id="c32e0-172">Однако при открытии этого файла в редакторе вы увидите кнопку **Добавить конфигурацию...**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-172">However, when you open this file in the editor, you will see an **Add Configuration...** button.</span></span>
<span data-ttu-id="c32e0-173">Можете нажать ее, чтобы добавить дополнительные конфигурации отладки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c32e0-173">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="c32e0-174">Одной из полезных конфигураций является **PowerShell: Launch Script**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-174">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
<span data-ttu-id="c32e0-175">С помощью этой конфигурации можно указать определенный файл с дополнительными аргументами, которые нужно запускать при каждом нажатии клавиши F5 независимо от того, какой именно файл активен в редакторе.</span><span class="sxs-lookup"><span data-stu-id="c32e0-175">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

<span data-ttu-id="c32e0-176">После задания конфигурации отладки можно указать конфигурацию, используемую во время сеанса отладки, выбрав ее в раскрывающемся списке конфигураций отладки на панели инструментов представления **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="c32e0-176">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="c32e0-177">Существует несколько блогов, которые могут оказаться полезными при начале работы с расширением PowerShell для Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="c32e0-177">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code</span></span>

- <span data-ttu-id="c32e0-178">Visual Studio Code: [расширение PowerShell][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="c32e0-178">Visual Studio Code: [PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="c32e0-179">[Написание и отладка в сценариев PowerShell в Visual Studio Code][debug]</span><span class="sxs-lookup"><span data-stu-id="c32e0-179">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="c32e0-180">[Руководство по отладке Visual Studio Code][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="c32e0-180">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="c32e0-181">[Отладка PowerShell в Visual Studio Code][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="c32e0-181">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="c32e0-182">[Приступая к разработке PowerShell в Visual Studio Code][getting-started]</span><span class="sxs-lookup"><span data-stu-id="c32e0-182">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="c32e0-183">[Функции редактирования Visual Studio Code для разработки PowerShell. Часть 1][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="c32e0-183">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="c32e0-184">[Функции редактирования Visual Studio Code для разработки PowerShell. Часть 2][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="c32e0-184">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="c32e0-185">[Отладка сценария PowerShell в Visual Studio Code. Часть 1][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="c32e0-185">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="c32e0-186">[Отладка сценария PowerShell в Visual Studio Code. Часть 2][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="c32e0-186">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-macOS-and-Linux.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]:https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]:https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]:https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]:https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]:https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="c32e0-187">Расширение PowerShell для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c32e0-187">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="c32e0-188">Исходный код расширения PowerShell доступен на [GitHub](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="c32e0-188">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>
