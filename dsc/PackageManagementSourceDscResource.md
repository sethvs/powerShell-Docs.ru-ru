---
title: "Ресурс PackageManagementSource DSC"
ms.date: 
keywords: powershell,DSC
description: 
ms.topic: article
author: brywang-msft
manager: kriscv
ms.prod: powershell
ms.openlocfilehash: 22e61490e7b3f98335334a2703ec9639cbdaa87e
ms.sourcegitcommit: 89e7ae30faff5f96641fc72764bdc76e0e257bc2
translationtype: HT
---
# <a name="dsc-packagemanagementsource-resource"></a>Ресурс PackageManagementSource DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **PackageManagementSource** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм регистрации или ее отмены для источников управления пакетами на целевом узле. **Источники управления пакетами, зарегистрированные этим способом, регистрируются в контексте системы, доступной для учетной записи системы или подсистемы DSC.** Для этого ресурса требуется модуль **PackageManagement**: http://PowerShellGallery.com.

## <a name="syntax"></a>Синтаксис

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имя источника пакета, который будет зарегистрирован в системе или регистрация которого будет отменена.| 
| Ensure| Определяет, будет ли зарегистрирован источник пакета или его регистрация будет отменена.| 
| InstallationPolicy| Определяет, доверяете ли вы источнику пакета. Одно из двух значений: "Untrusted", "Trusted".| 
| ProviderName| Указывает имя поставщика OneGet, с помощью которого вы можете взаимодействовать с источником пакета.| 
| SourceUri| Указывает URI источника пакета.| 
| SourceCredential| Предоставляет доступ к пакету в удаленном источнике.| 

## <a name="example"></a>Пример

В этом примере регистрируется источник пакета http://nuget.org с помощью ресурса DSC **PackageManagementSource**.

```powershell
Configuration PackageManagementSourceTest
{    
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }
}
```
