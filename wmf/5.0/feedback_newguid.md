---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 91c115c7f0553cd5edf7fecf04e6a5c71c0a1aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="new-guid"></a>New-Guid
Часто в сценарии (или при создании ресурсов DSC) требуется уникальный идентификатор. Здесь можно использовать GUID, для создания которых достаточно вызвать класс Guid платформы .NET Framework, однако наличие командлета делает этот процесс более очевидным и удобным для конечных пользователей, которые еще не знакомы с данным классом .NET Framework:

PS C:\\&gt; New-Guid

GUID

----

e19d6ea5-3cc2-4db9-8095-0cdaed5a703d