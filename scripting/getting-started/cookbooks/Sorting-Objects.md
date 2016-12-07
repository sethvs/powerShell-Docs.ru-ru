---
title: "Сортировка объектов"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 99ca62261f8302673f886149a7715ce06efa16cb
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="sorting-objects"></a>Сортировка объектов
Можно упорядочить отображаемые данные с помощью командлета **Sort-Object**, чтобы упростить их проверку. **Sort-Object** принимает имя одного или нескольких свойств, по значениям которых выполняется сортировка, и возвращает отсортированные данные.

Рассмотрим проблему перечисления экземпляров Win32\_SystemDriver. Если требуется отсортировать по **State** и затем по **Name**, можно ввести:

```
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Хотя выводимые данные довольно длинные, можно просмотреть сгруппированные элементы с одинаковым состоянием:

```
Name           State   Started DisplayName
----           -----   ------- -----------
ACPI           Running    True Microsoft ACPI Driver
AFD            Running    True AFD
AmdK7          Running    True AMD K7 Processor Driver
AsyncMac       Running    True RAS Asynchronous Media Driver
...
Abiosdsk       Stopped   False Abiosdsk
ACPIEC         Stopped   False ACPIEC
aec            Stopped   False Microsoft Kernel Acoustic Echo Canceller
...
```

Можно также отсортировать объекты в обратном порядке, указав параметр **Descending**. При этом имена сортируются в обратном алфавитном порядке, а числа сортируются по убыванию.

```
PS> Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name -Descending | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap

Name           State   Started DisplayName
----           -----   ------- -----------
WS2IFSL        Stopped   False Windows Socket 2.0 Non-IFS Service Provider Supp
                               ort Environment
wceusbsh       Stopped   False Windows CE USB Serial Host Driver...
...
wdmaud         Running    True Microsoft WINMM WDM Audio Compatibility Driver
Wanarp         Running    True Remote Access IP ARP Driver
...
```

