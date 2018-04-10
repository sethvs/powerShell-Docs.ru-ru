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
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>Частоты для RefreshMode и ConfigurationMode не должны быть кратными друг другу

В предыдущей версии DSC локальный диспетчер конфигураций рассматривал `RefreshFrequencyMins` и `ConfigurationModeFrequencyMins` как кратные друг другу. В WMF 5.0 RTM эти свойства обрабатываются независимо друг от друга.

Дополнительные сведения см. в разделе [Настройка локального диспетчера конфигураций](https://msdn.microsoft.com/powershell/dsc/metaconfig).