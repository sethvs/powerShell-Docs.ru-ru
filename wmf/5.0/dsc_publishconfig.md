---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 136e16ae74e54f3bc9d0623178257df1e9104aac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="deliver-a-configuration-document-without-applying"></a>Доставка документа конфигурации без применения

Командлет [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) копирует MOF-файл на целевой узел без применения конфигурации.
Конфигурация применяется во время следующей проверки согласованности или при запуске командлета [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx).