---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 4fc146f84588d368ac3eb819e3acb4cb8c5d8793
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="2586a-102">Подробные сведения о состоянии LCM</span><span class="sxs-lookup"><span data-stu-id="2586a-102">Detailed information about LCM state</span></span>

<span data-ttu-id="2586a-103">Мы внесли улучшения процесс предоставления сведений о состоянии LCM.</span><span class="sxs-lookup"><span data-stu-id="2586a-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="2586a-104">LCMState, возвращаемый Get-DscLocalConfigurationManager, теперь может содержать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2586a-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="2586a-105">**Idle**</span><span class="sxs-lookup"><span data-stu-id="2586a-105">**Idle**</span></span>
* <span data-ttu-id="2586a-106">**Busy**</span><span class="sxs-lookup"><span data-stu-id="2586a-106">**Busy**</span></span>
* <span data-ttu-id="2586a-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="2586a-107">**PendingReboot**</span></span>
* <span data-ttu-id="2586a-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2586a-108">**PendingConfiguration**</span></span>

<span data-ttu-id="2586a-109">Мы также добавили свойство LCMStateDetail, содержащее дополнительные сведения о состоянии.</span><span class="sxs-lookup"><span data-stu-id="2586a-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>

