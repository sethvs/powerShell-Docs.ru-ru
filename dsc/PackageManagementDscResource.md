---
title: "Ресурс PackageManagement DSC"
ms.date: 
keywords: powershell,DSC
description: 
ms.topic: article
author: brywang-msft
manager: kriscv
ms.prod: powershell
ms.openlocfilehash: 33775be230a4e92e22784d991338510510f69889
ms.sourcegitcommit: 89e7ae30faff5f96641fc72764bdc76e0e257bc2
translationtype: HT
---
# <a name="dsc-packagemanagement-resource"></a>Ресурс PackageManagement DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **PackageManagement** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм установки пакетов управления пакетами на целевом узле или их удаления. Для этого ресурса требуется модуль **PackageManagement**: http://PowerShellGallery.com.

## <a name="syntax"></a>Синтаксис

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   | 
|---|---| 
| Название| Указывает имя устанавливаемого или удаляемого пакета.| 
| Источник| Указывает имя источника пакета, в котором его можно найти. Это может быть URI или источник, зарегистрированный с помощью ресурса DSC Register-PackageSource или PackageManagementSource. MSFT_PackageManagementSource ресурса DSC может также зарегистрировать источник пакета.| 
| Ensure| Определяет, следует ли установить или удалить пакет.| 
| RequiredVersion| Указывает точную версию пакета, который вы хотите установить. Если вы не укажете этот параметр, ресурс DSC установит новейшую версию пакета, соответствующую максимальной версии, указанной в параметре MaximumVersion.| 
| MinimumVersion| Указывает минимальную версию пакета, которую вы хотите установить. Если вы не добавите этот параметр, ресурс DSC установит новейшую версию пакета, соответствующую максимальной версии, указанной в параметре MaximumVersion.| 
| MaximumVersion| Указывает максимальную версию пакета, которую вы хотите установить. Если вы не укажете этот параметр, ресурс DSC установит новейшую версию пакета.| 
| SourceCredential | Указывает учетную запись пользователя с правами для установки пакета для заданного поставщика или источника пакетов.| 
| ProviderName| Указывает имя поставщика пакетов, на который распространяется область поиска пакетов. Чтобы получить имена поставщика, запустите командлет Get-PackageProvider.| 
| AdditionalParameters| Специальные параметры поставщика, которые передаются как хэш-таблица. Например, для поставщика NuGet можно передать дополнительные параметры, такие как DestinationPath.| 

## <a name="additional-parameters"></a>Дополнительные параметры
В следующей таблице перечислены параметры свойства AdditionalParameters.
|  Параметр  | Описание   | 
|---|---|
| DestinationPath| Используется поставщиками, такими как встроенный поставщик NuGet. Указывает расположение файла, в котором вы хотите установить пакет.|
| InstallationPolicy| Используется поставщиками, такими как встроенный поставщик NuGet. Определяет, доверяете ли вы источнику пакета. Одно из двух значений: "Untrusted", "Trusted".|

## <a name="example"></a>Пример

В этом примере устанавливается пакет NuGet **JQuery** и модуль PowerShell **GistProvider** с помощью ресурса DSC **PackageManagement**. В этом примере сначала обеспечивается доступность нужных источников пакета, а затем определяется ожидаемое состояние пакетов **JQuery** и **GistProvider** (для NuGet и PowerShell).

```powershell
Configuration PackageTest
{    
    PackageManagementSource SourceRepository 
    { 
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }    
    
    PackageManagementSource PSGallery 
    { 
        Ensure      = "Present" 
        Name        = "psgallery" 
        ProviderName= "PowerShellGet" 
        SourceUri   = "https://www.powershellgallery.com/api/v2/"   
        InstallationPolicy ="Trusted" 
    } 
          
    PackageManagement NugetPackage 
    { 
        Ensure               = "Present"  
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1" 
        DependsOn            = "[PackageManagementSource]SourceRepository" 
    }
    
    PackageManagement PSModule 
    { 
        Ensure               = "Present"  
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery" 
    }
}
```