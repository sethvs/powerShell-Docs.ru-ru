---
ms.date: 2017-10-16
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Применение конфигураций"
ms.openlocfilehash: 4285dbe04c9745ec2a859e479848da2881c18de0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="enacting-configurations"></a><span data-ttu-id="967d8-103">Применение конфигураций</span><span class="sxs-lookup"><span data-stu-id="967d8-103">Enacting configurations</span></span>

><span data-ttu-id="967d8-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="967d8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="967d8-105">Настройку требуемого состояния PowerShell (DSC) можно применять двумя способами: в режиме принудительной отправки и в режиме опроса.</span><span class="sxs-lookup"><span data-stu-id="967d8-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="967d8-106">Режим принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="967d8-106">Push mode</span></span>

<span data-ttu-id="967d8-107">![Режим принудительной отправки](images/pushModel.png "Принципы работы")</span><span class="sxs-lookup"><span data-stu-id="967d8-107">![Push mode](images/pushModel.png "How push mode works")</span></span>

<span data-ttu-id="967d8-108">Режим принудительной отправки означает, что пользователь активно применяет конфигурацию к целевому узлу, вызывая командлет [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx).</span><span class="sxs-lookup"><span data-stu-id="967d8-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span>

<span data-ttu-id="967d8-109">Созданную и скомпилированную конфигурацию можно применить в режиме принудительной отправки, вызвав командлет [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) и указав в качестве значения параметра -Path для этого командлета путь к MOF-файлу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="967d8-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span>
<span data-ttu-id="967d8-110">Например, если MOF-файл конфигурации находится в каталоге `C:\DSC\Configurations\localhost.mof`, его можно применить на локальном компьютере, выполнив следующую команду: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="967d8-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="967d8-111">__Примечание__. По умолчанию DSC выполняет конфигурацию в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="967d8-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="967d8-112">Для интерактивного выполнения конфигурации вызовите командлет [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) с параметром __-wait__.</span><span class="sxs-lookup"><span data-stu-id="967d8-112">To run the configuration interactively, call the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) with the __-Wait__ parameter.</span></span>

## <a name="pull-mode"></a><span data-ttu-id="967d8-113">Режим опроса</span><span class="sxs-lookup"><span data-stu-id="967d8-113">Pull mode</span></span>

<span data-ttu-id="967d8-114">![Режим запросов](images/pullModel.png "Принципы работы")</span><span class="sxs-lookup"><span data-stu-id="967d8-114">![Pull Mode](images/pullModel.png "How pull mode works")</span></span>

<span data-ttu-id="967d8-115">В режиме опроса на опрашивающих клиентах настраивается получение конфигураций требуемого состояния из удаленной опрашивающей службы.</span><span class="sxs-lookup"><span data-stu-id="967d8-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull service.</span></span>
<span data-ttu-id="967d8-116">Опрашивающая служба при этом настраивается для размещения службы DSC. Затем производится подготовка с использованием конфигураций и ресурсов, которые требуются опрашивающим клиентам.</span><span class="sxs-lookup"><span data-stu-id="967d8-116">Likewise, the pull service has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span>
<span data-ttu-id="967d8-117">На каждом опрашивающем сервере задается расписание событий периодической проверки соответствия для конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="967d8-117">Each of the pull clients has a scheduled event that performs a periodic compliance check on the configuration of the node.</span></span>
<span data-ttu-id="967d8-118">При первой активации события локальный диспетчер конфигураций (LCM) на опрашивающем клиенте отправляет в опрашивающую службу запрос на получение конфигурации, указанной в LCM.</span><span class="sxs-lookup"><span data-stu-id="967d8-118">When the event is triggered the first time, the Local Configuration Manager (LCM) on the pull client makes a request to the pull service to get the configuration specified in the LCM.</span></span>
<span data-ttu-id="967d8-119">Если такая конфигурация в опрашивающей службе обнаруживается и проходит начальные проверки допустимости, она скачивается на опрашивающий клиент, где LCM ее выполняет.</span><span class="sxs-lookup"><span data-stu-id="967d8-119">If that configuration exists on the pull service, and it passes initial validation checks, the configuration is downloaded to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="967d8-120">LCM регулярно проверяет, соответствует ли клиент конфигурации, в интервалы, заданные свойством **ConfigurationModeFrequencyMins** LCM.</span><span class="sxs-lookup"><span data-stu-id="967d8-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span>
<span data-ttu-id="967d8-121">LCM регулярно проверяет наличие обновленных конфигураций в опрашивающей службе с интервалами, заданными свойством LCM **RefreshModeFrequency**.</span><span class="sxs-lookup"><span data-stu-id="967d8-121">The LCM checks for updated configurations on the pull service at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span>
<span data-ttu-id="967d8-122">Дополнительные сведения о настройке LCM см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="967d8-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

<span data-ttu-id="967d8-123">Рекомендуемое решение для размещения опрашивающей службы — облачная служба DSC, [служба автоматизации Azure](https://azure.microsoft.com/en-us/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="967d8-123">The recommended solution for hosting a Pull Service, is the DSC cloud service, [Azure Automation](https://azure.microsoft.com/en-us/services/automation/).</span></span>
<span data-ttu-id="967d8-124">Это размещенное решение, которое предоставляет возможности администрирования и создания отчетов с графическим представлением, а также централизованного управления.</span><span class="sxs-lookup"><span data-stu-id="967d8-124">This is hosted solution provides graphical management, reporting, and centralized administration.</span></span>

<span data-ttu-id="967d8-125">Дополнительные сведения о настройке опрашивающей службы в Windows Server см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="967d8-125">For more information on setting up a Pull Service on Windows Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>
<span data-ttu-id="967d8-126">Но помните, что функциональность этой реализации ограничена, и для интеграции требуются некоторые самостоятельные действия.</span><span class="sxs-lookup"><span data-stu-id="967d8-126">Understand however, that this implementation has limited features and does require some "do it yourself" integration.</span></span>

<span data-ttu-id="967d8-127">В следующих разделах описана опрашивающая служба и клиенты:</span><span class="sxs-lookup"><span data-stu-id="967d8-127">The following topics explain pull service and clients:</span></span>

- <span data-ttu-id="967d8-128">[Обзор DSC службы автоматизации Azure](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="967d8-128">[Azure Automation DSC Overview](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)</span></span>
- [<span data-ttu-id="967d8-129">Настройка опрашивающего SMB-сервера</span><span class="sxs-lookup"><span data-stu-id="967d8-129">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="967d8-130">Настройка опрашивающего клиента</span><span class="sxs-lookup"><span data-stu-id="967d8-130">Configuring a pull client</span></span>](pullClientConfigID.md)
