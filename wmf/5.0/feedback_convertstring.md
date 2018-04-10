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
# <a name="convert-string"></a><span data-ttu-id="1fd9d-102">Convert-String</span><span class="sxs-lookup"><span data-stu-id="1fd9d-102">Convert-String</span></span>
<span data-ttu-id="1fd9d-103">**Convert-String** предоставляет функциональность "магическая замена".</span><span class="sxs-lookup"><span data-stu-id="1fd9d-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="1fd9d-104">Укажите примеры того, как должен выглядеть текст в исходном и итоговом виде, чтобы **Convert-String** автоматически отформатировал текста.</span><span class="sxs-lookup"><span data-stu-id="1fd9d-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="1fd9d-105">Продемонстрируем это — возьмем имя и фамилию человека и заменим их последовательностью из фамилии, точки, первой буквы имени и точки.</span><span class="sxs-lookup"><span data-stu-id="1fd9d-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="1fd9d-106">Попробуйте сделать это с помощью регулярного выражения и посмотрите, сколько времени для этого потребуется.</span><span class="sxs-lookup"><span data-stu-id="1fd9d-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```