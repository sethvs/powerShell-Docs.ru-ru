---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: e503f9a4462e94fce42ffcdcc0976d261c051f87
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="declare-implemented-interface"></a><span data-ttu-id="43172-102">Объявление реализованного интерфейса</span><span class="sxs-lookup"><span data-stu-id="43172-102">Declare Implemented Interface</span></span>

<span data-ttu-id="43172-103">Реализованные интерфейсы можно объявить после базовых типов или сразу после двоеточия (:), если базовый тип не указан.</span><span class="sxs-lookup"><span data-stu-id="43172-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="43172-104">Все имена типов следует разделять запятыми.</span><span class="sxs-lookup"><span data-stu-id="43172-104">Separate all type names by using commas.</span></span> <span data-ttu-id="43172-105">Это очень похоже на синтаксис C#.</span><span class="sxs-lookup"><span data-stu-id="43172-105">It’s very similar to C# syntax.</span></span>

```PowerShell
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

