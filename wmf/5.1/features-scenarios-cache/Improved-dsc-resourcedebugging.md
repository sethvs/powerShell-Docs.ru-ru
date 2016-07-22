---
title: "Усовершенствования в отладке ресурсов DSC"
author: jaimeo
contributor: amitsara
translationtype: Human Translation
ms.sourcegitcommit: e39aa2e5cbda0c83e24e21c4459d957d8baaff25
ms.openlocfilehash: 33c3fcffdeb281b205ecc48f7cdd470b79e9e068

---


## Усовершенствования в отладке ресурсов DSC

В WMF 5.0 отладчик PowerShell не останавливался непосредственно в методах для работы с ресурсами класса (Get, Set, Test).
Эта проблема устранена. Теперь отладчик будет останавливаться в методах для работы с ресурсами класса точно так же, как в методах для работы с ресурсами на основе MOF.



<!--HONumber=Jul16_HO3-->


