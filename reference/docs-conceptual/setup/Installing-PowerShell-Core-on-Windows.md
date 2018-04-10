# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="39d66-101">Установка PowerShell Core в Windows</span><span class="sxs-lookup"><span data-stu-id="39d66-101">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="39d66-102">MSI</span><span class="sxs-lookup"><span data-stu-id="39d66-102">MSI</span></span>

<span data-ttu-id="39d66-103">Чтобы установить PowerShell на клиенте Windows или в Windows Server (работает в Windows 7 с пакетом обновления 1 (SP1), Server 2008 R2 и более поздних версий), скачайте пакет MSI из с нашей страницы [выпусков][] GitHub.</span><span class="sxs-lookup"><span data-stu-id="39d66-103">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>

<span data-ttu-id="39d66-104">MSI-файл имеет следующий вид: `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`.</span><span class="sxs-lookup"><span data-stu-id="39d66-104">The MSI file looks like this - `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`</span></span>
<!-- TODO: should be updated to point to the Download Center as well -->

<span data-ttu-id="39d66-105">После скачивания дважды щелкните установщик и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="39d66-105">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="39d66-106">После установки в меню "Пуск" появляется ярлык.</span><span class="sxs-lookup"><span data-stu-id="39d66-106">There is a shortcut placed in the Start Menu upon installation.</span></span>

