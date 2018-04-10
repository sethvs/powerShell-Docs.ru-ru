---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Find-RoleCapability
ms.openlocfilehash: 89aacd604d54f6a5e9752790be65cc3bcc77c8e1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="find-rolecapability"></a><span data-ttu-id="3ea51-103">Find-RoleCapability</span><span class="sxs-lookup"><span data-stu-id="3ea51-103">Find-RoleCapability</span></span>

<span data-ttu-id="3ea51-104">Находит возможности ролей в модулях.</span><span class="sxs-lookup"><span data-stu-id="3ea51-104">Finds role capabilities in modules.</span></span>

## <a name="description"></a><span data-ttu-id="3ea51-105">Описание</span><span class="sxs-lookup"><span data-stu-id="3ea51-105">Description</span></span>
<span data-ttu-id="3ea51-106">Командлет Find-RoleCapability находит возможности ролей PowerShell в модулях.</span><span class="sxs-lookup"><span data-stu-id="3ea51-106">The Find-RoleCapability cmdlet finds PowerShell role capabilities in modules.</span></span> <span data-ttu-id="3ea51-107">Find-RoleCapability ищет модули в зарегистрированных репозиториях.</span><span class="sxs-lookup"><span data-stu-id="3ea51-107">Find-RoleCapability searches modules in registered repositories.</span></span>
<span data-ttu-id="3ea51-108">Для каждой возможности роли, найденной командлетом, он возвращает объект PSGetRoleCapabilityInfo.</span><span class="sxs-lookup"><span data-stu-id="3ea51-108">For each role capability that this cmdlet finds, it returns a PSGetRoleCapabilityInfo object.</span></span> <span data-ttu-id="3ea51-109">Вы можете передать объект PSGetRoleCapabilityInfo в командлет Install-Module для установки модуля, содержащего эту возможность роли.</span><span class="sxs-lookup"><span data-stu-id="3ea51-109">You can pass a PSGetRoleCapabilityInfo object to the Install-Module cmdlet to install the module that contains the role capability.</span></span>
<span data-ttu-id="3ea51-110">Возможности ролей PowerShell определяют, какие команды, приложения и т. п. будут доступны пользователю в конечной точке Just Enough Administration (JEA).</span><span class="sxs-lookup"><span data-stu-id="3ea51-110">PowerShell role capabilities define which commands, applications, and so on are available to a user at a Just Enough Administration (JEA) endpoint.</span></span> <span data-ttu-id="3ea51-111">Возможности ролей определяются файлами с расширением PSRC.</span><span class="sxs-lookup"><span data-stu-id="3ea51-111">Role capabilities are defined by files with a .psrc extension.</span></span>

- <span data-ttu-id="3ea51-112">Командлет Find-RoleCapability позволяет выполнять фильтрацию с помощью параметров версии: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="3ea51-112">Find-RoleCapability can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="3ea51-113">Эти параметры являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="3ea51-113">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="3ea51-114">Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="3ea51-114">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="3ea51-115">Если параметр RequiredVersion не указан, командлет Find-RoleCapability возвращает последнюю версию модуля не ниже указанной минимальной версии или последнюю версию модуля, если минимальная версия не указана.</span><span class="sxs-lookup"><span data-stu-id="3ea51-115">If the RequiredVersion parameter is not specified, Find-RoleCapability returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="3ea51-116">Если параметр RequiredVersion указан, Find-RoleCapability возвращает только версию модуля, которая точно совпадает с указанной версией.</span><span class="sxs-lookup"><span data-stu-id="3ea51-116">If the RequiredVersion parameter is specified, Find-RoleCapability only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="3ea51-117">Командлет Find-RoleCapability позволяет фильтровать метаданные модуля с помощью параметра -Tag.</span><span class="sxs-lookup"><span data-stu-id="3ea51-117">Find-RoleCapability can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="3ea51-118">Find-RoleCapability позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.</span><span class="sxs-lookup"><span data-stu-id="3ea51-118">Find-RoleCapability can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="3ea51-119">Find-RoleCapability может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="3ea51-119">Find-RoleCapability can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="3ea51-120">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="3ea51-120">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="3ea51-121">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="3ea51-121">Cmdlet online help reference</span></span>

[<span data-ttu-id="3ea51-122">Find-RoleCapability</span><span class="sxs-lookup"><span data-stu-id="3ea51-122">Find-RoleCapability</span></span>](http://go.microsoft.com/fwlink/?LinkId=718029)

## <a name="example-commands"></a><span data-ttu-id="3ea51-123">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="3ea51-123">Example commands</span></span>
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```