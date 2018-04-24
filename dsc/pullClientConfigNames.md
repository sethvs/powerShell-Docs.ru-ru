---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Настройка опрашивающего клиента с помощью имен конфигураций
ms.openlocfilehash: 7c8f204cc646e52ad5e953d6c7ad9e4e906d8a5b
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a>Настройка опрашивающего клиента с помощью имен конфигураций

> Область применения: Windows PowerShell 5.0

> [!IMPORTANT]
> Опрашивающий сервер (компонент Windows *служба DSC*) — поддерживаемый компонент Windows Server, но реализация новых функций и возможностей для него не планируется. Рекомендуется начать перенос управляемых клиентов на [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (включает возможности опрашивающего сервера в Windows Server) или на одно из решений сообщества, указанных [в следующем списке](pullserver.md#community-solutions-for-pull-service).

Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций.
Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию.
Чтобы настроить LCM, создайте специальный тип конфигурации, помеченный атрибутом **DSCLocalConfigurationManager**.
Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).

> **Примечание**. Этот раздел относится к PowerShell 5.0.
Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md)

Следующий сценарий настраивает LCM для получения конфигураций с сервера CONTOSO-PullSrv:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
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
PullClientConfigNames
```

В сценарии блок **ConfigurationRepositoryWeb** задает опрашивающий сервер.
Свойство **ServerURL** указывает конечную точку для опрашивающего сервера.

Свойство **RegistrationKey** является общим ключом между всеми узлами клиента для опрашивающего сервера и их опрашивающего сервера.
Те же значения хранятся в файле на опрашивающем сервере.

Свойство **ConfigurationNames** представляет собой массив, указывающий имена конфигураций, предназначенных для узла клиента.
На опрашивающем сервере необходимо назвать MOF-файл конфигурации для этого узла клиента *ConfigurationNames*.mof, где *ConfigurationNames* соответствует значению свойства **ConfigurationNames**, заданному в этой метаконфигурации.

>**Примечание.** Если для параметра **ConfigurationNames** указано больше одного значения, в конфигурации необходимо также указать блоки **PartialConfiguration**.
Сведения о частичных конфигурациях см. в статье [Частичные конфигурации службы настройки требуемого состояния PowerShell](partialConfigs.md).

После запуска этого скрипта будет создана новая выходная папка **PullClientConfigNames**, в которую будет помещен MOF-файл метаконфигурации.
В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.

Чтобы применить конфигурацию, вызовите командлет **Set-DscLocalConfigurationManager**, в параметре **Path** которого задано расположение MOF-файла метаконфигурации.

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> **Примечание**. Ключи регистрации работают только с опрашивающими веб-серверами.
Вам по-прежнему следует использовать **ConfigurationID** с опрашивающим SMB-сервером.
Сведения о настройке опрашивающего сервера с использованием **ConfigurationID** см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](PullClientConfigNames.md)

## <a name="resource-and-report-servers"></a>Серверы ресурсов и отчетов

Если указать только блок **ConfigurationRepositoryWeb** или **ConfigurationRepositoryShare** в конфигурации LCM (как в предыдущем примере), опрашивающий клиент будет получать ресурсы с указанного сервера, но не будет отправлять отчеты на этот сервер.
Можно использовать один и тот же опрашивающий сервер для конфигураций, ресурсов и создания отчетов, но необходимо создать блок **ReportRepositoryWeb** для настройки отчетов.
В следующем примере показана метаконфигурация, которая настраивает клиент для опроса конфигураций и ресурсов и отправки данных отчетов на одном опрашивающем сервере.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
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

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigNames
```

При этом можно указать различные опрашивающие серверы для ресурсов и отчетов.
Чтобы указать сервер ресурсов, используйте **ResourceRepositoryWeb** (для опрашивающего веб-сервера) или блок **ResourceRepositoryShare** (для опрашивающего SMB-сервера).
Чтобы указать сервер отчетов, используйте блок **ReportRepositoryWeb**.
Сервер отчетов не может быть SMB-сервером.
Следующая метаконфигурация настраивает опрашивающий клиент для получения конфигураций из **CONTOSO-PullSrv** и ресурсов из **CONTOSO-ResourceSrv**, а также для отправки отчетов о состоянии на **CONTOSO-ReportSrv**:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
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
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>См. также

* [Настройка опрашивающего клиента с идентификатором конфигурации](PullClientConfigNames.md)
* [Настройка опрашивающего веб-сервера DSC](pullServer.md)