---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс PackageManagementSource DSC"
ms.openlocfilehash: 80d157aff5bf7685a797baaf6a26215f02473096
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-packagemanagementsource-resource"></a><span data-ttu-id="cd3de-103">Ресурс PackageManagementSource DSC</span><span class="sxs-lookup"><span data-stu-id="cd3de-103">DSC PackageManagementSource Resource</span></span>

> <span data-ttu-id="cd3de-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cd3de-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="cd3de-105">Ресурс **PackageManagementSource** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм регистрации или ее отмены для источников управления пакетами на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="cd3de-105">The **PackageManagementSource** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to register or unregister Package Management sources on a target node.</span></span> <span data-ttu-id="cd3de-106">**Источники управления пакетами, зарегистрированные этим способом, регистрируются в контексте системы, доступной для учетной записи системы или подсистемы DSC.**</span><span class="sxs-lookup"><span data-stu-id="cd3de-106">**Package Management sources registered in this way are registered under the System context, usable by the System account or by the DSC engine.**</span></span> <span data-ttu-id="cd3de-107">Для этого ресурса требуется модуль **PackageManagement**: http://PowerShellGallery.com.</span><span class="sxs-lookup"><span data-stu-id="cd3de-107">This resource requires the **PackageManagement** module, available from http://PowerShellGallery.com.</span></span>

## <a name="syntax"></a><span data-ttu-id="cd3de-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="cd3de-108">Syntax</span></span>

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="cd3de-109">Свойства</span><span class="sxs-lookup"><span data-stu-id="cd3de-109">Properties</span></span>
|  <span data-ttu-id="cd3de-110">Свойство</span><span class="sxs-lookup"><span data-stu-id="cd3de-110">Property</span></span>  |  <span data-ttu-id="cd3de-111">Описание</span><span class="sxs-lookup"><span data-stu-id="cd3de-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="cd3de-112">Название</span><span class="sxs-lookup"><span data-stu-id="cd3de-112">Name</span></span>| <span data-ttu-id="cd3de-113">Указывает имя источника пакета, который будет зарегистрирован в системе или регистрация которого будет отменена.</span><span class="sxs-lookup"><span data-stu-id="cd3de-113">Specifies the name of the package source to be registered or unregistered on your system.</span></span>| 
| <span data-ttu-id="cd3de-114">Ensure</span><span class="sxs-lookup"><span data-stu-id="cd3de-114">Ensure</span></span>| <span data-ttu-id="cd3de-115">Определяет, будет ли зарегистрирован источник пакета или его регистрация будет отменена.</span><span class="sxs-lookup"><span data-stu-id="cd3de-115">Determines whether the package source is to be registered or unregistered.</span></span>| 
| <span data-ttu-id="cd3de-116">InstallationPolicy</span><span class="sxs-lookup"><span data-stu-id="cd3de-116">InstallationPolicy</span></span>| <span data-ttu-id="cd3de-117">Определяет, доверяете ли вы источнику пакета.</span><span class="sxs-lookup"><span data-stu-id="cd3de-117">Determines whether you trust the package source.</span></span> <span data-ttu-id="cd3de-118">Одно из двух значений: "Untrusted", "Trusted".</span><span class="sxs-lookup"><span data-stu-id="cd3de-118">One of: "Untrusted", "Trusted".</span></span>| 
| <span data-ttu-id="cd3de-119">ProviderName</span><span class="sxs-lookup"><span data-stu-id="cd3de-119">ProviderName</span></span>| <span data-ttu-id="cd3de-120">Указывает имя поставщика OneGet, с помощью которого вы можете взаимодействовать с источником пакета.</span><span class="sxs-lookup"><span data-stu-id="cd3de-120">Specifies the name of the OneGet provider through which you can interop with the package source.</span></span>| 
| <span data-ttu-id="cd3de-121">SourceUri</span><span class="sxs-lookup"><span data-stu-id="cd3de-121">SourceUri</span></span>| <span data-ttu-id="cd3de-122">Указывает URI источника пакета.</span><span class="sxs-lookup"><span data-stu-id="cd3de-122">Specifies the URI of the package source.</span></span>| 
| <span data-ttu-id="cd3de-123">SourceCredential</span><span class="sxs-lookup"><span data-stu-id="cd3de-123">SourceCredential</span></span>| <span data-ttu-id="cd3de-124">Предоставляет доступ к пакету в удаленном источнике.</span><span class="sxs-lookup"><span data-stu-id="cd3de-124">Provides access to the package on a remote source.</span></span>| 

## <a name="example"></a><span data-ttu-id="cd3de-125">Пример</span><span class="sxs-lookup"><span data-stu-id="cd3de-125">Example</span></span>

<span data-ttu-id="cd3de-126">В этом примере регистрируется источник пакета http://nuget.org с помощью ресурса DSC **PackageManagementSource**.</span><span class="sxs-lookup"><span data-stu-id="cd3de-126">This example registers the http://nuget.org package source using the **PackageManagementSource** DSC resource.</span></span>

```powershell
Configuration PackageManagementSourceTest
{    
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }
}
```

