---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Раздел реестра DSCAutomationHostEnabled
ms.openlocfilehash: 9fd71120b4959a7b14094922b453b05b217f3736
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
>Область применения: Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>Раздел реестра DSCAutomationHostEnabled

DSC использует раздел реестра **DSCAutomationHostEnabled** в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** для включения конфигурации компьютера при начальной загрузке.
DSCAutomationHostEnabled поддерживает три режима:

|  Значение DSCAutomationHostEnabled  |  Описание   |
|---|---|
0 | Отключение настройки компьютера при загрузке системы. |
1 | Включение настройки компьютера при загрузке системы. |
2 | Включение настройки компьютера, только если DSC находится в состоянии ожидания или в текущем состоянии. Это значение по умолчанию. |

## <a name="see-also"></a>См. также

Пример использования этой функции для запуска конфигураций при начальной загрузке системы см. в разделе [Настройка виртуальных машин при начальной загрузке с помощью DSC](bootstrapDsc.md).