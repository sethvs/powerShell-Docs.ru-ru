---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Просмотр структуры объектов (Get-Member)"
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: eaa6cc44ecab04c76b90418115f388f6ff30e437
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="4453b-103">Просмотр структуры объектов (Get-Member)</span><span class="sxs-lookup"><span data-stu-id="4453b-103">Viewing Object Structure (Get-Member)</span></span>
<span data-ttu-id="4453b-104">Поскольку объекты играют ключевую роль в Windows PowerShell, существует несколько собственных команд для работы с произвольными типами объектов.</span><span class="sxs-lookup"><span data-stu-id="4453b-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="4453b-105">Наиболее важной является команда **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="4453b-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="4453b-106">Объекты, возвращаемые командой, проще всего проанализировать, передав ее выходные данные в командлет **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="4453b-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="4453b-107">Командлет **Get-Member** показывает формальное имя типа объекта и полный список его элементов.</span><span class="sxs-lookup"><span data-stu-id="4453b-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="4453b-108">Количество возвращаемых элементов иногда может быть просто огромным.</span><span class="sxs-lookup"><span data-stu-id="4453b-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="4453b-109">Например, объект процесса может иметь более ста элементов.</span><span class="sxs-lookup"><span data-stu-id="4453b-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="4453b-110">Чтобы просмотреть все элементы объекта процесса и вывести все выходные данные, введите:</span><span class="sxs-lookup"><span data-stu-id="4453b-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```
PS> Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="4453b-111">Выходные данные этой команды выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4453b-111">The output from this command will look something like this:</span></span>

```
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

<span data-ttu-id="4453b-112">Этот длинный перечень сведений можно сделать гораздо удобнее, отфильтровав нужные элементы.</span><span class="sxs-lookup"><span data-stu-id="4453b-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="4453b-113">Команда **Get-Member** позволяет вывести только те элементы, которые являются свойствами.</span><span class="sxs-lookup"><span data-stu-id="4453b-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="4453b-114">Существует несколько форм свойств.</span><span class="sxs-lookup"><span data-stu-id="4453b-114">There are several forms of properties.</span></span> <span data-ttu-id="4453b-115">Командлет отображает свойства любого типа, если для параметра **Get-MemberMemberType** задано значение **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4453b-115">The cmdlet displays properties of any type if we set the **Get-MemberMemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="4453b-116">Полученный список по-прежнему очень длинный, но работать с ним немного удобнее:</span><span class="sxs-lookup"><span data-stu-id="4453b-116">The resulting list is still very long, but a bit more manageable:</span></span>

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> <span data-ttu-id="4453b-117">Для MemberType разрешены следующие значения: AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet и All.</span><span class="sxs-lookup"><span data-stu-id="4453b-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="4453b-118">Для процесса существует более шестидесяти свойств.</span><span class="sxs-lookup"><span data-stu-id="4453b-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="4453b-119">Windows PowerShell часто показывает лишь небольшое число свойств для известного объекта, так как в противном случае выдается не поддающийся управлению объем информации.</span><span class="sxs-lookup"><span data-stu-id="4453b-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="4453b-120">Windows PowerShell определяет способ отображения типа объекта с помощью сведений, хранящихся в XML-файлах, имена которых заканчиваются на .format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="4453b-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="4453b-121">Данные форматирования для объектов процессов, которые являются объектами System.Diagnostics.Process .NET, хранятся в PowerShellCore.format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="4453b-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in PowerShellCore.format.ps1xml.</span></span>

<span data-ttu-id="4453b-122">Если требуется просмотреть свойства, отличные от отображаемых Windows PowerShell по умолчанию, необходимо самостоятельно отформатировать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="4453b-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="4453b-123">Это можно сделать с помощью командлетов форматирования.</span><span class="sxs-lookup"><span data-stu-id="4453b-123">This can be done by using the format cmdlets.</span></span>

