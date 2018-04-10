---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 302a347b0f4c9c322f7701e8d6a721f9ffba9b59
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="convert-string"></a>Convert-String
**Convert-String** предоставляет функциональность "магическая замена". Укажите примеры того, как должен выглядеть текст в исходном и итоговом виде, чтобы **Convert-String** автоматически отформатировал текста. Продемонстрируем это — возьмем имя и фамилию человека и заменим их последовательностью из фамилии, точки, первой буквы имени и точки. Попробуйте сделать это с помощью регулярного выражения и посмотрите, сколько времени для этого потребуется.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```