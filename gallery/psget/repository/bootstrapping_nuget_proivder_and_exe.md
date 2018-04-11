---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Начальная загрузка поставщика NuGet и NuGet.exe
ms.openlocfilehash: 1c8d99491aec6d2a598facb909c1f36f4bb979e7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="bootstrap-both-nuget-provider-and-nugetexe-or-bootstrap-only-nuget-provider"></a><span data-ttu-id="db45b-103">Начальная загрузка поставщика NuGet и NuGet.exe или начальная загрузка только поставщика NuGet</span><span class="sxs-lookup"><span data-stu-id="db45b-103">Bootstrap both NuGet provider and NuGet.exe or bootstrap only NuGet provider</span></span>

<span data-ttu-id="db45b-104">Файл NuGet.exe включен в последний поставщик NuGet.</span><span class="sxs-lookup"><span data-stu-id="db45b-104">NuGet.exe is not included in the latest NuGet provider.</span></span>
<span data-ttu-id="db45b-105">Для операций публикации модулей или скриптов PowerShellGet требуется двоичный исполняемый файл NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="db45b-105">For publish operations of either a module or script, PowerShellGet requires the binary executable NuGet.exe.</span></span>
<span data-ttu-id="db45b-106">Для всех других операций, включая *поиск*, *установку*, *сохранение* и *удаление*, требуется только поставщик NuGet.</span><span class="sxs-lookup"><span data-stu-id="db45b-106">Only the NuGet provider is required for all other operations, including *find*, *install*, *save*, and *uninstall*.</span></span>
<span data-ttu-id="db45b-107">PowerShellGet содержит логику обработки совместной начальной загрузки поставщика NuGet и NuGet.exe или начальной загрузки только поставщика NuGet.</span><span class="sxs-lookup"><span data-stu-id="db45b-107">PowerShellGet includes logic to handle either a combined bootstrap of the NuGet provider and NuGet.exe, or bootstrap of only the NuGet provider.</span></span>
<span data-ttu-id="db45b-108">В любом случае должно появиться только одно сообщение запроса.</span><span class="sxs-lookup"><span data-stu-id="db45b-108">In either case, only a single prompt message should occur.</span></span>
<span data-ttu-id="db45b-109">Если компьютер не подключен к Интернету, пользователь или администратор должен скопировать на него доверенный экземпляр поставщика NuGet и/или файл NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="db45b-109">If the machine is not connected to the Internet, the user or an administrator must copy a trusted instance of the NuGet provider and/or the NuGet.exe file to the disconnected machine.</span></span>

><span data-ttu-id="db45b-110">**Примечание.** Начиная с версии 6, поставщик NuGet содержится в установке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db45b-110">**Note**: Starting with version 6, the NuGet provider is included in the installation of PowerShell.</span></span> [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="db45b-111">Устранение ошибки, при которой поставщик NuGet не устанавливается на автономный компьютер</span><span class="sxs-lookup"><span data-stu-id="db45b-111">Resolving error when the NuGet provider has not been installed on a machine that is Internet connected</span></span>

```powershell
PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n
Find-Module : NuGet provider is required to interact with NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed.
At line:1 char:1
+ Find-Module -Repository PSGallery -Verbose -Name Contoso
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Find-Module], InvalidOperationException
   + FullyQualifiedErrorId : CouldNotInstallNuGetProvider,Find-Module

PS C:\> Find-Module -Repository PSGallery -Verbose -Name Contoso

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Contoso                             Module     PSGallery        Contoso module
```
## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="db45b-112">Устранение ошибки, при которой во время операции публикации на автономном компьютере доступен поставщик NuGet, но недоступен NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="db45b-112">Resolving error when the NuGet provider is available and NuGet.exe is not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="db45b-113">Устранение ошибки, при которой во время операции публикации на автономном компьютере недоступны поставщик NuGet и NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="db45b-113">Resolving error when both NuGet provider and NuGet.exe are not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed and NuGet.exe is available under
one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetBinaries,Publish-Module

PS C:\> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="db45b-114">Ручной режим начальной загрузки поставщика NuGet на автономный компьютер</span><span class="sxs-lookup"><span data-stu-id="db45b-114">Manually bootstrapping the NuGet provider on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="db45b-115">В указанных выше случаях предполагается, что компьютер подключен к Интернету и может скачать файлы из общедоступного расположения.</span><span class="sxs-lookup"><span data-stu-id="db45b-115">The processes demonstrated above assume the machine is connected to the Internet and can download files from a public location.</span></span>
<span data-ttu-id="db45b-116">Если это невозможно, единственным вариантом является начальная загрузка на компьютере с помощью процессов, приведенных выше, и ручное копирование поставщика на изолированный узел с помощью автономного доверенного процесса.</span><span class="sxs-lookup"><span data-stu-id="db45b-116">If that is not possible, the only option is to bootstrap a machine using the processes given above, and manually copy the provider to the isolated node through an offline trusted process.</span></span>
<span data-ttu-id="db45b-117">Наиболее распространенный случай использования такого сценария — это когда частная коллекция доступна для поддержки изолированной среды.</span><span class="sxs-lookup"><span data-stu-id="db45b-117">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>

