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
<a id="detailed-information-about-lcm-state" class="xliff"></a>
# Подробные сведения о состоянии LCM

Мы внесли улучшения процесс предоставления сведений о состоянии LCM. LCMState, возвращаемый Get-DscLocalConfigurationManager, теперь может содержать следующие значения:

* **Idle**
* **Busy**
* **PendingReboot**
* **PendingConfiguration**

Мы также добавили свойство LCMStateDetail, содержащее дополнительные сведения о состоянии.

