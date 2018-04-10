---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC WindowsPackageCab
ms.openlocfilehash: af45956c1fe8cffa1d7fd779847eded9e3f6b51e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowspackagecab-resource"></a>Ресурс DSC WindowsPackageCab

> Область применения: Windows PowerShell 5.1 и более поздних версий.

Ресурс **WindowsPackageCab** в службе настройки требуемого состояния Windows PowerShell (DSC) предоставляет механизм установки пакетов CAB-файлов Windows на целевом узле или их удаления.

На целевом узле должен быть установлен модуль DISM PowerShell. Дополнительные сведения см. в статье [Use DISM in Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14) (Использование DISM в Windows PowerShell)


## <a name="syntax"></a>Синтаксис

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   |
|---|---|
| Name| Указывает имя пакета, для которого требуется обеспечить определенное состояние.|
| Ensure| Указывает, установлен ли пакет. Если это свойство имеет значение Absent, пакет не устанавливается (а если он уже установлен, то удаляется). Если это свойство имеет значение Present (по умолчанию), пакет устанавливается.|
| путь| Указывает путь к файлу пакета.|
| LogPath| Указывает полный путь к папке, где нужно сохранить файл журнала для установки или удаления пакета.|
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: "DependsOn = "[ResourceType]ResourceName"".|

## <a name="example"></a>Пример

Ниже приведен пример конфигурации, которая принимает входные параметры и гарантирует, что CAB-файл, указанный в параметре `$Name`, установлен.

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```