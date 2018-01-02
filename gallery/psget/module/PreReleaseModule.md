---
ms.date: 2017-09-26
contributor: keithb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: PrereleaseModule
ms.openlocfilehash: d2c629d0e0ec0d4a4adafe5994a37d3985d13a06
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="prerelease-module-versions"></a><span data-ttu-id="78a6b-103">Предварительные версии модулей</span><span class="sxs-lookup"><span data-stu-id="78a6b-103">Prerelease Module Versions</span></span>
<span data-ttu-id="78a6b-104">Начиная с версии 1.6.0, PowerShellGet и коллекция PowerShell поддерживают маркировку версий с номерами выше 1.0.0 как предварительных.</span><span class="sxs-lookup"><span data-stu-id="78a6b-104">Starting with version 1.6.0, PowerShellGet and the PowerShell Gallery provide support for tagging versions greater than 1.0.0 as a prerelease.</span></span> <span data-ttu-id="78a6b-105">До этого номера предварительных версий должны были обязательно начинаться с 0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-105">Prior to this feature, prerelease items were limited to having a version beginning with 0.</span></span> <span data-ttu-id="78a6b-106">Такая возможность добавлена, чтобы улучшить поддержку соглашения о версиях [SemVer 1.0.0](http://semver.org/spec/v1.0.0.html) и при этом сохранить обратную совместимость с PowerShell версий 3 и выше, а также с текущими версиями PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="78a6b-106">The goal of these features is to provide greater support for [SemVer v1.0.0](http://semver.org/spec/v1.0.0.html) versioning convention without breaking backwards compatibility with PowerShell versions 3 and above, or existing versions of PowerShellGet.</span></span> <span data-ttu-id="78a6b-107">Этот раздел описывает особенности присвоения версий модулям.</span><span class="sxs-lookup"><span data-stu-id="78a6b-107">This topic focuses on the module-specific features.</span></span> <span data-ttu-id="78a6b-108">Аналогичные возможности для сценариев см. в разделе [Предварительные версии сценариев](../script/PrereleaseScript.md).</span><span class="sxs-lookup"><span data-stu-id="78a6b-108">The equivalent features for scripts are in the [Prerelease Versions of Scripts](../script/PrereleaseScript.md) topic.</span></span> <span data-ttu-id="78a6b-109">Благодаря этой возможности издатель может присвоить своему модулю или сценарию предварительную версию 2.5.0-alpha, а затем выпустить готовую к использованию версию 2.5.0, которая заменит предварительную.</span><span class="sxs-lookup"><span data-stu-id="78a6b-109">Using these features, publishers can identify a module or script as version 2.5.0-alpha, and later release a production-ready version 2.5.0 that supersedes the prerelease version.</span></span> 

<span data-ttu-id="78a6b-110">На высоком уровне возможности для предварительных версий модулей включают следующее.</span><span class="sxs-lookup"><span data-stu-id="78a6b-110">At a high level, the prerelease module features include:</span></span>

* <span data-ttu-id="78a6b-111">Добавление строки предварительной версии в раздел PSData манифеста модуля определяет версию модуля как предварительную.</span><span class="sxs-lookup"><span data-stu-id="78a6b-111">Adding a Prerelease string to the PSData section of the module manifest identifies the module as a prerelease version.</span></span> <span data-ttu-id="78a6b-112">При публикации модуля в коллекции PowerShell эти данные извлекаются из манифеста и используются для определения элементов с предварительными версиями.</span><span class="sxs-lookup"><span data-stu-id="78a6b-112">When the module is published to the PowerShell Gallery, this data is extracted from the manifest, and used to identify prerelease items.</span></span>
* <span data-ttu-id="78a6b-113">Для получения предварительных версий необходимо добавить флаг -AllowPrerelease к следующим командам PowerShellGet: Find-Module, Install-Module, Update-Module и Save-Module.</span><span class="sxs-lookup"><span data-stu-id="78a6b-113">Acquiring prerelease items requires adding -AllowPrerelease flag to the PowerShellGet commands Find-Module, Install-Module, Update-Module, and Save-Module.</span></span> <span data-ttu-id="78a6b-114">Если этот флаг не поставлен, предварительные версии не отображаются.</span><span class="sxs-lookup"><span data-stu-id="78a6b-114">If the flag is not specified, prerelease items will not be shown.</span></span>  
* <span data-ttu-id="78a6b-115">Версии модулей, отображаемые Find-Module и Get-InstalledModule, а также в коллекции PowerShell, будут отображаться как одна строка с добавлением строки предварительной версии, например: 2.5.0-alpha.</span><span class="sxs-lookup"><span data-stu-id="78a6b-115">Module versions displayed by Find-Module, Get-InstalledModule, and in the PowerShell Gallery will be displayed as a single string with the Prerelease string appended, as in 2.5.0-alpha.</span></span> 

