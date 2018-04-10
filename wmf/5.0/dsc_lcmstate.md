---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: baa35e9acd24d6f6155acf617a0d2c2210742af7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="315dc-102">Подробные сведения о состоянии LCM</span><span class="sxs-lookup"><span data-stu-id="315dc-102">Detailed information about LCM state</span></span>

<span data-ttu-id="315dc-103">Мы внесли улучшения процесс предоставления сведений о состоянии LCM.</span><span class="sxs-lookup"><span data-stu-id="315dc-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="315dc-104">LCMState, возвращаемый Get-DscLocalConfigurationManager, теперь может содержать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="315dc-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="315dc-105">**Idle**</span><span class="sxs-lookup"><span data-stu-id="315dc-105">**Idle**</span></span>
* <span data-ttu-id="315dc-106">**Busy**</span><span class="sxs-lookup"><span data-stu-id="315dc-106">**Busy**</span></span>
* <span data-ttu-id="315dc-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="315dc-107">**PendingReboot**</span></span>
* <span data-ttu-id="315dc-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="315dc-108">**PendingConfiguration**</span></span>

<span data-ttu-id="315dc-109">Мы также добавили свойство LCMStateDetail, содержащее дополнительные сведения о состоянии.</span><span class="sxs-lookup"><span data-stu-id="315dc-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>