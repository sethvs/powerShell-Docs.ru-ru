---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Раздел реестра DSCAutomationHostEnabled"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
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


