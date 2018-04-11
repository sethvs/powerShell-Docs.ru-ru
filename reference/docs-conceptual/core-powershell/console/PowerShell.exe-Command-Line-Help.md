---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Справка по командной строке PowerShell.exe
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 60b6a7e310821a4092b0972b7abbdae0e2d5f738
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="5be0a-103">Справка по командной строке PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="5be0a-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="5be0a-104">Вы можете использовать PowerShell.exe для запуска сеанса PowerShell из командной строки другого средства, такого как Cmd.exe, или использовать его в командной строке PowerShell для запуска нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="5be0a-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="5be0a-105">Используйте указанные параметры для настройки сеанса.</span><span class="sxs-lookup"><span data-stu-id="5be0a-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="5be0a-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5be0a-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="5be0a-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="5be0a-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="5be0a-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="5be0a-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="5be0a-109">Принимает строковую версию команды в кодировке Base 64.</span><span class="sxs-lookup"><span data-stu-id="5be0a-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="5be0a-110">Используйте этот параметр для отправки в PowerShell команд, требующих сложных кавычек или фигурных скобок.</span><span class="sxs-lookup"><span data-stu-id="5be0a-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="5be0a-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="5be0a-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="5be0a-112">Задает политику выполнения по умолчанию для текущего сеанса и сохраняет ее в переменной среды $env:PSExecutionPolicyPreference.</span><span class="sxs-lookup"><span data-stu-id="5be0a-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="5be0a-113">Этот параметр не изменяет политику выполнения PowerShell, заданную в реестре.</span><span class="sxs-lookup"><span data-stu-id="5be0a-113">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="5be0a-114">Дополнительные сведения о политиках выполнения PowerShell, включая список допустимых значений, см. в статье [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="5be0a-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="5be0a-115">-File <FilePath> \[<Parameters>]</span><span class="sxs-lookup"><span data-stu-id="5be0a-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="5be0a-116">Запускает указанный сценарий в локальной области ("с точкой"), чтобы создаваемые сценарием функции и переменные были доступны в текущем сеансе.</span><span class="sxs-lookup"><span data-stu-id="5be0a-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="5be0a-117">Введите путь к файлу сценария и любые параметры.</span><span class="sxs-lookup"><span data-stu-id="5be0a-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="5be0a-118">Параметр **File** должен быть последним в команде, поскольку все символы, введенные после параметра **File**, интерпретируются как путь к файлу сценария и следующие за ним параметры сценария.</span><span class="sxs-lookup"><span data-stu-id="5be0a-118">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="5be0a-119">Параметры сценария и их значения можно включить в значение параметра **File**.</span><span class="sxs-lookup"><span data-stu-id="5be0a-119">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="5be0a-120">Пример: `-File .\Get-Script.ps1 -Domain Central`. Обратите внимание, что передаваемые в сценарий параметры имеют вид строк литералов (после интерпретации текущей оболочкой).</span><span class="sxs-lookup"><span data-stu-id="5be0a-120">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="5be0a-121">Например, если вы находитесь в cmd.exe и хотите передать значение переменной среды, используйте синтаксис cmd.exe: `powershell -File .\test.ps1 -Sample %windir%`. Если вы используете синтаксис PowerShell, в этом примере сценарий получит литерал "$env:windir", а не значение этой переменной среды: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="5be0a-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="5be0a-122">Обычно параметры-переключатели сценария включаются или опускаются.</span><span class="sxs-lookup"><span data-stu-id="5be0a-122">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="5be0a-123">Например, приведенная ниже команда использует параметр **All** файла сценария Get-Script.ps1: `-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="5be0a-123">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="5be0a-124">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="5be0a-124">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="5be0a-125">Описывает формат данных, отправляемых в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-125">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="5be0a-126">Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).</span><span class="sxs-lookup"><span data-stu-id="5be0a-126">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="5be0a-127">-Mta</span><span class="sxs-lookup"><span data-stu-id="5be0a-127">-Mta</span></span>

<span data-ttu-id="5be0a-128">Запускает PowerShell с использованием многопотокового подразделения.</span><span class="sxs-lookup"><span data-stu-id="5be0a-128">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="5be0a-129">Этот параметр впервые появился в PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="5be0a-129">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="5be0a-130">В PowerShell 3.0 по умолчанию используется однопотоковое подразделение (STA).</span><span class="sxs-lookup"><span data-stu-id="5be0a-130">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="5be0a-131">В PowerShell 2.0 по умолчанию используется многопотоковое подразделение (MTA).</span><span class="sxs-lookup"><span data-stu-id="5be0a-131">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="5be0a-132">-NoExit</span><span class="sxs-lookup"><span data-stu-id="5be0a-132">-NoExit</span></span>

<span data-ttu-id="5be0a-133">Не завершает работу после выполнения команд запуска.</span><span class="sxs-lookup"><span data-stu-id="5be0a-133">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="5be0a-134">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="5be0a-134">-NoLogo</span></span>

<span data-ttu-id="5be0a-135">Скрывает баннер авторских прав при запуске программы.</span><span class="sxs-lookup"><span data-stu-id="5be0a-135">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="5be0a-136">-NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5be0a-136">-NonInteractive</span></span>

<span data-ttu-id="5be0a-137">Не предоставляет пользователю интерактивную командную строку.</span><span class="sxs-lookup"><span data-stu-id="5be0a-137">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="5be0a-138">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="5be0a-138">-NoProfile</span></span>

<span data-ttu-id="5be0a-139">Не загружает профиль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-139">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="5be0a-140">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="5be0a-140">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="5be0a-141">Определяет формат выходных данных PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-141">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="5be0a-142">Допустимые значения: "Text" (текстовые строки) или "XML" (сериализованный формат CLIXML).</span><span class="sxs-lookup"><span data-stu-id="5be0a-142">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="5be0a-143">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="5be0a-143">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="5be0a-144">Загружает указанный файл консоли PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-144">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="5be0a-145">Введите путь и имя файла консоли.</span><span class="sxs-lookup"><span data-stu-id="5be0a-145">Enter the path and name of the console file.</span></span> <span data-ttu-id="5be0a-146">Чтобы создать файл консоли, используйте командлет [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-146">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="5be0a-147">-Sta</span><span class="sxs-lookup"><span data-stu-id="5be0a-147">-Sta</span></span>

<span data-ttu-id="5be0a-148">Запускает PowerShell с использованием многопотокового подразделения.</span><span class="sxs-lookup"><span data-stu-id="5be0a-148">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="5be0a-149">В PowerShell 3.0 по умолчанию используется однопотоковое подразделение (STA).</span><span class="sxs-lookup"><span data-stu-id="5be0a-149">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="5be0a-150">В PowerShell 2.0 по умолчанию используется многопотоковое подразделение (MTA).</span><span class="sxs-lookup"><span data-stu-id="5be0a-150">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="5be0a-151">-Version <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="5be0a-151">-Version <PowerShell Version></span></span>

<span data-ttu-id="5be0a-152">Запускает заданную версию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-152">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="5be0a-153">Указанная версия должна быть установлена в системе.</span><span class="sxs-lookup"><span data-stu-id="5be0a-153">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="5be0a-154">Если на компьютере установлен PowerShell 3.0, допустимыми значениями являются "3.0" и "2.0".</span><span class="sxs-lookup"><span data-stu-id="5be0a-154">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="5be0a-155">По умолчанию используется значение "3.0".</span><span class="sxs-lookup"><span data-stu-id="5be0a-155">The default value is "3.0".</span></span>

<span data-ttu-id="5be0a-156">Если PowerShell 3.0 не установлен, допустимо только значение "2.0".</span><span class="sxs-lookup"><span data-stu-id="5be0a-156">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="5be0a-157">Другие значения игнорируются.</span><span class="sxs-lookup"><span data-stu-id="5be0a-157">Other values are ignored.</span></span>

<span data-ttu-id="5be0a-158">Дополнительные сведения см. в статье "[Установка Windows PowerShell](../../setup/installing-windows-powershell.md)".</span><span class="sxs-lookup"><span data-stu-id="5be0a-158">For more information, see "[Installing Windows PowerShell](../../setup/installing-windows-powershell.md)".</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="5be0a-159">-WindowStyle <Window style></span><span class="sxs-lookup"><span data-stu-id="5be0a-159">-WindowStyle <Window style></span></span>

<span data-ttu-id="5be0a-160">Задает стиль окна для сеанса.</span><span class="sxs-lookup"><span data-stu-id="5be0a-160">Sets the window style for the session.</span></span> <span data-ttu-id="5be0a-161">Допустимые значения: Normal, Minimized, Maximized и Hidden.</span><span class="sxs-lookup"><span data-stu-id="5be0a-161">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="5be0a-162">-Command</span><span class="sxs-lookup"><span data-stu-id="5be0a-162">-Command</span></span>

<span data-ttu-id="5be0a-163">Выполняет указанные команды (вместе с параметрами) как введенные в командной строке PowerShell и завершает работу, если не указан параметр NoExit.</span><span class="sxs-lookup"><span data-stu-id="5be0a-163">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="5be0a-164">В сущности, любой текст после `-Command` отправляется в PowerShell в виде одной командной строки (это поведение отличается от того, как отправляемые в сценарий параметры обрабатываются `-File`).</span><span class="sxs-lookup"><span data-stu-id="5be0a-164">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="5be0a-165">Значением Command может быть строка "-".</span><span class="sxs-lookup"><span data-stu-id="5be0a-165">The value of Command can be "-", a string.</span></span> <span data-ttu-id="5be0a-166">или блок сценария.</span><span class="sxs-lookup"><span data-stu-id="5be0a-166">or a script block.</span></span> <span data-ttu-id="5be0a-167">Если для Command задано значение "-", текст команды считывается из стандартного ввода.</span><span class="sxs-lookup"><span data-stu-id="5be0a-167">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="5be0a-168">Блоки сценариев должны быть заключены в фигурные скобки ({}).</span><span class="sxs-lookup"><span data-stu-id="5be0a-168">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="5be0a-169">Указать блок сценария можно только при использовании PowerShell.exe в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5be0a-169">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="5be0a-170">Результаты сценария возвращаются родительской оболочке как десериализованные объекты XML, а не как активные объекты.</span><span class="sxs-lookup"><span data-stu-id="5be0a-170">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="5be0a-171">Если значением Command является строка, параметр **Command** должен быть последним в команде, так как любой знак, введенный после команды, интерпретируется как ее аргумент.</span><span class="sxs-lookup"><span data-stu-id="5be0a-171">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="5be0a-172">При написании строки для запуска команды PowerShell используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="5be0a-172">To write a string that runs a PowerShell command, use the format:</span></span>

```powershell
"& {<command>}"
```

<span data-ttu-id="5be0a-173">где кавычки отделяют строку, а оператор вызова (&) запускает выполнение команды.</span><span class="sxs-lookup"><span data-stu-id="5be0a-173">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="5be0a-174">-Help, -?, /?</span><span class="sxs-lookup"><span data-stu-id="5be0a-174">-Help, -?, /?</span></span>

<span data-ttu-id="5be0a-175">Показывает это сообщение.</span><span class="sxs-lookup"><span data-stu-id="5be0a-175">Shows this message.</span></span> <span data-ttu-id="5be0a-176">При вводе команды PowerShell.exe в PowerShell добавляйте в начало параметров команды дефис (-), а не косую черту (/).</span><span class="sxs-lookup"><span data-stu-id="5be0a-176">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="5be0a-177">В Cmd.exe можно использовать как дефис, так и косую черту.</span><span class="sxs-lookup"><span data-stu-id="5be0a-177">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="5be0a-178">Замечание по устранению неполадок. Обратите внимание, что в PowerShell 2.0 запуск некоторых программ в консоли Windows PowerShell завершается ошибкой с кодом LastExitCode 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="5be0a-178">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="5be0a-179">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="5be0a-179">EXAMPLES</span></span>

```powershell
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a PowerShell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate way to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```