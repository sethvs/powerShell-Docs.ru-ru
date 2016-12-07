---
title: "Ресурс DSC WindowsOptionalFeature"
ms.date: 2016-05-24
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 26d140d68760ec92b3b6cbc31d0735eaaf671d9c
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-windowsoptionalfeature-resource"></a>Ресурс DSC WindowsOptionalFeature

> Область применения: Windows PowerShell 5.0

Ресурс **WindowsOptionalFeature** в DSC Windows PowerShell предоставляет механизм включения дополнительных компонентов на целевом узле.

## <a name="syntax"></a>Синтаксис

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имя компонента, который необходимо включить или отключить.| 
| Ensure| Указывает, включен ли компонент. Чтобы включить компонент, установите это свойство равным Present, чтобы отключить — равным Absent.|
| Источник| Не реализовано.|
| NoWindowsUpdateCheck| Указывает, обращается ли система DISM к Центру обновления Windows при поиске исходных файлов для включения компонента. Если задано значение $true, система DISM не обращается к Центру обновления Windows.|
| RemoveFilesOnDisable| Задайте значение **$true**, чтобы удалить все файлы, связанные с компонентом, при его отключении (то есть когда свойству **Ensure** присваивается значение Absent).|
| Уровень журнала| Максимальный уровень результатов, показываемый в журналах. Допустимые значения: ErrorsOnly (в журналы записываются только ошибки), ErrorsAndWarning (в журналы записываются ошибки и предупреждения) и ErrorsAndWarningAndInformation (в журналы записываются ошибки, предупреждения и отладочные сведения).|
| LogPath| Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
 



