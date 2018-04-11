---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс PackageManagement DSC
ms.openlocfilehash: e6eea9f0bae42e131976dacb9813da759ff31239
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-packagemanagement-resource"></a><span data-ttu-id="890ef-103">Ресурс PackageManagement DSC</span><span class="sxs-lookup"><span data-stu-id="890ef-103">DSC PackageManagement Resource</span></span>

> <span data-ttu-id="890ef-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="890ef-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="890ef-105">Ресурс **PackageManagement** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм установки пакетов управления пакетами на целевом узле или их удаления.</span><span class="sxs-lookup"><span data-stu-id="890ef-105">The **PackageManagement** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Package Management packages on a target node.</span></span> <span data-ttu-id="890ef-106">Для этого ресурса требуется модуль **PackageManagement**, доступный из http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="890ef-106">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="890ef-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="890ef-107">Syntax</span></span>

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="890ef-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="890ef-108">Properties</span></span>
|  <span data-ttu-id="890ef-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="890ef-109">Property</span></span>  |  <span data-ttu-id="890ef-110">Описание</span><span class="sxs-lookup"><span data-stu-id="890ef-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="890ef-111">Name</span><span class="sxs-lookup"><span data-stu-id="890ef-111">Name</span></span>| <span data-ttu-id="890ef-112">Указывает имя устанавливаемого или удаляемого пакета.</span><span class="sxs-lookup"><span data-stu-id="890ef-112">Specifies the name of the Package to be installed or uninstalled.</span></span>|
| <span data-ttu-id="890ef-113">Источник</span><span class="sxs-lookup"><span data-stu-id="890ef-113">Source</span></span>| <span data-ttu-id="890ef-114">Указывает имя источника пакета, в котором его можно найти.</span><span class="sxs-lookup"><span data-stu-id="890ef-114">Specifies the name of the package source where the package can be found.</span></span> <span data-ttu-id="890ef-115">Это может быть URI или источник, зарегистрированный с помощью ресурса DSC Register-PackageSource или PackageManagementSource.</span><span class="sxs-lookup"><span data-stu-id="890ef-115">This can either be a URI or a source registered with Register-PackageSource or PackageManagementSource DSC resource.</span></span> <span data-ttu-id="890ef-116">MSFT_PackageManagementSource ресурса DSC может также зарегистрировать источник пакета.</span><span class="sxs-lookup"><span data-stu-id="890ef-116">The DSC resource MSFT_PackageManagementSource can also register a package source.</span></span>|
| <span data-ttu-id="890ef-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="890ef-117">Ensure</span></span>| <span data-ttu-id="890ef-118">Определяет, следует ли установить или удалить пакет.</span><span class="sxs-lookup"><span data-stu-id="890ef-118">Determines whether the package is to be installed or uninstalled.</span></span>|
| <span data-ttu-id="890ef-119">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="890ef-119">RequiredVersion</span></span>| <span data-ttu-id="890ef-120">Указывает точную версию пакета, который вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="890ef-120">Specifies the exact version of the package that you want to install.</span></span> <span data-ttu-id="890ef-121">Если вы не укажете этот параметр, ресурс DSC установит новейшую версию пакета, соответствующую максимальной версии, указанной в параметре MaximumVersion.</span><span class="sxs-lookup"><span data-stu-id="890ef-121">If you do not specify this parameter, this DSC resource installs the newest available version of the package that also satisfies any maximum version specified by the MaximumVersion parameter.</span></span>|
| <span data-ttu-id="890ef-122">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="890ef-122">MinimumVersion</span></span>| <span data-ttu-id="890ef-123">Указывает минимальную версию пакета, которую вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="890ef-123">Specifies the minimum allowed version of the package that you want to install.</span></span> <span data-ttu-id="890ef-124">Если вы не добавите этот параметр, ресурс DSC установит новейшую версию пакета, соответствующую максимальной версии, указанной в параметре MaximumVersion.</span><span class="sxs-lookup"><span data-stu-id="890ef-124">If you do not add this parameter, this DSC resource intalls the highest available version of the package that also satisfies any maximum specified version specified by the MaximumVersion parameter.</span></span>|
| <span data-ttu-id="890ef-125">MaximumVersion</span><span class="sxs-lookup"><span data-stu-id="890ef-125">MaximumVersion</span></span>| <span data-ttu-id="890ef-126">Указывает максимальную версию пакета, которую вы хотите установить.</span><span class="sxs-lookup"><span data-stu-id="890ef-126">Specifies the maximum allowed version of the package that you want to install.</span></span> <span data-ttu-id="890ef-127">Если вы не укажете этот параметр, ресурс DSC установит новейшую версию пакета.</span><span class="sxs-lookup"><span data-stu-id="890ef-127">If you do not specify this parameter, this DSC resource installs the highest-numbered available version of the package.</span></span>|
| <span data-ttu-id="890ef-128">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="890ef-128">SourceCredential</span></span> | <span data-ttu-id="890ef-129">Указывает учетную запись пользователя с правами для установки пакета для заданного поставщика или источника пакетов.</span><span class="sxs-lookup"><span data-stu-id="890ef-129">Specifies a user account that has rights to install a package for a specified package provider or source.</span></span>|
| <span data-ttu-id="890ef-130">ProviderName</span><span class="sxs-lookup"><span data-stu-id="890ef-130">ProviderName</span></span>| <span data-ttu-id="890ef-131">Указывает имя поставщика пакетов, на который распространяется область поиска пакетов.</span><span class="sxs-lookup"><span data-stu-id="890ef-131">Specifies a package provider name to which to scope your package search.</span></span> <span data-ttu-id="890ef-132">Чтобы получить имена поставщика, запустите командлет Get-PackageProvider.</span><span class="sxs-lookup"><span data-stu-id="890ef-132">You can get package provider names by running the Get-PackageProvider cmdlet.</span></span>|
| <span data-ttu-id="890ef-133">AdditionalParameters</span><span class="sxs-lookup"><span data-stu-id="890ef-133">AdditionalParameters</span></span>| <span data-ttu-id="890ef-134">Специальные параметры поставщика, которые передаются как хэш-таблица.</span><span class="sxs-lookup"><span data-stu-id="890ef-134">Provider specific parameters that are passed as an Hashtable.</span></span> <span data-ttu-id="890ef-135">Например, для поставщика NuGet можно передать дополнительные параметры, такие как DestinationPath.</span><span class="sxs-lookup"><span data-stu-id="890ef-135">For example, for NuGet provider you can pass additional parameters like DestinationPath.</span></span>|

