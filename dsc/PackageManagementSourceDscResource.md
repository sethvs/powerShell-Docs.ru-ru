---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс PackageManagementSource DSC"
ms.openlocfilehash: 80d157aff5bf7685a797baaf6a26215f02473096
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
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

