---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Сортировка объектов
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 272d550a67b206f9924ebe143eca2f5906c0a304
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="sorting-objects"></a>Сортировка объектов

Можно упорядочить отображаемые данные с помощью командлета **Sort-Object**, чтобы упростить их проверку. **Sort-Object** принимает имя одного или нескольких свойств, по значениям которых выполняется сортировка, и возвращает отсортированные данные.

Рассмотрим проблему перечисления экземпляров Win32\_SystemDriver. Если требуется отсортировать по **State** и затем по **Name**, можно ввести:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

Хотя выводимые данные довольно длинные, можно просмотреть сгруппированные элементы с одинаковым состоянием:

```output
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