---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Работа с принтерами
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: 5638629fdf79371c8eff9ee9194b642034250fff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="working-with-printers"></a>Работа с принтерами

Windows PowerShell можно использовать для управления принтерами с помощью инструментария WMI и COM-объекта WScript.Network с сервера сценариев Windows. Мы будем использовать сочетание обоих средств, чтобы продемонстрировать выполнение конкретных задач.

### <a name="listing-printer-connections"></a>Вывод подключений принтеров

Самый простой способ вывести список принтеров, установленных на компьютере, — использовать класс **Win32_Printer** инструментария WMI.

```powershell
Get-WmiObject -Class Win32_Printer -ComputerName
```

Список принтеров можно также вывести с помощью COM-объекта **WScript.Network**, который обычно используется в сценариях сервера сценариев Windows:

```powershell
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Поскольку эта команда возвращает простую коллекцию строк из имен портов и принтеров без отличительных меток, ее непросто интерпретировать.

### <a name="adding-a-network-printer"></a>Добавление сетевого принтера

Чтобы добавить сетевой принтер, используйте **WScript.Network**:

```powershell
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Установка принтера по умолчанию

Чтобы задать принтер по умолчанию с помощью инструментария WMI, найдите принтер в коллекции **Win32_Printer**, а затем вызовите метод **SetDefaultPrinter**.

```powershell
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** немного проще в использовании, так как содержит метод **SetDefaultPrinter**, который принимает в качестве аргумента только имя принтера:

```powershell
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Удаление подключения принтера

Чтобы удалить подключение принтера, используйте метод **WScript.Network RemovePrinterConnection**:

```powershell
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```