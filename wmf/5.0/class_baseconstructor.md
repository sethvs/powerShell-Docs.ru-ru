---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 1fd6d80d6b7effb4bd98c1594d64e531c4e5c9b5
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2017
---
# <a name="call-base-class-constructor"></a><span data-ttu-id="fc10c-102">Вызов конструктора базовых классов</span><span class="sxs-lookup"><span data-stu-id="fc10c-102">Call Base Class Constructor</span></span>

<span data-ttu-id="fc10c-103">Чтобы вызвать конструктор базовых классов из подкласса, используйте ключевое слово **base**:</span><span class="sxs-lookup"><span data-stu-id="fc10c-103">To call a base class constructor from a subclass, use the keyword **base**:</span></span>

```powershell
class A 
{
    [int]$a

    A([int]$a)
    {
        $this.a = $a
    }
}

class B : A
{
    B() : base(103) {}
}

[B]::new().a # return 103
```

<span data-ttu-id="fc10c-104">Если базовый класс имеет конструктор по умолчанию (без параметров), явный вызов конструктора можно опустить:</span><span class="sxs-lookup"><span data-stu-id="fc10c-104">If a base class has a default (no parameter) constructor, you can omit an explicit constructor call:</span></span>

```powershell
class C : B
{
    C([int]$c) {}
}
```

