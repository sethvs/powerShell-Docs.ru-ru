---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: psgallery_профиль_правила_scriptanalyzer
ms.openlocfilehash: ff575ab56f07312658d111bccd7793b64ac071ea
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="f5cf5-103">Профиль правила ScriptAnazlyer для коллекции</span><span class="sxs-lookup"><span data-stu-id="f5cf5-103">ScriptAnazlyer Rule Profile for Gallery</span></span>
<span data-ttu-id="f5cf5-104">Для обеспечения качества элементов, опубликованных в коллекции PowerShell, запускаются правила [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer), чтобы определить наличие любых нарушений в отправленных скриптах.</span><span class="sxs-lookup"><span data-stu-id="f5cf5-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="f5cf5-105">Список правил, выполняемых в ScriptAnalyzer, можно найти на [странице GitHub](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="f5cf5-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="f5cf5-106">По любым вопросам, связанным с применяемыми правилами, обращайтесь к администраторам коллекции PowerShell или создайте запрос в поддержку ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="f5cf5-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="f5cf5-107">Результаты работы ScriptAnalyzer будут отображаться на каждой странице отдельного элемента в коллекции в готовящемся выпуске.</span><span class="sxs-lookup"><span data-stu-id="f5cf5-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="f5cf5-108">Владельцам элементов рекомендуется проверять опубликованные элементы на наличие серьезных ошибок.</span><span class="sxs-lookup"><span data-stu-id="f5cf5-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>