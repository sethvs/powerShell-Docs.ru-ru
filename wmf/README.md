---
title: Windows Management Framework (WMF)
ms.date: 2017-02-14
keywords: PowerShell, WMF
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: 749dd8b19592cb5f40a5aed32d28edeb5cb2dfc9
ms.sourcegitcommit: bb2c52577a519c0599a0b3c961f749fe0df70a45
translationtype: HT
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
