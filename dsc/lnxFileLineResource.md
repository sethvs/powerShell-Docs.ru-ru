---
title: "Ресурса nxFileLine в DSC для Linux"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 9196129e79272d8bee717ef8a5d42fb590760a0f
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-for-linux-nxfileline-resource"></a>Ресурса nxFileLine в DSC для Linux

Ресурс **nxFileLine** в DSC PowerShell предоставляет механизм управления строками в файле конфигурации на узле Linux.

## <a name="syntax"></a>Синтаксис

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Свойства

|  Свойство |  Описание | 
|---|---|
| FilePath| Полный путь к файлу для управления строками на целевом узле.| 
| ContainsLine| Строка, которая должна существовать в файле. Если в файле эта строка отсутствует, она будет добавлена. Свойство **ContainsLine** является обязательным, но, если оно не требуется, можно задать в качестве его значения пустую строку ("ContainsLine ="").| 
| DoesNotContainPattern| Шаблон регулярных выражений для строк, которые не должны присутствовать в файле. Присутствующие в файле строки, которые соответствуют этому регулярному выражению, будут удалены.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Пример

В этом примере показывается, как использовать ресурс **nxFileLine** для настройки файла `/etc/sudoers`, чтобы пользователь monuser не требовал использовать телетайп (TTY).

```
Import-DSCResource -Module nx 

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
} 
```

