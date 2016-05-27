---
title:  Выбор частей объектов с помощью Select-Object 
ms.date:  2016-05-11
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
ms.assetid:  72e64b1a-d351-4500-9da3-24d8a71d7a92
---

# Выбор частей объектов (Select-Object)
Командлет **Select-Object** позволяет создать новые пользовательские объекты Windows PowerShell со свойствами, выбранными из объектов, которые используются для их создания. Введите следующую команду, чтобы создать новый объект, который содержит только свойства Name и FreeSpace класса WMI Win32_LogicalDisk:

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

После выполнения этой команды тип данных неизвестен, но, если передать результат в Get-Member после Select-Object, можно узнать о наличии нового типа объекта — PSCustomObject:

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

Select-Object можно использовать по-разному. Одним из применений является репликация данных, которые затем можно изменить. Теперь мы можем решить проблему, с которой столкнулись в предыдущем разделе. Можно изменить значение FreeSpace в созданных объектах, а результат будет включать описательную метку:

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```



<!--HONumber=May16_HO2-->


