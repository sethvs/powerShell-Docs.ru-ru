---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 2c007321789ae22b4a2e048d2d64162b065f9a75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="declare-implemented-interface"></a>Объявление реализованного интерфейса

Реализованные интерфейсы можно объявить после базовых типов или сразу после двоеточия (:), если базовый тип не указан. Все имена типов следует разделять запятыми. Это очень похоже на синтаксис C#.

```powershell
class MyComparable : system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}

class MyComparableBar : bar, system.IComparable
{
    [int] CompareTo([object] $obj)
    {
        return 0;
    }
}
```