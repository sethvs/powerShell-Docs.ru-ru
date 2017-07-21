---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 6caff8c06174a1dcb990ed8e5062ccca5848dbb8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="convert-string"></a><span data-ttu-id="931d1-102">Convert-String</span><span class="sxs-lookup"><span data-stu-id="931d1-102">Convert-String</span></span>
<span data-ttu-id="931d1-103">**Convert-String** предоставляет функциональность "магическая замена".</span><span class="sxs-lookup"><span data-stu-id="931d1-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="931d1-104">Укажите примеры того, как должен выглядеть текст в исходном и итоговом виде, чтобы **Convert-String** автоматически отформатировал текста.</span><span class="sxs-lookup"><span data-stu-id="931d1-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="931d1-105">Продемонстрируем это — возьмем имя и фамилию человека и заменим их последовательностью из фамилии, точки, первой буквы имени и точки.</span><span class="sxs-lookup"><span data-stu-id="931d1-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="931d1-106">Попробуйте сделать это с помощью регулярного выражения и посмотрите, сколько времени для этого потребуется.</span><span class="sxs-lookup"><span data-stu-id="931d1-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```

