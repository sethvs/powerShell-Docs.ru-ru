---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Создание конвейера непрерывной интеграции и непрерывного развертывания с помощью DSC"
ms.openlocfilehash: 6d21faef6e58068456c6c454b4d50b7a9415850b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="building-a-continuous-integration-and-continuous-deplyoment-pipeline-with-dsc"></a><span data-ttu-id="ba1ad-103">Создание конвейера непрерывной интеграции и непрерывного развертывания с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="ba1ad-103">Building a Continuous Integration and Continuous Deplyoment pipeline with DSC</span></span>

<span data-ttu-id="ba1ad-104">В этом примере показано, как создать конвейер непрерывной интеграции и непрерывного развертывания с помощью PowerShell, DSC, Pester и Visual Studio Team Foundation Server.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="ba1ad-105">После создания и настройки конвейера его можно использовать для полного развертывания, настройки и проверки DNS-сервера и связанных записей узла.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span> <span data-ttu-id="ba1ad-106">Этот процесс имитирует первую часть конвейера, которая будет использоваться в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="ba1ad-107">Автоматический конвейер непрерывной интеграции и развертывания помогает быстро и надежно обновлять программное обеспечение, следя за тем, чтоб весь код проверялся и чтобы текущая сборка была доступна в любое время.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba1ad-108">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="ba1ad-108">Prerequisites</span></span>

