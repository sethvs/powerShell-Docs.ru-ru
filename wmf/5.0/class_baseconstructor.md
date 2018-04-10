---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 3269c8cc871f22488b64fb072dac72698983f360
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="call-base-class-constructor"></a>Вызов конструктора базовых классов

Чтобы вызвать конструктор базовых классов из подкласса, используйте ключевое слово **base**:

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

Если базовый класс имеет конструктор по умолчанию (без параметров), явный вызов конструктора можно опустить:

```powershell
class C : B
{
    C([int]$c) {}
}
```