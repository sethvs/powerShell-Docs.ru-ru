---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC,PowerShell,конфигурация,установка"
title: "Ресурс DSC WindowsFeatureSet"
ms.openlocfilehash: 3cdabc36ef35c2bf912ac54393fe40024a8e8bc0
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsfeatureset-resource"></a>Ресурс DSC WindowsFeatureSet

> Область применения: Windows PowerShell 5.0

Ресурс **WindowsFeatureSet** в DSC Windows PowerShell предоставляет механизм добавления и удаления ролей и компонентов на целевом узле.
Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс WindowsFeature](windowsfeatureResource.md) для каждого компонента, указанного в свойстве `Name`.

Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких компонентов Windows.

## <a name="syntax"></a>Синтаксис

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]] 
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   | 
|---|---| 
| Название| Имена ролей или компонентов, которые необходимо добавить или удалить. Это свойство аналогично свойству **Name** командлета [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) и не содержит отображаемые имена ролей или компонентов.| 
| Учетные данные| Учетные данные для добавления или удаления ролей или компонентов.| 
| Ensure| Указывает, добавляются ли роли или компоненты. Чтобы добавить роли или компоненты, установите это свойство равным Present, чтобы удалить — равным Absent.| 
| IncludeAllSubFeature| Присвойте этому свойству значение **$true**, чтобы включить все необходимые дополнительные компоненты для компонентов, указанных в свойстве **Name**.| 
| LogPath| Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| Источник| Указывает расположение исходного файла для установки, если он необходим.| 

## <a name="example"></a>Пример

Приведенная ниже конфигурация обеспечивает установку компонентов **Веб-сервер** (IIS) и **SMTP-сервер**, а также всех их дополнительных компонентов.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        } 
    }
}
```

