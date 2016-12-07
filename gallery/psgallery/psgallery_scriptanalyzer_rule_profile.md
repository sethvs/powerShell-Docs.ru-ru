---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psgallery_профиль_правила_scriptanalyzer"
ms.technology: powershell
ms.openlocfilehash: 3274b66203044c0ed9fc1135cea7472428eb753e
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a>Профиль правила ScriptAnazlyer для коллекции
Для обеспечения качества элементов, опубликованных в коллекции PowerShell, запускаются правила [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer), чтобы определить наличие любых нарушений в отправленных скриптах.

Список правил, выполняемых в ScriptAnalyzer, можно найти на [странице GitHub](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
По любым вопросам, связанным с применяемыми правилами, обращайтесь к администраторам коллекции PowerShell или создайте запрос в поддержку ScriptAnalzyer.

Результаты работы ScriptAnalyzer будут отображаться на каждой странице отдельного элемента в коллекции в готовящемся выпуске. Владельцам элементов рекомендуется проверять опубликованные элементы на наличие серьезных ошибок.

