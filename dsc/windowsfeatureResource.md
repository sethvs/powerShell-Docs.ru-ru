---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс WindowsFeature в DSC"
ms.openlocfilehash: a3433577a122f6c7e31360e094a089f6ceef77c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="dsc-windowsfeature-resource" class="xliff"></a>
# Ресурс WindowsFeature в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **WindowsFeature** в DSC Windows PowerShell предоставляет механизм добавления и удаления ролей и компонентов на целевом узле.

<a id="syntax" class="xliff"></a>
## Синтаксис

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

<a id="properties" class="xliff"></a>
## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имя роли или компонента, которые необходимо добавить или удалить. Это свойство аналогично свойству __Name__ командлета [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) и не является отображаемым именем роли или компонента.| 
| Учетные данные| Указывает учетные данные для добавления или удаления роли или компонента.| 
| Ensure| Указывает, добавляется или удаляется роль или компонент. Чтобы добавить роль или компонент, установите это свойство равным Present, чтобы удалить — равным Absent.| 
| IncludeAllSubFeature| Присвойте этому свойству значение __$true__ для синхронизации состояния всех необходимых дополнительных компонентов с состоянием компонента, указанного в свойстве __Name__.| 
| LogPath| Указывает путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| Источник| Указывает расположение исходного файла для установки, если он необходим.| 

<a id="example" class="xliff"></a>
## Пример
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```

