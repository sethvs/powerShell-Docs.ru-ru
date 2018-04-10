---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 27f8fab6a72e7f3a3f510f5a9e503bbfb8a8f618
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="on-demand-pull-of-dsc-configurations"></a>Извлечение по запросу для конфигураций DSC

Новый командлет Update-DscConfiguration активирует извлечение с опрашивающих серверов, определенных в метаконфигурации. Такое поведение часто называется "оперативным извлечением".


После активации извлечение осуществляется точно так же, как и в обычном случае:

1. Контрольная сумма для текущей конфигурации сравнивается с контрольной суммой конфигурации на опрашивающем сервере.
2. Если они совпадают, процедура завершается успешно без применения конфигурации.
3. Если они различаются, конфигурация извлекается с опрашивающего сервера и применяется.

**Примечание.** Если Meta-Configuration RefreshMode = "Push", этот командлет возвращает ошибку, поэтому он всегда не выполняет никаких действий, когда целевой узел находится в режиме Push.

```powershell
Update-DscConfiguration     [[-ComputerName] <string[]>]
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-Credential<pscredential>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]

Update-DscConfiguration     -CimSession <CimSession[]>
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]
```