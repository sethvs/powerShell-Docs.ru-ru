---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: psget_заполнениезависимостеймодуля
ms.openlocfilehash: c4c9f203e9c526ff532c2388acb6334515d66934
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a><span data-ttu-id="da8cf-103">Логика для подготовки зависимостей модуля во время операции публикации</span><span class="sxs-lookup"><span data-stu-id="da8cf-103">Logic for preparing the module dependencies during Publish operation</span></span>
1.  <span data-ttu-id="da8cf-104">Модули, перечисленные в списке RequiredModules, считаются зависимостями.</span><span class="sxs-lookup"><span data-stu-id="da8cf-104">Modules listed as part of RequiredModules are considered as dependencies.</span></span>
2.  <span data-ttu-id="da8cf-105">Модули, перечисленные в списке NestedModules, база модуля которых не находится под указанной базой модуля, считаются зависимостями.</span><span class="sxs-lookup"><span data-stu-id="da8cf-105">Modules listed as part of NestedModules, whose module base is not under the specified module base, are considered as dependencies.</span></span>

3.  <span data-ttu-id="da8cf-106">Указанные выше зависимости должны быть доступны в том же целевом репозитории, иначе операция публикации приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="da8cf-106">Above dependencies should be available on the same target repository, otherwise publish operation will result in an error.</span></span>
    <span data-ttu-id="da8cf-107">Например, если SnippetPx недоступен в репозитории, возникнет следующая ошибка.</span><span class="sxs-lookup"><span data-stu-id="da8cf-107">For example: If 'SnippetPx' is not available on the repository, below error will be thrown.</span></span>
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  <span data-ttu-id="da8cf-108">Некоторые зависимости модуля могут управляться извне; в этом случае они должны добавляться в запись ExternalModuleDependencies раздела PSData манифеста модуля.</span><span class="sxs-lookup"><span data-stu-id="da8cf-108">Some module dependencies can be managed externally, in that case they should be added to the ExternalModuleDependencies entry in the PSData section of the module manifest.</span></span>
    <span data-ttu-id="da8cf-109">Ниже приводится часть вышеупомянутого сообщения об ошибке</span><span class="sxs-lookup"><span data-stu-id="da8cf-109">Below part in the above error message</span></span>
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

<span data-ttu-id="da8cf-110">*Во время установки модуля подготовленный выше список зависимостей используется для установки зависимостей.*</span><span class="sxs-lookup"><span data-stu-id="da8cf-110">*During the module installation, above prepared dependencies list is used for installing the dependencies.*</span></span>

<span data-ttu-id="da8cf-111">*Убедитесь, что зависимости вашего модуля доступны в разделе $env:PSModulePath в системе во время публикации.*</span><span class="sxs-lookup"><span data-stu-id="da8cf-111">*Please ensure that your module’s dependencies are available under $env:PSModulePath on your system during publish operation.*</span></span>