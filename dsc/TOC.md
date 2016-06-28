# [Обзор](overview.md)

# [Конфигурации](configurations.md)
## [Применение конфигураций](enactingConfigurations.md)
## [Использование ресурсов с несколькими версиями](sxsResource.md)
## [Запуск DSC с учетными данными пользователя](runAsUser.md)
## [Указание межузловых зависимостей](crossNodeDependencies.md)
## [Данные конфигурации](configData.md)
### [Параметры учетных данных в данных конфигурации](configDataCredentials.md)
## [Защита MOF-файла конфигурации](secureMOF.md)
## [Частичные конфигурации](partialConfigs.md)
## [Запись поддержки конфигураций DSC](configHelp.md)

# [Ресурсы](resources.md)
## [Встроенные ресурсы](builtInResource.md)
### [Ресурс Archive](archiveResource.md)
### [Ресурс Environment](environmentResource.md)
### [Ресурс File](fileResource.md)
### [Ресурс Group](groupResource.md)
### [Ресурс Log](logResource.md)
### [Ресурс Package](packageResource.md)
### [Ресурс Registry](registryResource.md)
### [Ресурс Script](scriptResource.md)
### [Ресурс Service](serviceResource.md)
### [Ресурс пользователя](userResource.md)
### [Ресурс WindowsFeature](windowsfeatureResource.md)
### [Ресурс WindowsProcess](windowsProcessResource.md)
## [Создание пользовательских ресурсов](authoringResource.md) 
### [Настраиваемые ресурсы на основе MOF-файла](authoringResourceMOF.md)
#### [Ресурс на основе MOF-файла в C#](authoringResourceMofCS.md)
### [Настраиваемые ресурсы на основе классов](authoringResourceClass.md)
### [Составные ресурсы](authoringResourceComposite.md)
### [Запись ресурса DSC с одним экземпляром (рекомендуется)](singleInstance.md)
### [Контрольный список для создания ресурсов](resourceAuthoringChecklist.md)
## [Отладка ресурсов DSC](debugResource.md)
## [Прямой вызов методов ресурсов DSC](directCallResource.md)

# [Настройка локального диспетчера конфигураций (LCM)](metaConfig.md)
## [Настройка LCM в PowerShell 4.0](metaConfig4.md)

# Модель опроса DSC
## [Настройка опрашивающего веб-сервера](pullServer.md)
## [Настройка опрашивающего SMB-сервера DSC](pullServerSMB.md)
## [Настройка опрашивающего клиента](pullClient.md)
### [Настройка опрашивающего клиента с помощью имен конфигураций](pullClientConfigNames.md)
### [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md)
## [Использование сервера отчетов DSC](reportServer.md)
## [Рекомендации по опрашивающим серверам](secureServer.md)

# [Устранение неполадок в DSC](troubleshooting.md)

# [Использование DSC на сервере Nano Server](nanoDsc.md)

# DSC в Linux
## [Начало работы с DSC в Linux](lnxGettingStarted.md)
## [Встроенные ресурсы для Linux](lnxBuiltInResources.md)
### [Ресурс nxArchive](lnxArchiveResource.md)
### [Ресурс nxEnvironment](lnxEnvironmentResource.md)
### [Ресурс nxFile](lnxFileResource.md)
### [Ресурс nxFileLine](lnxFileLineResource.md)
### [Ресурс nxGroup](lnxGroupResource.md)
### [Ресурс nxPackage](lnxPackageResource.md)
### [Ресурс nxService](lnxServiceResource.md)
### [Ресурс nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md)
### [Ресурс nxUser](lnxUserResource.md)

# Справочник по MOF-файлам DSC
## [Класс MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager.md)
### [Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-applyconfiguration.md)
### [Метод DisableDebugConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)
### [Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)
### [Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfiguration.md)
### [Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)
### [Метод GetConfigurationStatus класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)
### [Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)
### [Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)
### [Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-removeconfiguration.md)
### [Метод ResourceGet класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourceget.md)
### [Метод ResourceSet класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourceset.md)
### [Метод ResourceTest класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-resourcetest.md)
### [Метод RollBack класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-rollback.md)
### [Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfiguration.md)
### [Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)
### [Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)
### [Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)
### [Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-stopconfiguration.md)
### [Метод TestConfiguration класса MSFT_DSCLocalConfigurationManager](msft-dsclocalconfigurationmanager-testconfiguration.md)

# Дополнительные ресурсы
## [Технические документы](whitepapers.md)



<!--HONumber=Jun16_HO4-->


