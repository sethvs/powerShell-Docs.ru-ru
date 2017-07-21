---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 69188738333a853a16e6ea68689ecba5dc632225
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="6919e-102">Поддержка параллельных версий в PowerShell 5.0 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="6919e-102">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="6919e-103">Теперь в командлетах Install-Module, Update-Module и Publish-Module, выполняемых в Windows PowerShell 5.0 или более поздней версии, имеется поддержка параллельных (SxS) версий модуля.</span><span class="sxs-lookup"><span data-stu-id="6919e-103">There is now side-by-side (SxS) module version support in Install-Module, Update-Module, and Publish-Module cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>
<span data-ttu-id="6919e-104">Кроме того, мы добавили в командлет Publish-Module параметр -RequiredVersion для указания публикуемой версии.</span><span class="sxs-lookup"><span data-stu-id="6919e-104">Also, we have added a -RequiredVersion parameter to the Publish-Module cmdlet to specify the version to be published.</span></span> <span data-ttu-id="6919e-105">Параметр Path теперь поддерживает базовый путь к модулю с папкой версии.</span><span class="sxs-lookup"><span data-stu-id="6919e-105">The Path parameter now supports the module base path with the version folder.</span></span>

<span data-ttu-id="6919e-106">**Примеры использования Install-Module**</span><span class="sxs-lookup"><span data-stu-id="6919e-106">**Install-Module examples:**</span></span>
```powershell
PS C:\\windows\\system32&gt; Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
PS C:\\windows\\system32&gt; Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase
Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

PS C:\\windows\\system32&gt; Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
PS C:\\windows\\system32&gt; Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase
Name       : PSScriptAnalyzer 
Version    : 1.1.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.1
Name       : PSScriptAnalyzer
Version    : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

PS C:\\windows\\system32&gt; Get-InstalledModule -Name PSScriptAnalyzer -AllVersions
Version    Name                                Type       Repository           Description            
-------    ----                                ----       ----------           -----------            
1.1.0      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis... 
1.1.1      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis...
```

