---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 403a79e17b832b5c58fd21a138fcebb8adb76d40
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="call-base-class-constructor"></a><span data-ttu-id="44628-102">Вызов конструктора базовых классов</span><span class="sxs-lookup"><span data-stu-id="44628-102">Call Base Class Constructor</span></span>

<span data-ttu-id="44628-103">Чтобы вызвать конструктор базовых классов из подкласса, используйте ключевое слово **base**:</span><span class="sxs-lookup"><span data-stu-id="44628-103">To call a base class constructor from a subclass, use the keyword **base**:</span></span>

```PowerShell
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

<span data-ttu-id="44628-104">Если базовый класс имеет конструктор по умолчанию (без параметров), явный вызов конструктора можно опустить:</span><span class="sxs-lookup"><span data-stu-id="44628-104">If a base class has a default (no parameter) constructor, you can omit an explicit constructor call:</span></span>

```PowerShell
class C : B
{
    C([int]$c) {}
}
```

