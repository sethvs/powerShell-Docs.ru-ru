---
title: Сортировка объектов
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
---
# Сортировка объектов
Можно упорядочить отображаемые данные с помощью командлета **Sort-Object** для упрощения их проверки. **Sort-Object** принимает имя одного или нескольких свойств, по значениям которых выполняется сортировка, и возвращает отсортированные данные.

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



<!--HONumber=Apr16_HO1-->


