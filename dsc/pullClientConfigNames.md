# Настройка опрашивающего клиента с помощью имен конфигураций

> Область применения: Windows PowerShell 5.0

Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций. Для этого необходимо настроить локальный диспетчер конфигураций (LCM), указав нужную информацию. Чтобы настроить LCM, создайте специальный тип конфигурации, назначив атрибут **DSCLocalConfigurationManager**. Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).

> **Примечание**. Этот раздел относится к PowerShell 5.0. Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md)

Следующий сценарий настраивает LCM для получения конфигураций с сервера CONTOSO-PullSrv:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
            
        }      
    }
}
PullClientConfigID
```

В сценарии блок **ConfigurationRepositoryWeb** задает опрашивающий сервер. Свойство **ServerURL** указывает конечную точку для опрашивающего сервера.

Свойство **RegistrationKey** является общим ключом между всеми узлами клиента для опрашивающего сервера и их опрашивающего сервера. Те же значения хранятся в файле на опрашивающем сервере. Свойство **ConfigurationNames** указывает имя конфигурации, предназначенное для узла клиента. На опрашивающем сервере необходимо назвать MOF-файл конфигурации для этого узла клиента *ConfigurationNames*.mof, где *ConfigurationNames* соответствует значению свойства **ConfigurationNames**, заданному в этой метаконфигурации.

После запуска этого сценария будет создана новая выходная папка **PullClientConfigID**, в которую будет помещен MOF-файл метаконфигурации. В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.

Чтобы применить конфигурацию, вызовите командлет **Set-DscLocalConfigurationManager**, в параметре **Path** которого задано расположение MOF-файла метаконфигурации. Пример: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

> **Примечание**. Ключи регистрации работают только с опрашивающими веб-серверами. Вам по-прежнему следует использовать **ConfigurationID** с опрашивающим SMB-сервером. Сведения о настройке опрашивающего сервера с использованием **ConfigurationID** см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md)

## Серверы ресурсов и отчетов

По умолчанию узел клиента получает нужные ресурсы от опрашивающего сервера и передает на него состояние. Однако вы можете указать другие опрашивающие серверы для ресурсов и отчетов.
Чтобы указать сервер ресурсов, используйте **ResourceRepositoryWeb** (для опрашивающего веб-сервера) или блок **ResourceRepositoryShare** (для опрашивающего SMB-сервера).
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
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
        
        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
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

* [Настройка опрашивающего клиента с идентификатором конфигурации](pullClientConfigID.md)
* [Настройка опрашивающего веб-сервера DSC](pullServer.md)
<!--HONumber=Feb16_HO4-->
