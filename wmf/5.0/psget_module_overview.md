---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 2c7e718bc518b332cb4303ef73b1bf5c924ca471
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a><span data-ttu-id="6c4c4-102">Обнаружение, установка и инвентаризация модуля PowerShell с помощью PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="6c4c4-102">PowerShell Module Discovery, Install and Inventory with PowerShellGet</span></span>
 
<span data-ttu-id="6c4c4-103">PowerShellGet входит в состав этого выпуска WMF:</span><span class="sxs-lookup"><span data-stu-id="6c4c4-103">PowerShellGet is included in this release of WMF:</span></span>
-   <span data-ttu-id="6c4c4-104">Find-Module позволяет фильтровать метаданные модуля с помощью параметра -Tag.</span><span class="sxs-lookup"><span data-stu-id="6c4c4-104">Find-Module can filter on module metadata with the -Tag parameter</span></span>
-   <span data-ttu-id="6c4c4-105">Find-Module позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.</span><span class="sxs-lookup"><span data-stu-id="6c4c4-105">Find-Module can filter on repository-specific search language with the -Filter parameter</span></span>
-   <span data-ttu-id="6c4c4-106">Find-Module позволяет фильтровать содержимое модуля с помощью параметров -Command, -DscResource и -Includes.</span><span class="sxs-lookup"><span data-stu-id="6c4c4-106">Find-Module can filter based on module contents with the -Command, -DscResource, and -Includes parameters</span></span>
-   <span data-ttu-id="6c4c4-107">Find-DscResource позволяет обнаруживать отдельные ресурсы DSC в репозитории.</span><span class="sxs-lookup"><span data-stu-id="6c4c4-107">Find-DscResource allows discovery of individual DSC resources in repositories</span></span>
-   <span data-ttu-id="6c4c4-108">Поддержка установки из общих папок и публикации в них с помощью NuGet</span><span class="sxs-lookup"><span data-stu-id="6c4c4-108">Support for installing from and publishing to file shares with NuGet</span></span>

## <a name="example-commands"></a><span data-ttu-id="6c4c4-109">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="6c4c4-109">Example commands</span></span>
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a><span data-ttu-id="6c4c4-110">Новые функции в PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="6c4c4-110">New features in PowerShellGet</span></span>
-   <span data-ttu-id="6c4c4-111">Поддержка параллельных версий в Windows PowerShell 5.0 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="6c4c4-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
-   <span data-ttu-id="6c4c4-112">Поддержка установки зависимостей модулей</span><span class="sxs-lookup"><span data-stu-id="6c4c4-112">Module dependency installation support</span></span>
-   <span data-ttu-id="6c4c4-113">Три новых командлета</span><span class="sxs-lookup"><span data-stu-id="6c4c4-113">Three new cmdlets</span></span>
    -   <span data-ttu-id="6c4c4-114">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="6c4c4-114">Get-InstalledModule</span></span>
    -   <span data-ttu-id="6c4c4-115">Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="6c4c4-115">Uninstall-Module</span></span>
    -   <span data-ttu-id="6c4c4-116">Save-Module</span><span class="sxs-lookup"><span data-stu-id="6c4c4-116">Save-Module</span></span>
    
