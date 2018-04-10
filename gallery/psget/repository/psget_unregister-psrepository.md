---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Unregister-PSRepository
ms.openlocfilehash: 7847e223ae7edd9ec2417d104e5e8130f92a59cf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="unregister-psrepository"></a><span data-ttu-id="95b4b-103">Unregister-PSRepository</span><span class="sxs-lookup"><span data-stu-id="95b4b-103">Unregister-PSRepository</span></span>

<span data-ttu-id="95b4b-104">Отмена регистрации репозитория.</span><span class="sxs-lookup"><span data-stu-id="95b4b-104">Unregisters a repository.</span></span>

## <a name="description"></a><span data-ttu-id="95b4b-105">Описание</span><span class="sxs-lookup"><span data-stu-id="95b4b-105">Description</span></span>

<span data-ttu-id="95b4b-106">Командлет Unregister-PSRepository отменяет регистрацию репозитория для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="95b4b-106">The Unregister-PSRepository cmdlet unregisters a repository for the current user.</span></span>
- <span data-ttu-id="95b4b-107">Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.</span><span class="sxs-lookup"><span data-stu-id="95b4b-107">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
- <span data-ttu-id="95b4b-108">Пользователи могут повторно зарегистрировать PSGallery, просто выполнив команду `Register-PSRepository -Default`.</span><span class="sxs-lookup"><span data-stu-id="95b4b-108">Users can re-register the PSGallery by simply running `Register-PSRepository -Default`</span></span>
- <span data-ttu-id="95b4b-109">Так как PSGallery — это репозиторий для публикации по умолчанию в командлетах Publish-Module и Publish-Script, возникнет ошибка, если коллекция PSGallery недоступна в списке зарегистрированных репозиториев.</span><span class="sxs-lookup"><span data-stu-id="95b4b-109">Since PSGallery is the default publish repository in Publish-Module and Publish-Script cmdlets, an error will be thrown if PSGallery is not available in the registered repository list.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="95b4b-110">Синтаксис командлета</span><span class="sxs-lookup"><span data-stu-id="95b4b-110">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="95b4b-111">Ссылка на раздел справки по командлету в Интернете</span><span class="sxs-lookup"><span data-stu-id="95b4b-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="95b4b-112">Unregister-PSRepository</span><span class="sxs-lookup"><span data-stu-id="95b4b-112">Unregister-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a><span data-ttu-id="95b4b-113">Примеры команд</span><span class="sxs-lookup"><span data-stu-id="95b4b-113">Example commands</span></span>

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a><span data-ttu-id="95b4b-114">Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.</span><span class="sxs-lookup"><span data-stu-id="95b4b-114">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```