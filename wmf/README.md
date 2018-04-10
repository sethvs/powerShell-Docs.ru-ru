---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: Windows Management Framework (WMF)
ms.openlocfilehash: 715ac6fe5df47066415a65d91a0982fd7070a426
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-management-framework"></a>Windows Management Framework

Windows Management Framework (WMF) — это механизм доставки, который предоставляет согласованный интерфейс управления различными версиями Windows и Windows Server.
Установив WMF, клиенты получают возможность легко обеспечивать взаимодействие внутри различных сочетаний операционных систем в своих средах.
Благодаря платформе WMF обновления функций управления в определенном выпуске Windows или Windows Server становятся доступными для установки в более ранних версиях Windows и Windows Server (как правило, в двух предыдущих версиях).

При установке WMF добавляются или обновляются следующие компоненты:

- Windows PowerShell
- Windows PowerShell Desired State Configuration (DSC)
- Интегрированная среда сценариев Windows PowerShell (ISE)
- Удаленное управление Windows (WinRM)
- Инструментарий управления Windows (WMI)
- Веб-службы Windows PowerShell (расширение IIS OData для управления)
- Инвентаризация программного обеспечения (SIL)
- Поставщик CIM диспетчера сервера

## <a name="wmf-release-notes"></a>Заметки о выпуске WMF

Сведения о различных улучшениях в PowerShell и других компонентах определенной версии WMF см. по следующим ссылкам на заметки о выпусках:

- [WMF 5.1](5.1/release-notes.md)
- [WMF 5.0](5.0/releasenotes.md)
- [WMF 4.0](https://download.microsoft.com/download/3/D/6/3D61D262-8549-4769-A660-230B67E15B25/Windows%20Management%20Framework%204%200%20Release%20Notes.docx)
- [WMF 3.0](https://download.microsoft.com/download/E/7/6/E76850B8-DA6E-4FF5-8CCE-A24FC513FD16/WMF%203%20Release%20Notes.docx)

## <a name="wmf-availability-across-windows-operating-systems"></a>Доступность WMF в различных операционных системах Windows

| Версия операционной системы | [WMF 5.1](https://aka.ms/wmf51download) | [WMF 5.0](https://aka.ms/wmf5download) | [WMF 4.0](https://aka.ms/wmf4download) |  [WMF 3.0](https://aka.ms/wmf3download) | [WMF 2.0](https://aka.ms/wmf2download) |
| ------------------------ | ----------- | ----------- | ----------- | ------------ |  ------------- |
| Windows Server 2016 | Входит в комплект поставки |  |  |  |  |
| Windows 10 | Входит в комплект поставки | Входит в комплект поставки  | | | |
| Windows Server 2012 R2| Да | Да | Входит в комплект поставки |  |  |
| Windows 8.1 | Да | Да |  Входит в комплект поставки |  |  |
| Windows Server 2012 | Да | Да | Да |  Входит в комплект поставки | |
| Windows 8 |  |  |  | Входит в комплект поставки | |
| Windows Server 2008 R2 с пакетом обновления 1 (SP1) | Да | Да | Да |  Да| Входит в комплект поставки |
| Windows 7 с пакетом обновления 1 (SP1)  | Да | Да | Да | Да | Входит в комплект поставки |
| Windows Server 2008 с пакетом обновления 2 (SP2) | | | | Да | Да |
| Windows Vista | | | | | Да |
| Windows Server 2003| | | |  | Да |
| Windows XP | | | |  | Да |

**"Входит в комплект поставки"**: функции `specified WMF` были включены в указанную версию Windows и Windows Server.
Поэтому установка `specified WMF` в указанных версиях операционных систем не требуется.