<span data-ttu-id="db45b-118">После выполнения перечисленных выше процедур для начальной загрузки компьютера, подключенного к Интернету, вы увидите файлы поставщика в расположении:</span><span class="sxs-lookup"><span data-stu-id="db45b-118">After following the process above to bootstrap an Internet connected machine, you will find provider files in the location:</span></span>
```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

<span data-ttu-id="db45b-119">Структура папок или файлов поставщика NuGet будет следующей (возможно, с другим номером версии):</span><span class="sxs-lookup"><span data-stu-id="db45b-119">The folder/file structure of the NuGet provider will be (possibly with a different version number):</span></span>

<span data-ttu-id="db45b-120">NuGet</span><span class="sxs-lookup"><span data-stu-id="db45b-120">NuGet</span></span><br>
<span data-ttu-id="db45b-121">--2.8.5.208</span><span class="sxs-lookup"><span data-stu-id="db45b-121">--2.8.5.208</span></span><br>
<span data-ttu-id="db45b-122">---Microsoft.PackageManagement.NuGetProvider.dll</span><span class="sxs-lookup"><span data-stu-id="db45b-122">----Microsoft.PackageManagement.NuGetProvider.dll</span></span>

<span data-ttu-id="db45b-123">Скопируйте эти папки и файл с помощью доверенного процесса на автономные компьютеры.</span><span class="sxs-lookup"><span data-stu-id="db45b-123">Copy these folders and file using a trusted process to the offline machines.</span></span>

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="db45b-124">Ручной режим начальной загрузки поставщика NuGet на автономном компьютере для поддержки операций публикации</span><span class="sxs-lookup"><span data-stu-id="db45b-124">Manually bootstrapping NuGet.exe to support publish operations on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="db45b-125">Если компьютер будет использоваться для публикации модулей или скриптов в частной коллекции с помощью командлетов *Publish-Module* или *Publish-Script*, помимо выполнения начальной загрузки поставщика NuGet вручную потребуется двоичный исполняемый файл NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="db45b-125">In addition to the process to manually bootstrap the NuGet provider, if the machine will be used to publish modules or scripts to a private gallery using the *Publish-Module* or *Publish-Script* cmdlets, the NuGet.exe binary executable file will be required.</span></span>
<span data-ttu-id="db45b-126">Наиболее распространенный случай использования такого сценария — это когда частная коллекция доступна для поддержки изолированной среды.</span><span class="sxs-lookup"><span data-stu-id="db45b-126">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>
<span data-ttu-id="db45b-127">Существует два варианта получения файла NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="db45b-127">There are two options to obtain the NuGet.exe file.</span></span>

<span data-ttu-id="db45b-128">Первый вариант — выполнить начальную загрузку на компьютере, подключенном к Интернету, и скопировать файлы на автономные компьютеры с помощью доверенного процесса.</span><span class="sxs-lookup"><span data-stu-id="db45b-128">One option is to bootstrap a machine that is Internet connected and copy the files to the offline machines using a trusted process.</span></span>
<span data-ttu-id="db45b-129">После начальной загрузки подключенного к Интернету компьютера двоичный файл NuGet.exe будет находиться в одной из двух папок:</span><span class="sxs-lookup"><span data-stu-id="db45b-129">After bootstrapping the Internet connected machine, the NuGet.exe binary will be located in one of two folders:</span></span>

<span data-ttu-id="db45b-130">При выполнении командлетов *Publish-Module* или *Publish-Script* с повышенным уровнем разрешений (от имени администратора):</span><span class="sxs-lookup"><span data-stu-id="db45b-130">If the *Publish-Module* or *Publish-Script* cmdlets were executed with elevated permissions (As an Administrator):</span></span>
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="db45b-131">Если командлеты выполнялись от имени пользователя без разрешения более высокого уровня:</span><span class="sxs-lookup"><span data-stu-id="db45b-131">If the cmdlets were executed as a user without elevated permissions:</span></span>
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

<span data-ttu-id="db45b-132">Второй вариант — загрузить NuGet.exe с веб-сайта NuGet.Org: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)</span><span class="sxs-lookup"><span data-stu-id="db45b-132">A second option is to download NuGet.exe from the NuGet.Org website: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)</span></span><br>
<span data-ttu-id="db45b-133">При выборе версии для рабочих компьютеров убедитесь, что это версия позднее 2.8.5.208, и определите версию с пометкой "рекомендуется".</span><span class="sxs-lookup"><span data-stu-id="db45b-133">When selecting a NugGet version for production machines, make sure it is later than 2.8.5.208, and identify the version that has been labeled "recommended".</span></span>
<span data-ttu-id="db45b-134">Обязательно разблокируйте файл, если он был скачан с помощью браузера.</span><span class="sxs-lookup"><span data-stu-id="db45b-134">Remember to unblock the file if it was downloaded using a browser.</span></span>
<span data-ttu-id="db45b-135">Это можно сделать с помощью командлета *Unblock-File*.</span><span class="sxs-lookup"><span data-stu-id="db45b-135">This can be performed by using the *Unblock-File* cmdlet.</span></span>

<span data-ttu-id="db45b-136">В любом случае можно скопировать файл NuGet.exe в любое расположение в *$env:path*, но стандартные расположения следующие:</span><span class="sxs-lookup"><span data-stu-id="db45b-136">In either case, the NuGet.exe file can be copied to any location in *$env:path*, but the standard locations are:</span></span>

<span data-ttu-id="db45b-137">Чтобы сделать доступным исполняемый файл, чтобы все пользователи могли использовать командлеты *Publish-Module* и *Publish-Script*, используйте следующее:</span><span class="sxs-lookup"><span data-stu-id="db45b-137">To make the executable available so that all users can use *Publish-Module* and *Publish-Script* cmdlets:</span></span>
```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="db45b-138">Чтобы сделать доступным исполняемый файл только для конкретных пользователей, скопируйте его в расположение профиля только нужного пользователя:</span><span class="sxs-lookup"><span data-stu-id="db45b-138">To make the executable available to only a specific user, copy to the location within only that user's profile:</span></span>
```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```