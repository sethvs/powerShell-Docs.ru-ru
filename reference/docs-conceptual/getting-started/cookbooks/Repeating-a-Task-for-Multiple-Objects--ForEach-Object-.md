---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Повторение задачи для нескольких объектов (ForEach-Object)
ms.assetid: 6697a12d-2470-4ed6-b5bb-c35e5d525eb6
ms.openlocfilehash: 8b8002af3ade0905421760ce29cdc84b084236e9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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

Можно преобразовать FreeSpace в мегабайты, дважды разделив каждое значение на 1024. После первого деления данные представлены в килобайтах, после второго — в мегабайтах. Это можно сделать в блоке сценария ForEach-Object, введя следующее:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {($_.FreeSpace)/1024.0/1024.0}
48318.01171875
```

К сожалению, в результате получаются данные без соответствующей метки. Так как свойства инструментария WMI, такие как это, доступны только для чтения, непосредственное преобразование FreeSpace невозможно. Если ввести следующее:

```powershell
Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Отображается сообщение об ошибке:

```output
"FreeSpace" is a ReadOnly property.
At line:1 char:70
+ Get-WmiObject -Class Win32_LogicalDisk | ForEach-Object -Process {$_.F <<<< r
eeSpace = ($_.FreeSpace)/1024.0/1024.0}
```

Вы можете реорганизовать данные с помощью некоторых усовершенствованных методик, однако проще создать объект с помощью **Select-Object**.