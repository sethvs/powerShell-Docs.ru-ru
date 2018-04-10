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
# <a name="declare-implemented-interface"></a><span data-ttu-id="1fde2-102">Объявление реализованного интерфейса</span><span class="sxs-lookup"><span data-stu-id="1fde2-102">Declare Implemented Interface</span></span>

<span data-ttu-id="1fde2-103">Реализованные интерфейсы можно объявить после базовых типов или сразу после двоеточия (:), если базовый тип не указан.</span><span class="sxs-lookup"><span data-stu-id="1fde2-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="1fde2-104">Все имена типов следует разделять запятыми.</span><span class="sxs-lookup"><span data-stu-id="1fde2-104">Separate all type names by using commas.</span></span> <span data-ttu-id="1fde2-105">Это очень похоже на синтаксис C#.</span><span class="sxs-lookup"><span data-stu-id="1fde2-105">It’s very similar to C# syntax.</span></span>

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