* <span data-ttu-id="39d66-107">По умолчанию пакет устанавливается в каталог `$env:ProgramFiles\PowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="39d66-107">By default the package is installed to `$env:ProgramFiles\PowerShell\`</span></span>
* <span data-ttu-id="39d66-108">Вы можете запустить PowerShell с помощью меню "Пуск" или файла `$env:ProgramFiles\PowerShell\pwsh.exe`.</span><span class="sxs-lookup"><span data-stu-id="39d66-108">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="39d66-109">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="39d66-109">Prerequisites</span></span>

<span data-ttu-id="39d66-110">Чтобы включить удаленное взаимодействие PowerShell через WSMan, нужно выполнить следующие условия:</span><span class="sxs-lookup"><span data-stu-id="39d66-110">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

* <span data-ttu-id="39d66-111">Установите [универсальную среду выполнения C](https://www.microsoft.com/download/details.aspx?id=50410) в версиях Windows, предшествующих Windows 10.</span><span class="sxs-lookup"><span data-stu-id="39d66-111">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="39d66-112">Ее можно скачать самостоятельно или через Центр обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="39d66-112">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="39d66-113">Поддерживаемые системы, где установлены все исправления (включая дополнительные пакеты), уже содержат ее.</span><span class="sxs-lookup"><span data-stu-id="39d66-113">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
* <span data-ttu-id="39d66-114">Установите Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) или более поздней версии ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) в Windows 7 и Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="39d66-114">Install the Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) or newer ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="39d66-115">ZIP</span><span class="sxs-lookup"><span data-stu-id="39d66-115">ZIP</span></span>

<span data-ttu-id="39d66-116">Для поддержки расширенных сценариев развертывания доступны ZIP-архивы двоичных файлов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39d66-116">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="39d66-117">Следует отметить, что при использовании ZIP-архива проверка предварительных условий, как в случае с пакетом MSI, не производится.</span><span class="sxs-lookup"><span data-stu-id="39d66-117">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="39d66-118">Поэтому для правильной работы удаленного взаимодействия через WSMan в версиях Windows, предшествующих Windows 10, убедитесь, что [предварительные условия](#prerequisites) соблюдены.</span><span class="sxs-lookup"><span data-stu-id="39d66-118">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-nano-server"></a><span data-ttu-id="39d66-119">Развертывание на Nano Server</span><span class="sxs-lookup"><span data-stu-id="39d66-119">Deploying on Nano Server</span></span>

<span data-ttu-id="39d66-120">Эти инструкции предполагают, что версия PowerShell уже запущена на образе Nano Server и была создана с помощью [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="39d66-120">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="39d66-121">ОС Nano Server работает без монитора, и двоичные файлы PowerShell Core можно развернуть двумя способами:</span><span class="sxs-lookup"><span data-stu-id="39d66-121">Nano Server is a "headless" OS and deployment of PowerShell Core binaries can happen in two different ways:</span></span>

1. <span data-ttu-id="39d66-122">Автономно — подключите виртуальный жесткий диск Nano Server и распакуйте содержимое ZIP-файла в выбранное расположение в этом образе.</span><span class="sxs-lookup"><span data-stu-id="39d66-122">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
1. <span data-ttu-id="39d66-123">В сети — передайте ZIP-файл через сеанс PowerShell и распакуйте его в выбранное расположение.</span><span class="sxs-lookup"><span data-stu-id="39d66-123">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="39d66-124">В обоих случаях вам понадобится ZIP-пакет выпуска x64 Windows 10 и потребуется выполнять команды в экземпляре PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="39d66-124">In both cases, you will need the Windows 10 x64 Zip release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="39d66-125">Автономное развертывание PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="39d66-125">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="39d66-126">С помощью любой служебной программы ZIP распакуйте пакет в каталог, находящийся внутри подключенного образа Nano Server.</span><span class="sxs-lookup"><span data-stu-id="39d66-126">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
1. <span data-ttu-id="39d66-127">Отключите образ и загрузите его.</span><span class="sxs-lookup"><span data-stu-id="39d66-127">Unmount the image and boot it.</span></span>
1. <span data-ttu-id="39d66-128">Подключитесь к входящему экземпляру Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39d66-128">Connect to the inbox instance of Windows PowerShell.</span></span>
1. <span data-ttu-id="39d66-129">Следуйте инструкциям, чтобы создать конечную точку удаленного взаимодействия с помощью [методики использования другого экземпляра](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="39d66-129">Follow the instructions to create a remoting endpoint using the [another instance technique](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="39d66-130">Автономное PowerShell Core в сети</span><span class="sxs-lookup"><span data-stu-id="39d66-130">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="39d66-131">Следующие шаги описывают развертывание PowerShell Core в запущенном экземпляре Nano Server, а также настройку его удаленной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="39d66-131">The following steps will guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

* <span data-ttu-id="39d66-132">Подключитесь к входящему экземпляру Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="39d66-132">Connect to the inbox instance of Windows PowerShell</span></span>

```powershell
$session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
```

* <span data-ttu-id="39d66-133">Скопируйте файл на экземпляр Nano Server:</span><span class="sxs-lookup"><span data-stu-id="39d66-133">Copy the file to the Nano Server instance</span></span>

```powershell
Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
```

* <span data-ttu-id="39d66-134">Войдите в сеанс:</span><span class="sxs-lookup"><span data-stu-id="39d66-134">Enter the session</span></span>

```powershell
Enter-PSSession $session
```

* <span data-ttu-id="39d66-135">Извлеките ZIP-файл:</span><span class="sxs-lookup"><span data-stu-id="39d66-135">Extract the Zip file</span></span>

```powershell
# Insert the appropriate version.
Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
```

* <span data-ttu-id="39d66-136">Если вам требуется удаленное взаимодействие на основе WSMan, следуйте инструкциям, чтобы создать конечную точку удаленного взаимодействия с помощью [методики использования другого экземпляра](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="39d66-136">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the [another instance technique](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="39d66-137">Инструкции по созданию конечной точки удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="39d66-137">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="39d66-138">PowerShell Core поддерживает протокол удаленного взаимодействия PowerShell (PSRP) через SSH и WSMan.</span><span class="sxs-lookup"><span data-stu-id="39d66-138">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span> <span data-ttu-id="39d66-139">Дополнительная информация:</span><span class="sxs-lookup"><span data-stu-id="39d66-139">For more information, see:</span></span>

* <span data-ttu-id="39d66-140">[Удаленное взаимодействие через SSH в PowerShell Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="39d66-140">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
* <span data-ttu-id="39d66-141">[Удаленное взаимодействие через WSMan в PowerShell Core][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="39d66-141">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="39d66-142">Указания по установке артефакта</span><span class="sxs-lookup"><span data-stu-id="39d66-142">Artifact Installation Instructions</span></span>

<span data-ttu-id="39d66-143">Мы публикуем архив с кодом CoreCLR для каждой сборки CI с [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="39d66-143">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

## <a name="coreclr-artifacts"></a><span data-ttu-id="39d66-144">Артефакты CoreCLR</span><span class="sxs-lookup"><span data-stu-id="39d66-144">CoreCLR Artifacts</span></span>

* <span data-ttu-id="39d66-145">Скачайте ZIP-пакет с вкладки **artifacts** конкретной сборки.</span><span class="sxs-lookup"><span data-stu-id="39d66-145">Download zip package from **artifacts** tab of the particular build.</span></span>
* <span data-ttu-id="39d66-146">Разблокируйте ZIP-файл: щелкните правой кнопкой мыши в проводнике, выберите "Свойства", установите флажок "Разблокировать" и выберите "Применить".</span><span class="sxs-lookup"><span data-stu-id="39d66-146">Unblock zip file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
* <span data-ttu-id="39d66-147">Извлеките содержимое ZIP-файла в каталог `bin`.</span><span class="sxs-lookup"><span data-stu-id="39d66-147">Extract zip file to `bin` directory</span></span>
* `./bin/pwsh.exe`

<!-- [download-center]: TODO -->
[выпусков]: https://github.com/PowerShell/PowerShell/releases
[releases]: https://github.com/PowerShell/PowerShell/releases
[signing]: ../../tools/Sign-Package.ps1
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell