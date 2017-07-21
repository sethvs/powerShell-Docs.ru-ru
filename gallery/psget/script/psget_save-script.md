---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: Save-Script
ms.openlocfilehash: 7b692d33e3f86a89505b8d37c0da4177f3dff2c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="save-script"></a><span data-ttu-id="9a469-103">Save-Script</span><span class="sxs-lookup"><span data-stu-id="9a469-103">Save-Script</span></span>

<span data-ttu-id="9a469-104">Командлет Save-Script позволяет просмотреть файл сценария, сохранив его в указанном расположении.</span><span class="sxs-lookup"><span data-stu-id="9a469-104">Save-Script cmdlet lets you to review the script file by saving it to a specified location.</span></span>

## <a name="description"></a><span data-ttu-id="9a469-105">Описание</span><span class="sxs-lookup"><span data-stu-id="9a469-105">Description</span></span>

<span data-ttu-id="9a469-106">Командлет Save-Script сохраняет указанный скрипт.</span><span class="sxs-lookup"><span data-stu-id="9a469-106">The Save-Script cmdlet saves the specified script.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="9a469-107">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="9a469-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="9a469-108">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="9a469-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="9a469-109">Save-Script</span><span class="sxs-lookup"><span data-stu-id="9a469-109">Save-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a><span data-ttu-id="9a469-110">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="9a469-110">Example commands</span></span>

### <a name="example-1-save-a-script-from-a-repository"></a><span data-ttu-id="9a469-111">Пример 1. Сохранение скрипта из репозитория</span><span class="sxs-lookup"><span data-stu-id="9a469-111">Example 1: Save a script from a repository</span></span>
<span data-ttu-id="9a469-112">Эта команда сохраняет последнюю версию скрипта Fabrikam-ClientScript из репозитория GalleryINT в локальную папку C:\ScriptSharingDemo.</span><span class="sxs-lookup"><span data-stu-id="9a469-112">This command saves the latest version of the script Fabrikam-ClientScript from GalleryINT repository to the local folder C:\ScriptSharingDemo</span></span>

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a><span data-ttu-id="9a469-113">Пример 2. Сохранение версии скрипта по конвейеру из командлета Find-Script</span><span class="sxs-lookup"><span data-stu-id="9a469-113">Example 2: Save a version of a script by piping from the Find-Script cmdlet</span></span>

<span data-ttu-id="9a469-114">Первая команда находит версию 1.5 скрипта Fabrikam-ClientScript в репозитории GalleryINT и сохраняет ее в папку C:\ScriptSharingDemo.</span><span class="sxs-lookup"><span data-stu-id="9a469-114">The first command finds version 1.5 of Fabrikam-ClientScript from the repository GalleryINT and saves it to the folder C:\ScriptSharingDemo</span></span>

<span data-ttu-id="9a469-115">Вторая команда проверяет метаданные сохраненного скрипта.</span><span class="sxs-lookup"><span data-stu-id="9a469-115">The second command validates the saved script metadata.</span></span>

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

