---
title: "Ресурс Script в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 56eb7ef230d84cc5f5679f39e13e2019205c65f5
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-script-resource"></a>Ресурс Script в DSC

 
> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **Script** в DSC Windows PowerShell предоставляет механизм запуска блоков сценариев на целевых узлах. Ресурс `Script` имеет свойства `GetScript`, `SetScript` и `TestScript`. Эти свойства должны быть заданы для блоков сценария, выполняемых на каждом целевом узле. 

Блок сценария `GetScript` должен возвращать хэш-таблицу, представляющую состояние текущего узла. Хэш-таблица должна содержать только один ключ `Result`, а значение должно иметь тип `String`. Выходные значения этого блока необязательны. DSC не выполняет никаких действий с выходными данными этого блока сценария.

Блок сценария `TestScript` должен определять, требуется ли изменение текущего узла. Он должен возвращать значение `$true`, если состояние узла актуально. Он должен возвращать значение `$false`, если конфигурация узла устарела и должна быть обновлена блоком сценария `SetScript`. Блок сценария `TestScript` вызывается DSC.

Блок сценария `SetScript` должен изменить узел. Он вызывается DSC, если блок `TestScript` возвращает значение `$false`.

Если необходимо использовать переменные из сценария конфигурации в блоках сценария `GetScript`, `TestScript` или `SetScript`, используйте область `$using:` (см. пример ниже).


## <a name="syntax"></a>Синтаксис

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Свойства

|  Свойство  |  Описание   | 
|---|---| 
| GetScript| Предоставляет блок сценария Windows PowerShell, который выполняется при вызове командлета [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx). Этот блок должен возвращать хэш-таблицу. Хэш-таблица должна содержать только один ключ **Result**, а значение должно иметь тип **String**.| 
| SetScript| Предоставляет блок сценария Windows PowerShell. При вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) в первую очередь выполняется блок **TestScript**. Если блок **TestScript** возвращает **$false**, будет запущен блок **SetScript**. Если блок **TestScript** возвращает **$true**, то блок **SetScript** запущен не будет.| 
| TestScript| Предоставляет блок сценария Windows PowerShell. Этот блок запускается при вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx). Если он возвращает **$false**, будет запущен блок SetScript. Если он возвращает **$true**, блок SetScript запущен не будет. Кроме того, блок **TestScript** запускается при вызове командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx). Однако в этом случае блок **SetScript** не будет запущен независимо от того, какое значение возвращает блок TestScript. Блок **TestScript** должен вернуть True, если фактическая конфигурация соответствует текущей конфигурации требуемого состояния, и False в противном случае. (Текущей конфигурацией требуемого состояния является последняя конфигурация, активированная на узле, который использует DSC.)| 
| Учетные данные| Указывает учетные данные, используемые для запуска этого сценария, если они необходимы.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.

## <a name="example-1"></a>Пример 1
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript = 
        { 
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
    }
}
```

## <a name="example-2"></a>Пример 2.
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Result' = "Version: $currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
            if( $state['Version'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Version'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = { 
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

Этот ресурс записывает версию конфигурации в текстовый файл. Эта версия доступна на клиентском компьютере, но не на узлах, поэтому ее необходимо передать во все блоки сценария ресурса `Script` с помощью области PowerShell `using`. При создании MOF-файла узла значение переменной `$version` считывается из текстового файла на клиентском компьютере. DSC заменяет переменные `$using:version` в каждом блоке сценария значением переменной `$version`.

