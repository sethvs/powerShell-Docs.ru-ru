---
title: "Повторение задачи для нескольких объектов с помощью ForEach-Object"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 4b219e4499482eafa6eddf1461b74c62ba091d1a
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="repeating-a-task-for-multiple-objects-foreach-object"></a>Повторение задачи для нескольких объектов (ForEach-Object)
Командлет **ForEach-Object** использует блоки сценариев и дескриптор $_ текущего объекта конвейера, чтобы вы могли выполнить команду для каждого объекта в конвейере. Это можно использовать для выполнения некоторых сложных задач.

Одним из случаев, где это может пригодиться, является обработка данных, делающая их более полезными. Например, класс Win32_LogicalDisk из инструментария WMI можно использовать для возврата сведений о свободном пространстве на каждом локальном диске. Данные возвращаются в виде байтов, что затрудняет их восприятие:

```
PS> Get-WmiObject -Class Win32_LogicalDisk

DeviceID     : C:
DriveType    : 3
ProviderName :
FreeSpace    : 50665070592
Size         : 203912880128
VolumeName   : Local Disk
```

Можно преобразовать FreeSpace в мегабайты, дважды разделив каждое значение на 1024. После первого деления данные представлены в килобайтах, после второго — в мегабайтах. Это можно сделать в блоке сценария ForEach-Object, введя следующее:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

К сожалению, в результате получаются данные без соответствующей метки. Так как свойства инструментария WMI, такие как это, доступны только для чтения, непосредственное преобразование FreeSpace невозможно. Если ввести следующее:

```
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Отображается сообщение об ошибке:

```
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Вы можете реорганизовать данные с помощью некоторых усовершенствованных методик, однако проще создать объект с помощью **Select-Object**.

