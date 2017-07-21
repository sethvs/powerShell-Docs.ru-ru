---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: Find-DscResource
ms.openlocfilehash: 37ba7925d6f73c453126f25e0818b3f8839d3b3b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="find-dscresource"></a><span data-ttu-id="26ed4-103">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="26ed4-103">Find-DscResource</span></span>

<span data-ttu-id="26ed4-104">Находит ресурсы DSC в модулях.</span><span class="sxs-lookup"><span data-stu-id="26ed4-104">Finds DSC Resources in modules.</span></span>

## <a name="description"></a><span data-ttu-id="26ed4-105">Описание</span><span class="sxs-lookup"><span data-stu-id="26ed4-105">Description</span></span>

<span data-ttu-id="26ed4-106">Командлет Find-DscResource ищет ресурсы [настройки требуемого состояния (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview), имеющиеся в модулях, соответствующих заданному условию, из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="26ed4-106">The Find-DscResource cmdlet finds [Desired State Configuration (DSC)](https://msdn.microsoft.com/en-us/PowerShell/dsc/overview) resources contained in modules that match the specified criteria from registered repositories.</span></span>
<span data-ttu-id="26ed4-107">Для каждого модуля, найденного командлетом Find-DscResource, он возвращает объект PSGetDscResourceInfo, который можно передать в командлет Install-Module, чтобы установить возвращенные этим командлетом модули, содержащие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="26ed4-107">For each module that this cmdlet finds, Find-DscResource returns a PSGetDscResourceInfo object that you can pipe to Install-Module to install the modules containing the resources that this cmdlet returns.</span></span>

<span data-ttu-id="26ed4-108">DSC — это новая платформа управления в Windows PowerShell, позволяющая развертывать данные конфигураций для служб программного обеспечения, а также управлять этими данными и средой, в которой выполняются такие службы.</span><span class="sxs-lookup"><span data-stu-id="26ed4-108">DSC is a new management platform in Windows PowerShell that enables deploying and managing configuration data for software services and managing the environment in which these services run.</span></span>

<span data-ttu-id="26ed4-109">Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC.</span><span class="sxs-lookup"><span data-stu-id="26ed4-109">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="26ed4-110">В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).</span><span class="sxs-lookup"><span data-stu-id="26ed4-110">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="26ed4-111">Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="26ed4-111">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span> <span data-ttu-id="26ed4-112">Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="26ed4-112">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

- <span data-ttu-id="26ed4-113">Командлет Find-DscResource позволяет выполнять фильтрацию с помощью параметров версии: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="26ed4-113">Find-DscResource can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="26ed4-114">Эти параметры являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="26ed4-114">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="26ed4-115">Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="26ed4-115">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="26ed4-116">Если параметр RequiredVersion не указан, командлет Find-DscResource возвращает последнюю версию модуля не ниже указанной минимальной версии или последнюю версию модуля, если минимальная версия не указана.</span><span class="sxs-lookup"><span data-stu-id="26ed4-116">If the RequiredVersion parameter is not specified, Find-DscResource returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="26ed4-117">Если параметр RequiredVersion указан, Find-DscResource возвращает только версию модуля, которая точно совпадает с указанной версией.</span><span class="sxs-lookup"><span data-stu-id="26ed4-117">If the RequiredVersion parameter is specified, Find-DscResource only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="26ed4-118">Find-DscResource позволяет фильтровать метаданные модуля с помощью параметра -Tag</span><span class="sxs-lookup"><span data-stu-id="26ed4-118">Find-DscResource can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="26ed4-119">Find-DscResource позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.</span><span class="sxs-lookup"><span data-stu-id="26ed4-119">Find-DscResource can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="26ed4-120">Find-DscResource может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="26ed4-120">Find-DscResource can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="26ed4-121">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="26ed4-121">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-DscResource -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="26ed4-122">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="26ed4-122">Cmdlet online help reference</span></span>

[<span data-ttu-id="26ed4-123">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="26ed4-123">Find-DscResource</span></span>](http://go.microsoft.com/fwlink/?LinkId=517196)

## <a name="example-commands"></a><span data-ttu-id="26ed4-124">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="26ed4-124">Example commands</span></span>
```powershell

# Find a specific DSC Resource
Find-DscResource -Name xIisFeatureDelegation

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
xIisFeatureDelegation               1.10.0.0   xWebAdministration                  PSGallery

# Find all available DSC Resources from all registered repositories
Find-DscResource

# Find a DSC resource by name
Find-DscResource -Name xWebsite

# Find multiple DSC Resources
Find-DscResource -Name xIisHandler, xFirewall

# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking
Find-DscResource -ModuleName xWebAdministration

# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

# Find available DSC Resources from few registered repositories
Find-DscResource -Repository PSGallery,PrivatePSGallery

# Find all DSC Resources in a specified repository
Find-DscResource -Repository PSGallery

# Find DSC Resources from all versions of a module
Find-DscResource -ModuleName xNetworking -AllVersions

# Find DSC Resources with module name and MinimumVersion.
Find-DscResource -ModuleName xNetworking -MinimumVersion 1.1

# Find DSC Resources with module name and exact version
Find-DscResource -ModuleName xNetworking -RequiredVersion 2.1.1

# Find DSC Resources defined modules with -Filter based search. -Filter searches in description and module names
Find-DscResource -Filter Domain

# Find all DSC Resources with tags Azure or DSC in module metadata
Find-DscResource -Tag Azure, DSC

```

