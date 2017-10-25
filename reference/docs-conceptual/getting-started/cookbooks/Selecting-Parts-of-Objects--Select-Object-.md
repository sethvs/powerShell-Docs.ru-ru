---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Выбор частей объектов (Select-Object)"
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 8c9633e80f63e1d474c46fa772108aee4f79751d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="selecting-parts-of-objects-select-object"></a><span data-ttu-id="6b589-103">Выбор частей объектов (Select-Object)</span><span class="sxs-lookup"><span data-stu-id="6b589-103">Selecting Parts of Objects (Select-Object)</span></span>
<span data-ttu-id="6b589-104">Командлет **Select-Object** позволяет создать пользовательские объекты Windows PowerShell со свойствами, выбранными из объектов, которые используются для их создания.</span><span class="sxs-lookup"><span data-stu-id="6b589-104">You can use the **Select-Object** cmdlet to create new, custom Windows PowerShell objects that contain properties selected from the objects you use to create them.</span></span> <span data-ttu-id="6b589-105">Введите следующую команду, чтобы создать объект, который содержит только свойства Name и FreeSpace класса WMI Win32_LogicalDisk.</span><span class="sxs-lookup"><span data-stu-id="6b589-105">Type the following command to create a new object that includes only the Name and FreeSpace properties of the Win32_LogicalDisk WMI class:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

<span data-ttu-id="6b589-106">После выполнения этой команды тип данных неизвестен, но если передать результат в Get-Member после Select-Object, можно узнать о наличии нового типа объекта — PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="6b589-106">You cannot see the type of data after issuing that command, but if you pipe the result to Get-Member after the Select-Object, you can tell that you have a new type of object, a PSCustomObject:</span></span>

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

<span data-ttu-id="6b589-107">Select-Object можно использовать по-разному.</span><span class="sxs-lookup"><span data-stu-id="6b589-107">Select-Object has many uses.</span></span> <span data-ttu-id="6b589-108">Одним из применений является репликация данных, которые затем можно изменить.</span><span class="sxs-lookup"><span data-stu-id="6b589-108">One of them is replicating data that you can then modify.</span></span> <span data-ttu-id="6b589-109">Теперь мы можем решить проблему, с которой столкнулись в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="6b589-109">We can now handle the problem we ran across in the previous section.</span></span> <span data-ttu-id="6b589-110">Можно изменить значение FreeSpace в созданных объектах, а результат будет включать описательную метку.</span><span class="sxs-lookup"><span data-stu-id="6b589-110">We can update the value of FreeSpace in our newly-created objects and the output will include the descriptive label:</span></span>

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```

