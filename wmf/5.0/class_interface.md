---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 968e78beb8df77588a08a9ce8732e4abcadde4d0
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2017
---
# <a name="declare-implemented-interface"></a><span data-ttu-id="d5d01-102">Объявление реализованного интерфейса</span><span class="sxs-lookup"><span data-stu-id="d5d01-102">Declare Implemented Interface</span></span>

<span data-ttu-id="d5d01-103">Реализованные интерфейсы можно объявить после базовых типов или сразу после двоеточия (:), если базовый тип не указан.</span><span class="sxs-lookup"><span data-stu-id="d5d01-103">You can declare implemented interfaces after base types, or immediately after a colon (:), if there is no base type specified.</span></span> <span data-ttu-id="d5d01-104">Все имена типов следует разделять запятыми.</span><span class="sxs-lookup"><span data-stu-id="d5d01-104">Separate all type names by using commas.</span></span> <span data-ttu-id="d5d01-105">Это очень похоже на синтаксис C#.</span><span class="sxs-lookup"><span data-stu-id="d5d01-105">It’s very similar to C# syntax.</span></span>

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

