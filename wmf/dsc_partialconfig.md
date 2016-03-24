# Настройка узла с помощью нескольких фрагментов конфигурации (неполные конфигурации)

WMF 5.0 помогает доставлять документы конфигурации на узел фрагментами. Чтобы узел получил несколько фрагментов документа конфигурации, его локальной диспетчер конфигураций (LCM) должен быть настроен на указание ожидаемых фрагментов, как показано в следующем примере:

```powershell
[DSCLocalConfigurationManager()]
configuration SQLServerDSCSettings
{
    Node localhost
    {
        Settings
        {
            ConfigurationModeFrequencyMins = 30
        }

        ConfigurationRepositoryWeb OSConfigServer
        {
            ServerURL = "https://corp.contoso.com/OSConfigServer/PSDSCPullServer.svc"
        }

        ConfigurationRepositoryWeb SQLConfigServer
        {
            ServerURL = "https://corp.contoso.com/SQLConfigServer/PSDSCPullServer.svc"
        }

        PartialConfiguration OSConfig
        {
            Description = 'Configuration for the Base OS'
            ExclusiveResources = 'PSDesiredStateConfiguration\*'
            ConfigurationSource = '[ConfigurationRepositoryWeb]OSConfigServer'
        }

        PartialConfiguration SQLConfig
        {
            Description = 'Configuration for the SQL Server'
            ConfigurationSource = '[ConfigurationRepositoryWeb]SQLConfigServer'
            DependsOn = '[PartialConfiguration]OSConfig'
        }
    }
}
```

В неполной конфигурации ее имя должно совпадать со значением в LCM. В приведенном выше примере конфигурации должны называться `OSConfig` и `SQLConfig`.

Настройка LCM на работу с неполными конфигурациями позволяет управлять ими, но не обеспечивает функции безопасности.<!--HONumber=Mar16_HO2-->
