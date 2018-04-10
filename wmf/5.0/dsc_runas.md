---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 3fe24bd7f9e2ed7af2e18c211a47c39a6a460d99
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="automatic-runas-support-for-dsc-resources"></a><span data-ttu-id="42260-102">Поддержка автоматического запуска от имени для ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="42260-102">Automatic RunAs support for DSC Resources</span></span>

<span data-ttu-id="42260-103">WMF 5.0 включает в себя поддержку выполнения **любого** ресурса DSC с заданным набором учетных данных с помощью свойства `PsDscRunAsCredential`.</span><span class="sxs-lookup"><span data-stu-id="42260-103">WMF 5.0 includes support for running **any** DSC resource under a specified set of credentials by using the property `PsDscRunAsCredential`.</span></span>

<span data-ttu-id="42260-104">Дополнительные сведения см. в разделе [Запуск DSC с учетными данными пользователя](https://msdn.microsoft.com/powershell/dsc/runasuser).</span><span class="sxs-lookup"><span data-stu-id="42260-104">For more information, see [Running DSC with user credentials](https://msdn.microsoft.com/powershell/dsc/runasuser).</span></span>