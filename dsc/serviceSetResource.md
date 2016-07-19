---
title: "Ресурс DSC ServiceSet"
ms.date: 2016-05-23
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 12438bc9c6e4211b6a31550fa25334a20fde6846
ms.openlocfilehash: 871d697626a0376e8f1f27bdbbf16d8612a56a79

---

# Ресурс DSC ServiceSet

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0


Ресурс **ServiceSet** в DSC Windows PowerShell предоставляет механизм управления службами на целевом узле. Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс Service](serviceResource.md) для каждой службы, указанной в свойстве `Name`.

Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких служб.

## Синтаксис

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    
}
```

## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имена служб. Обратите внимание на то, что иногда они отличаются от отображаемых имен. Список служб и их текущее состояние можно получить с помощью командлета [Get-Service](https://technet.microsoft.com/en-us/library/hh849804.aspx).|
| StartupType| Указывает тип запуска службы. Допустимые значения этого свойства: **Automatic**, **Disabled** и **Manual**.|  
| BuiltInAccount| Указывает учетную запись, используемую службами для входа. Допустимые значения этого свойства: **LocalService**, **LocalSystem** и **NetworkService**.| 
| State| Указывает состояние, в котором должны находиться службы: **Stopped** или **Running**.| 
| Ensure| Указывает, имеются ли службы в системе. Если службы не должны существовать, присвойте этому свойству значение **Absent**. Если целевые службы должны существовать, укажите значение **Present** (используется по умолчанию).|
| Учетные данные| Указывает учетные данные для учетной записи, от имени которой будет запускаться ресурс службы. Это свойство нельзя использовать одновременно со свойством **BuiltinAccount**.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — *ResourceName*, а его тип — *ResourceType*, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 



## Пример

Приведенная ниже конфигурация запускает службы "Windows Audio" и "Службы удаленных рабочих столов".

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```




<!--HONumber=Jul16_HO1-->


