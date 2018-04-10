---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Настройка опрашивающего клиента с помощью имен конфигураций
ms.openlocfilehash: dd0526b118b404854b1e9b445ca50bdaafdd01c7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a><span data-ttu-id="f55b1-103">Настройка опрашивающего клиента с помощью имен конфигураций</span><span class="sxs-lookup"><span data-stu-id="f55b1-103">Setting up a pull client using configuration names</span></span>

> <span data-ttu-id="f55b1-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f55b1-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="f55b1-105">Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций.</span><span class="sxs-lookup"><span data-stu-id="f55b1-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span>
<span data-ttu-id="f55b1-106">Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию.</span><span class="sxs-lookup"><span data-stu-id="f55b1-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span>
<span data-ttu-id="f55b1-107">Чтобы настроить LCM, создайте специальный тип конфигурации, помеченный атрибутом **DSCLocalConfigurationManager**.</span><span class="sxs-lookup"><span data-stu-id="f55b1-107">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span>
<span data-ttu-id="f55b1-108">Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="f55b1-108">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="f55b1-109">**Примечание**. Этот раздел относится к PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="f55b1-109">**Note**: This topic applies to PowerShell 5.0.</span></span>
<span data-ttu-id="f55b1-110">Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="f55b1-110">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="f55b1-111">Следующий сценарий настраивает LCM для получения конфигураций с сервера CONTOSO-PullSrv:</span><span class="sxs-lookup"><span data-stu-id="f55b1-111">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv":</span></span>

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

<span data-ttu-id="f55b1-112">В сценарии блок **ConfigurationRepositoryWeb** задает опрашивающий сервер.</span><span class="sxs-lookup"><span data-stu-id="f55b1-112">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span>
<span data-ttu-id="f55b1-113">Свойство **ServerURL** указывает конечную точку для опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="f55b1-113">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

<span data-ttu-id="f55b1-114">Свойство **RegistrationKey** является общим ключом между всеми узлами клиента для опрашивающего сервера и их опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="f55b1-114">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span>
<span data-ttu-id="f55b1-115">Те же значения хранятся в файле на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="f55b1-115">The same value is stored in a file on the pull server.</span></span>

<span data-ttu-id="f55b1-116">Свойство **ConfigurationNames** представляет собой массив, указывающий имена конфигураций, предназначенных для узла клиента.</span><span class="sxs-lookup"><span data-stu-id="f55b1-116">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
<span data-ttu-id="f55b1-117">На опрашивающем сервере необходимо назвать MOF-файл конфигурации для этого узла клиента *ConfigurationNames*.mof, где *ConfigurationNames* соответствует значению свойства **ConfigurationNames**, заданному в этой метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="f55b1-117">On the pull server, the configuration MOF file for this client node must be named *ConfigurationNames*.mof, where *ConfigurationNames* matches the value of the **ConfigurationNames** property you set in this metaconfiguration.</span></span>

><span data-ttu-id="f55b1-118">**Примечание.** Если для параметра **ConfigurationNames** указано больше одного значения, в конфигурации необходимо также указать блоки **PartialConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="f55b1-118">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
<span data-ttu-id="f55b1-119">Сведения о частичных конфигурациях см. в статье [Частичные конфигурации службы настройки требуемого состояния PowerShell](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="f55b1-119">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

<span data-ttu-id="f55b1-120">После запуска этого скрипта будет создана новая выходная папка **PullClientConfigNames**, в которую будет помещен MOF-файл метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="f55b1-120">After this script runs, it creates a new output folder named **PullClientConfigNames** and puts a metaconfiguration MOF file there.</span></span>
<span data-ttu-id="f55b1-121">В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="f55b1-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="f55b1-122">Чтобы применить конфигурацию, вызовите командлет **Set-DscLocalConfigurationManager**, в параметре **Path** которого задано расположение MOF-файла метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="f55b1-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span>

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> <span data-ttu-id="f55b1-123">**Примечание**. Ключи регистрации работают только с опрашивающими веб-серверами.</span><span class="sxs-lookup"><span data-stu-id="f55b1-123">**Note**: Registration keys work only with web pull servers.</span></span>
<span data-ttu-id="f55b1-124">Вам по-прежнему следует использовать **ConfigurationID** с опрашивающим SMB-сервером.</span><span class="sxs-lookup"><span data-stu-id="f55b1-124">You must still use **ConfigurationID** with an SMB pull server.</span></span>
<span data-ttu-id="f55b1-125">Сведения о настройке опрашивающего сервера с использованием **ConfigurationID** см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](PullClientConfigNames.md)</span><span class="sxs-lookup"><span data-stu-id="f55b1-125">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](PullClientConfigNames.md)</span></span>

## <a name="resource-and-report-servers"></a><span data-ttu-id="f55b1-126">Серверы ресурсов и отчетов</span><span class="sxs-lookup"><span data-stu-id="f55b1-126">Resource and report servers</span></span>

<span data-ttu-id="f55b1-127">Если указать только блок **ConfigurationRepositoryWeb** или **ConfigurationRepositoryShare** в конфигурации LCM (как в предыдущем примере), опрашивающий клиент будет получать ресурсы с указанного сервера, но не будет отправлять отчеты на этот сервер.</span><span class="sxs-lookup"><span data-stu-id="f55b1-127">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span>
<span data-ttu-id="f55b1-128">Можно использовать один и тот же опрашивающий сервер для конфигураций, ресурсов и создания отчетов, но необходимо создать блок **ReportRepositoryWeb** для настройки отчетов.</span><span class="sxs-lookup"><span data-stu-id="f55b1-128">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>
<span data-ttu-id="f55b1-129">В следующем примере показана метаконфигурация, которая настраивает клиент для опроса конфигураций и ресурсов и отправки данных отчетов на одном опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="f55b1-129">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="f55b1-130">При этом можно указать различные опрашивающие серверы для ресурсов и отчетов.</span><span class="sxs-lookup"><span data-stu-id="f55b1-130">You can also specify different pull servers for resources and reporting.</span></span>
<span data-ttu-id="f55b1-131">Чтобы указать сервер ресурсов, используйте **ResourceRepositoryWeb** (для опрашивающего веб-сервера) или блок **ResourceRepositoryShare** (для опрашивающего SMB-сервера).</span><span class="sxs-lookup"><span data-stu-id="f55b1-131">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="f55b1-132">Чтобы указать сервер отчетов, используйте блок **ReportRepositoryWeb**.</span><span class="sxs-lookup"><span data-stu-id="f55b1-132">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span>
<span data-ttu-id="f55b1-133">Сервер отчетов не может быть SMB-сервером.</span><span class="sxs-lookup"><span data-stu-id="f55b1-133">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="f55b1-134">Следующая метаконфигурация настраивает опрашивающий клиент для получения конфигураций из **CONTOSO-PullSrv** и ресурсов из **CONTOSO-ResourceSrv**, а также для отправки отчетов о состоянии на **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="f55b1-134">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f55b1-135">См. также</span><span class="sxs-lookup"><span data-stu-id="f55b1-135">See Also</span></span>

* [<span data-ttu-id="f55b1-136">Настройка опрашивающего клиента с идентификатором конфигурации</span><span class="sxs-lookup"><span data-stu-id="f55b1-136">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="f55b1-137">Настройка опрашивающего веб-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="f55b1-137">Setting up a DSC web pull server</span></span>](pullServer.md)