---
title: "Ресурс Service в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: bda348e6597f31b8dfa2014e5c34c5d3bc7bca15
ms.openlocfilehash: 10123359213df7180388d9251e032c2bbb673143

---

# Ресурс Service в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0


Ресурс **Service** в DSC Windows PowerShell предоставляет механизм управления службами на целевом узле.

## Синтаксис

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имя службы. Обратите внимание! Иногда оно отличается от отображаемого имени. Список служб и их текущее состояние можно получить с помощью командлета Get-Service.| 
| BuiltInAccount| Указывает учетную запись, используемую службой для входа. Допустимые значения этого свойства: **LocalService**, **LocalSystem** и **NetworkService**.| 
| Учетные данные| Указывает учетные данные для учетной записи, от имени которой будет запускаться служба. Это свойство нельзя использовать одновременно со свойством __BuiltinAccount__.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| StartupType| Указывает тип запуска службы. Допустимые значения этого свойства: **Automatic**, **Disabled** и **Manual**.| 
| State| Указывает состояние, в котором должна находиться служба.| 
| Описание | Указывает описание целевой службы.| 
| DisplayName | Указывает отображаемое имя целевой службы.| 
| Ensure | Указывает, имеется ли целевая служба в системе. Если целевая служба не должна существовать, укажите для этого свойства значение **Absent**. Если целевая служба должна существовать, укажите значение **Present** (используется по умолчанию).|
| путь | Указывает путь к двоичному файлу для новой службы.| 

## Пример

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```




<!--HONumber=Jul16_HO1-->