<span data-ttu-id="78a6b-116">Ниже приведено подробное описание этих возможностей.</span><span class="sxs-lookup"><span data-stu-id="78a6b-116">Details for the features are included below.</span></span> 

<span data-ttu-id="78a6b-117">Данные изменения совместимы с PowerShell 3.0, 4.0 и 5 и не влияют на поддержку версий модулей, встроенную в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78a6b-117">These changes do not affect the module version support that is built into PowerShell, and are compatible with PowerShell 3.0, 4.0, and 5.</span></span> 

## <a name="identifying-a-module-version-as-a-prerelease"></a><span data-ttu-id="78a6b-118">Определение версии модуля как предварительной</span><span class="sxs-lookup"><span data-stu-id="78a6b-118">Identifying a module version as a prerelease</span></span> 

<span data-ttu-id="78a6b-119">Для использования предварительных версий в PowerShellGet необходимо заполнить два поля в манифесте модуля.</span><span class="sxs-lookup"><span data-stu-id="78a6b-119">PowerShellGet support for prerelease versions requires the use of two fields within the Module Manifest:</span></span>

* <span data-ttu-id="78a6b-120">Версия в поле ModuleVersion манифеста модуля должна состоять из трех частей и соответствовать текущей системе версий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78a6b-120">The ModuleVersion included in the module manifest must be a 3-part version if a prerelease version is used, and must comply with existing PowerShell versioning.</span></span> <span data-ttu-id="78a6b-121">Формат версии должен быть вида A.B.C, где A, B и C — целые числа.</span><span class="sxs-lookup"><span data-stu-id="78a6b-121">The version format would be A.B.C, where A, B, and C are all integers.</span></span> 
* <span data-ttu-id="78a6b-122">Строка предварительной версии задается в подразделе PSData раздела PrivateData в манифесте модуля.</span><span class="sxs-lookup"><span data-stu-id="78a6b-122">The Prerelease string is specified in the module manifest, in the PSData section of PrivateData.</span></span> <span data-ttu-id="78a6b-123">Ниже приведены подробные требования к строке предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="78a6b-123">Detailed requirements on the Prerelease string are below.</span></span> 

<span data-ttu-id="78a6b-124">Пример раздела манифеста модуля, определяющего версию модуля как предварительную</span><span class="sxs-lookup"><span data-stu-id="78a6b-124">An example section of a module manifest that defines a module as a prerelease would look like the following:</span></span>
```powershell
@{
    ModuleVersion = '2.5.0'
    #---
    PrivateData = @{
        PSData = @{
            Prerelease = 'alpha'
        }
    }
}
```

<span data-ttu-id="78a6b-125">Подробные требования к строке предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="78a6b-125">The detailed requirements for Prerelease string are:</span></span> 

