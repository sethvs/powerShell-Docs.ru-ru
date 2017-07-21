---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка опрашивающего клиента с помощью идентификатора конфигурации"
ms.openlocfilehash: 5ab57ae908ada102b0d57971542eff09d102fb8f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a><span data-ttu-id="6802a-103">Настройка опрашивающего клиента с помощью идентификатора конфигурации</span><span class="sxs-lookup"><span data-stu-id="6802a-103">Setting up a pull client using configuration ID</span></span>

> <span data-ttu-id="6802a-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6802a-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="6802a-105">Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций.</span><span class="sxs-lookup"><span data-stu-id="6802a-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="6802a-106">Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию.</span><span class="sxs-lookup"><span data-stu-id="6802a-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="6802a-107">Чтобы настроить LCM, создайте специальный тип конфигурации, помеченный с помощью атрибута **DSCLocalConfigurationManager**.</span><span class="sxs-lookup"><span data-stu-id="6802a-107">To configure the LCM, you create a special type of configuration, derated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="6802a-108">Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="6802a-108">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="6802a-109">**Примечание**. Этот раздел относится к PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="6802a-109">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="6802a-110">Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="6802a-110">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="6802a-111">Следующий сценарий настраивает LCM для опроса конфигураций с сервера CONTOSO-PullSrv.</span><span class="sxs-lookup"><span data-stu-id="6802a-111">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

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

<span data-ttu-id="6802a-112">В сценарии блок **ConfigurationRepositoryWeb** задает опрашивающий сервер.</span><span class="sxs-lookup"><span data-stu-id="6802a-112">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="6802a-113">**ServerURL**</span><span class="sxs-lookup"><span data-stu-id="6802a-113">The **ServerURL**</span></span>

<span data-ttu-id="6802a-114">После запуска этого сценария будет создана новая выходная папка **PullClientConfigID**, в которую будет помещен MOF-файл метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="6802a-114">After this script runs, it creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="6802a-115">В этом случае MOF-файл метаконфигурации будет называться `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="6802a-115">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="6802a-116">Чтобы применить конфигурацию, вызовите командлет **Set-DscLocalConfigurationManager**, в параметре **Path** которого задано расположение MOF-файла метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="6802a-116">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="6802a-117">Пример: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span><span class="sxs-lookup"><span data-stu-id="6802a-117">For example: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span></span>

## <a name="configuration-id"></a><span data-ttu-id="6802a-118">Идентификатор конфигурации</span><span class="sxs-lookup"><span data-stu-id="6802a-118">Configuration ID</span></span>

<span data-ttu-id="6802a-119">Сценарий задает для свойства **ConfigurationID** LCM значение GUID, созданное специально для этой цели (вы можете создать GUID, используя командлет **New-Guid**).</span><span class="sxs-lookup"><span data-stu-id="6802a-119">The script sets the **ConfigurationID** property of LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="6802a-120">Идентификатор **ConfigurationID** — это то, что LCM использует для поиска соответствующей конфигурации на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="6802a-120">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="6802a-121">MOF-файл конфигурации на опрашивающем сервере должен быть назван _ConfigurationID_.mof, где _ConfigurationID_ является значением свойства **ConfigurationID** LCM целевого узла.</span><span class="sxs-lookup"><span data-stu-id="6802a-121">The configuration MOF file on the pull server must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="smb-pull-server"></a><span data-ttu-id="6802a-122">Опрашивающий SMB-сервер</span><span class="sxs-lookup"><span data-stu-id="6802a-122">SMB pull server</span></span>

<span data-ttu-id="6802a-123">Чтобы настроить на клиенте опрос конфигураций с SMB-сервера, используйте блок **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="6802a-123">To set up a client to pull configurations from an SMB server, use a **ConfigurationRepositoryShare** block.</span></span> <span data-ttu-id="6802a-124">В блоке **ConfigurationRepositoryShare** укажите путь к серверу, задав свойство **SourcePath**.</span><span class="sxs-lookup"><span data-stu-id="6802a-124">In a **ConfigurationRepositoryShare** block, you specify the path to the server by setting the **SourcePath** property.</span></span> <span data-ttu-id="6802a-125">Следующая метаконфигурация настраивает на целевом узле опрос с опрашивающего SMB-сервера **SMBPullServer**.</span><span class="sxs-lookup"><span data-stu-id="6802a-125">The following metaconfiguration configures the target node to pull from an SMB pull server named **SMBPullServer**.</span></span>

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

## <a name="resource-and-report-servers"></a><span data-ttu-id="6802a-126">Серверы ресурсов и отчетов</span><span class="sxs-lookup"><span data-stu-id="6802a-126">Resource and report servers</span></span>

<span data-ttu-id="6802a-127">Если указать только блок **ConfigurationRepositoryWeb** или **ConfigurationRepositoryShare** в конфигурации LCM (как в предыдущем примере), опрашивающий клиент будет получать ресурсы с указанного сервера, но не будет отправлять отчеты на этот сервер.</span><span class="sxs-lookup"><span data-stu-id="6802a-127">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span> <span data-ttu-id="6802a-128">Можно использовать один и тот же опрашивающий сервер для конфигураций, ресурсов и создания отчетов, но необходимо создать блок **ReportRepositoryWeb** для настройки отчетов.</span><span class="sxs-lookup"><span data-stu-id="6802a-128">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span> 

<span data-ttu-id="6802a-129">В следующем примере показана метаконфигурация, которая настраивает клиент для опроса конфигураций и ресурсов и отправки данных отчетов на одном опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="6802a-129">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="6802a-130">При этом можно указать различные опрашивающие серверы для ресурсов и отчетов.</span><span class="sxs-lookup"><span data-stu-id="6802a-130">You can also specify different pull servers for resources and reporting.</span></span> <span data-ttu-id="6802a-131">Чтобы указать сервер ресурсов, используйте **ResourceRepositoryWeb** (для опрашивающего веб-сервера) или блок **ResourceRepositoryShare** (для опрашивающего SMB-сервера).</span><span class="sxs-lookup"><span data-stu-id="6802a-131">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="6802a-132">Чтобы указать сервер отчетов, используйте блок **ReportRepositoryWeb**.</span><span class="sxs-lookup"><span data-stu-id="6802a-132">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="6802a-133">Сервер отчетов не может быть SMB-сервером.</span><span class="sxs-lookup"><span data-stu-id="6802a-133">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="6802a-134">Следующая метаконфигурация настраивает опрашивающий клиент для получения конфигураций из **CONTOSO-PullSrv** и ресурсов из **CONTOSO-ResourceSrv**, а также для отправки отчетов о состоянии на **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="6802a-134">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="6802a-135">См. также</span><span class="sxs-lookup"><span data-stu-id="6802a-135">See Also</span></span>

* [<span data-ttu-id="6802a-136">Настройка опрашивающего клиента с именами конфигураций</span><span class="sxs-lookup"><span data-stu-id="6802a-136">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)

