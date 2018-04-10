---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Get-PSRepository
ms.openlocfilehash: 97279a8ed0087c835fb924991484959cd7237016
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="get-psrepository"></a><span data-ttu-id="70f74-103">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="70f74-103">Get-PSRepository</span></span>

<span data-ttu-id="70f74-104">Возвращает информацию о зарегистрированных репозиториях, которая есть на компьютере.</span><span class="sxs-lookup"><span data-stu-id="70f74-104">Gets the registered repositories on a computer.</span></span>

## <a name="description"></a><span data-ttu-id="70f74-105">Описание</span><span class="sxs-lookup"><span data-stu-id="70f74-105">Description</span></span>

<span data-ttu-id="70f74-106">Командлет Get-PSRepository возвращает репозитории модуля PowerShell, зарегистрированные для текущего пользователя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="70f74-106">The Get-PSRepository cmdlet gets PowerShell module repositories that are registered for the current user on a computer.</span></span>

<span data-ttu-id="70f74-107">Для каждого зарегистрированного репозитория Get-PSRepository возвращает объект PSRepository, который при необходимости может быть передан в командлет Unregister-PSRepository для отмены регистрации зарегистрированного репозитория.</span><span class="sxs-lookup"><span data-stu-id="70f74-107">For each registered repository, Get-PSRepository returns a PSRepository object which can optionally be piped to Unregister-PSRepository for unregistering a registered repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="70f74-108">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="70f74-108">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="70f74-109">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="70f74-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="70f74-110">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="70f74-110">Get-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a><span data-ttu-id="70f74-111">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="70f74-111">Example commands</span></span>

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