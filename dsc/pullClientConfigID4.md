---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0"
ms.openlocfilehash: 19328018d276cddd0877869b0ec69c14c51e4b85
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a><span data-ttu-id="f4807-103">Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="f4807-103">Setting up a pull client using configuration ID in PowerShell 4.0</span></span>

><span data-ttu-id="f4807-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f4807-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f4807-105">Для каждого целевого узла нужно задать использование опрашивающего режима и URL-адреса, по которому можно подключиться к опрашивающему серверу для получения конфигураций.</span><span class="sxs-lookup"><span data-stu-id="f4807-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="f4807-106">Для этого потребуется настроить локальный диспетчер конфигураций (LCM), указав обязательную информацию.</span><span class="sxs-lookup"><span data-stu-id="f4807-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="f4807-107">Чтобы настроить LCM, создайте специальный тип конфигурации, известный как "метаконфигурация".</span><span class="sxs-lookup"><span data-stu-id="f4807-107">To configure the LCM, you create a special type of configuration known as a "metaconfiguration".</span></span> <span data-ttu-id="f4807-108">Дополнительные сведения о настройке LCM см. в разделе [Локальный диспетчер конфигураций для службы настройки требуемого состояния Windows PowerShell 4.0](metaConfig4.md)</span><span class="sxs-lookup"><span data-stu-id="f4807-108">For more information about configuring the LCM, see [Windows PowerShell 4.0 Desired State Configuration Local Configuration Manager](metaConfig4.md)</span></span>

<span data-ttu-id="f4807-109">Следующий сценарий настраивает LCM для опроса конфигураций с сервера с именем "PullServer".</span><span class="sxs-lookup"><span data-stu-id="f4807-109">The following script configures the LCM to pull configurations from a server named "PullServer":</span></span>

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

<span data-ttu-id="f4807-110">В сценарии **DownloadManagerCustomData** передает URL-адрес опрашивающего сервера и (в этом примере) разрешает небезопасное подключение.</span><span class="sxs-lookup"><span data-stu-id="f4807-110">In the script, **DownloadManagerCustomData** passes the URL of the pull server and (for this example) allows an unsecured connection.</span></span> 

<span data-ttu-id="f4807-111">После запуска этого сценария будет создана новая выходная папка **SimpleMetaConfigurationForPull**, в которую будет помещен MOF-файл метаконфигурации.</span><span class="sxs-lookup"><span data-stu-id="f4807-111">After this script runs, it creates a new output folder called **SimpleMetaConfigurationForPull** and puts a metaconfiguration MOF file there.</span></span>

<span data-ttu-id="f4807-112">Для применения конфигурации используйте **Set-DscLocalConfigurationManager** с параметрами **ComputerName** (используйте localhost) и **Path** (путь к расположению файла localhost.meta.mof на целевом узле).</span><span class="sxs-lookup"><span data-stu-id="f4807-112">To apply the configuration, use **Set-DscLocalConfigurationManager** with parameters for **ComputerName** (use “localhost”) and **Path** (the path to the location of the target node’s localhost.meta.mof file).</span></span> <span data-ttu-id="f4807-113">Например:</span><span class="sxs-lookup"><span data-stu-id="f4807-113">For example:</span></span> 
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="f4807-114">Идентификатор конфигурации</span><span class="sxs-lookup"><span data-stu-id="f4807-114">Configuration ID</span></span>
<span data-ttu-id="f4807-115">Сценарий заносит в свойство **ConfigurationID** LCM значение GUID, которое было создано специально для этой цели (создать GUID можно, используя командлет **New-Guid**).</span><span class="sxs-lookup"><span data-stu-id="f4807-115">The script sets the **ConfigurationID** property of the LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="f4807-116">Идентификатор **ConfigurationID** — это то, что LCM использует для поиска соответствующей конфигурации на опрашивающем сервере.</span><span class="sxs-lookup"><span data-stu-id="f4807-116">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="f4807-117">MOF-файл конфигурации на опрашивающем сервере должен иметь имя `ConfigurationID.mof`, где *ConfigurationID* является значением свойства **ConfigurationID** LCM целевого узла.</span><span class="sxs-lookup"><span data-stu-id="f4807-117">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="pulling-from-an-smb-server"></a><span data-ttu-id="f4807-118">Опрос с SMB-сервера</span><span class="sxs-lookup"><span data-stu-id="f4807-118">Pulling from an SMB server</span></span>

<span data-ttu-id="f4807-119">Если опрашивающий сервер настроен как файловый ресурс SMB, а не веб-служба, укажите **DscFileDownloadManager** вместо **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="f4807-119">If the pull server is set up as an SMB file share, rather than a web service, you specify the **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span>
<span data-ttu-id="f4807-120">**DscFileDownloadManager** принимает свойство **SourcePath** вместо **ServerUrl**.</span><span class="sxs-lookup"><span data-stu-id="f4807-120">The **DscFileDownloadManager** takes a **SourcePath** property instead of **ServerUrl**.</span></span> <span data-ttu-id="f4807-121">Следующий сценарий настраивает LCM для опроса конфигураций из общего ресурса SMB "SmbDscShare" на сервере "CONTOSO-SERVER".</span><span class="sxs-lookup"><span data-stu-id="f4807-121">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER":</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f4807-122">См. также</span><span class="sxs-lookup"><span data-stu-id="f4807-122">See Also</span></span>

- [<span data-ttu-id="f4807-123">Настройка опрашивающего веб-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="f4807-123">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="f4807-124">Настройка опрашивающего SMB-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="f4807-124">Setting up a DSC SMB pull server</span></span>](pullServerSMB.md)

