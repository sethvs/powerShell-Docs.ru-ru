---
title: "Заметки о выпуске WMF 5.1"
ms.date: 2017-01-20
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: keithb
manager: carmonm
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 48821f41b7a05860dc9f6a8916817f8e9ca28e6d
ms.sourcegitcommit: 9fe4d1ef90fd11267a00e955d80ed6d27c8d7d5a
translationtype: HT
---
# <a name="windows-management-framework-wmf-51-release-notes"></a>Заметки о выпуске Windows Management Framework (WMF) 5.1 #

WMF 5.1 включает компоненты PowerShell, WMI, WinRM и Software Inventory and Licensing (SIL), которые были выпущены с Windows Server 2016.
Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:

- Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.
- Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.
- Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.
- Улучшения отладки для классов DSC и PowerShell.
- Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.
- Ответы на разные запросы пользователей и решение проблем.

**Важные примечания.**

- **Для WMF 5.1 требуется .NET Framework 4.5.2**. Если платформа .NET 4.5.2 не установлена, установка будет выполнена, но основные функции не будут работать. Инструкции см. в разделе [Установка и настройка WMF 5.1](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure).
- Перед установкой WMF 5.1 RTM нужно удалить предварительную версию WMF 5.1.
- WMF 5.1 можно установить непосредственно на WMF 5.0 или WMF 4.0.
- Устанавливать WMF 4.0 перед установкой WMF 5.1 в Windows 7 и Windows Server 2008 R2 __не требуется__. Эта проблема имела место для предварительной версии WMF 5.1 и была устранена.  