## <a name="additional-parameters"></a><span data-ttu-id="890ef-136">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="890ef-136">Additional Parameters</span></span>
<span data-ttu-id="890ef-137">В следующей таблице перечислены параметры свойства AdditionalParameters.</span><span class="sxs-lookup"><span data-stu-id="890ef-137">The following table lists options for the AdditionalParameters property.</span></span>
|  <span data-ttu-id="890ef-138">Параметр</span><span class="sxs-lookup"><span data-stu-id="890ef-138">Parameter</span></span>  | <span data-ttu-id="890ef-139">Описание</span><span class="sxs-lookup"><span data-stu-id="890ef-139">Description</span></span>   |
|---|---|
| <span data-ttu-id="890ef-140">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="890ef-140">DestinationPath</span></span>| <span data-ttu-id="890ef-141">Используется поставщиками, такими как встроенный поставщик NuGet.</span><span class="sxs-lookup"><span data-stu-id="890ef-141">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="890ef-142">Указывает расположение файла, в котором вы хотите установить пакет.</span><span class="sxs-lookup"><span data-stu-id="890ef-142">Specifies a file location where you want the package to be installed.</span></span>|
| <span data-ttu-id="890ef-143">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="890ef-143">InstallationPolicy</span></span>| <span data-ttu-id="890ef-144">Используется поставщиками, такими как встроенный поставщик NuGet.</span><span class="sxs-lookup"><span data-stu-id="890ef-144">Used by providers such as the built-in Nuget Provider.</span></span> <span data-ttu-id="890ef-145">Определяет, доверяете ли вы источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="890ef-145">Determines whether you trust the package's source.</span></span> <span data-ttu-id="890ef-146">Одно из двух значений: "Untrusted", "Trusted".</span><span class="sxs-lookup"><span data-stu-id="890ef-146">One of: "Untrusted", "Trusted".</span></span>|

## <a name="example"></a><span data-ttu-id="890ef-147">Пример</span><span class="sxs-lookup"><span data-stu-id="890ef-147">Example</span></span>

<span data-ttu-id="890ef-148">В этом примере устанавливается пакет NuGet **JQuery** и модуль PowerShell **GistProvider** с помощью ресурса DSC **PackageManagement**.</span><span class="sxs-lookup"><span data-stu-id="890ef-148">This example installs the **JQuery** NuGet package and **GistProvider** PowerShell module using the **PackageManagement** DSC resource.</span></span> <span data-ttu-id="890ef-149">В этом примере сначала обеспечивается доступность нужных источников пакета, а затем определяется ожидаемое состояние пакетов **JQuery** и **GistProvider** (для NuGet и PowerShell).</span><span class="sxs-lookup"><span data-stu-id="890ef-149">This example first ensures the required package sources are available then defines the expected state of the **JQuery** and **GistProvider** packages (NuGet and PowerShell, respectively).</span></span>

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceUri   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceUri   = "https://www.powershellgallery.com/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagement NugetPackage
    {
        Ensure               = "Present"
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1"
        DependsOn            = "[PackageManagementSource]SourceRepository"
    }

    PackageManagement PSModule
    {
        Ensure               = "Present"
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery"
    }
}
```