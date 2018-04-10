---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 4def20aa95f66ab23c9eee575150bc3db02541d8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="class-based-dsc-resources"></a><span data-ttu-id="42d29-102">Ресурсы DSC, основанные на классах</span><span class="sxs-lookup"><span data-stu-id="42d29-102">Class-based DSC Resources</span></span>

## <a name="defining-dsc-resources-with-classes"></a><span data-ttu-id="42d29-103">Определение ресурсов DSC с помощью классов</span><span class="sxs-lookup"><span data-stu-id="42d29-103">Defining DSC resources with classes</span></span>

<span data-ttu-id="42d29-104">Основываясь на полученных отзывах, мы упростили создание и использование ресурсов DSC на основе классов.</span><span class="sxs-lookup"><span data-stu-id="42d29-104">Based on feedback, we’ve made authoring class-based DSC resources simpler and easier to understand.</span></span>
<span data-ttu-id="42d29-105">Ресурс DSC на основе класса и поставщик ресурсов DSC командлета имеют следующие отличия.</span><span class="sxs-lookup"><span data-stu-id="42d29-105">The major differences between a class-based DSC resource and a cmdlet DSC resource provider are:</span></span>

* <span data-ttu-id="42d29-106">MOF-файл для схемы не требуется.</span><span class="sxs-lookup"><span data-stu-id="42d29-106">A MOF file for the schema is not required.</span></span>
* <span data-ttu-id="42d29-107">Вложенная папка **DSCResource** в папке модуля не требуется.</span><span class="sxs-lookup"><span data-stu-id="42d29-107">A **DSCResource** subfolder in the module folder is not required.</span></span>
* <span data-ttu-id="42d29-108">Файл модуля PowerShell может содержать несколько классов ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="42d29-108">A PowerShell module file can contain multiple DSC resource classes.</span></span>

<span data-ttu-id="42d29-109">Дополнительные сведения см. в разделе [Написание пользовательских ресурсов DSC с использованием классов PowerShell](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span><span class="sxs-lookup"><span data-stu-id="42d29-109">For more information, see [Writing a custom DSC resource with PowerShell classes](https://msdn.microsoft.com/powershell/dsc/authoringresource).</span></span>