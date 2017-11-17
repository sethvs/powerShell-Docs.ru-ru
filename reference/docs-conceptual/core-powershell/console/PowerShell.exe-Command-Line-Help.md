---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Справка по командной строке PowerShell.exe"
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 262c21e44e509746314ed44d91bb3de16a4b854b
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/07/2017
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="9949e-103">Справка по командной строке PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="9949e-103">PowerShell.exe Command-Line Help</span></span>
<span data-ttu-id="9949e-104">Запустите сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-104">a Windows PowerShell session.</span></span> <span data-ttu-id="9949e-105">Вы можете использовать PowerShell.exe для запуска сеанса PowerShell из командной строки другого средства, такого как Cmd.exe, или использовать его в командной строке PowerShell для запуска нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="9949e-105">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="9949e-106">Используйте указанные параметры для настройки сеанса.</span><span class="sxs-lookup"><span data-stu-id="9949e-106">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="9949e-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="9949e-107">Syntax</span></span>

```syntax
PowerShell[.exe]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-File <FilePath> [<Args>]]
       [-InputFormat {Text | XML}] 
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive] 
       [-NoProfile] 
       [-OutputFormat {Text | XML}] 
       [-PSConsoleFile <FilePath> | -Version <PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]
        

PowerShell[.exe] -Help | -? | /?
```

