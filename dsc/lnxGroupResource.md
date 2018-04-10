---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxGroup в DSC для Linux
ms.openlocfilehash: 750b7c38a38fb8a7781585a3a7776f832ee62495
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxgroup-resource"></a>Ресурс nxGroup в DSC для Linux

Ресурс **nxGroup** в DSC PowerShell предоставляет механизм управления локальными группами на узле Linux.

## <a name="syntax"></a>Синтаксис

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a>Свойства

|  Свойство |  Описание |
|---|---|
| GroupName| Указывает имя группы, для которой требуется обеспечить определенное состояние.|
| Ensure| Определяет, нужно ли проверять существование группы. Чтобы убедиться, что группа существует, укажите для этого свойства значение Present. Чтобы убедиться, что группа не существует, укажите для этого свойства значение Absent. Значение по умолчанию — Present.|
| Члены группы| Указывает членов группы.|
| MembersToInclude| Указывает пользователей, которых нужно добавить в группу.|
| MembersToExclude| Указывает пользователей, которых нужно исключить из группы.|
| PreferredGroupID| По возможности задает в качестве идентификатора группы указанное значение. Если этот идентификатор группы сейчас используется, выбирается следующий доступный идентификатор группы.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Пример

В следующем примере удостоверяется, что пользователь monuser существует и является членом группы DBusers.

```
Import-DSCResource -Module nx

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}

nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"
}
}
```