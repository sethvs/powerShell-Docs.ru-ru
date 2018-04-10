---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс WindowsProcess в DSC
ms.openlocfilehash: 236a48fd4449a96f2297c152bce65253dd2fd08d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsprocess-resource"></a>Ресурс WindowsProcess в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **WindowsProcess** в DSC Windows PowerShell предоставляет механизм настройки процессов на целевом узле.

## <a name="syntax"></a>Синтаксис

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   |
|---|---|
| Аргументы| Указывает строку аргументов, которая будет передана процессу "как есть". Если необходимо передать несколько аргументов, поместите их все в эту строку.|
| путь| Путь к исполняемому файлу процесса. Если это имя исполняемого файла (а не полный путь к нему), ресурс DSC будет искать переменную среды **Path** (`$env:Path`), чтобы найти исполняемый файл. Если значение этого свойства — полный путь, ресурс DSC не будет использовать переменную среды **Path** для поиска файла и вызовет ошибку в случае отсутствия пути. Относительные пути не допускаются.|
| Учетные данные| Указывает учетные данные для запуска процесса.|
| Ensure| Указывает, существует ли процесс. Если процесс существует, укажите для этого свойства значение Present. В противном случае укажите значение Absent. Значение по умолчанию — Present.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: 'DependsOn = "[ResourceType]ResourceName"''.|
| StandardErrorPath| Указывает путь к каталогу для записи стандартных ошибок. Все существующие файлы в этом каталоге будут перезаписаны.|
| StandardInputPath| Указывает расположение стандартного ввода.|
| StandardOutputPath| Указывает расположение стандартного вывода. Все существующие файлы в этом каталоге будут перезаписаны.|
| WorkingDirectory| Указывает расположение, которое будет использоваться в качестве текущего рабочего каталога для процесса.|