## <a name="parameters"></a><span data-ttu-id="9949e-108">Параметры</span><span class="sxs-lookup"><span data-stu-id="9949e-108">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="9949e-109">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="9949e-109">-EncodedCommand <Base64EncodedCommand></span></span>
<span data-ttu-id="9949e-110">Принимает строковую версию команды в кодировке Base 64.</span><span class="sxs-lookup"><span data-stu-id="9949e-110">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="9949e-111">Используйте этот параметр для отправки в PowerShell команд, требующих сложных кавычек или фигурных скобок.</span><span class="sxs-lookup"><span data-stu-id="9949e-111">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="9949e-112">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="9949e-112">-ExecutionPolicy <ExecutionPolicy></span></span>
<span data-ttu-id="9949e-113">Задает политику выполнения по умолчанию для текущего сеанса и сохраняет ее в переменной среды $env:PSExecutionPolicyPreference.</span><span class="sxs-lookup"><span data-stu-id="9949e-113">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="9949e-114">Этот параметр не изменяет политику выполнения PowerShell, заданную в реестре.</span><span class="sxs-lookup"><span data-stu-id="9949e-114">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="9949e-115">Дополнительные сведения о политиках выполнения PowerShell, включая список допустимых значений, см. в статье about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span><span class="sxs-lookup"><span data-stu-id="9949e-115">For information about PowerShell execution policies, including a list of valid values, see about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="9949e-116">-File <FilePath> \[<Parameters>]</span><span class="sxs-lookup"><span data-stu-id="9949e-116">-File <FilePath> \[<Parameters>]</span></span>
<span data-ttu-id="9949e-117">Запускает указанный сценарий в локальной области ("с точкой"), чтобы создаваемые сценарием функции и переменные были доступны в текущем сеансе.</span><span class="sxs-lookup"><span data-stu-id="9949e-117">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="9949e-118">Введите путь к файлу сценария и любые параметры.</span><span class="sxs-lookup"><span data-stu-id="9949e-118">Enter the script file path and any parameters.</span></span> <span data-ttu-id="9949e-119">Параметр **File** должен быть последним в команде, поскольку все символы, введенные после параметра **File**, интерпретируются как путь к файлу сценария и следующие за ним параметры сценария.</span><span class="sxs-lookup"><span data-stu-id="9949e-119">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="9949e-120">Параметры сценария и их значения можно включить в значение параметра **File**.</span><span class="sxs-lookup"><span data-stu-id="9949e-120">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="9949e-121">Пример: `-File .\Get-Script.ps1 -Domain Central`. Обратите внимание, что передаваемые в сценарий параметры имеют вид строк литералов (после интерпретации текущей оболочкой).</span><span class="sxs-lookup"><span data-stu-id="9949e-121">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="9949e-122">Например, если вы находитесь в cmd.exe и хотите передать значение переменной среды, используйте синтаксис cmd.exe: `powershell -File .\test.ps1 -Sample %windir%`. Если вы используете синтаксис PowerShell, в этом примере сценарий получит литерал "$env:windir", а не значение этой переменной среды: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="9949e-122">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="9949e-123">Обычно параметры-переключатели сценария включаются или опускаются.</span><span class="sxs-lookup"><span data-stu-id="9949e-123">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="9949e-124">Например, приведенная ниже команда использует параметр **All** файла сценария Get-Script.ps1: `-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="9949e-124">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="9949e-125">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="9949e-125">\-InputFormat {Text | XML}</span></span>
<span data-ttu-id="9949e-126">Описывает формат данных, отправляемых в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-126">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="9949e-127">Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).</span><span class="sxs-lookup"><span data-stu-id="9949e-127">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="9949e-128">-Mta</span><span class="sxs-lookup"><span data-stu-id="9949e-128">-Mta</span></span>
<span data-ttu-id="9949e-129">Запускает PowerShell с использованием многопотокового подразделения.</span><span class="sxs-lookup"><span data-stu-id="9949e-129">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="9949e-130">Этот параметр впервые появился в PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="9949e-130">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="9949e-131">В PowerShell 3.0 по умолчанию используется однопотоковое подразделение (STA).</span><span class="sxs-lookup"><span data-stu-id="9949e-131">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="9949e-132">В PowerShell 2.0 по умолчанию используется многопотоковое подразделение (MTA).</span><span class="sxs-lookup"><span data-stu-id="9949e-132">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="9949e-133">-NoExit</span><span class="sxs-lookup"><span data-stu-id="9949e-133">-NoExit</span></span>
<span data-ttu-id="9949e-134">Не завершает работу после выполнения команд запуска.</span><span class="sxs-lookup"><span data-stu-id="9949e-134">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="9949e-135">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="9949e-135">-NoLogo</span></span>
<span data-ttu-id="9949e-136">Скрывает баннер авторских прав при запуске программы.</span><span class="sxs-lookup"><span data-stu-id="9949e-136">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="9949e-137">-NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9949e-137">-NonInteractive</span></span>
<span data-ttu-id="9949e-138">Не предоставляет пользователю интерактивную командную строку.</span><span class="sxs-lookup"><span data-stu-id="9949e-138">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="9949e-139">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="9949e-139">-NoProfile</span></span>
<span data-ttu-id="9949e-140">Не загружает профиль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-140">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="9949e-141">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="9949e-141">-OutputFormat {Text | XML}</span></span>
<span data-ttu-id="9949e-142">Определяет формат выходных данных PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-142">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="9949e-143">Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).</span><span class="sxs-lookup"><span data-stu-id="9949e-143">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="9949e-144">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="9949e-144">-PSConsoleFile <FilePath></span></span>
<span data-ttu-id="9949e-145">Загружает указанный файл консоли PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-145">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="9949e-146">Введите путь и имя файла консоли.</span><span class="sxs-lookup"><span data-stu-id="9949e-146">Enter the path and name of the console file.</span></span> <span data-ttu-id="9949e-147">Для создания файла консоли используйте командлет [Export-Console](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-147">To create a console file, use the [Export-Console](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="9949e-148">-Sta</span><span class="sxs-lookup"><span data-stu-id="9949e-148">-Sta</span></span>
<span data-ttu-id="9949e-149">Запускает PowerShell с использованием многопотокового подразделения.</span><span class="sxs-lookup"><span data-stu-id="9949e-149">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="9949e-150">В PowerShell 3.0 по умолчанию используется однопотоковое подразделение (STA).</span><span class="sxs-lookup"><span data-stu-id="9949e-150">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="9949e-151">В PowerShell 2.0 по умолчанию используется многопотоковое подразделение (MTA).</span><span class="sxs-lookup"><span data-stu-id="9949e-151">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="9949e-152">-Version <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="9949e-152">-Version <PowerShell Version></span></span>
<span data-ttu-id="9949e-153">Запускает заданную версию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-153">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="9949e-154">Указанная версия должна быть установлена в системе.</span><span class="sxs-lookup"><span data-stu-id="9949e-154">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="9949e-155">Если на компьютере установлен PowerShell 3.0, допустимыми значениями являются "3.0" и "2.0".</span><span class="sxs-lookup"><span data-stu-id="9949e-155">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="9949e-156">По умолчанию используется значение "3.0".</span><span class="sxs-lookup"><span data-stu-id="9949e-156">The default value is "3.0".</span></span>

<span data-ttu-id="9949e-157">Если PowerShell 3.0 не установлен, допустимо только значение "2.0".</span><span class="sxs-lookup"><span data-stu-id="9949e-157">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="9949e-158">Другие значения игнорируются.</span><span class="sxs-lookup"><span data-stu-id="9949e-158">Other values are ignored.</span></span>

<span data-ttu-id="9949e-159">Дополнительные сведения см. в разделе "Установка PowerShell" статьи [Начало работы с PowerShell [старый MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span><span class="sxs-lookup"><span data-stu-id="9949e-159">For more information, see "Installing PowerShell" in the [Getting Started with PowerShell [OLD MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="9949e-160">-WindowStyle <Window style></span><span class="sxs-lookup"><span data-stu-id="9949e-160">-WindowStyle <Window style></span></span>
<span data-ttu-id="9949e-161">Задает стиль окна для сеанса.</span><span class="sxs-lookup"><span data-stu-id="9949e-161">Sets the window style for the session.</span></span> <span data-ttu-id="9949e-162">Допустимые значения: Normal, Minimized, Maximized и Hidden.</span><span class="sxs-lookup"><span data-stu-id="9949e-162">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="9949e-163">-Command</span><span class="sxs-lookup"><span data-stu-id="9949e-163">-Command</span></span>
<span data-ttu-id="9949e-164">Выполняет указанные команды (вместе с параметрами) как введенные в командной строке PowerShell и завершает работу, если не указан параметр NoExit.</span><span class="sxs-lookup"><span data-stu-id="9949e-164">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="9949e-165">В сущности, любой текст после `-Command` отправляется в PowerShell в виде одной командной строки (это поведение отличается от того, как отправляемые в сценарий параметры обрабатываются `-File`).</span><span class="sxs-lookup"><span data-stu-id="9949e-165">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="9949e-166">Значением Command может быть строка "-".</span><span class="sxs-lookup"><span data-stu-id="9949e-166">The value of Command can be "-", a string.</span></span> <span data-ttu-id="9949e-167">или блок сценария.</span><span class="sxs-lookup"><span data-stu-id="9949e-167">or a script block.</span></span> <span data-ttu-id="9949e-168">Если для Command задано значение "-", текст команды считывается из стандартного ввода.</span><span class="sxs-lookup"><span data-stu-id="9949e-168">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="9949e-169">Блоки сценариев должны быть заключены в фигурные скобки ({}).</span><span class="sxs-lookup"><span data-stu-id="9949e-169">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="9949e-170">Указать блок сценария можно только при использовании PowerShell.exe в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9949e-170">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="9949e-171">Результаты сценария возвращаются родительской оболочке как десериализованные объекты XML, а не как активные объекты.</span><span class="sxs-lookup"><span data-stu-id="9949e-171">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="9949e-172">Если значением Command является строка, параметр **Command** должен быть последним в команде, так как любой знак, введенный после команды, интерпретируется как ее аргумент.</span><span class="sxs-lookup"><span data-stu-id="9949e-172">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="9949e-173">При написании строки для запуска команды PowerShell используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="9949e-173">To write a string that runs a PowerShell command, use the format:</span></span>

```
"& {<command>}"
```

<span data-ttu-id="9949e-174">где кавычки отделяют строку, а оператор вызова (&) запускает выполнение команды.</span><span class="sxs-lookup"><span data-stu-id="9949e-174">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="9949e-175">-Help, -?, /?</span><span class="sxs-lookup"><span data-stu-id="9949e-175">-Help, -?, /?</span></span>
<span data-ttu-id="9949e-176">Показывает это сообщение.</span><span class="sxs-lookup"><span data-stu-id="9949e-176">Shows this message.</span></span> <span data-ttu-id="9949e-177">При вводе команды PowerShell.exe в PowerShell добавляйте в начало параметров команды дефис (-), а не косую черту (/).</span><span class="sxs-lookup"><span data-stu-id="9949e-177">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="9949e-178">В Cmd.exe можно использовать как дефис, так и косую черту.</span><span class="sxs-lookup"><span data-stu-id="9949e-178">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="9949e-179">Замечание по устранению неполадок. Обратите внимание, что в PowerShell 2.0 запуск некоторых программ в консоли Windows PowerShell завершается ошибкой с кодом LastExitCode 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="9949e-179">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="9949e-180">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="9949e-180">EXAMPLES</span></span>

```
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a Powerhell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate wayh to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```

