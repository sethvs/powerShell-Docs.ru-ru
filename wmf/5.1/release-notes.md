---
title: "Заметки о выпуске WMF 5.1"
ms.date: 2016-07-27
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: jkeithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 15de6aca52624134998b2d08fcfff9e1bcc1af7b
ms.sourcegitcommit: f75fc25411ce6a768596d3438e385c43c4f0bf71
translationtype: HT
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>Заметки о выпуске Windows Management Framework (WMF) 5.1 #

WMF 5.1 включает компоненты PowerShell, WMI, WinRM и Software Inventory and Licensing (SIL), которые выпускаются с Windows Server 2016. Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:

- Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.
- Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.
- Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.
- Улучшения отладки для классов DSC и PowerShell.
- Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.
- Ответы на разные запросы пользователей и решение проблем.

**Важные примечания.**

- **Для WMF 5.1 требуется .NET Framework4.5**. Если платформа .NET 4.5 не установлена, установка будет выполнена, но основные функции не будут работать. Инструкции см. в разделе [Установка и настройка WMF 5.1](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure). 
- Перед установкой WMF 5.1 RTM нужно удалить предварительную версию WMF 5.1.
- WMF 5.1 можно установить непосредственно на WMF 5.0 или WMF 4.0.
- Устанавливать WMF 4.0 перед установкой WMF 5.1 в Windows 7 и Windows Server 2008 R2 __не требуется__. Эта проблема имела место для предварительной версии WMF 5.1 и была устранена.  


