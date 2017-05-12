---
title: "Раздел реестра DSCAutomationHostEnabled"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: eb5889668136def1b47a4999374711460a08179c
ms.sourcegitcommit: 6057e6d22ef8a2095af610e0d681e751366a9773
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2017
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


