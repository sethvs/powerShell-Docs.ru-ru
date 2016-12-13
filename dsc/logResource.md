---
title: "Ресурс Log в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: fe905237f5f0672f6e5e0cd399e1b71058417d9c
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-log-resource"></a>Ресурс Log в DSC 

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс __Log__ в DSC Windows PowerShell предоставляет механизм записи сообщений в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

ПРИМЕЧАНИЕ. По умолчанию включены только операционные журналы DSC.
Чтобы журнал аналитики стал доступным или видимым, его необходимо включить.
См. следующую статью.

[Где находятся журналы событий DSC?](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   | 
|---|---| 
| Сообщение| Указывает сообщение для записи в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.| 
| DependsOn | Указывает, что перед записью этого сообщения в журнал необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Пример

В следующем примере показано, как добавить сообщение в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.

> **Примечание**. Если этот ресурс настроен, при выполнении командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) всегда возвращается значение **$false**.

```powershell 
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```

