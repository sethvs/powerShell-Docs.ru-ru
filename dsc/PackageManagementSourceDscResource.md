---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс PackageManagementSource DSC
ms.openlocfilehash: 8c0cb5a3b0a019ddb5ed995406f499298103b07c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-packagemanagementsource-resource"></a>Ресурс PackageManagementSource DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **PackageManagementSource** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм регистрации или ее отмены для источников управления пакетами на целевом узле. **Источники управления пакетами, зарегистрированные этим способом, регистрируются в контексте системы, доступной для учетной записи системы или подсистемы DSC.** Для этого ресурса требуется модуль **PackageManagement**, доступный из http://PowerShellGallery.com.

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
| Name| Указывает имя источника пакета, который будет зарегистрирован в системе или регистрация которого будет отменена.|
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