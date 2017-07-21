---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery,psget"
title: "Коллекция PowerShell"
ms.openlocfilehash: 3e324f15b251822163c3ea9b6655767419a5ac4e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="dcd6a-103">Коллекция PowerShell</span><span class="sxs-lookup"><span data-stu-id="dcd6a-103">The PowerShell Gallery</span></span>

<span data-ttu-id="dcd6a-104">Коллекция PowerShell — это центральный репозиторий для хранения содержимого PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="dcd6a-105">Именно в коллекции можно найти новые команды PowerShell или ресурсы настройки требуемого состояния (DSC).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-105">You can find new PowerShell commands or Desired State Configuration (DSC) resources in the Gallery.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="dcd6a-106">Обзор PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="dcd6a-106">PowerShellGet Overview</span></span>

<span data-ttu-id="dcd6a-107">Модуль PowerShellGet содержит командлеты для обнаружения, установки, обновления и публикации артефактов PowerShell, таких как модули, ресурсы DSC, возможности ролей и скрипты с веб-сайта https://www.PowerShellGallery.com и других частных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-107">PowerShellGet module contains cmdlets for discovering, installing, updating and publishing the PowerShell artifacts like Modules, DSC Resources, Role Capabilities and Scripts from the https://www.PowerShellGallery.com and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="dcd6a-108">Начало работы с коллекцией</span><span class="sxs-lookup"><span data-stu-id="dcd6a-108">Getting Started with the Gallery</span></span>

<span data-ttu-id="dcd6a-109">Для установки элементов из коллекции требуется последняя версия модуля PowerShellGet, доступная в Windows 10, в Windows Management Framework (WMF) 5.0 или в установщике на основе MSI (для PowerShell 3 и 4).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-109">Installing items from the Gallery requires the latest version of the PowerShellGet module, which is available in Windows 10, in Windows Management Framework (WMF) 5.0, or in the MSI-based installer (for PowerShell 3 and 4).</span></span>

- <span data-ttu-id="dcd6a-110">[**Скачать Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span><span class="sxs-lookup"><span data-stu-id="dcd6a-110">[**Get Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span></span>
- <span data-ttu-id="dcd6a-111">[**Скачать WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175) или</span><span class="sxs-lookup"><span data-stu-id="dcd6a-111">[**Get WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175), or</span></span>
- [<span data-ttu-id="dcd6a-112">**Скачать установщик MSI**</span><span class="sxs-lookup"><span data-stu-id="dcd6a-112">**Get MSI Installer**</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

<span data-ttu-id="dcd6a-113">Последняя версия модуля [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) позволяет:</span><span class="sxs-lookup"><span data-stu-id="dcd6a-113">With the latest [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) module, you can:</span></span>

-   <span data-ttu-id="dcd6a-114">Выполнять поиск по элементам в коллекции командлетами [**Find-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Find-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-114">Search through items in the Gallery with [**Find-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) and [**Find-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)</span></span>
-   <span data-ttu-id="dcd6a-115">Сохранять элементы в систему из коллекции командлетами [**Save-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Save-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-115">Save items to your system from the Gallery with [**Save-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) and [**Save-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)</span></span>
-   <span data-ttu-id="dcd6a-116">Устанавливать элементы из коллекции командлетами [**Install-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Install-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-116">Install items from the Gallery with [**Install-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) and [**Install-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)</span></span>
-   <span data-ttu-id="dcd6a-117">Отправлять элементы в коллекцию командлетами [**Publish-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Publish-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-117">Upload items to the Gallery with [**Publish-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) and [**Publish-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)</span></span>
-   <span data-ttu-id="dcd6a-118">Добавлять собственный репозиторий командлетом [**Register-PSRepository**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-118">Add your own custom repository with [**Register-PSRepository**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409)</span></span>

<span data-ttu-id="dcd6a-119">Дополнительные сведения об использовании команд PowerShellGet при работе с коллекцией см. в статье [Начало работы](psgallery/psgallery_gettingstarted.md).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-119">Check out the [Getting Started](psgallery/psgallery_gettingstarted.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="dcd6a-120">Вы также можете запустить командлет *Update-Help -Module PowerShellGet*, чтобы установить локальную справку по этим командам.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-120">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="dcd6a-121">Поддерживаемые операционные системы</span><span class="sxs-lookup"><span data-stu-id="dcd6a-121">Supported Operating Systems</span></span>

<span data-ttu-id="dcd6a-122">Для модуля **PowerShellGet** требуется **PowerShell 3.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-122">The **PowerShellGet** module requires **PowerShell 3.0 or newer**.</span></span>

<span data-ttu-id="dcd6a-123">Таким образом, для **PowerShellGet** требуется одна из следующих операционных систем:</span><span class="sxs-lookup"><span data-stu-id="dcd6a-123">Therefore, **PowerShellGet** requires one of the following operating systems:</span></span>

- <span data-ttu-id="dcd6a-124">Windows 10</span><span class="sxs-lookup"><span data-stu-id="dcd6a-124">Windows 10</span></span>
- <span data-ttu-id="dcd6a-125">Windows 8.1 Профессиональная</span><span class="sxs-lookup"><span data-stu-id="dcd6a-125">Windows 8.1 Pro</span></span>
- <span data-ttu-id="dcd6a-126">Windows 8.1 Корпоративная</span><span class="sxs-lookup"><span data-stu-id="dcd6a-126">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="dcd6a-127">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="dcd6a-127">Windows 7 SP1</span></span>
- <span data-ttu-id="dcd6a-128">Windows Server 2016 TP5</span><span class="sxs-lookup"><span data-stu-id="dcd6a-128">Windows Server 2016 TP5</span></span>
- <span data-ttu-id="dcd6a-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dcd6a-129">Windows Server 2012 R2</span></span>
- <span data-ttu-id="dcd6a-130">Windows Server 2008 R2 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="dcd6a-130">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="dcd6a-131">Для **PowerShellGet** также требуется .NET Framework 4.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dcd6a-131">**PowerShellGet** also  requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="dcd6a-132">Установить .NET Framework 4.5 или более поздней версии можно [отсюда](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-132">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).</span></span>


## <a name="got-a-question-have-feedback"></a><span data-ttu-id="dcd6a-133">Возник вопрос?</span><span class="sxs-lookup"><span data-stu-id="dcd6a-133">Got a question?</span></span> <span data-ttu-id="dcd6a-134">Хотите поделиться мнением?</span><span class="sxs-lookup"><span data-stu-id="dcd6a-134">Have feedback?</span></span>

<span data-ttu-id="dcd6a-135">Дополнительные сведения о коллекции PowerShell и PowerShellGet см. на странице [Начало работы](psgallery/psgallery_gettingstarted.md).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-135">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](psgallery/psgallery_gettingstarted.md) page.</span></span> <span data-ttu-id="dcd6a-136">Оставить отзыв или сообщить о проблеме можно на сайте [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="dcd6a-136">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>

