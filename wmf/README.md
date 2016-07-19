---
title: Windows Management Framework (WMF)
ms.date: 2016-05-16
keywords: PowerShell, WMF
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
translationtype: Human Translation
ms.sourcegitcommit: b32cb86b7a18fee929cc81360d81f479571a74c2
ms.openlocfilehash: a7ef0ddf4d093a89f32f3484dfbef78fb159f0c2

---

# Windows Management Framework

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

## Заметки о выпуске WMF
Сведения о различных улучшениях в PowerShell и других компонентах определенной версии WMF см. по следующим ссылкам на заметки о выпусках:


- [WMF 5.1 (предварительная версия)](5.1/release-notes.md)
- [WMF 5.0](5.0/releasenotes.md)


## Доступность WMF в различных операционных системах Windows

>TODO: добавить ссылки на конкретные DLC WMF в заголовок столбца

| Версия операционной системы | [Предварительная версия WMF 5.1 *]() | [WMF 5.0]() | [WMF 4.0]() |  [WMF 3.0]() | [WMF 2.0]() |
| ------------------------ | ----------- | ----------- | ----------- | ------------ |  ------------- |
| Windows Server 2016 | Входит в комплект поставки * | Входит в комплект поставки * |  |  |  |
| Windows 10 | Входит в комплект поставки * | Входит в комплект поставки *  | | | |  
| Windows Server 2012 R2| ?? | Да | Входит в комплект поставки |  |  |
| Windows 8.1 | ?? | Да |  Входит в комплект поставки |  |  |
| Windows Server 2012 | ?? | Да | Да |  Входит в комплект поставки | |
| Windows 8 |  |  |  | Входит в комплект поставки | |
| Windows Server 2008 R2 с пакетом обновления 1 (SP1) | ?? | Да | Да |  Да| Входит в комплект поставки |
| Windows 7 с пакетом обновления 1 (SP1)  | ?? | Да | Да | Да | Входит в комплект поставки |
| Windows Server 2008 с пакетом обновления 2 (SP2) | | | | Да | Да |
| Windows Vista | | | | | Да |
| Windows Server 2003| | | |  | Да |
| Windows XP | | | |  | Да |

>TODO: объяснить значение значка * в приведенной выше таблице



<!--HONumber=Jul16_HO1-->


