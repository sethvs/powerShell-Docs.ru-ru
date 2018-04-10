---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0
ms.openlocfilehash: 7074d842b7b99ef3fb6498b6dbc1e561b14caf16
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a><span data-ttu-id="23bfe-103">Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="23bfe-103">Setting up a pull client using configuration ID in PowerShell 4.0</span></span>

><span data-ttu-id="23bfe-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="23bfe-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="23bfe-105">Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций.</span><span class="sxs-lookup"><span data-stu-id="23bfe-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="23bfe-106">Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию.</span><span class="sxs-lookup"><span data-stu-id="23bfe-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="23bfe-107">Чтобы настроить LCM, создайте специальный тип конфигурации, известный как "метаконфигурация".</span><span class="sxs-lookup"><span data-stu-id="23bfe-107">To configure the LCM, you create a special type of configuration known as a "metaconfiguration".</span></span> <span data-ttu-id="23bfe-108">Дополнительные сведения о настройке LCM см. в разделе [Локальный диспетчер конфигураций для службы настройки требуемого состояния Windows PowerShell 4.0](metaConfig4.md)</span><span class="sxs-lookup"><span data-stu-id="23bfe-108">For more information about configuring the LCM, see [Windows PowerShell 4.0 Desired State Configuration Local Configuration Manager](metaConfig4.md)</span></span>

<span data-ttu-id="23bfe-109">Следующий сценарий настраивает LCM для опроса конфигураций с сервера с именем "PullServer".</span><span class="sxs-lookup"><span data-stu-id="23bfe-109">The following script configures the LCM to pull configurations from a server named "PullServer":</span></span>

```powershell
Configuration SimpleMetaConfigurationForPull
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    }
}
SimpleMetaConfigurationForPull -Output "."
```

<span data-ttu-id="23bfe-110">В сценарии **DownloadManagerCustomData** передает URL-адрес опрашивающего сервера и (в этом примере) разрешает небезопасное подключение.</span><span class="sxs-lookup"><span data-stu-id="23bfe-110">In the script, **DownloadManagerCustomData** passes the URL of the pull server and (for this example) allows an unsecured connection.</span></span>

<span data-ttu-id="23bfe-111">После запуска этого сценария будет создана новая выходная папка **SimpleMetaConfigurationForPull**, в которую будет помещен MOF-файл метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="23bfe-111">After this script runs, it creates a new output folder called **SimpleMetaConfigurationForPull** and puts a metaconfiguration MOF file there.</span></span>

<span data-ttu-id="23bfe-112">Для применения конфигурации используйте **Set-DscLocalConfigurationManager** с параметрами **ComputerName** (используйте localhost) и **Path** (путь к расположению файла localhost.meta.mof на целевом узле).</span><span class="sxs-lookup"><span data-stu-id="23bfe-112">To apply the configuration, use **Set-DscLocalConfigurationManager** with parameters for **ComputerName** (use “localhost”) and **Path** (the path to the location of the target node’s localhost.meta.mof file).</span></span> <span data-ttu-id="23bfe-113">Например:</span><span class="sxs-lookup"><span data-stu-id="23bfe-113">For example:</span></span>
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="23bfe-114">Идентификатор конфигурации</span><span class="sxs-lookup"><span data-stu-id="23bfe-114">Configuration ID</span></span>
<span data-ttu-id="23bfe-115">Сценарий заносит в свойство **ConfigurationID** LCM значение GUID, которое было создано специально для этой цели (создать GUID можно, используя командлет **New-Guid**).</span><span class="sxs-lookup"><span data-stu-id="23bfe-115">The script sets the **ConfigurationID** property of the LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="23bfe-116">Идентификатор **ConfigurationID** — это то, что LCM использует для поиска соответствующей конфигурации на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="23bfe-116">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="23bfe-117">MOF-файл конфигурации на опрашивающем сервере должен иметь имя `ConfigurationID.mof`, где *ConfigurationID* является значением свойства **ConfigurationID** LCM целевого узла.</span><span class="sxs-lookup"><span data-stu-id="23bfe-117">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="pulling-from-an-smb-server"></a><span data-ttu-id="23bfe-118">Опрос с SMB-сервера</span><span class="sxs-lookup"><span data-stu-id="23bfe-118">Pulling from an SMB server</span></span>

<span data-ttu-id="23bfe-119">Если опрашивающий сервер настроен как файловый ресурс SMB, а не веб-служба, укажите **DscFileDownloadManager** вместо **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="23bfe-119">If the pull server is set up as an SMB file share, rather than a web service, you specify the **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span>
<span data-ttu-id="23bfe-120">**DscFileDownloadManager** принимает свойство **SourcePath** вместо **ServerUrl**.</span><span class="sxs-lookup"><span data-stu-id="23bfe-120">The **DscFileDownloadManager** takes a **SourcePath** property instead of **ServerUrl**.</span></span> <span data-ttu-id="23bfe-121">Следующий сценарий настраивает LCM для опроса конфигураций из общего ресурса SMB "SmbDscShare" на сервере "CONTOSO-SERVER".</span><span class="sxs-lookup"><span data-stu-id="23bfe-121">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER":</span></span>

```powershell
Configuration SimpleMetaConfigurationForPull
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    }
}
SimpleMetaConfigurationForPull -Output "."
```

## <a name="see-also"></a><span data-ttu-id="23bfe-122">См. также</span><span class="sxs-lookup"><span data-stu-id="23bfe-122">See Also</span></span>

- [<span data-ttu-id="23bfe-123">Настройка опрашивающего веб-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="23bfe-123">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="23bfe-124">Настройка опрашивающего SMB-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="23bfe-124">Setting up a DSC SMB pull server</span></span>](pullServerSMB.md)