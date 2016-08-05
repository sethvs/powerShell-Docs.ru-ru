---
title: "Заметки о выпуске WMF 5.1 (предварительная версия)"
ms.date: 2016-07-27
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
translationtype: Human Translation
ms.sourcegitcommit: 5eb9eae6257cdb57f4f778b5dddf5aa7ef9d10bb
ms.openlocfilehash: 12f2c084ab92134b733ee037c3d9fbd512af2e4c

---

# Заметки о выпуске Windows Management Framework (WMF) 5.1 Preview #

WMF 5.1 Preview включает компоненты PowerShell, WMI, WinRM и Software Inventory and Licensing (SIL), которые выпускаются с Windows Server 2016. Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:

- Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.
- Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.
- Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.
- Улучшения отладки для классов DSC и PowerShell.
- Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.
- Ответы на разные запросы пользователей и решение проблем.

**Важные примечания.**

- **Для WMF 5.1 Preview нужна платформа Windows Management Framework 4.6**. Если платформа .NET 4.6 не установлена, установка будет выполнена, но основные функции не будут работать. Инструкции см. в разделе [Установка и настройка WMF 5.1 (Preview)](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure). 
- **WMF 5.1 Preview сейчас не поддерживается в рабочих** развертываниях. Она предназначена для создания предварительного представления о содержимом выпуска, а также для отправки отзывов группе PowerShell.
- WMF 5.1 Preview можно установить непосредственно на WMF 5.0.
- WMF 4.0 сейчас требуется для установки WMF 5.1 Preview на Windows 7 и Windows Server 2008. Это известная проблема. Это требование будет удалено до финального выпуска.
- Для установки будущих версий WMF 5.1, включая RTM, потребуется удалить WMF 5.1 Preview.



<!--HONumber=Jul16_HO5-->


