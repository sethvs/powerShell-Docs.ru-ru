---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForSome"
ms.openlocfilehash: cbe16c543f0eeb62dbe1fb439af2f9147f1bc210
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforsome-resource"></a>Ресурс DSC WaitForSome

> Область применения: Windows PowerShell 5.0 и более поздних версий.

Ресурс настройки требуемого состояния **WaitForAny** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.

Ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на минимальном числе узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**. 


## <a name="syntax"></a>Синтаксис

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   | 
|---|---| 
| NodeCount| Минимальное количество узлов, которые должны быть в требуемом состоянии для успешного выполнения этого ресурса.|
| NodeName| Целевые узлы ресурса, с которым настраивается отношение зависимости.| 
| ResourceName| Имя ресурса, с которым настраивается отношение зависимости.| 
| RetryIntervalSec| Количество секунд перед повторной попыткой. Минимальное значение — 1.| 
| RetryCount| Максимальное число повторных попыток.| 
| ThrottleLimit| Количество одновременно подключаемых компьютеров. Значение по умолчанию — New-CimSession.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|
| PsDscRunAsCredential | См. статью [Запуск DSC с учетными данными пользователя](https://docs.microsoft.com/en-us/powershell/dsc/runasuser). |


## <a name="example"></a>Пример

Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).

