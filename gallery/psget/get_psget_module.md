---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: "Получение модуля PowerShellGet"
ms.openlocfilehash: a5a323b17709e519ec57623a9dd7499e591bbed5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a name="get-powershellget-module"></a><span data-ttu-id="82622-103">Получение модуля PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="82622-103">Get PowerShellGet Module</span></span>
========================

### <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="82622-104">Модуль PowerShellGet входит в комплект поставки в следующих выпусках:</span><span class="sxs-lookup"><span data-stu-id="82622-104">PowerShellGet is an in-box module in the following releases</span></span>
- <span data-ttu-id="82622-105">[Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) или более поздняя версия;</span><span class="sxs-lookup"><span data-stu-id="82622-105">[Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) or newer</span></span>
- <span data-ttu-id="82622-106">[Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) или более поздняя версия;</span><span class="sxs-lookup"><span data-stu-id="82622-106">[Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) or newer</span></span>
- <span data-ttu-id="82622-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) или более поздняя версия;</span><span class="sxs-lookup"><span data-stu-id="82622-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) or newer</span></span>
- <span data-ttu-id="82622-108">[PowerShell 6](https://github.com/PowerShell/PowerShell/releases).</span><span class="sxs-lookup"><span data-stu-id="82622-108">[PowerShell 6](https://github.com/PowerShell/PowerShell/releases)</span></span>

### <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="82622-109">Получение модуля PowerShellGet для PowerShell версии 3.0 и 4.0</span><span class="sxs-lookup"><span data-stu-id="82622-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>
- [<span data-ttu-id="82622-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="82622-110">PackageManagement MSI</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) 

### <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="82622-111">Получение последней версии из коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="82622-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="82622-112">Перед обновлением PowerShellGet всегда устанавливайте последний поставщик Nuget.</span><span class="sxs-lookup"><span data-stu-id="82622-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="82622-113">Для этого выполните следующую команду в сеансе PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="82622-113">To do that, run the following in an elevated PowerShell session.</span></span>
```powershell
Install-PackageProvider Nuget –Force
Exit
```

#### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="82622-114">Для систем с PowerShell 5.0 (или более поздней версии) можно установить последнюю версию PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="82622-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span> 
- <span data-ttu-id="82622-115">Чтобы сделать это в Windows 10, Windows Server 2016, любой системе с установленным WMF 5.0 или 5.1 или любой системе с PowerShell 6, выполните следующие команды из сеанса PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="82622-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>
```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- <span data-ttu-id="82622-116">Update-Module позволяет получить более новые версии.</span><span class="sxs-lookup"><span data-stu-id="82622-116">Use Update-Module to get newer versions.</span></span>
```powershell
Update-Module -Name PowerShellGet
Exit
```

#### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a><span data-ttu-id="82622-117">Для систем под управлением PowerShell 3 или PowerShell 4, на которых установлено [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="82622-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span></span>

- <span data-ttu-id="82622-118">Используйте командлеты PowerShellGet ниже из сеанса PowerShell с повышенными привилегиями, чтобы сохранить модули в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="82622-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- <span data-ttu-id="82622-119">Убедитесь, что модули PowerShellGet и PackageManagment не загружены в других процессах.</span><span class="sxs-lookup"><span data-stu-id="82622-119">Ensure that PowerShellGet and PackageManagment modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="82622-120">Удалите содержимое папок `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` и `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\`.</span><span class="sxs-lookup"><span data-stu-id="82622-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="82622-121">Снова откройте консоль PS с повышенным уровнем разрешений, а затем выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="82622-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force