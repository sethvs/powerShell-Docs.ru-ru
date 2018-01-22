# <a name="ws-management-wsman-remoting-in-powershell-core"></a><span data-ttu-id="d5dd9-101">Удаленное взаимодействие с WS-Management (WSMan) в PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="d5dd9-101">WS-Management (WSMan) Remoting in PowerShell Core</span></span> 

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="d5dd9-102">Инструкции по созданию конечной точки удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="d5dd9-102">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="d5dd9-103">Пакет PowerShell Core для Windows включает подключаемый модуль WinRM (`pwrshplugin.dll`) и сценарий установки (`Install-PowerShellRemoting.ps1`) в `$PSHome`.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-103">The PowerShell Core package for Windows includes a WinRM plug-in (`pwrshplugin.dll`) and an installation script (`Install-PowerShellRemoting.ps1`) in `$PSHome`.</span></span>
<span data-ttu-id="d5dd9-104">Эти файлы позволяют PowerShell принимать входящие удаленные подключения PowerShell, когда указана его конечная точка.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-104">These files enable PowerShell to accept incoming PowerShell remote connections when its endpoint is specified.</span></span>

### <a name="motivation"></a><span data-ttu-id="d5dd9-105">Причины для использования</span><span class="sxs-lookup"><span data-stu-id="d5dd9-105">Motivation</span></span>

<span data-ttu-id="d5dd9-106">Установка PowerShell может устанавливать удаленные сеансы PowerShell с компьютерами, используя `New-PSSession` и `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-106">An installation of PowerShell can establish PowerShell sessions to remote computers using `New-PSSession` and `Enter-PSSession`.</span></span>
<span data-ttu-id="d5dd9-107">Чтобы включить прием входящих удаленных подключений PowerShell, пользователю нужно создать конечную точку удаленного взаимодействия WinRM.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-107">To enable it to accept incoming PowerShell remote connections, the user must create a WinRM remoting endpoint.</span></span>
<span data-ttu-id="d5dd9-108">Это сценарий, требующий явного согласия, в котором пользователь запускает Install-PowerShellRemoting.ps1 для создания конечной точки WinRM.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-108">This is an explicit opt-in scenario where the user runs Install-PowerShellRemoting.ps1 to create the WinRM endpoint.</span></span>
<span data-ttu-id="d5dd9-109">Сценарий установки — это временное решение, пока в `Enable-PSRemoting` не будет добавлена дополнительная функциональность для выполнения данной задачи.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-109">The installation script is a short-term solution until we add additional functionality to `Enable-PSRemoting` to perform the same action.</span></span>
<span data-ttu-id="d5dd9-110">Дополнительные сведения см. в описании вопроса [1193](https://github.com/PowerShell/PowerShell/issues/1193).</span><span class="sxs-lookup"><span data-stu-id="d5dd9-110">For more details, please see issue [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span></span>

### <a name="script-actions"></a><span data-ttu-id="d5dd9-111">Действия сценария</span><span class="sxs-lookup"><span data-stu-id="d5dd9-111">Script Actions</span></span>

<span data-ttu-id="d5dd9-112">Сценарий</span><span class="sxs-lookup"><span data-stu-id="d5dd9-112">The script</span></span>

1. <span data-ttu-id="d5dd9-113">Создает каталог для подключаемого модуля в расположении %windir%\System32\PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-113">Creates a directory for the plug-in within %windir%\System32\PowerShell</span></span>
1. <span data-ttu-id="d5dd9-114">Копирует туда pwrshplugin.dll.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-114">Copies pwrshplugin.dll to that location</span></span>
1. <span data-ttu-id="d5dd9-115">Создает файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-115">Generates a configuration file</span></span>
1. <span data-ttu-id="d5dd9-116">Регистрирует этот подключаемый модуль в службе WinRM.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-116">Registers that plug-in with WinRM</span></span>

### <a name="registration"></a><span data-ttu-id="d5dd9-117">Регистрация</span><span class="sxs-lookup"><span data-stu-id="d5dd9-117">Registration</span></span>

<span data-ttu-id="d5dd9-118">Сценарий следует запускать в сеансе PowerShell с правами администратора, и выполняется он в двух режимах.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-118">The script must be executed within an Administrator-level PowerShell session and runs in two modes.</span></span>

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a><span data-ttu-id="d5dd9-119">Выполнение экземпляром PowerShell, где он будет зарегистрирован</span><span class="sxs-lookup"><span data-stu-id="d5dd9-119">Executed by the instance of PowerShell that it will register</span></span>

``` powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a><span data-ttu-id="d5dd9-120">Выполнение экземпляром PowerShell, отличным от того, где он будет зарегистрирован</span><span class="sxs-lookup"><span data-stu-id="d5dd9-120">Executed by another instance of PowerShell on behalf of the instance that it will register</span></span>

``` powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

<span data-ttu-id="d5dd9-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="d5dd9-121">For Example:</span></span>

``` powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

<span data-ttu-id="d5dd9-122">**Примечание**. Сценарий регистрации удаленного взаимодействия перезапускает WinRM, поэтому сразу после его запуска все существующие сеансы PSRP завершаются.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-122">**NOTE:** The remoting registration script will restart WinRM, so all existing PSRP sessions will terminate immediately after the script is run.</span></span> <span data-ttu-id="d5dd9-123">Если запустить его во время удаленного сеанса, соединение будет разорвано.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-123">If run during a remote session, this will terminate the connection.</span></span>

## <a name="how-to-connect-to-the-new-endpoint"></a><span data-ttu-id="d5dd9-124">Подключение к новой конечной точке</span><span class="sxs-lookup"><span data-stu-id="d5dd9-124">How to Connect to the New Endpoint</span></span>

<span data-ttu-id="d5dd9-125">Создайте сеанс PowerShell с новой конечной точкой PowerShell, указав `-ConfigurationName "some endpoint name"`.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-125">Create a PowerShell session to the new PowerShell endpoint by specifying `-ConfigurationName "some endpoint name"`.</span></span> <span data-ttu-id="d5dd9-126">Чтобы подключиться к экземпляру PowerShell из примера выше, используйте одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="d5dd9-126">To connect to the PowerShell instance from the example above, use either:</span></span>

``` powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

<span data-ttu-id="d5dd9-127">Обратите внимание, что вызовы `New-PSSession` и `Enter-PSSession`, которые не указывают `-ConfigurationName`, ориентируются на конечную точку PowerShell по умолчанию — `microsoft.powershell`.</span><span class="sxs-lookup"><span data-stu-id="d5dd9-127">Note that `New-PSSession` and `Enter-PSSession` invocations that do not specify `-ConfigurationName` will target the default PowerShell endpoint, `microsoft.powershell`.</span></span>
