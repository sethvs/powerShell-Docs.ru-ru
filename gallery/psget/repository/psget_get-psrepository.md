---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: Get-PSRepository
ms.openlocfilehash: 96f87428312c233757aa5fcae405a192aadff385
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="get-psrepository"></a><span data-ttu-id="285c1-103">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="285c1-103">Get-PSRepository</span></span>

<span data-ttu-id="285c1-104">Возвращает информацию о зарегистрированных репозиториях, которая есть на компьютере.</span><span class="sxs-lookup"><span data-stu-id="285c1-104">Gets the registered repositories on a computer.</span></span>

## <a name="description"></a><span data-ttu-id="285c1-105">Описание</span><span class="sxs-lookup"><span data-stu-id="285c1-105">Description</span></span>

<span data-ttu-id="285c1-106">Командлет Get-PSRepository возвращает репозитории модуля PowerShell, зарегистрированные для текущего пользователя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="285c1-106">The Get-PSRepository cmdlet gets PowerShell module repositories that are registered for the current user on a computer.</span></span>

<span data-ttu-id="285c1-107">Для каждого зарегистрированного репозитория Get-PSRepository возвращает объект PSRepository, который при необходимости может быть передан в командлет Unregister-PSRepository для отмены регистрации зарегистрированного репозитория.</span><span class="sxs-lookup"><span data-stu-id="285c1-107">For each registered repository, Get-PSRepository returns a PSRepository object which can optionally be piped to Unregister-PSRepository for unregistering a registered repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="285c1-108">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="285c1-108">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="285c1-109">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="285c1-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="285c1-110">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="285c1-110">Get-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a><span data-ttu-id="285c1-111">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="285c1-111">Example commands</span></span>

```powershell

# Properties of Get-PSRepository returned object
Get-PSRepository PSGallery | Format-List * -Force

Name                      : PSGallery
SourceLocation            : https://www.powershellgallery.com/api/v2/
Trusted                   : False
Registered                : True
InstallationPolicy        : Untrusted
PackageManagementProvider : NuGet
PublishLocation           : https://www.powershellgallery.com/api/v2/package/
ScriptSourceLocation      : https://www.powershellgallery.com/api/v2/items/psscript/
ScriptPublishLocation     : https://www.powershellgallery.com/api/v2/package/
ProviderOptions           : {}

# Get all registered repositories
Get-PSRepository

# Get a specific registered repository
Get-PSRepository PSGallery

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/

# Get registered repository with wildcards
Get-PSRepository *Gallery*

```

