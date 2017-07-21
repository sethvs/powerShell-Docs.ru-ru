---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Применение конфигураций"
ms.openlocfilehash: db82788650186eb82f67b30b24cd45b719bbe314
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="enacting-configurations"></a><span data-ttu-id="40fbb-103">Применение конфигураций</span><span class="sxs-lookup"><span data-stu-id="40fbb-103">Enacting configurations</span></span>

><span data-ttu-id="40fbb-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="40fbb-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="40fbb-105">Настройку требуемого состояния PowerShell (DSC) можно применять двумя способами: в режиме принудительной отправки и в режиме опроса.</span><span class="sxs-lookup"><span data-stu-id="40fbb-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="40fbb-106">Режим принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="40fbb-106">Push mode</span></span>

<span data-ttu-id="40fbb-107">![Режим принудительной отправки](images/Push.png "Принципы работы")</span><span class="sxs-lookup"><span data-stu-id="40fbb-107">![Push mode](images/Push.png "How push mode works")</span></span>

<span data-ttu-id="40fbb-108">Режим принудительной отправки означает, что пользователь активно применяет конфигурацию к целевому узлу, вызывая командлет [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx).</span><span class="sxs-lookup"><span data-stu-id="40fbb-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span>

<span data-ttu-id="40fbb-109">Созданную и скомпилированную конфигурацию можно применить в режиме принудительной отправки, вызвав командлет [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) и указав в качестве значения параметра -Path для этого командлета путь к MOF-файлу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40fbb-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span> <span data-ttu-id="40fbb-110">Например, если MOF-файл конфигурации находится в каталоге `C:\DSC\Configurations\localhost.mof`, его можно применить на локальном компьютере, выполнив следующую команду: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="40fbb-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="40fbb-111">__Примечание__. По умолчанию DSC выполняет конфигурацию в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="40fbb-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="40fbb-112">Для интерактивного выполнения конфигурации вызовите командлет [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) с параметром __-wait__.</span><span class="sxs-lookup"><span data-stu-id="40fbb-112">To run the configuration interactively, call the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) with the __-Wait__ parameter.</span></span>


## <a name="pull-mode"></a><span data-ttu-id="40fbb-113">Режим опроса</span><span class="sxs-lookup"><span data-stu-id="40fbb-113">Pull mode</span></span>

<span data-ttu-id="40fbb-114">![Режим запросов](images/Pull.png "Принципы работы")</span><span class="sxs-lookup"><span data-stu-id="40fbb-114">![Pull Mode](images/Pull.png "How pull mode works")</span></span>

<span data-ttu-id="40fbb-115">В режиме опроса на опрашивающих клиентах настраивается получение конфигураций требуемого состояния с удаленного опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="40fbb-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull server.</span></span> <span data-ttu-id="40fbb-116">На опрашивающем сервере при этом настраивается размещение службы DSC и производится подготовка с использованием конфигураций и ресурсов, которые требуются опрашивающим клиентам.</span><span class="sxs-lookup"><span data-stu-id="40fbb-116">Likewise, the pull server has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span> <span data-ttu-id="40fbb-117">На каждом опрашивающем сервере задается расписание задачи периодической проверки соответствия для конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="40fbb-117">Each one of the pull clients has a scheduled task that performs a periodic compliance check on the configuration of the node.</span></span> <span data-ttu-id="40fbb-118">При первой активации события локальный диспетчер конфигураций (LCM) на опрашивающем клиенте делает запрос опрашивающего сервера, чтобы получить конфигурацию, указанную в LCM.</span><span class="sxs-lookup"><span data-stu-id="40fbb-118">When the event is triggered the first time, it the Local Configuration Manager (LCM) on the pull client makes a request to the pull server to get the configuration specified in the LCM.</span></span> <span data-ttu-id="40fbb-119">Если такая конфигурация на опрашивающем сервере есть и проходит начальные проверки допустимости, она передается на опрашивающий клиент, где LCM ее выполняет.</span><span class="sxs-lookup"><span data-stu-id="40fbb-119">If that configuration exists on the pull server, and it passes initial validation checks, the configuration is transmitted to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="40fbb-120">LCM регулярно проверяет, соответствует ли клиент конфигурации, в интервалы, заданные свойством **ConfigurationModeFrequencyMins** LCM.</span><span class="sxs-lookup"><span data-stu-id="40fbb-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="40fbb-121">LCM регулярно проверяет наличие обновленных конфигураций на опрашивающем сервере в интервалы, заданные свойством **RefreshModeFrequency** LCM.</span><span class="sxs-lookup"><span data-stu-id="40fbb-121">The LCM checks for updated configurations on the pull server at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span> <span data-ttu-id="40fbb-122">Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="40fbb-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

<span data-ttu-id="40fbb-123">Дополнительные сведения о настройке опрашивающего сервера DSC см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="40fbb-123">For more information on setting up a DSC Pull Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>

<span data-ttu-id="40fbb-124">Если вы предпочитаете использовать для размещения опрашивающего сервера веб-службу, обратитесь к [службе автоматизации Azure DSC](https://azure.microsoft.com/en-us/documentation/articles/automation-dsc-overview/).</span><span class="sxs-lookup"><span data-stu-id="40fbb-124">If you would prefer to take advantage of an online service to host Pull Server functionality, see the [Azure Automation DSC](https://azure.microsoft.com/en-us/documentation/articles/automation-dsc-overview/) service.</span></span>

<span data-ttu-id="40fbb-125">В следующих разделах показано, как настраивать опрашивающие серверы и клиенты:</span><span class="sxs-lookup"><span data-stu-id="40fbb-125">The following topics explain how to set up pull servers and clients:</span></span>

- [<span data-ttu-id="40fbb-126">Настройка опрашивающего веб-сервера</span><span class="sxs-lookup"><span data-stu-id="40fbb-126">Setting up a web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="40fbb-127">Настройка опрашивающего SMB-сервера</span><span class="sxs-lookup"><span data-stu-id="40fbb-127">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="40fbb-128">Настройка опрашивающего клиента</span><span class="sxs-lookup"><span data-stu-id="40fbb-128">Configuring a pull client</span></span>](pullClientConfigID.md)

