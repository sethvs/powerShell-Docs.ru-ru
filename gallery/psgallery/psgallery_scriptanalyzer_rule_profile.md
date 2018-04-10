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
# <a name="scriptanazlyer-rule-profile-for-gallery"></a>Профиль правила ScriptAnazlyer для коллекции
Для обеспечения качества элементов, опубликованных в коллекции PowerShell, запускаются правила [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer), чтобы определить наличие любых нарушений в отправленных скриптах.

Список правил, выполняемых в ScriptAnalyzer, можно найти на [странице GitHub](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
По любым вопросам, связанным с применяемыми правилами, обращайтесь к администраторам коллекции PowerShell или создайте запрос в поддержку ScriptAnalzyer.

Результаты работы ScriptAnalyzer будут отображаться на каждой странице отдельного элемента в коллекции в готовящемся выпуске. Владельцам элементов рекомендуется проверять опубликованные элементы на наличие серьезных ошибок.