* <span data-ttu-id="78a6b-126">Строку предварительной версии можно указать, только если версия в поле ModuleVersion состоит из трех сегментов в виде <основная_версия>.<дополнительная_версия>.<сборка>.</span><span class="sxs-lookup"><span data-stu-id="78a6b-126">Prerelease string may only be specified when the ModuleVersion is 3 segments for Major.Minor.Build.</span></span> <span data-ttu-id="78a6b-127">Это соответствует соглашению о версиях SemVer 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-127">This aligns with SemVer v1.0.0.</span></span>
* <span data-ttu-id="78a6b-128">Разделителем между номером сборки и строкой предварительной версии является дефис.</span><span class="sxs-lookup"><span data-stu-id="78a6b-128">A hyphen is the delimiter between the Build number and the Prerelease string.</span></span> <span data-ttu-id="78a6b-129">Дефис может включен в строку предварительной версии только как первый символ.</span><span class="sxs-lookup"><span data-stu-id="78a6b-129">A hyphen may be included in the Prerelease string as the first character, only.</span></span>
* <span data-ttu-id="78a6b-130">Строка предварительной версии может содержать только буквенно-цифровые символы ASCII [0-9A-Za-z-].</span><span class="sxs-lookup"><span data-stu-id="78a6b-130">The Prerelease string may contain only ASCII alphanumerics [0-9A-Za-z-].</span></span> <span data-ttu-id="78a6b-131">Рекомендуем начинать эту строку с буквы, так как в таком случае проще отличать предварительные версии при просмотре списка элементов.</span><span class="sxs-lookup"><span data-stu-id="78a6b-131">It is a best practice to begin the Prerelease string with an alpha character, as it will be easier to identify that this is a prerelease version when scanning a list of items.</span></span> 
* <span data-ttu-id="78a6b-132">В настоящий момент поддерживается только SemVer версии 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-132">Only SemVer v1.0.0 prerelease strings are supported at this time.</span></span> <span data-ttu-id="78a6b-133">Строка предварительной версии __не должна__ содержать ни точек, ни символов + [.+], которые допустимы в SemVer 2.0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-133">Prerelease string __must not__ contain either period or + [.+], which are allowed in SemVer 2.0.</span></span> 
* <span data-ttu-id="78a6b-134">Пример поддерживаемых строк предварительной версии: -alpha, -alpha1, -BETA, -update20171020</span><span class="sxs-lookup"><span data-stu-id="78a6b-134">Examples of supported Prerelease string are: -alpha, -alpha1, -BETA, -update20171020</span></span>

<span data-ttu-id="78a6b-135">__Влияние предварительных версий на порядок сортировки и установочные папки__</span><span class="sxs-lookup"><span data-stu-id="78a6b-135">__Prerelease versioning impact on sort order and installation folders__</span></span>

