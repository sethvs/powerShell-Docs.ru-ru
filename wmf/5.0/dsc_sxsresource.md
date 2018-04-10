---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: a565f2befddc32f5088fa3e158f58d2dd78d41b4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a><span data-ttu-id="882d7-102">Поддержка параллельного управления версиями модулей для ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="882d7-102">Side-By-Side Module Versioning Support for DSC Resources</span></span>

<span data-ttu-id="882d7-103">Модули, содержащие ресурсы DSC, могут быть установлены параллельно, а конфигурации DSC могут использовать конкретную версию ресурса, установленного в системе.</span><span class="sxs-lookup"><span data-stu-id="882d7-103">Modules containing DSC resources can be installed side-by-side, and DSC configurations can use a specific version of the resource that is installed on the system.</span></span>

<span data-ttu-id="882d7-104">Дополнительные сведения см. в разделе [Использование ресурсов с несколькими версиями](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span><span class="sxs-lookup"><span data-stu-id="882d7-104">For more information, see [Using resources with multiple versions](https://msdn.microsoft.com/powershell/dsc/sxsresource).</span></span>

## <a name="known-issues"></a><span data-ttu-id="882d7-105">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="882d7-105">Known issues</span></span>

<span data-ttu-id="882d7-106">Ниже перечислены известные с параллельной установкой в этом выпуске:</span><span class="sxs-lookup"><span data-stu-id="882d7-106">In this release, the following are known issues of side-by-side installation:</span></span>

-   <span data-ttu-id="882d7-107">Использование двух различных версий ресурса DSC в одной конфигурации не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="882d7-107">Using two different versions of the DSC resource within the same configuration is not supported.</span></span>