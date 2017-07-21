---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 30055cff87159df98029e25409782e0fe2f0bae4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="5a65b-102">Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу</span><span class="sxs-lookup"><span data-stu-id="5a65b-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="5a65b-103">В предыдущей версии DSC локальный диспетчер конфигураций рассматривал `RefreshFrequencyMins` и `ConfigurationModeFrequencyMins` как кратные друг другу.</span><span class="sxs-lookup"><span data-stu-id="5a65b-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="5a65b-104">В WMF 5.0 RTM эти свойства обрабатываются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="5a65b-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span> 

<span data-ttu-id="5a65b-105">Дополнительные сведения см. в разделе [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="5a65b-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>

