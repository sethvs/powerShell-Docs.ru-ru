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
# <a name="detailed-information-about-lcm-state"></a>Подробные сведения о состоянии LCM

Мы внесли улучшения процесс предоставления сведений о состоянии LCM. LCMState, возвращаемый Get-DscLocalConfigurationManager, теперь может содержать следующие значения:

* **Idle**
* **Busy**
* **PendingReboot**
* **PendingConfiguration**

Мы также добавили свойство LCMStateDetail, содержащее дополнительные сведения о состоянии.