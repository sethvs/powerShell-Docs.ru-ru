---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForAny"
ms.openlocfilehash: ba1873cc0ecfc4596cbad5b61b4a52b61ea4778a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-waitforany-resource"></a>Ресурс DSC WaitForAny

> Область применения: Windows PowerShell 5.1 и более поздних версий.

Ресурс настройки требуемого состояния **WaitForSome** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.

Этот ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на всех целевых узлах, определенных в свойстве **NodeName**.


## <a name="syntax"></a>Синтаксис

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   | 
|---|---| 
| ResourceName| Имя ресурса, с которым настраивается отношение зависимости.| 
| NodeName| Целевые узлы ресурса, с которым настраивается отношение зависимости.| 
| RetryIntervalSec| Количество секунд перед повторной попыткой. Минимальное значение — 1.| 
| RetryCount| Максимальное число повторных попыток.| 
| ThrottleLimit| Количество одновременно подключаемых компьютеров. Значение по умолчанию — New-CimSession.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|


## <a name="example"></a>Пример

Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).

