# Настройка опрашивающего клиента с помощью идентификатора конфигурации

> Область применения: Windows PowerShell 5.0

Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций. Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию. Чтобы настроить LCM, создайте специальный тип конфигурации, помеченный с помощью атрибута DSCLocalConfigurationManager. Дополнительные сведения о настройке LCM см. в разделе Настройка локального диспетчера конфигураций.

> Примечание. Этот раздел относится к PowerShell 5.0. Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0.

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
            ConfigurationID = 1d545e3b-60c3-47a0-bf65-5afc05182fd0'
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

В сценарии блок ConfigurationRepositoryWeb задает опрашивающий сервер. ServerURL

После запуска этого сценария будет создана новая выходная папка PullClientConfigID, в которую будет помещен MOF-файл метаконфигурации. В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.

Чтобы применить конфигурацию, вызовите командлет Set-DscLocalConfigurationManager, в параметре Path которого задано расположение MOF-файла метаконфигурации. Пример: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## Идентификатор конфигурации

Сценарий задает для свойства ConfigurationID LCM значение GUID, созданное специально для этой цели (создать GUID можно, используя командлет New-Guid). Идентификатор ConfigurationID — это то, что LCM использует для поиска соответствующей конфигурации на опрашивающем сервере. MOF-файл конфигурации на опрашивающем сервере должен быть назван ConfigurationID.mof, где ConfigurationID является значением свойства ConfigurationID LCM целевого узла.

## Опрашивающий SMB-сервер

Чтобы настроить на клиенте опрос конфигураций с SMB-сервера, используйте блок ConfigurationRepositoryShare. В блоке ConfigurationRepositoryShare укажите путь к серверу, задав свойство SourcePath. Следующая метаконфигурация настраивает на целевом узле опрос с опрашивающего SMB-сервера SMBPullServer.

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
        ConfigurationRepositoryWeb SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'
            
        }     
    }
}
PullClientConfigID
```

## Серверы ресурсов и отчетов

Если указать только блок ConfigurationRepositoryWeb или ConfigurationRepositoryShare в конфигурации LCM (как в предыдущем примере), опрашивающий клиент будет получать 
ресурсы с указанного сервера, но не будет отправлять отчеты на этот сервер. Можно использовать один и тот же опрашивающий сервер для конфигурации, ресурсов и создания отчетов, но необходимо создать 
блок ReportRepositoryWeb для настройки отчетов. 

В следующем примере показана метаконфигурация, которая настраивает клиент для опроса конфигураций и ресурсов и отправки данных отчета на одном
опрашивающем сервере.

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

При этом можно указать различные опрашивающие серверы для ресурсов и отчетов. Чтобы указать сервер ресурсов, используйте блок ResourceRepositoryWeb (для опрашивающего веб-сервера) или 
ResourceRepositoryShare (для опрашивающего SMB-сервера).
Чтобы указать сервер отчетов, используйте блок ReportRepositoryWeb. Сервер отчетов не может быть SMB-сервером.
Следующая метаконфигурация настраивает для опрашивающего клиента получение конфигураций с CONTOSO-PullSrv, ресурсов — с CONTOSO-ResourceSrv, а также отправку отчетов о состоянии на CONTOSO-ReportSrv.

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

## См. также

* [Настройка опрашивающего клиента с именами конфигурации](pullClientConfigNames.md)

<!--HONumber=Mar16_HO4-->