<span data-ttu-id="78a6b-136">При использовании предварительных версий изменяется порядок сортировки, что имеет значение при публикации сценариев в коллекции PowerShell и при установке модулей с помощью команд PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="78a6b-136">Sort order changes when using a prerelease version, which is important when publishing to the PowerShell Gallery, and when installing modules using PowerShellGet commands.</span></span> <span data-ttu-id="78a6b-137">Если строка предварительной версии задана для двух модулей, то сортировка производится по части строки, следующей после дефиса.</span><span class="sxs-lookup"><span data-stu-id="78a6b-137">If the Prerelease string is specified for two modules, the sort order is based on the string portion following the hyphen.</span></span> <span data-ttu-id="78a6b-138">Таким образом версия 2.5.0-alpha меньше, чем 2.5.0-beta, а последняя меньше, чем 2.5.0-gamma.</span><span class="sxs-lookup"><span data-stu-id="78a6b-138">So, version 2.5.0-alpha is less than 2.5.0-beta, which is less than 2.5.0-gamma.</span></span> <span data-ttu-id="78a6b-139">Если два модуля обладают одинаковым значением ModuleVersion и только у одного из них есть строка предварительной версии, то готовым к использованию модулем будет считаться модуль без этой строки и при сортировке он будет указываться, как имеющий более высокую версию по отношению к предварительной (включающей строку предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="78a6b-139">If two modules have the same ModuleVersion, and only one has a Prerelease string, the module without the Prerelease string is assumed to be the production-ready version and will be sorted as a greater version than the prerelease version (which includes the Prerelease string).</span></span> <span data-ttu-id="78a6b-140">Например: при сравнении версий 2.5.0 и 2.5.0-beta, будет считаться, что версия 2.5.0 имеет больший номер.</span><span class="sxs-lookup"><span data-stu-id="78a6b-140">As an example, when comparing releases 2.5.0 and 2.5.0-beta, the 2.5.0 version will be considered the greater of the two.</span></span> 

<span data-ttu-id="78a6b-141">По умолчанию при публикации в коллекции PowerShell новый модуль обязательно должен иметь более высокую версию, чем все модули, опубликованные ранее.</span><span class="sxs-lookup"><span data-stu-id="78a6b-141">When publishing to the PowerShell Gallery, by default the version of the module being published must have a greater version than any previously-published version that is in the PowerShell Gallery.</span></span> 

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a><span data-ttu-id="78a6b-142">Поиск и получение предварительных версий при помощи команд PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="78a6b-142">Finding and acquiring prerelease items using PowerShellGet commands</span></span>

<span data-ttu-id="78a6b-143">Для работы с предварительными версиями при помощи PowerShellGet-команд Find-Module, Install-Module, Update-Module и Save-Module необходимо добавлять флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="78a6b-143">Dealing with prerelease items using PowerShellGet Find-Module, Install-Module, Update-Module, and Save-Module commands requires adding the -AllowPrerelease flag.</span></span> <span data-ttu-id="78a6b-144">Если задан флаг -AllowPrerelease, то в результат выполнения команды будут включены предварительные версии элементов при их наличии.</span><span class="sxs-lookup"><span data-stu-id="78a6b-144">If -AllowPrerelease is specified, prerelease items will be included if they are present.</span></span>
<span data-ttu-id="78a6b-145">Если флаг -AllowPrerelease не задан, то предварительные версии не отображаются.</span><span class="sxs-lookup"><span data-stu-id="78a6b-145">If -AllowPrerelease flag is not specified, prerelease items will not be shown.</span></span> 

<span data-ttu-id="78a6b-146">Единственным исключением является команда Get-InstalledModule и в некоторых случаях команда Uninstall-Module.</span><span class="sxs-lookup"><span data-stu-id="78a6b-146">The only exceptions to this in the PowerShellGet module commands are Get-InstalledModule, and some cases with Uninstall-Module.</span></span> 

* <span data-ttu-id="78a6b-147">Команда Get-InstalledModule всегда автоматически показывает информацию о предварительных версиях в строке версии для модулей.</span><span class="sxs-lookup"><span data-stu-id="78a6b-147">Get-InstalledModule always will automatically show the prerelease information in the version string for modules.</span></span> 
* <span data-ttu-id="78a6b-148">Если __номер версии не указан__, то по умолчанию команда Uninstall-Module удалит самую последнюю версию модуля.</span><span class="sxs-lookup"><span data-stu-id="78a6b-148">Uninstall-Module will by default uninstall the most recent version of a module, if __no version__ is specified.</span></span> <span data-ttu-id="78a6b-149">Такое поведение команды осталось неизменным.</span><span class="sxs-lookup"><span data-stu-id="78a6b-149">That behavior has not changed.</span></span> <span data-ttu-id="78a6b-150">Если в параметре -RequiredVersion указана предварительная версия, то необходимо будет также указать флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="78a6b-150">However, if a prerelease version is specified using -RequiredVersion, -AllowPrerelease will be required.</span></span> 

## <a name="examples"></a><span data-ttu-id="78a6b-151">Примеры</span><span class="sxs-lookup"><span data-stu-id="78a6b-151">Examples</span></span>
```powershell
# Assume the PowerShell Gallery has TestPackage module versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> find-module TestPackage 

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

# To install a prerelease, always specify -AllowPrerelease. Specifying a prerelease version string is not sufficient. 

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

<span data-ttu-id="78a6b-152">Не поддерживается одновременная установка модулей, версии которых отличаются только значением предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="78a6b-152">Side-by-side installation of versions of a module that differ only due to the prerelease specified is not supported.</span></span> <span data-ttu-id="78a6b-153">При использовании PowerShellGet разные версии одного модуля могут быть установлены одновременно. Каждая из них помещается в папку с именем, использующим значение ModuleVersion.</span><span class="sxs-lookup"><span data-stu-id="78a6b-153">When installing a module using PowerShellGet, different versions of the same module are installed side-by-side by creating a folder name using the ModuleVersion.</span></span> <span data-ttu-id="78a6b-154">ModuleVersion используется для имени папки без добавления строки предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="78a6b-154">The ModuleVersion, without the prerelease string, is used for the folder name.</span></span> <span data-ttu-id="78a6b-155">Если пользователь установит модуль MyModule версии 2.5.0-alpha, этот модуль будет помещен в папку MyModule\2.5.0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-155">If a user installs MyModule version 2.5.0-alpha, it will be installed to the MyModule\2.5.0 folder.</span></span> <span data-ttu-id="78a6b-156">Если пользователь затем установит версию 2.5.0-beta, то она __перезапишет__ содержимое папки MyModule\2.5.0.</span><span class="sxs-lookup"><span data-stu-id="78a6b-156">If the user then installs 2.5.0-beta, the 2.5.0-beta version will __over-write__ the contents of the folder MyModule\2.5.0.</span></span> <span data-ttu-id="78a6b-157">Одним из преимуществ такого подхода является то, что нет необходимости удалять предварительную версию после установки версии, готовой к использованию.</span><span class="sxs-lookup"><span data-stu-id="78a6b-157">One advantage to this approach is that there is no need to un-install the prerelease version after installing the production-ready version.</span></span> <span data-ttu-id="78a6b-158">Пример ниже иллюстрирует работу этого правила.</span><span class="sxs-lookup"><span data-stu-id="78a6b-158">The example below shows what to expect:</span></span>


``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-beta     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

<span data-ttu-id="78a6b-159">Если не задан флаг -RequiredVersion, то команда Uninstall-Module удалит самую последнюю версию модуля.</span><span class="sxs-lookup"><span data-stu-id="78a6b-159">Uninstall-Module will remove the latest version of a module when -RequiredVersion is not supplied.</span></span> <span data-ttu-id="78a6b-160">Если в параметре -RequiredVersion указана предварительная версия, то необходимо обязательно добавить к команде флаг -AllowPrerelease.</span><span class="sxs-lookup"><span data-stu-id="78a6b-160">If -RequiredVersion is specified, and is a prerelease, -AllowPrerelease must be added to the command.</span></span> 

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta
Uninstall-Module : The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-Module



C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...


```



## <a name="more-details"></a><span data-ttu-id="78a6b-161">Дополнительные подробности</span><span class="sxs-lookup"><span data-stu-id="78a6b-161">More details</span></span>
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[<span data-ttu-id="78a6b-162">Предварительные версии сценариев</span><span class="sxs-lookup"><span data-stu-id="78a6b-162">Prerelease Script Versions</span></span>](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[<span data-ttu-id="78a6b-163">Find-Module</span><span class="sxs-lookup"><span data-stu-id="78a6b-163">Find-Module</span></span>](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[<span data-ttu-id="78a6b-164">Install-Module</span><span class="sxs-lookup"><span data-stu-id="78a6b-164">Install-Module</span></span>](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[<span data-ttu-id="78a6b-165">Save-Module</span><span class="sxs-lookup"><span data-stu-id="78a6b-165">Save-Module</span></span>](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[<span data-ttu-id="78a6b-166">Update-Module</span><span class="sxs-lookup"><span data-stu-id="78a6b-166">Update-Module</span></span>](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[<span data-ttu-id="78a6b-167">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="78a6b-167">Get-InstalledModule</span></span>](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[<span data-ttu-id="78a6b-168">Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="78a6b-168">UnInstall-Module</span></span>](./psget_uninstall-module.md)
