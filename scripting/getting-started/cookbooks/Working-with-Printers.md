---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "Работа с принтерами"
ms.technology: powershell
ms.assetid: 4f29ead3-f83b-4706-ac3e-f2154ff38dc5
ms.openlocfilehash: a75d0fc653bda7b368d3e1978d828040c3e67e3f
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="working-with-printers"></a>Работа с принтерами
Windows PowerShell можно использовать для управления принтерами с помощью инструментария WMI и COM-объекта WScript.Network с сервера сценариев Windows. Мы будем использовать сочетание обоих средств, чтобы продемонстрировать выполнение конкретных задач.

### <a name="listing-printer-connections"></a>Вывод подключений принтеров
Самый простой способ вывести список принтеров, установленных на компьютере, — использовать класс **Win32_Printer** инструментария WMI.

```
Get-WmiObject -Class Win32_Printer -ComputerName
```

Список принтеров можно также вывести с помощью COM-объекта **WScript.Network**, который обычно используется в сценариях сервера сценариев Windows:

```
(New-Object -ComObject WScript.Network).EnumPrinterConnections()
```

Поскольку эта команда возвращает простую коллекцию строк из имен портов и принтеров без отличительных меток, ее непросто интерпретировать.

### <a name="adding-a-network-printer"></a>Добавление сетевого принтера
Чтобы добавить сетевой принтер, используйте **WScript.Network**:

```
(New-Object -ComObject WScript.Network).AddWindowsPrinterConnection("\\Printserver01\Xerox5")
```

### <a name="setting-a-default-printer"></a>Установка принтера по умолчанию
Чтобы задать принтер по умолчанию с помощью инструментария WMI, найдите принтер в коллекции **Win32_Printer**, а затем вызовите метод **SetDefaultPrinter**.

```
(Get-WmiObject -ComputerName . -Class Win32_Printer -Filter "Name='HP LaserJet 5Si'").SetDefaultPrinter()
```

**WScript.Network** немного проще в использовании, так как содержит метод **SetDefaultPrinter**, который принимает в качестве аргумента только имя принтера:

```
(New-Object -ComObject WScript.Network).SetDefaultPrinter('HP LaserJet 5Si')
```

### <a name="removing-a-printer-connection"></a>Удаление подключения принтера
Чтобы удалить подключение принтера, используйте метод **WScript.Network RemovePrinterConnection**:

```
(New-Object -ComObject WScript.Network).RemovePrinterConnection("\\Printserver01\Xerox5")
```

