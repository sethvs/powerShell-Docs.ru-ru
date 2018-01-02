---
ms.date: 2017-10-17
contributor: keithb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: PrereleaseScript
ms.openlocfilehash: 2787e63944953d631b079f9e86a60ea5f3da768f
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="prerelease-versions-of-scripts"></a><span data-ttu-id="0bd5a-103">Предварительные версии сценариев</span><span class="sxs-lookup"><span data-stu-id="0bd5a-103">Prerelease Versions of Scripts</span></span>

<span data-ttu-id="0bd5a-104">Начиная с версии 1.6.0, PowerShellGet и коллекция PowerShell поддерживают маркировку версий с номерами выше 1.0.0 как предварительных.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="0bd5a-105">До этого номера предварительных версий должны были обязательно начинаться с 0.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="0bd5a-106">Такая возможность добавлена, чтобы улучшить поддержку соглашения о версиях [SemVer 1.0.0](http://semver.org/spec/v1.0.0.html) и при этом сохранить обратную совместимость с PowerShell версий 3 и выше, а также с текущими версиями PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="0bd5a-107">Этот раздел описывает особенности присвоения версий сценариям.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-107">This topic focuses on the script-specific features.</span></span> <span data-ttu-id="0bd5a-108">Аналогичные возможности для модулей см. в разделе [Предварительные версии модулей](../module/PrereleaseModule.md).</span><span class="sxs-lookup"><span data-stu-id="0bd5a-108">The equivalent features for modules are in the [Prerelease Module Versions](../module/PrereleaseModule.md) topic.</span></span> <span data-ttu-id="0bd5a-109">Благодаря этой возможности издатель может присвоить своему сценарию предварительную версию 2.5.0-alpha, а затем выпустить готовую к использованию версию 2.5.0, которая заменит предварительную.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-109">Using these features, publishers can identify a script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span> 

<span data-ttu-id="0bd5a-110">На высоком уровне возможности для предварительных версий сценариев включают:</span><span class="sxs-lookup"><span data-stu-id="0bd5a-110">At a high level, the prerelease script features include:</span></span>

* <span data-ttu-id="0bd5a-111">добавление суффикса PrereleaseString в строку версии в манифесте сценария.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-111">Adding a PrereleaseString suffix to the version string in the script manifest.</span></span> <span data-ttu-id="0bd5a-112">При публикации сценариев в коллекцию PowerShell эти данные извлекаются из манифеста и используются для определения элементов с предварительными версиями.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-112">When the scripts is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
* <span data-ttu-id="0bd5a-113">Для получения предварительных версий необходимо добавить флаг -AllowPrerelease к следующим командам PowerShellGet: Find-Script, Install-Script, Update-Script и Save-Script.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Script, Install-Script, Update-Script, and Save-Script.</span></span> <span data-ttu-id="0bd5a-114">Если этот флаг не поставлен, предварительные версии не отображаются.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-114">If the flag is not specified, prerelease items will not be shown.</span></span> 
* <span data-ttu-id="0bd5a-115">Версии сценариев, отображаемые командлетами Find-Script и Get-InstalledScript, а также версии в коллекции PowerShell будут отображаться с параметром PrereleaseString, например: 2.5.0-alpha.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-115">Script versions displayed by Find-Script, Get-InstalledScript, and in the PowerShell Gallery will be displayed with the PrereleaseString, as in 2.5.0-alpha.</span></span> 

<span data-ttu-id="0bd5a-116">Ниже приведено подробное описание этих возможностей.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-116">Details for the features are included below.</span></span> 


## <a name="identifying-a-script-version-as-a-prerelease"></a><span data-ttu-id="0bd5a-117">Определение версии сценария как предварительной</span><span class="sxs-lookup"><span data-stu-id="0bd5a-117">Identifying a script version as a prerelease</span></span> 

<span data-ttu-id="0bd5a-118">Реализация предварительных версий в PowerShellGet для сценариев проще, чем для модулей.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-118">PowerShellGet support for prerelease versions is easier for scripts than modules.</span></span> <span data-ttu-id="0bd5a-119">Контроль версий сценариев поддерживается только в PowerShellGet, поэтому добавление суффикса к номеру предварительной версии не вызовет проблем совместимости.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-119">Script versioning is only supported by PowerShellGet, so there are no compatibility issues caused by adding the prerelease string.</span></span> <span data-ttu-id="0bd5a-120">Для определения версии сценария в коллекции PowerShell как предварительной, добавьте суффикс предварительной версии к правильно сформированной строке версии в метаданных сценария.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-120">To identify a script in the PowerShell Gallery as a prerelease, add a prerelease suffix to a properly-formatted version string in the script metadata.</span></span> 

<span data-ttu-id="0bd5a-121">Пример манифеста сценария с предварительной версией</span><span class="sxs-lookup"><span data-stu-id="0bd5a-121">An example section of a script manifest with a prerelease version would look like the following:</span></span>
```powershell
<#PSScriptInfo
            
.VERSION 3.2.1-alpha12
            
.GUID 

...

#>

```

<span data-ttu-id="0bd5a-122">Для использования суффикса предварительной версии строка версии должна удовлетворять следующим условиям.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-122">To use a prerelease suffix, the version string must meet the following requirements:</span></span> 

* <span data-ttu-id="0bd5a-123">Суффикс предварительной версии можно указать, только если версия состоит из трех сегментов в виде <основная_версия>.<дополнительная_версия>.<сборка>.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-123">A prerelease suffix may only be specified when the Version is 3 segments for Major.Minor.Build.</span></span> <span data-ttu-id="0bd5a-124">Это соответствует соглашению о версиях SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-124">This aligns with SemVer v1.0.0</span></span>
* <span data-ttu-id="0bd5a-125">Суффикс предварительной версии — это строка, которая начинается с дефиса и может содержать буквенно-цифровые символы ASCII [0-9A-Za-z-].</span><span class="sxs-lookup"><span data-stu-id="0bd5a-125">The prerelease suffix is a string which begins with a hyphen, and may contain ASCII alphanumerics [0-9A-Za-z-]</span></span>
* <span data-ttu-id="0bd5a-126">В настоящий момент поддерживается только SemVer версии 1.0.0, поэтому суффикс предварительной версии __не должен__ содержать ни точек, ни символов + [.+], которые допустимы в SemVer 2.0.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-126">Only SemVer v1.0.0 prerelease strings are supported at this time, so the prerelease suffix __must not__ contain either period or + [.+], which are allowed in SemVer 2.0</span></span> 
* <span data-ttu-id="0bd5a-127">Пример допустимых строк PrereleaseString: -alpha, -alpha1, -BETA, -update20171020</span><span class="sxs-lookup"><span data-stu-id="0bd5a-127">Examples of supported PrereleaseString strings are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="0bd5a-128">__Влияние предварительных версий на порядок сортировки и установочные папки__</span><span class="sxs-lookup"><span data-stu-id="0bd5a-128">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="0bd5a-129">При использовании предварительных версий изменяется порядок сортировки, что имеет значение при публикации сценариев в коллекции PowerShell и при установке сценариев с помощью команд PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-129">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing scripts using PowerShellGet commands.</span></span> <span data-ttu-id="0bd5a-130">Если существует две версии сценария с одним номером, то сортировка производится по части строки, следующей после дефиса.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-130">If two scripts versions with the version number exist, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="0bd5a-131">Таким образом версия 2.5.0-alpha меньше, чем 2.5.0-beta, а последняя меньше, чем 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-131">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="0bd5a-132">Если два сценария имеют одинаковый номер версии и только у одного из них есть строка PrereleaseString, то готовым к использованию будет считаться сценарий __без__ суффикса предварительной версии и при сортировке он будет указываться, как имеющий более высокую версию по отношению к предварительной.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-132">If two scripts have the same version number, and only one has a PrereleaseString, the script __without__ the prerelease suffix is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version.</span></span> <span data-ttu-id="0bd5a-133">Например: при сравнении версий 2.5.0 и 2.5.0-beta, будет считаться, что версия 2.5.0 имеет больший номер.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-133">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span> 

<span data-ttu-id="0bd5a-134">По умолчанию при публикации в коллекцию PowerShell новый сценарий обязательно должен иметь более высокую версию, чем все сценарии, опубликованные ранее.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-134">When publishing to the PowerShell Gallery, by default the version of the script being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> <span data-ttu-id="0bd5a-135">Издатель может обновить версию 2.5.0-alpha версией 2.5.0-beta или 2.5.0 (без суффикса предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="0bd5a-135">A publisher may update version 2.5.0-alpha with 2.5.0-beta, or with 2.5.0 (with no prerelease suffix).</span></span>

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="0bd5a-136">Поиск и получение предварительных версий при помощи команд PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="0bd5a-136">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="0bd5a-137">Для работы с предварительными версиями при помощи PowerShellGet-команд Find-Script, Install-Script, Update-Script и Save-Script необходимо добавлять флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-137">Dealing with prerelease items using PowerShellGet Find-Script, Install-Script, Update-Script, and Save-Script commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="0bd5a-138">Если задан флаг -AllowPrerelease, то в результат выполнения команды будут включены предварительные версии элементов при их наличии.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-138">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span>
<span data-ttu-id="0bd5a-139">Если флаг -AllowPrerelease не задан, то предварительные версии не отображаются.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-139">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span> 

<span data-ttu-id="0bd5a-140">Единственным исключением является команда Get-InstalledScript и в некоторых случаях команда Uninstall-Script.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-140">The only exceptions to this in the PowerShellGet script commands are Get-InstalledScript, and some cases with Uninstall-Script.</span></span> 

* <span data-ttu-id="0bd5a-141">Команда Get-InstalledScript всегда автоматически отображает информацию о предварительных версиях в строке версии при ее наличии.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-141">Get-InstalledScript always will automatically show the prerelease information in the version string if it is present.</span></span> 
* <span data-ttu-id="0bd5a-142">Если __номер версии не указан__, то по умолчанию команда Uninstall-Script удалит самую последнюю версию сценария.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-142">Uninstall-Script will by default uninstall the most recent version of a script, if __no version__ is specified.</span></span> <span data-ttu-id="0bd5a-143">Такое поведение команды осталось неизменным.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-143">That behavior has not changed.</span></span> <span data-ttu-id="0bd5a-144">Если в параметре -RequiredVersion указана предварительная версия, то необходимо будет также указать флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-144">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span> 

## <a name="examples"></a><span data-ttu-id="0bd5a-145">Примеры</span><span class="sxs-lookup"><span data-stu-id="0bd5a-145">Examples</span></span>
```powershell
# Assume the PowerShell Gallery has TestPackage versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> Find-Script TestPackage 

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Find-Script TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# To install a prerelease, you must specify -AllowPrerelease. Specifying a prerelease version string is not sufficient. 

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and script name 'TestPackage'.
Try Get-PSRepository to see all available registered script repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

# Note that Get-InstalledScript shows the prerelease version. 
# If -RequiredVersion is not specified, all installed scripts will be displayed by Get-InstalledScript
```

<span data-ttu-id="0bd5a-146">Если не задан флаг -RequiredVersion, то команда Uninstall-Script удалит текущую версию сценария.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-146">Uninstall-Script will remove the current version of a script when -RequiredVersion is not supplied.</span></span> <span data-ttu-id="0bd5a-147">Если в параметре -RequiredVersion указана предварительная версия, то необходимо обязательно добавить к команде флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="0bd5a-147">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span> 

``` powershell
C:\windows\system32> Get-InstalledScript TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to PowerShe...

C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha
Uninstall-Script: The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Script TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Script], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-script


C:\windows\system32> Uninstall-Script TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
# Since script versions are not installed side-by-side, the above could be simply "Uninstall-Script TestPackage"

C:\windows\system32> Get-Installedscript TestPackage
PackageManagement\Get-Package : No match was found for the specified search criteria and script names 'testpackage'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.5.0.0\PSModule.psm1:4088 char:9
+         PackageManagement\Get-Package @PSBoundParameters | Microsoft. ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...lets.GetPackage:GetPackage) [Get-Package], Exception
    + FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.GetPackage


```



## <a name="more-details"></a><span data-ttu-id="0bd5a-148">Дополнительные подробности</span><span class="sxs-lookup"><span data-stu-id="0bd5a-148">More details</span></span>
### <a name="prerelease-module-versionsmoduleprereleasemodulemd"></a>[<span data-ttu-id="0bd5a-149">Предварительные версии модулей</span><span class="sxs-lookup"><span data-stu-id="0bd5a-149">Prerelease Module Versions</span></span>](../module/PrereleaseModule.md)
### <a name="find-scriptpsgetfind-scriptmd"></a>[<span data-ttu-id="0bd5a-150">Find-Script</span><span class="sxs-lookup"><span data-stu-id="0bd5a-150">Find-script</span></span>](./psget_find-script.md)
### <a name="install-scriptpsgetinstall-scriptmd"></a>[<span data-ttu-id="0bd5a-151">Install-Script</span><span class="sxs-lookup"><span data-stu-id="0bd5a-151">Install-script</span></span>](./psget_install-script.md)
### <a name="save-scriptpsgetsave-scriptmd"></a>[<span data-ttu-id="0bd5a-152">Save-Script</span><span class="sxs-lookup"><span data-stu-id="0bd5a-152">Save-script</span></span>](./psget_save-script.md)
### <a name="update-scriptpsgetupdate-scriptmd"></a>[<span data-ttu-id="0bd5a-153">Update-Script</span><span class="sxs-lookup"><span data-stu-id="0bd5a-153">Update-script</span></span>](./psget_update-script.md)
### <a name="get-installedscriptpsgetget-installedscriptmd"></a>[<span data-ttu-id="0bd5a-154">Get-InstalledScript</span><span class="sxs-lookup"><span data-stu-id="0bd5a-154">Get-Installedscript</span></span>](./psget_get-installedscript.md)
### <a name="uninstall-scriptpsgetuninstall-scriptmd"></a>[<span data-ttu-id="0bd5a-155">Uninstall-Script</span><span class="sxs-lookup"><span data-stu-id="0bd5a-155">UnInstall-script</span></span>](./psget_uninstall-script.md)
