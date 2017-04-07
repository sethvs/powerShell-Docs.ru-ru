---
title: "Вложение конфигураций"
ms.date: 2017-03-27
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: carmonm
ms.prod: powershell
ms.openlocfilehash: 3afc4c87b1bc54e5f251a3a54eab5f448900f124
ms.sourcegitcommit: 65250232157bb1c742d7d385933b8abc24a570fb
translationtype: HT
---
# <a name="nesting-dsc-configurations"></a>Вложение конфигураций DSC

Вложенная конфигурация (также называемая составной конфигурацией) — это конфигурация, которая вызывается в составе другой конфигурации подобно ресурсу.
Обе конфигурации должны быть определены в одном файле.

Давайте рассмотрим простой пример:

```powershell
Configuration FileConfig 
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }
    
}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

В этом примере `FileConfig` принимает два обязательных параметра — **CopyFrom** и **CopyTo**, — которые используются как значения для свойств **SourcePath** и **DestinationPath** в блоке ресурсов `File`. Конфигурация `NestedConfig` вызывает конфигурацию `FileConfig`, как будто это ресурс.
Свойства в блоке ресурсов `NestedConfig` (**CopyFrom** и **CopyTo**) — параметры конфигурации `FileConfig`.

## <a name="see-also"></a>См. также

- [Составные ресурсы: использование DSC как ресурса](authoringResourceComposite.md)
