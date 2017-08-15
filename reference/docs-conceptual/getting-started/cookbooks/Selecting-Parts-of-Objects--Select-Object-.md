---
ms.date: 2017-06-05T00:00:00.000Z
keywords: "powershell,командлет"
title: "Выбор частей объектов (Select-Object)"
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 8c9633e80f63e1d474c46fa772108aee4f79751d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="selecting-parts-of-objects-select-object"></a>Выбор частей объектов (Select-Object)
Командлет **Select-Object** позволяет создать пользовательские объекты Windows PowerShell со свойствами, выбранными из объектов, которые используются для их создания. Введите следующую команду, чтобы создать объект, который содержит только свойства Name и FreeSpace класса WMI Win32_LogicalDisk.

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

После выполнения этой команды тип данных неизвестен, но если передать результат в Get-Member после Select-Object, можно узнать о наличии нового типа объекта — PSCustomObject.

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

Select-Object можно использовать по-разному. Одним из применений является репликация данных, которые затем можно изменить. Теперь мы можем решить проблему, с которой столкнулись в предыдущем разделе. Можно изменить значение FreeSpace в созданных объектах, а результат будет включать описательную метку.

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```

