---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Find-Command
ms.openlocfilehash: 26ddf4824816db245131a0fc95b7d2a88bef8f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="find-command"></a><span data-ttu-id="b2c68-103">Find-Command</span><span class="sxs-lookup"><span data-stu-id="b2c68-103">Find-Command</span></span>

<span data-ttu-id="b2c68-104">Ищет команды PowerShell в модулях.</span><span class="sxs-lookup"><span data-stu-id="b2c68-104">Finds PowerShell commands in modules.</span></span>

## <a name="description"></a><span data-ttu-id="b2c68-105">Описание</span><span class="sxs-lookup"><span data-stu-id="b2c68-105">Description</span></span>
<span data-ttu-id="b2c68-106">Командлет Find-Command ищет команды PowerShell, такие как командлеты, псевдонимы, функции и рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="b2c68-106">The Find-Command cmdlet finds PowerShell commands such as cmdlets, aliases, functions, and workflows.</span></span> <span data-ttu-id="b2c68-107">Find-Command ищет их в модулях из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="b2c68-107">Find-Command searches modules in registered repositories.</span></span>
<span data-ttu-id="b2c68-108">Для каждой команды, им обнаруженной, он возвращает объект PSGetCommandInfo.</span><span class="sxs-lookup"><span data-stu-id="b2c68-108">For each command that this cmdlet finds, it returns a PSGetCommandInfo object.</span></span> <span data-ttu-id="b2c68-109">Вы можете передать объект PSGetCommandInfo в командлет Install-Module для установки модуля, содержащего конкретную команду.</span><span class="sxs-lookup"><span data-stu-id="b2c68-109">You can pass a PSGetCommandInfo object to the Install-Module cmdlet to install the module that contains the command.</span></span>

- <span data-ttu-id="b2c68-110">Командлет Find-Command позволяет выполнять фильтрацию при помощи параметров версии: MinimumVersion, RequiredVersion, AllVersions.</span><span class="sxs-lookup"><span data-stu-id="b2c68-110">Find-Command can filter with version parameters: MinimumVersion, RequiredVersion, AllVersions.</span></span>
  - <span data-ttu-id="b2c68-111">Эти параметры являются взаимоисключающими.</span><span class="sxs-lookup"><span data-stu-id="b2c68-111">These parameters are mutually exclusive.</span></span>
  - <span data-ttu-id="b2c68-112">Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="b2c68-112">These version parameters are allowed only with the single module name without any wildcards.</span></span>
  - <span data-ttu-id="b2c68-113">Если параметр RequiredVersion не указан, командлет Find-Command возвращает последнюю версию модуля, которая не ниже указанной минимальной версии, или последнюю версию модуля, если минимальная версия не указана.</span><span class="sxs-lookup"><span data-stu-id="b2c68-113">If the RequiredVersion parameter is not specified, Find-Command returns the latest version of the module that is equal to or greater than the minimum version specified or the latest version of the module if no minimum version is specified.</span></span>
  - <span data-ttu-id="b2c68-114">Если параметр RequiredVersion указан, Find-Command возвращает только версию модуля, которая точно совпадает с указанной версией.</span><span class="sxs-lookup"><span data-stu-id="b2c68-114">If the RequiredVersion parameter is specified, Find-Command only returns the version of the module that exactly matches the specified version.</span></span>
- <span data-ttu-id="b2c68-115">Find-Command позволяет фильтровать метаданные модуля при помощи параметра -Tag.</span><span class="sxs-lookup"><span data-stu-id="b2c68-115">Find-Command can filter on module metadata with the -Tag parameter</span></span>
- <span data-ttu-id="b2c68-116">Find-Command позволяет фильтровать язык поиска для определенного репозитория при помощи параметра -Filter.</span><span class="sxs-lookup"><span data-stu-id="b2c68-116">Find-Command can filter on repository-specific search language with the -Filter parameter.</span></span>
- <span data-ttu-id="b2c68-117">Find-Command может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="b2c68-117">Find-Command can filter on modules from all or few of the registered repositories.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="b2c68-118">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="b2c68-118">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="b2c68-119">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="b2c68-119">Cmdlet online help reference</span></span>

[<span data-ttu-id="b2c68-120">Find-Command</span><span class="sxs-lookup"><span data-stu-id="b2c68-120">Find-Command</span></span>](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a><span data-ttu-id="b2c68-121">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="b2c68-121">Example commands</span></span>
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```