<span data-ttu-id="ba1ad-109">Чтобы использовать этот пример, следует ознакомиться со следующим:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="ba1ad-110">Основные понятия непрерывной интеграции и развертывания.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-110">CI-CD concepts.</span></span> <span data-ttu-id="ba1ad-111">Хороший справочник можно найти в документе [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf) (Модель конвейера выпуска).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="ba1ad-112">Система управления версиями [Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="ba1ad-113">Платформа тестирования [Pester](https://github.com/pester/Pester).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- <span data-ttu-id="ba1ad-114">[Team Foundation Server](https://www.visualstudio.com/tfs/).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-114">[Team Foundation Server](https://www.visualstudio.com/tfs/)</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="ba1ad-115">Что вам понадобится</span><span class="sxs-lookup"><span data-stu-id="ba1ad-115">What you will need</span></span>

<span data-ttu-id="ba1ad-116">Чтобы собрать и запустить этот пример, необходима среда из нескольких компьютеров или виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="ba1ad-117">клиент</span><span class="sxs-lookup"><span data-stu-id="ba1ad-117">Client</span></span>

<span data-ttu-id="ba1ad-118">Это компьютер, на котором вы будете выполнять всю работу по настройке и запуску примера.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="ba1ad-119">Это должен быть компьютер Windows, на котором установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-119">The client computer must be a Windows computer with the following installed:</span></span>
- <span data-ttu-id="ba1ad-120">[Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-120">[Git](https://git-scm.com/)</span></span>
- <span data-ttu-id="ba1ad-121">Локальный репозиторий Git, клонированный из https://github.com/PowerShell/Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="ba1ad-122">Текстовый редактор, такой как [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="ba1ad-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="ba1ad-123">TFSSrv1</span></span>

<span data-ttu-id="ba1ad-124">Компьютер, на котором размещен сервер TFS и где определяется сборка и выпуск.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="ba1ad-125">На этом компьютере должен быть установлен [Team Foundation Server 2017](https://www.visualstudio.com/tfs/).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="ba1ad-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="ba1ad-126">BuildAgent</span></span>

<span data-ttu-id="ba1ad-127">Компьютер, на котором запущен агент сборки Windows, создающий проект.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="ba1ad-128">На этом компьютере должен быть установлен и запущен агент сборки Windows.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="ba1ad-129">Дополнительные сведения о том, как устанавливать и запускать агент сборки Windows, см. в статье [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) (Развертывание агента в Windows).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-129">See [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="ba1ad-130">Кроме того, необходимо установить модули DSC `xDnsServer` и `xNetworking` на этом компьютере.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="ba1ad-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="ba1ad-131">TestAgent1</span></span>

<span data-ttu-id="ba1ad-132">В этом примере это компьютер, настроенный как DNS-сервер с помощью конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="ba1ad-133">На компьютере должен быть запущен [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="ba1ad-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="ba1ad-134">TestAgent2</span></span>

<span data-ttu-id="ba1ad-135">Это компьютер, на котором размещается веб-сайт, настраиваемый в этом примере.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="ba1ad-136">На компьютере должен быть запущен [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span> 

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="ba1ad-137">Добавление кода в TFS</span><span class="sxs-lookup"><span data-stu-id="ba1ad-137">Add the code to TFS</span></span>

<span data-ttu-id="ba1ad-138">Начнем с создания репозитория Git в TFS и импорта кода из локального репозитория на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="ba1ad-139">Если вы еще не клонировали репозиторий Demo_CI на клиентский компьютер, сделайте это сейчас, выполнив следующую команду Git:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="ba1ad-140">На клиентском компьютере перейдите к серверу TFS в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="ba1ad-141">На сервере TFS [создайте командный проект](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) с именем Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-141">In TFS, [Create a new team project](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) named Demo_CI.</span></span>

    <span data-ttu-id="ba1ad-142">Убедитесь, что для **управления версиями** задано значение **Git**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="ba1ad-143">На клиентском компьютере сделайте удаленным репозиторий, созданный в TFS, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

    `git remote add tfs <YourTFSRepoURL>`

    <span data-ttu-id="ba1ad-144">Где `<YourTFSRepoURL>` — это URL-адрес клона репозитория TFS, созданного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

    <span data-ttu-id="ba1ad-145">Если вы не знаете, где можно найти этот URL-адрес, см. в статье [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone) (Клонирование имеющегося репозитория Git).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-145">If you don't know where to find this URL, see [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span></span>
1. <span data-ttu-id="ba1ad-146">Отправьте код из локального репозитория в репозиторий TFS с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

    `git push tfs --all`
1. <span data-ttu-id="ba1ad-147">Репозиторий TFS будет заполнен кодом из Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-147">The TFS repository will be populated with the Demo_CI code.</span></span>

><span data-ttu-id="ba1ad-148">**Примечание.** В этом примере используется код ветви `ci-cd-example` из репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-148">**Note:** This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
><span data-ttu-id="ba1ad-149">Задайте эту ветвь как ветвь по умолчанию в проекте TFS и для создаваемых триггеров непрерывной интеграции и развертывания.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="ba1ad-150">Общие сведения о коде</span><span class="sxs-lookup"><span data-stu-id="ba1ad-150">Understanding the code</span></span>

<span data-ttu-id="ba1ad-151">Прежде чем создать сборку и конвейеры развертывания, давайте взглянем на часть кода, чтобы понять, что происходит.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="ba1ad-152">На клиентском компьютере откройте любой удобный текстовый редактор и перейдите в корневую папку своего репозитория Git Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="ba1ad-153">Конфигурация DSC</span><span class="sxs-lookup"><span data-stu-id="ba1ad-153">The DSC configuration</span></span>

<span data-ttu-id="ba1ad-154">Откройте файл `DNSServer.ps1` (из корня локального репозитория Demo_CI, `./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="ba1ad-155">Этот файл содержит конфигурации DSC, которые настраивают DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="ba1ad-156">Ниже они приведены в полном объеме:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-156">Here it is in its entirety:</span></span>

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

<span data-ttu-id="ba1ad-157">Обратите внимание на инструкцию `Node`:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="ba1ad-158">Она находит все узлы, определенные как имеющие роль `DNSServer` в [данных конфигурации](configData.md), которые создаются с помощью скрипта `DevEnv.ps1`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="ba1ad-159">При выполнении непрерывной интеграции важно использовать данные конфигурации для определения узлов, так как сведения об узле, скорее всего, изменятся между средами. Использование данных конфигурации позволит вам легко вносить изменения в сведения об узле без изменения кода конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-159">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="ba1ad-160">В первом блоке ресурсов конфигурация вызывает [WindowsFeature](windowsFeatureResource.md), чтобы убедиться, что функция DNS включена.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-160">In the first resource block, the configuration calls the [WindowsFeature](windowsFeatureResource.md) to ensure that the DNS feature is enabled.</span></span> <span data-ttu-id="ba1ad-161">Следующие блоки ресурсов вызывают ресурсы из модуля [xDnsServer ](https://github.com/PowerShell/xDnsServer), чтобы настроить основную зону и записи DNS.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-161">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="ba1ad-162">Обратите внимание, что два блока `xDnsRecord` упаковываются в циклы `foreach`, которые проходят через массивы данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-162">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="ba1ad-163">При этом данные конфигурации создаются скриптом `DevEnv.ps1`, который мы рассмотрим далее.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-163">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="ba1ad-164">Данные конфигурации</span><span class="sxs-lookup"><span data-stu-id="ba1ad-164">Configuration data</span></span>

<span data-ttu-id="ba1ad-165">Файл `DevEnv.ps1` (из корня локального репозитория Demo_CI, `./InfraDNS/DevEnv.ps1`) указывает данные конфигурации среды в хэш-таблице, а затем передает эту хэш-таблицу вызову к функции `New-DscConfigurationDataDocument`, которая определяется в `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-165">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="ba1ad-166">Файл `DevEnv.ps1`:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-166">The `DevEnv.ps1` file:</span></span>

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

<span data-ttu-id="ba1ad-167">Функция `New-DscConfigurationDataDocument` (определяется в `\Assets\DscPipelineTools\DscPipelineTools.psm1`) программным образом создает документ данных конфигурации из хэш-таблицы (данные узла) и массива (данные, отличные от данных узла), которые передаются как параметры `RawEnvData` и `OtherEnvData`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-167">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="ba1ad-168">В нашем случае используется только параметр `RawEnvData`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-168">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="ba1ad-169">Скрипт сборки psake</span><span class="sxs-lookup"><span data-stu-id="ba1ad-169">The psake build script</span></span>

<span data-ttu-id="ba1ad-170">Скрипт сборки [psake](https://github.com/psake/psake), определенный в `Build.ps1` (из корня репозитория Demo_CI, `./InfraDNS/Build.ps1`), указывает задачи, которые являются частью сборки.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-170">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="ba1ad-171">Он также определяет, от каких задач зависят другие задачи.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-171">It also defines which other tasks each task depends on.</span></span> <span data-ttu-id="ba1ad-172">При вызове скрипт psake проверяет выполнение указанной задачи (или задачи с именем `Default`, если она не указана) и всех ее зависимостей (рекурсивно, т. е. выполняются зависимости зависимостей и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-172">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="ba1ad-173">В этом примере задача `Default` определяется как:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-173">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="ba1ad-174">В задаче `Default` нет самостоятельной реализации задачи, но есть зависимость от задачи `CompileConfigs`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-174">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="ba1ad-175">Полученная цепочка зависимостей обеспечивает выполнение всех задач в скрипте сборки.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-175">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="ba1ad-176">В этом примере скрипт psake вызывается путем вызова `Invoke-PSake` в файле `Initiate.ps1` (находится в корне репозитория Demo_CI):</span><span class="sxs-lookup"><span data-stu-id="ba1ad-176">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

<span data-ttu-id="ba1ad-177">При создании определения сборки для нашего примера в TFS мы предоставим наш файл скрипта psake в качестве параметра `fileName` для этого скрипта.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-177">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="ba1ad-178">Скрипт сборки определяет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-178">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="ba1ad-179">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="ba1ad-179">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="ba1ad-180">Выполняет файл `DevEnv.ps1`, создает конфигурационный файл данных.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-180">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="ba1ad-181">InstallModules</span><span class="sxs-lookup"><span data-stu-id="ba1ad-181">InstallModules</span></span>

<span data-ttu-id="ba1ad-182">Устанавливает модули, необходимые в конфигурации `DNSServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-182">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="ba1ad-183">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="ba1ad-183">ScriptAnalysis</span></span>

<span data-ttu-id="ba1ad-184">Вызывает [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-184">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="ba1ad-185">UnitTests</span><span class="sxs-lookup"><span data-stu-id="ba1ad-185">UnitTests</span></span>

<span data-ttu-id="ba1ad-186">Выполняет модульные тесты [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-186">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="ba1ad-187">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="ba1ad-187">CompileConfigs</span></span>

<span data-ttu-id="ba1ad-188">Компилирует конфигурацию (`DNSServer.ps1`) в файл типа MOF, используя данные конфигурации, созданные задачей `GenerateEnvironmentFiles`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-188">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="ba1ad-189">Clean</span><span class="sxs-lookup"><span data-stu-id="ba1ad-189">Clean</span></span>

<span data-ttu-id="ba1ad-190">Создает папки, используемые в примере, и удаляет все результаты тестирования, файлы данных конфигурации и модули из предыдущих выполнений.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-190">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="ba1ad-191">Развертывание скрипта psake</span><span class="sxs-lookup"><span data-stu-id="ba1ad-191">The psake deploy script</span></span>

<span data-ttu-id="ba1ad-192">Скрипт развертывания [psake](https://github.com/psake/psake), определяемый в `Deploy.ps1` (находится в корне репозитория Demo_CI, `./InfraDNS/Deploy.ps1`), указывает задачи, которые развертывают и запускают конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-192">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="ba1ad-193">`Deploy.ps1` определяет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-193">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="ba1ad-194">DeployModules</span><span class="sxs-lookup"><span data-stu-id="ba1ad-194">DeployModules</span></span>

<span data-ttu-id="ba1ad-195">Запускает сеанс PowerShell на `TestAgent1` и устанавливает модули, содержащие ресурсы DSC, которые необходимы для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-195">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="ba1ad-196">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="ba1ad-196">DeployConfigs</span></span>

<span data-ttu-id="ba1ad-197">Вызывает командлет [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) для выполнения конфигурации на `TestAgent1`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-197">Calls the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="ba1ad-198">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="ba1ad-198">IntegrationTests</span></span>

<span data-ttu-id="ba1ad-199">Выполняет интеграционные тесты [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-199">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="ba1ad-200">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="ba1ad-200">AcceptanceTests</span></span>

<span data-ttu-id="ba1ad-201">Выполняет приемочные тесты [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-201">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="ba1ad-202">Clean</span><span class="sxs-lookup"><span data-stu-id="ba1ad-202">Clean</span></span>

<span data-ttu-id="ba1ad-203">Удаляет все модули, установленные при предыдущих выполнениях, и проверяет существование папки с результатами теста.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-203">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="ba1ad-204">Скрипты тестирования</span><span class="sxs-lookup"><span data-stu-id="ba1ad-204">Test scripts</span></span>

<span data-ttu-id="ba1ad-205">Приемочные, интеграционные и модульные тесты определяются в скриптах в папке `Tests` (из корня репозитория Demo_CI, `./InfraDNS/Tests`), каждый в файлах с именем `DNSServer.tests.ps1` в соответствующих папках.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-205">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="ba1ad-206">Скрипты тестирования используют синтаксис [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-206">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="ba1ad-207">Модульные тесты</span><span class="sxs-lookup"><span data-stu-id="ba1ad-207">Unit tests</span></span>

<span data-ttu-id="ba1ad-208">Модульные тесты проверяют конфигурации DSC самостоятельно, чтобы убедиться, что конфигурации будут делать то, что ожидается при их запуске.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-208">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="ba1ad-209">Скрипт модульных тестов использует [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-209">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="ba1ad-210">Интеграционные тесты</span><span class="sxs-lookup"><span data-stu-id="ba1ad-210">Integration tests</span></span>

<span data-ttu-id="ba1ad-211">Интеграционные тесты проверяют конфигурацию системы, чтобы убедиться, что при интеграции с другими компонентами система настроена должным образом.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-211">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="ba1ad-212">Эти тесты выполняются на целевом узле после его настройки с помощью DSC.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-212">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="ba1ad-213">Скрипт интеграционного теста использует сочетание синтаксиса [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-213">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="ba1ad-214">Приемочные тесты</span><span class="sxs-lookup"><span data-stu-id="ba1ad-214">Acceptance tests</span></span>

<span data-ttu-id="ba1ad-215">Приемочные тесты проверяют систему, чтобы убедиться, что она правильно работает.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-215">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="ba1ad-216">Например, они проверяют, правильную ли информацию возвращает веб-страница при запросе.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-216">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="ba1ad-217">Эти тесты выполняются удаленно с целевого узла, чтобы протестировать реальные сценарии.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-217">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="ba1ad-218">Скрипт интеграционного теста использует сочетание синтаксиса [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-218">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="ba1ad-219">Определение сборки</span><span class="sxs-lookup"><span data-stu-id="ba1ad-219">Define the build</span></span>

<span data-ttu-id="ba1ad-220">Теперь, когда мы передали свой код в TFS и просмотрели, что он делает, определим нашу сборку.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-220">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="ba1ad-221">Здесь мы расскажем только о шагах сборки, которые вы добавите к ней.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-221">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="ba1ad-222">Инструкции о том, как создать определение сборки в TFS и поместить его в очередь, см. в [этой статье](https://www.visualstudio.com/en-us/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="ba1ad-222">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](https://www.visualstudio.com/en-us/docs/build/define/create).</span></span>

<span data-ttu-id="ba1ad-223">Создайте определение сборки (выберите шаблон **Пусто**) с именем InfraDNS.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-223">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="ba1ad-224">Добавьте следующие шаги к своему определению сборки:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-224">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="ba1ad-225">Сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-225">PowerShell Script</span></span>
- <span data-ttu-id="ba1ad-226">Публикация результатов тестирования.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-226">Publish Test Results</span></span>
- <span data-ttu-id="ba1ad-227">Копирование файлов.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-227">Copy Files</span></span>
- <span data-ttu-id="ba1ad-228">Публикация артефакта.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-228">Publish Artifact</span></span>

<span data-ttu-id="ba1ad-229">После добавления этих шагов сборки измените свойства каждого шага следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-229">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="ba1ad-230">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba1ad-230">PowerShell Script</span></span>

1. <span data-ttu-id="ba1ad-231">Задайте для свойства **Тип** значение `File Path`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-231">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="ba1ad-232">Задайте для свойства **Путь к скрипту** значение `initiate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-232">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="ba1ad-233">Добавьте параметр `-fileName build` к свойству **Аргументы**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-233">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="ba1ad-234">Этот шаг сборки запускает файл `initiate.ps1`, вызывающий скрипт сборки psake.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-234">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="ba1ad-235">Публикация результатов тестирования</span><span class="sxs-lookup"><span data-stu-id="ba1ad-235">Publish Test Results</span></span>

1. <span data-ttu-id="ba1ad-236">Задайте для свойства **Формат результатов теста** значение `NUnit`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-236">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="ba1ad-237">Задайте для свойства **Файлы результатов тестов** значение `InfraDNS/Tests/Results/*.xml`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-237">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="ba1ad-238">Задайте для свойства **Название тестового запуска** значение `Unit`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-238">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="ba1ad-239">Убедитесь, что выбраны **параметры управления** **Включен** и **Всегда запускать**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-239">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="ba1ad-240">На этом этапе сборки запускаются модульные тесты в скрипте Pester, рассмотренном ранее, и результаты сохраняются в папке `InfraDNS/Tests/Results/*.xml`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-240">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="ba1ad-241">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="ba1ad-241">Copy Files</span></span>

1. <span data-ttu-id="ba1ad-242">Добавьте следующие строки в раздел **Содержание**:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-242">Add each of the following lines to **Contents**:</span></span>

    ```
    initiate.ps1
    **\deploy.ps1
    **\Acceptance\**
    **\Integration\**
    ```

1. <span data-ttu-id="ba1ad-243">Задайте для параметра **TargetFolder** значение `$(BuildArtifactStagingDirectory)\`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-243">Set **TargetFolder** to `$(BuildArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="ba1ad-244">На этом шаге копируются сборка и скрипты тестирования в промежуточный каталог, чтобы их можно было опубликовать как артефакты сборки на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-244">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="ba1ad-245">Публикация артефакта</span><span class="sxs-lookup"><span data-stu-id="ba1ad-245">Publish Artifact</span></span>

1. <span data-ttu-id="ba1ad-246">Задайте для параметра **Путь к публикации** значение `$(Build.ArtifactStagingDirectory)\`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-246">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="ba1ad-247">Задайте для параметра **Имя артефакта** значение `Deploy`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-247">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="ba1ad-248">Задайте для параметра **Тип артефакта** значение `Server`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-248">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="ba1ad-249">Выберите `Enabled` в **параметрах управления**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-249">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="ba1ad-250">Включение непрерывной интеграции</span><span class="sxs-lookup"><span data-stu-id="ba1ad-250">Enable continuous integration</span></span>

<span data-ttu-id="ba1ad-251">Теперь мы создадим триггер, который активирует новую сборку проекта каждый раз, когда в ветке `ci-cd-example` репозитория Git отмечено изменение.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-251">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="ba1ad-252">В TFS откройте вкладку **Сборка и выпуск**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-252">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="ba1ad-253">Выберите определение сборки `DNS Infra` и щелкните **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-253">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="ba1ad-254">Откройте вкладку **Триггеры**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-254">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="ba1ad-255">Щелкните **Непрерывная интеграция (CI)** и в раскрывающемся списке ветви выберите `refs/heads/ci-cd-example`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-255">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="ba1ad-256">Щелкните **Сохранить**, а потом **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-256">Click **Save** and then **OK**</span></span>

<span data-ttu-id="ba1ad-257">Теперь любые изменения в репозитории Git TFS запускают автоматическую сборку.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-257">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="ba1ad-258">Создание определения выпуска</span><span class="sxs-lookup"><span data-stu-id="ba1ad-258">Create the release definition</span></span>

<span data-ttu-id="ba1ad-259">Создадим определение выпуска, чтобы проект развертывался в среду разработки с записью каждого кода после изменения.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-259">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="ba1ad-260">Для этого добавьте новые определения выпуска, связанные с созданным определением сборки `InfraDNS`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-260">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="ba1ad-261">Установите **непрерывное развертывание**, чтобы новый выпуск запускался при каждом завершении новой сборки</span><span class="sxs-lookup"><span data-stu-id="ba1ad-261">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="ba1ad-262">([How to: Work with release definitions ](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions) (Как работать с определениями выпуска)), и настройте его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-262">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="ba1ad-263">Добавьте следующие шаги к своему определению выпуска:</span><span class="sxs-lookup"><span data-stu-id="ba1ad-263">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="ba1ad-264">Сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-264">PowerShell Script</span></span>
- <span data-ttu-id="ba1ad-265">Публикация результатов тестирования.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-265">Publish Test Results</span></span>
- <span data-ttu-id="ba1ad-266">Публикация результатов тестирования.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-266">Publish Test Results</span></span>

<span data-ttu-id="ba1ad-267">Измените шаги следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-267">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="ba1ad-268">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba1ad-268">PowerShell Script</span></span>

1. <span data-ttu-id="ba1ad-269">Задайте для **пути к скрипту** значение `$(Build.DefinitionName)\Deploy\initiate.ps1"`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-269">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="ba1ad-270">Задайте для **аргументов** значение `-fileName Deploy`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-270">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="ba1ad-271">Первая публикация результатов тестирования</span><span class="sxs-lookup"><span data-stu-id="ba1ad-271">First Publish Test Results</span></span>

1. <span data-ttu-id="ba1ad-272">Выберите `NUnit` для поля **Формат результатов теста**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-272">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="ba1ad-273">Задайте в качестве **файлов результатов тестов** значение `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-273">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="ba1ad-274">Задайте в качестве **название тестового запуска** значение `Integration`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-274">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="ba1ad-275">В разделе **Параметры управления** установите параметр **Всегда запускать**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-275">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="ba1ad-276">Вторая публикация результатов тестирования</span><span class="sxs-lookup"><span data-stu-id="ba1ad-276">Second Publish Test Results</span></span>

1. <span data-ttu-id="ba1ad-277">Выберите `NUnit` для поля **Формат результатов теста**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-277">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="ba1ad-278">Задайте в качестве **файлов результатов тестов** значение `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-278">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="ba1ad-279">Задайте в качестве **название тестового запуска** значение `Acceptance`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-279">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="ba1ad-280">В разделе **Параметры управления** установите параметр **Всегда запускать**.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-280">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="ba1ad-281">Проверка результатов</span><span class="sxs-lookup"><span data-stu-id="ba1ad-281">Verify your results</span></span>

<span data-ttu-id="ba1ad-282">Теперь всякий раз, когда вы вносите изменения в ветку `ci-cd-example` ​​в TFS, запускается новая сборка.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-282">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="ba1ad-283">Если создание сборки успешно, запускается новое развертывание.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-283">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="ba1ad-284">Результаты развертывания можно проверить, открыв браузер на клиентском компьютере и перейдя на сайт `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-284">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba1ad-285">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba1ad-285">Next steps</span></span>

<span data-ttu-id="ba1ad-286">В этом примере настраивается DNS-сервер `TestAgent1`, чтобы URL-адрес `www.contoso.com` разрешался в `TestAgent2`, но на самом деле веб-сайт не развертывается.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-286">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="ba1ad-287">Структура для этого предоставляется в репозитории в папке `WebApp`.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-287">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="ba1ad-288">Заглушки для создания скриптов psake, тестов Pester и конфигурации DSC можно использовать для развертывания собственных веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="ba1ad-288">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>







