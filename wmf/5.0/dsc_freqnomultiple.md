---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: e1faf71436c8ba0ae02a166ce06d03de9f66f094
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="b6752-102">Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу</span><span class="sxs-lookup"><span data-stu-id="b6752-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="b6752-103">В предыдущей версии DSC локальный диспетчер конфигураций рассматривал `RefreshFrequencyMins` и `ConfigurationModeFrequencyMins` как кратные друг другу.</span><span class="sxs-lookup"><span data-stu-id="b6752-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="b6752-104">В WMF 5.0 RTM эти свойства обрабатываются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="b6752-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="b6752-105">Дополнительные сведения см. в разделе [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="b6752-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>