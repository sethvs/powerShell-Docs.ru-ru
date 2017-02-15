---
title: "Настройка опрашивающего клиента с помощью идентификатора конфигурации"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 66702defb6f16740d93e020ebd22374b161efc5f
ms.sourcegitcommit: 267688f61dcc76fd685c1c34a6c7bfd9be582046
translationtype: HT
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a>Настройка опрашивающего клиента с помощью идентификатора конфигурации

> Область применения: Windows PowerShell 5.0

Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций. Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию. Чтобы настроить LCM, создайте специальный тип конфигурации, помеченный с помощью атрибута **DSCLocalConfigurationManager**. Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).

> **Примечание**. Этот раздел относится к PowerShell 5.0. Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md)

Следующий сценарий настраивает LCM для опроса конфигураций с сервера CONTOSO-PullSrv.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }      
    }
}
PullClientConfigID
```

В сценарии блок **ConfigurationRepositoryWeb** задает опрашивающий сервер. **ServerURL**

После запуска этого сценария будет создана новая выходная папка **PullClientConfigID**, в которую будет помещен MOF-файл метаконфигурации. В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.

Чтобы применить конфигурацию, вызовите командлет **Set-DscLocalConfigurationManager**, в параметре **Path** которого задано расположение MOF-файла метаконфигурации. Пример: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## <a name="configuration-id"></a>Идентификатор конфигурации

Сценарий задает для свойства **ConfigurationID** LCM значение GUID, созданное специально для этой цели (вы можете создать GUID, используя командлет **New-Guid**). Идентификатор **ConfigurationID** — это то, что LCM использует для поиска соответствующей конфигурации на опрашивающем сервере. MOF-файл конфигурации на опрашивающем сервере должен быть назван _ConfigurationID_.mof, где _ConfigurationID_ является значением свойства **ConfigurationID** LCM целевого узла.

## <a name="smb-pull-server"></a>Опрашивающий SMB-сервер

Чтобы настроить на клиенте опрос конфигураций с SMB-сервера, используйте блок **ConfigurationRepositoryShare**. В блоке **ConfigurationRepositoryShare** укажите путь к серверу, задав свойство **SourcePath**. Следующая метаконфигурация настраивает на целевом узле опрос с опрашивающего SMB-сервера **SMBPullServer**.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryShare SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'
            
        }     
    }
}
PullClientConfigID
```

## <a name="resource-and-report-servers"></a>Серверы ресурсов и отчетов

Если указать только блок **ConfigurationRepositoryWeb** или **ConfigurationRepositoryShare** в конфигурации LCM (как в предыдущем примере), опрашивающий клиент будет получать ресурсы с указанного сервера, но не будет отправлять отчеты на этот сервер. Можно использовать один и тот же опрашивающий сервер для конфигураций, ресурсов и создания отчетов, но необходимо создать блок **ReportRepositoryWeb** для настройки отчетов. 

В следующем примере показана метаконфигурация, которая настраивает клиент для опроса конфигураций и ресурсов и отправки данных отчетов на одном опрашивающем сервере.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

При этом можно указать различные опрашивающие серверы для ресурсов и отчетов. Чтобы указать сервер ресурсов, используйте **ResourceRepositoryWeb** (для опрашивающего веб-сервера) или блок **ResourceRepositoryShare** (для опрашивающего SMB-сервера).
Чтобы указать сервер отчетов, используйте блок **ReportRepositoryWeb**. Сервер отчетов не может быть SMB-сервером.
Следующая метаконфигурация настраивает опрашивающий клиент для получения конфигураций из **CONTOSO-PullSrv** и ресурсов из **CONTOSO-ResourceSrv**, а также для отправки отчетов о состоянии на **CONTOSO-ReportSrv**:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## <a name="see-also"></a>См. также

* [Настройка опрашивающего клиента с именами конфигураций](pullClientConfigNames.md)

