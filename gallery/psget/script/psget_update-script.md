---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Update-Script
ms.openlocfilehash: 23e558a063689d263f68d34ec3b154be1c77ae89
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="update-script"></a><span data-ttu-id="1e0a0-103">Update-Script</span><span class="sxs-lookup"><span data-stu-id="1e0a0-103">Update-Script</span></span>

<span data-ttu-id="1e0a0-104">Командлет Update-Script позволяет выполнить обновление на месте для файлов сценариев, которые были установлены с помощью командлета Install-Script.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-104">Update-Script cmdlet lets you to do in-place update of the script files which were installed using Install-Script cmdlet.</span></span>

## <a name="description"></a><span data-ttu-id="1e0a0-105">Описание</span><span class="sxs-lookup"><span data-stu-id="1e0a0-105">Description</span></span>

<span data-ttu-id="1e0a0-106">Командлет Update-Script обновляет указанный скрипт из репозитория, из которого он был ранее установлен.</span><span class="sxs-lookup"><span data-stu-id="1e0a0-106">The Update-Script cmdlet updates the specified script from the repository from which it was previously installed.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="1e0a0-107">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="1e0a0-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Update-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="1e0a0-108">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="1e0a0-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="1e0a0-109">Update-Script</span><span class="sxs-lookup"><span data-stu-id="1e0a0-109">Update-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619787)

## <a name="example-commands"></a><span data-ttu-id="1e0a0-110">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="1e0a0-110">Example commands</span></span>
```powershell
Install-Script -Name Fabrikam-Script -RequiredVersion 1.0 -Repository GalleryINT -Scope
Get-InstalledScript -Name Fabrikam-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script

# Update a specific script to the required version
Update-Script -Name Fabrikam-Script -RequiredVersion 1.5
Get-InstalledScript -Name Fabrikam-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script

# Update a specific script to the required prerelease version
Update-Script -Name Fabrikam-Script -RequiredVersion 1.5.0-alpha -AllowPrerelease
Get-InstalledScript -Name Fabrikam-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.5.0-alpha Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script

# Update all installed scripts
Install-Script -Name Fabrikam-ServerScript -RequiredVersion 1.0 -Repository GalleryINT -Scope CurrentUser
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
1.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script
1.0 Fabrikam-ServerScript Script GalleryINT Description for the Fabrikam-ServerScript script
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script

Update-Script
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Fabrikam-Script Script GalleryINT Description for the Fabrikam-Script script
2.5 Fabrikam-ServerScript Script GalleryINT Description for the Fabrikam-ServerScript script
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
```