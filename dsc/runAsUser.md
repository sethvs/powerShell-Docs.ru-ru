---
title: "Запуск DSC с учетными данными пользователя"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 6477ae8575c83fc24150f9502515ff5b82bc8198
ms.openlocfilehash: dbe2c1ca2fb7dd65b49876f3bee6752ec9a24d6b

---

# Запуск DSC с учетными данными пользователя 

> Область применения: Windows PowerShell 5.0

Ресурс DSC можно запускать с определенным набором учетных данных. Для этого используется автоматическое свойство **PsDscRunAsCredential** в конфигурации. По умолчанию DSC запускает каждый ресурс в качестве системной учетной записи. Иногда бывает необходим запуск с учетной записью обычного пользователя, например, при установке MSI-пакетов в контексте определенного пользователя, при установке разделов реестра пользователя, доступе к конкретному локальному каталогу пользователя или сетевой папке.

У каждого ресурса есть свойство **PsDscRunAsCredential**, которому можно назначить учетные данные любого пользователя (объект [PSCredential](https://msdn.microsoft.com/en-us/library/ms572524(v=VS.85).aspx)).
Учетные данные можно жестко задать в качестве значения свойства конфигурации или установить в качестве значения [Get-Credential](https://technet.microsoft.com/en-us/library/hh849815.aspx). В этом случае пользователю будет предложено ввести учетные данные при компиляции конфигурации (дополнительные сведения о компиляции конфигураций см. в разделе [Конфигурации](configurations.md)).

>**Примечание**. Свойство **PsDscRunAsCredential** недоступно в PowerShell 4.0.

В следующем примере **Get-Credential** используется для запроса учетных данных пользователя. Ресурс [Registry](registryResource.md) используется для изменения раздела реестра, указывающего цвет фона для окна командной строки Windows.

```powershell
Configuration ChangeCmdBackGroundColor    
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        Registry CmdPath
        {
            Key                  = 'HKEY_CURRENT_USER\SOFTWARE\Microsoft\Command Processor'
            ValueName            = 'DefaultColor'
            ValueData            = '1F'
            ValueType            = 'DWORD'
            Ensure               = 'Present'
            Force                = $true
            Hex                  = $true
            PsDscRunAsCredential = Get-Credential
        }
    }                   
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

ChangeCmdBackGroundColor -ConfigurationData $configData
```
>**Примечание**. В этом примере предполагается, что у вас есть действительный сертификат в `C:\publicKeys\targetNode.cer` и что отображаемое значение представляет собой отпечаток этого сертификата.
>Сведения о шифровании учетных данных в MOF-файлах конфигурации DSC см. в разделе [Защита MOF-файла](secureMOF.md).




<!--HONumber=Jun16_HO4-->


