---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Update-Module
ms.openlocfilehash: 89b0111eda4421606843f108dca90519b2c9379e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="update-module"></a><span data-ttu-id="f4460-103">Update-Module</span><span class="sxs-lookup"><span data-stu-id="f4460-103">Update-Module</span></span>

<span data-ttu-id="f4460-104">Скачивает последние версии указанных модулей из веб-коллекции и устанавливает их на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f4460-104">Downloads and installs the newest version of specified modules from an online gallery to the local computer.</span></span>

## <a name="description"></a><span data-ttu-id="f4460-105">Описание</span><span class="sxs-lookup"><span data-stu-id="f4460-105">Description</span></span>

<span data-ttu-id="f4460-106">Командлет Update-Module устанавливает более новую версию модуля Windows PowerShell, который был установлен из веб-коллекции командлетом Install-Module на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="f4460-106">The Update-Module cmdlet installs a newer version of a Windows PowerShell module that was installed from the online gallery by running Install-Module on the local computer.</span></span>

<span data-ttu-id="f4460-107">По умолчанию устанавливается самая последняя версия указанного модуля, доступная в веб-коллекции, если не указана конкретная версия.</span><span class="sxs-lookup"><span data-stu-id="f4460-107">By default, the newest version of the specified module available in online gallery is installed, unless you specify a required version.</span></span> <span data-ttu-id="f4460-108">Можно обновить существующий установленный модуль, указав имя модуля. Командлет Update-Module ищет в $env:PSModulePath обновляемый модуль.</span><span class="sxs-lookup"><span data-stu-id="f4460-108">You can update an existing, installed module by specifying the name of the module; Update-Module searches $env:PSModulePath for the module that you want to update.</span></span>

<span data-ttu-id="f4460-109">При запуске Update-Module без параметра Name будут обновлены все модули, которые можно обновить на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f4460-109">Running Update-Module without the Name parameter updates all modules that can be updated on the local computer.</span></span>

### <a name="notes"></a><span data-ttu-id="f4460-110">Заметки</span><span class="sxs-lookup"><span data-stu-id="f4460-110">Notes</span></span>

- <span data-ttu-id="f4460-111">Этот командлет работает в Windows PowerShell 3.0 и последующих версиях в Windows 7, Windows Server 2008 R2 и более поздних версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="f4460-111">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>
- <span data-ttu-id="f4460-112">Если модуль, указанный в параметре Name, не был установлен командлетом Install-Module, возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="f4460-112">If the module that you specify with the Name parameter was not installed by using Install-Module, an error occurs.</span></span> <span data-ttu-id="f4460-113">Командлет Update-Module можно выполнять только для модулей, установленных из веб-коллекции при помощи Install-Module.</span><span class="sxs-lookup"><span data-stu-id="f4460-113">You can only run Update-Module on modules that you installed from the online gallery by running Install-Module.</span></span>
- <span data-ttu-id="f4460-114">Если командлет Update-Module пытается обновить двоичные файлы, которые используются, то он возвращает ошибку, указывающую на проблемные процессы и информирующую пользователя о необходимости повторного своего запуска после остановки таких процессов.</span><span class="sxs-lookup"><span data-stu-id="f4460-114">If Update-Module attempts to update binaries that are in use, Update-Module returns an error that identifies the problem processes, and informs the user to retry Update-Module after stopping the processes.</span></span>
- <span data-ttu-id="f4460-115">В PowerShell 5.0 и более поздних версиях при обновлении командлетом Update-Module модуля он добавляет последнюю (или указанную) версию модуля. Так старая и более новая версии размещаются параллельно в одном и том же каталоге.</span><span class="sxs-lookup"><span data-stu-id="f4460-115">On PowerShell 5.0 or newer versions, when Update-Module updates a module, it adds the latest (or specified) version of the module, so the older and newer versions are now side-by-side in the same directory.</span></span> <span data-ttu-id="f4460-116">Теперь было бы полезно показать пример выходных данных этих команд.</span><span class="sxs-lookup"><span data-stu-id="f4460-116">It would be useful to say so and to show an example of the output from these commands.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="f4460-117">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="f4460-117">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="f4460-118">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="f4460-118">Cmdlet online help reference</span></span>

[<span data-ttu-id="f4460-119">Update-Module</span><span class="sxs-lookup"><span data-stu-id="f4460-119">Update-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a><span data-ttu-id="f4460-120">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="f4460-120">Example commands</span></span>

```powershell
PS C:\windows\system32> Update-Module -Name ContosoServer -RequiredVersion 1.5
PS C:\windows\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.0
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
PS C:\windows\system32> Update-Module -Name ContosoServer
PS C:\windows\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.8.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.8.1
Name : ContosoServer
Version : 2.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\ContosoServer\1.0
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
```

### <a name="update-the-module-with-a-prerelease-version-requires--allowprerelease-flag"></a><span data-ttu-id="f4460-121">Обновление модуля с использованием предварительной версии, требуется флаг -AllowPrerelease</span><span class="sxs-lookup"><span data-stu-id="f4460-121">Update the module with a prerelease version, requires -AllowPrerelease flag</span></span>
```powershell
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module

PS C:\windows\system32> Find-Module ContosoServer -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
3.0.0-alpha    ConstosoServer                      MSPSGallery          The PowerShell Contoso Server deployment tools...

PS C:\windows\system32> Update-Module -Name ContosoServer -AllowPrerelease
PS C:\windows\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
3.0.0-alpha ContosoServer MSPSGallery ContosoServer module

```


### <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a><span data-ttu-id="f4460-122">Обновите модуль TestDepWithNestedRequiredModules1 с зависимостями.</span><span class="sxs-lookup"><span data-stu-id="f4460-122">Update the TestDepWithNestedRequiredModules1 module with dependencies.</span></span>
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module



```