---
ms.date: 08/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: Заметки о выпуске WMF 5.1
ms.openlocfilehash: 9df21afe52e79dc248871b999afead21f8678d52
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-management-framework-wmf-51"></a>Windows Management Framework (WMF) 5.1 #

WMF предоставляет пользователям возможность обновить существующие системы Windows до версий PowerShell, WMI, WinRM и Software Inventory Logging (SIL), которые были выпущены с Windows Server 2016.

Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:

- Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.
- Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.
- Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.
- Улучшения отладки для классов DSC и PowerShell.
- Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.
- Ответы на разные запросы пользователей и решение проблем.

Дополнительные сведения о новых возможностях в этом выпуске см. в разделах, перечисленных в статье [Новые сценарии и функции](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).

В разделе [Установка и настройка](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) перечисляются требования и предоставляются инструкции по установке для WMF.

В разделе [Совместимость](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) перечисляются версии WMF, которые можно установить на выпуски Windows.

В разделе [Совместимость продуктов](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) перечисляются приложения Майкрософт, которые не утвердили использование WMF 5.1.

Сведения для компонентов WMF можно найти в документации MSDN:

- [PowerShell 5.1](https://docs.microsoft.com/en-us/powershell/)
- [WMI](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)
- [WinRM](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)
- [Ведение журнала инвентаризации программного обеспечения](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)