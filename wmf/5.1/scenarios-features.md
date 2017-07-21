---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "Новые сценарии и возможности в WMF 5.1"
ms.openlocfilehash: 02c27711c886916da56bb382b1bc0187f1e30805
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="new-scenarios-and-features-in-wmf-51"></a><span data-ttu-id="41288-103">Новые сценарии и возможности в WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="41288-103">New Scenarios and Features in WMF 5.1</span></span> #

> <span data-ttu-id="41288-104">Примечание. Эта информация является предварительной и может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="41288-104">Note: This information is preliminary and subject to change.</span></span>

## <a name="powershell-editions"></a><span data-ttu-id="41288-105">Выпуски PowerShell</span><span class="sxs-lookup"><span data-stu-id="41288-105">PowerShell Editions</span></span> ##
<span data-ttu-id="41288-106">Начиная с версии 5.1 доступны различные выпуски среды PowerShell, что означает различные наборы возможностей и совместимость с разными платформами.</span><span class="sxs-lookup"><span data-stu-id="41288-106">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="41288-107">**Выпуск Desktop Edition:** построен на основе .NET Framework и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в полноценных выпусках Windows, таких как Server Core и Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="41288-107">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="41288-108">**Выпуск Core Edition:** построен на основе .NET Core и обеспечивает совместимость со скриптами и модулями, которые предназначены для версий PowerShell, выполняющихся в выпусках Windows с ограниченными возможностями, таких как Nano Server и Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="41288-108">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="41288-109">**Дополнительные сведения об использовании выпусков PowerShell**</span><span class="sxs-lookup"><span data-stu-id="41288-109">**Learn more about using PowerShell Editions**</span></span>
- [<span data-ttu-id="41288-110">Определение запущенного выпуска PowerShell</span><span class="sxs-lookup"><span data-stu-id="41288-110">Determine running edition of PowerShell</span></span>]()
- [<span data-ttu-id="41288-111">Объявление совместимости модуля с определенными версиями PowerShell</span><span class="sxs-lookup"><span data-stu-id="41288-111">Declare a module's compatibility to specific PowerShell versions</span></span>]()
- [<span data-ttu-id="41288-112">Фильтрация результатов командлета Get-Module по CompatiblePSEditions</span><span class="sxs-lookup"><span data-stu-id="41288-112">Filter Get-Module results by CompatiblePSEditions</span></span>]()
- [<span data-ttu-id="41288-113">Запрет на выполнение сценариев в несовместимых выпусках PowerShell</span><span class="sxs-lookup"><span data-stu-id="41288-113">Prevent script execution unless run on a compatible edition of PowerShell</span></span>]()

## <a name="catalog-cmdlets"></a><span data-ttu-id="41288-114">Командлеты для работы с каталогами</span><span class="sxs-lookup"><span data-stu-id="41288-114">Catalog Cmdlets</span></span>  

<span data-ttu-id="41288-115">Мы добавили два новых командлета для создания и проверки файлов каталога Windows в модуль [Microsoft.Powershell.Security](https://technet.microsoft.com/en-us/library/hh847877.aspx).</span><span class="sxs-lookup"><span data-stu-id="41288-115">Two new cmdlets have been added in the [Microsoft.PowerShell.Security](https://technet.microsoft.com/en-us/library/hh847877.aspx) module; these generate and validate Windows catalog files.</span></span>  

###<a name="new-filecatalog"></a><span data-ttu-id="41288-116">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="41288-116">New-FileCatalog</span></span> 
--------------------------------

<span data-ttu-id="41288-117">Командлет New-FileCatalog создает файл каталога Windows для набора файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="41288-117">New-FileCatalog creates a Windows catalog file for set of folders and files.</span></span> <span data-ttu-id="41288-118">Файл каталога содержит хэши для всех файлов, находящихся по указанным путям.</span><span class="sxs-lookup"><span data-stu-id="41288-118">This catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="41288-119">Пользователь может распространять набор папок вместе с соответствующим файлом каталога, представляющим этих папки.</span><span class="sxs-lookup"><span data-stu-id="41288-119">Users can distribute the set of folders along with corresponding catalog file representing those folders.</span></span> <span data-ttu-id="41288-120">С помощью файла каталога получатель может проверить, были ли изменены папки с момента создания каталога.</span><span class="sxs-lookup"><span data-stu-id="41288-120">This information is useful to validate whether any changes have been made to the folders since catalog creation time.</span></span>    

```PowerShell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="41288-121">Поддерживаются каталоги версий 1 и 2.</span><span class="sxs-lookup"><span data-stu-id="41288-121">Catalog versions 1 and 2 are supported.</span></span> <span data-ttu-id="41288-122">В версии 1 для создания хэшей файлов используется алгоритм хэширования SHA1, в версии 2 — SHA256.</span><span class="sxs-lookup"><span data-stu-id="41288-122">Version 1 uses the SHA1 hashing algorithm to create file hashes; version 2 uses SHA256.</span></span> <span data-ttu-id="41288-123">Каталог версии 2 не поддерживается в *Windows Server 2008 R2* и *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="41288-123">Catalog version 2 is not supported on *Windows Server 2008 R2* or *Windows 7*.</span></span> <span data-ttu-id="41288-124">На платформах *Windows 8*, *Windows Server 2012* и более поздней версии рекомендуется использовать каталог версии 2.</span><span class="sxs-lookup"><span data-stu-id="41288-124">You should use catalog version 2 on *Windows 8*, *Windows Server 2012*, and later operating systems.</span></span>  

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="41288-125">Следующая команда создает файл каталога.</span><span class="sxs-lookup"><span data-stu-id="41288-125">This creates the catalog file.</span></span> 

![](../images/CatalogFile1.jpg)  

![](../images/CatalogFile2.jpg) 

<span data-ttu-id="41288-126">Для проверки целостности файла каталога (Pester.cat в приведенном выше примере) его нужно подписать с помощью командлета [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).</span><span class="sxs-lookup"><span data-stu-id="41288-126">To verify the integrity of catalog file (Pester.cat in above example), sign it using [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>   


###<a name="test-filecatalog"></a><span data-ttu-id="41288-127">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="41288-127">Test-FileCatalog</span></span> 
--------------------------------

<span data-ttu-id="41288-128">Командлет Test-FileCatalog проверяет каталог, представляющий набор папок.</span><span class="sxs-lookup"><span data-stu-id="41288-128">Test-FileCatalog validates the catalog representing a set of folders.</span></span> 

```PowerShell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="41288-129">Этот командлет сравнивает все хэши файлов и их относительные пути в *каталоге* с хэшами и относительными путями на *диске*.</span><span class="sxs-lookup"><span data-stu-id="41288-129">This cmdlet compares all the files hashes and their relative paths found in *catalog* with ones on *disk*.</span></span> <span data-ttu-id="41288-130">При обнаружении любого несоответствия между хэшами файлов и путями он возвращает состояние *ValidationFailed*.</span><span class="sxs-lookup"><span data-stu-id="41288-130">If it detects any mismatch between file hashes and paths it returns the status as *ValidationFailed*.</span></span> <span data-ttu-id="41288-131">Все эти данные можно получить с помощью параметра *-Detailed*.</span><span class="sxs-lookup"><span data-stu-id="41288-131">Users can retrieve all this information by using the *-Detailed* parameter.</span></span> <span data-ttu-id="41288-132">Командлет также отображает состояние подписи каталога в свойстве *Signature*. Подпись также можно определить, вызвав командлет [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) и указав файл каталога.</span><span class="sxs-lookup"><span data-stu-id="41288-132">It also displays signing status of catalog in *Signature* property which is equivalent to calling [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet on the catalog file.</span></span> <span data-ttu-id="41288-133">Также можно исключить любые файлы из проверки, указав их в параметре *-FilesToSkip*.</span><span class="sxs-lookup"><span data-stu-id="41288-133">Users can also skip any file during validation by using the *-FilesToSkip* parameter.</span></span> 


## <a name="module-analysis-cache"></a><span data-ttu-id="41288-134">Кэш анализа модуля</span><span class="sxs-lookup"><span data-stu-id="41288-134">Module Analysis Cache</span></span> ##
<span data-ttu-id="41288-135">Начиная с версии WMF 5.1 среда PowerShell предоставляет средства управления файлом, в котором кэшируются сведения о модуле, например экспортируемые им команды.</span><span class="sxs-lookup"><span data-stu-id="41288-135">Starting with WMF 5.1, PowerShell provides control over the file that is used to cache data about a module, such as the commands it exports.</span></span>

<span data-ttu-id="41288-136">По умолчанию этот кэш хранится в файле `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="41288-136">By default, this cache is stored in the file `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="41288-137">Кэш обычно считывается при запуске в процессе поиска команды и записывается в фоновом потоке через некоторое время после импорта модуля.</span><span class="sxs-lookup"><span data-stu-id="41288-137">The cache is typically read at startup while searching for a command and is written on a background thread sometime after a module is imported.</span></span>

<span data-ttu-id="41288-138">Чтобы изменить расположение кэша по умолчанию, присвойте значение переменной среды `$env:PSModuleAnalysisCachePath` перед запуском PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41288-138">To change the default location of the cache, set the `$env:PSModuleAnalysisCachePath` environment variable before starting PowerShell.</span></span> <span data-ttu-id="41288-139">Изменения, вносимые в эту переменную среды, влияют только на дочерние процессы.</span><span class="sxs-lookup"><span data-stu-id="41288-139">Changes to this environment variable will only affect children processes.</span></span> <span data-ttu-id="41288-140">Значение должно быть полным путем (включая имя файла), на создание и запись файлов по которому у среды PowerShell есть разрешение.</span><span class="sxs-lookup"><span data-stu-id="41288-140">The value should name a full path (including filename) that PowerShell has permission to create and write files.</span></span> <span data-ttu-id="41288-141">Чтобы отключить файловый кэш, укажите в качестве этого значения недопустимое расположение, например:</span><span class="sxs-lookup"><span data-stu-id="41288-141">To disable the file cache, set this value to an invalid location, for example:</span></span>

```PowerShell
$env:PSModuleAnalysisCachePath = 'nul'
```

<span data-ttu-id="41288-142">Таким образом задается путь к недопустимому устройству.</span><span class="sxs-lookup"><span data-stu-id="41288-142">This sets the path to an invalid device.</span></span> <span data-ttu-id="41288-143">Если среда PowerShell не может осуществлять запись по указанному пути, ошибка не выводится; сообщения об ошибках можно получить, используя трассировщик:</span><span class="sxs-lookup"><span data-stu-id="41288-143">If PowerShell can't write to the path, no error is returned, but you can see error reporting by using a tracer:</span></span>

```PowerShell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

<span data-ttu-id="41288-144">При выгрузке кэша среда PowerShell ищет модули, которые больше не существуют, чтобы кэш не был излишне большим.</span><span class="sxs-lookup"><span data-stu-id="41288-144">When writing out the cache, PowerShell will check for modules that no longer exist to avoid an unnecessarily large cache.</span></span>
<span data-ttu-id="41288-145">Иногда эти проверки нежелательны. В этом случае их можно отключить, задав</span><span class="sxs-lookup"><span data-stu-id="41288-145">Sometimes these checks are not desirable, in which case you can turn them off by setting:</span></span>

```PowerShell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

<span data-ttu-id="41288-146">Новое значение этой переменной среды вступает в силу немедленно в текущем процессе.</span><span class="sxs-lookup"><span data-stu-id="41288-146">Setting this environment variable will take effect immediately in the current process.</span></span>

##<a name="specifying-module-version"></a><span data-ttu-id="41288-147">Указание версии модуля</span><span class="sxs-lookup"><span data-stu-id="41288-147">Specifying module version</span></span>

<span data-ttu-id="41288-148">В WMF 5.1 `using module` работает так же, как другие связанные с модулями конструкции в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41288-148">In WMF 5.1, `using module` behaves the same way as other module-related constructions in PowerShell.</span></span> <span data-ttu-id="41288-149">Ранее не было возможности указать определенную версию модуля; при наличии нескольких версий возникала ошибка.</span><span class="sxs-lookup"><span data-stu-id="41288-149">Previously, you had no way to specify a particular module version; if there were multiple versions present, this resulted in an error.</span></span>


<span data-ttu-id="41288-150">В WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="41288-150">In WMF 5.1:</span></span>

* <span data-ttu-id="41288-151">Можно использовать [хэш-таблицу](https://msdn.microsoft.com/en-us/library/jj136290(v=vs.85).aspx) `ModuleSpecification`.</span><span class="sxs-lookup"><span data-stu-id="41288-151">You can use `ModuleSpecification` [hash table](https://msdn.microsoft.com/en-us/library/jj136290(v=vs.85).aspx).</span></span> <span data-ttu-id="41288-152">Она имеет тот же формат, что и `Get-Module -FullyQualifiedName`.</span><span class="sxs-lookup"><span data-stu-id="41288-152">This hash table has the same format as `Get-Module -FullyQualifiedName`.</span></span>

<span data-ttu-id="41288-153">**Пример:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span><span class="sxs-lookup"><span data-stu-id="41288-153">**Example:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`</span></span>

* <span data-ttu-id="41288-154">Если имеется несколько версий модуля, в PowerShell используется **та же логика разрешения**, что и в `Import-Module`, и ошибка не выводится. Это поведение аналогично поведению `Import-Module` и `Import-DscResource`.</span><span class="sxs-lookup"><span data-stu-id="41288-154">If there are multiple versions of the module, PowerShell uses the **same resolution logic** as `Import-Module` and doesn't return an error--the same behavior as `Import-Module` and `Import-DscResource`.</span></span>


##<a name="improvements-to-pester"></a><span data-ttu-id="41288-155">Усовершенствования Pester</span><span class="sxs-lookup"><span data-stu-id="41288-155">Improvements to Pester</span></span>
<span data-ttu-id="41288-156">В WMF 5.1 версия Pester, распространяемая с PowerShell, была обновлена с 3.3.5 до 3.4.0. Также в репозиторий были отправлены изменения https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, которые улучшают работу Pester с Nano Server.</span><span class="sxs-lookup"><span data-stu-id="41288-156">In WMF 5.1, the version of Pester that ships with PowerShell has been updated from 3.3.5 to 3.4.0, with the addition of commit https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, which enables better behavior for Pester on Nano Server.</span></span> 

<span data-ttu-id="41288-157">Изменения, произошедшие в версиях с 3.3.5 по 3.4.0, можно найти в файле ChangeLog.md по следующей ссылке: https://github.com/pester/Pester/blob/master/CHANGELOG.md.</span><span class="sxs-lookup"><span data-stu-id="41288-157">You can review the changes in versions 3.3.5 to 3.4.0 by inspecting the ChangeLog.md file at: https://github.com/pester/Pester/blob/master/CHANGELOG.md</span></span>

