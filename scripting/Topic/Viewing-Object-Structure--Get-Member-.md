---
title: Просмотр структуры объектов (Get-Member)
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
---
# Просмотр структуры объектов (Get-Member)
Поскольку объекты играют ключевую роль в Windows PowerShell, существует несколько собственных команд для работы с произвольными типами объектов. Наиболее важной является команда **Get-Member**.

Объекты, возвращаемые командой, проще всего проанализировать, передав ее выходные данные в командлет **Get-Member**. Командлет **Get-Member** показывает формальное имя типа объекта и полный список его элементов. Количество возвращаемых элементов иногда может быть просто огромным. Например, объект процесса может иметь более ста элементов.

Чтобы просмотреть все элементы объекта процесса и вывести все выходные данные, введите:

```
PS> Get-Process | Get-Member | Out-Host -Paging
```

Выходные данные этой команды выглядят следующим образом:

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

Этот длинный перечень сведений можно сделать гораздо удобнее, отфильтровав нужные элементы. Команда **Get-Member** позволяет вывести только те элементы, которые являются свойствами. Существует несколько форм свойств. Командлет отображает свойства любого типа, если для параметра **Get-MemberMemberType** задано значение **Properties**. Полученный список по-прежнему очень длинный, но работать с ним немного удобнее:

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
> Для MemberType разрешены следующие значения: AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet и All.

Для процесса существует более шестидесяти свойств. Windows PowerShell часто показывает лишь небольшое число свойств для известного объекта, так как в противном случае выдается не поддающийся управлению объем информации.

> [!NOTE]
> Windows PowerShell определяет способ отображения типа объекта с помощью сведений, хранящихся в XML-файлах, имена которых заканчиваются на .format.ps1xml. Данные форматирования для объектов процессов, которые являются объектами System.Diagnostics.Process .NET, хранятся в PowerShellCore.format.ps1xml.

Если требуется просмотреть свойства, отличные от отображаемых Windows PowerShell по умолчанию, необходимо самостоятельно отформатировать выходные данные. Это можно сделать с помощью командлетов форматирования.



<!--HONumber=Apr16_HO1-->


