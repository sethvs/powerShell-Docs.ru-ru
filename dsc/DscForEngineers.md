---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Общие сведения о настройке требуемого состояния Windows PowerShell для руководителей"
ms.openlocfilehash: 50aaa407e02b8466a7df909711454e88b07c5c1f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="50f6e-103">Общие сведения о настройке требуемого состояния Windows PowerShell для инженеров</span><span class="sxs-lookup"><span data-stu-id="50f6e-103">Desired State Configuration Overview for Engineers</span></span> #

<span data-ttu-id="50f6e-104">В этом документе, предназначенном для групп разработки и эксплуатации, описаны преимущества настройки требуемого состояния (DSC) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50f6e-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="50f6e-105">Обзор значения DSC с более высокой точки зрения см. в статье [Общие сведения о настройке требуемого состояния Windows PowerShell для руководителей](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="50f6e-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="50f6e-106">Преимущества настройки требуемого состояния</span><span class="sxs-lookup"><span data-stu-id="50f6e-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="50f6e-107">Настройка требуемого состояния обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="50f6e-107">DSC exists to:</span></span>
- <span data-ttu-id="50f6e-108">упрощение написания скриптов для Windows;</span><span class="sxs-lookup"><span data-stu-id="50f6e-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="50f6e-109">повышение скорости итерации.</span><span class="sxs-lookup"><span data-stu-id="50f6e-109">Increase the speed of iteration</span></span>

<span data-ttu-id="50f6e-110">Понятие непрерывного развертывания становится все более важным.</span><span class="sxs-lookup"><span data-stu-id="50f6e-110">The concept of "continuous deployment" is becoming more important.</span></span> <span data-ttu-id="50f6e-111">Непрерывное развертывание означает возможность выполнять развертывание часто (возможно, несколько раз в день).</span><span class="sxs-lookup"><span data-stu-id="50f6e-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="50f6e-112">Эти развертывания предназначены не для исправления ошибок, а для быстрой публикации компонентов.</span><span class="sxs-lookup"><span data-stu-id="50f6e-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="50f6e-113">Разрабатывая новые компоненты и вводя их в эксплуатацию с максимальной простотой и надежностью, можно сократить время окупаемости новой бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="50f6e-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="50f6e-114">Существуют две тенденции, которые увеличивают эту потребность в оперативных действиях.</span><span class="sxs-lookup"><span data-stu-id="50f6e-114">There are two trends at play which exacerbate this need to move quickly.</span></span> <span data-ttu-id="50f6e-115">Переход на облачные вычисления подразумевает быстрые и масштабные изменения, но при этом постоянно сохраняется угроза сбоя.</span><span class="sxs-lookup"><span data-stu-id="50f6e-115">The move towards cloud computing implies rapid change, at scale, with a constant threat of failure.</span></span>
<span data-ttu-id="50f6e-116">Возможные последствия вынуждают использовать автоматизацию для обеспечения бесперебойной работы.</span><span class="sxs-lookup"><span data-stu-id="50f6e-116">These implications force automation in order to keep up.</span></span>
<span data-ttu-id="50f6e-117">В ответ на эти изменения и был разработан подход DevOps.</span><span class="sxs-lookup"><span data-stu-id="50f6e-117">The creation of the "DevOps" mentality is a response to these changes.</span></span> 


<span data-ttu-id="50f6e-118">DSC — это платформа, которая обеспечивает декларативное, автономное и идемпотентное (повторяемое) развертывание, настройку и соответствие требованиям.</span><span class="sxs-lookup"><span data-stu-id="50f6e-118">DSC is a platform that provides declarative, autonomous and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="50f6e-119">Платформа DSC гарантирует, что компоненты центра обработки данных имеют правильные настройки, что позволяет избежать ошибок и затратных сбоев при развертывании.</span><span class="sxs-lookup"><span data-stu-id="50f6e-119">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="50f6e-120">Рассматривая конфигурации DSC как часть кода приложения, DSC обеспечивает непрерывное развертывание.</span><span class="sxs-lookup"><span data-stu-id="50f6e-120">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="50f6e-121">Конфигурации DSC должны обновляться в составе приложения. Это является гарантией того, что сведения, необходимые для развертывания приложения, всегда актуальны и готовы к использованию.</span><span class="sxs-lookup"><span data-stu-id="50f6e-121">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>


## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="50f6e-122">"Я использую PowerShell. Зачем мне настройка требуемого состояния?"</span><span class="sxs-lookup"><span data-stu-id="50f6e-122">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="50f6e-123">Конфигурации DSC отделяют намерение ("что мне нужно") от его реализации ("каким образом это сделать").</span><span class="sxs-lookup"><span data-stu-id="50f6e-123">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="50f6e-124">Это означает, что логика выполнения содержится внутри ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50f6e-124">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="50f6e-125">Пользователи не должны знать, как реализовать или развернуть тот или иной компонент, если для него доступен ресурс DSC.</span><span class="sxs-lookup"><span data-stu-id="50f6e-125">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="50f6e-126">Это позволяет пользователям сосредоточиться на структуре развертывания.</span><span class="sxs-lookup"><span data-stu-id="50f6e-126">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="50f6e-127">Например, сценарий PowerShell должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="50f6e-127">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="50f6e-128">Это простой и понятный скрипт.</span><span class="sxs-lookup"><span data-stu-id="50f6e-128">This script is simple, comprehensible, and straightforward.</span></span> <span data-ttu-id="50f6e-129">Тем не менее при попытке использовать этот скрипт в рабочей среде возникнет ряд проблем.</span><span class="sxs-lookup"><span data-stu-id="50f6e-129">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="50f6e-130">Что произойдет, если выполнить этот скрипт два раза подряд?</span><span class="sxs-lookup"><span data-stu-id="50f6e-130">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="50f6e-131">Что произойдет, если у Боба раньше был полный доступ к общей папке?</span><span class="sxs-lookup"><span data-stu-id="50f6e-131">What happens if Bob previously had Full Access to the share?</span></span> 

<span data-ttu-id="50f6e-132">Чтобы компенсировать эти проблемы, "реальная" версия этого скрипта будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="50f6e-132">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

<span data-ttu-id="50f6e-133">Это более сложный скрипт с множеством выражений логики и обработкой ошибок.</span><span class="sxs-lookup"><span data-stu-id="50f6e-133">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="50f6e-134">Он сложнее, так как на этот раз вы указываете не что нужно сделать, а *как это сделать*.</span><span class="sxs-lookup"><span data-stu-id="50f6e-134">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="50f6e-135">DSC позволяет указать, что нужно сделать, абстрагируясь от базовой логики.</span><span class="sxs-lookup"><span data-stu-id="50f6e-135">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present" 
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"  
          ReadAccess  = "Alice"
          FullAccess  = "Bob"
          Description = "This is an updated description for this share"
      }
   }
} 
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

<span data-ttu-id="50f6e-136">Этот скрипт четко отформатирован и удобен для чтения.</span><span class="sxs-lookup"><span data-stu-id="50f6e-136">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="50f6e-137">Логические пути и обработка ошибок по-прежнему присутствуют в реализации [ресурсов](resources.md), но они невидимы для автора скрипта.</span><span class="sxs-lookup"><span data-stu-id="50f6e-137">The logic paths and error handling are still present in the [resource](resources.md) implementation, but invisible to the script author.</span></span> 



## <a name="separating-environment-from-structure"></a><span data-ttu-id="50f6e-138">Разделение среды и структуры</span><span class="sxs-lookup"><span data-stu-id="50f6e-138">Separating Environment from Structure</span></span>

<span data-ttu-id="50f6e-139">Обычно в DevOps используется несколько сред развертывания.</span><span class="sxs-lookup"><span data-stu-id="50f6e-139">A common pattern in DevOps is to have multiple environments for deployment.</span></span> <span data-ttu-id="50f6e-140">Например, у вас может быть среда разработки, используемая для быстрого создания прототипа нового кода.</span><span class="sxs-lookup"><span data-stu-id="50f6e-140">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="50f6e-141">Из среды разработки код переходит в среду тестирования, где другие пользователи могут проверить новые функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="50f6e-141">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="50f6e-142">Наконец код переходит в рабочую среду активного сайта.</span><span class="sxs-lookup"><span data-stu-id="50f6e-142">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="50f6e-143">Конфигурации DSC включают конвейер "разработка — тестирование — производство", который реализуется благодаря использованию [данных конфигурации](configData.md).</span><span class="sxs-lookup"><span data-stu-id="50f6e-143">DSC configurations accomodate this dev-test-prod pipeline through the use of [configuration data](configData.md).</span></span>
<span data-ttu-id="50f6e-144">Это позволяет отвлеченно рассматривать различия между структурой конфигурации и управляемыми узлами.</span><span class="sxs-lookup"><span data-stu-id="50f6e-144">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="50f6e-145">Например, вы можете определить конфигурацию, для которой требуется SQL Server, сервер IIS и сервер среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="50f6e-145">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span> <span data-ttu-id="50f6e-146">Независимо от того, к каким узлам относятся различные части этой конфигурации, эти три элемента всегда будет присутствовать.</span><span class="sxs-lookup"><span data-stu-id="50f6e-146">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="50f6e-147">С помощью данных конфигурации можно указать все три элемента на одном компьютере в среде разработки, разделить три элемента на трех разных компьютерах в тестовой среде и, наконец, на всех рабочих серверах в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="50f6e-147">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="50f6e-148">Чтобы выполнить развертывание в различных средах, можно вызвать `Start-DscConfiguration` с помощью правильных данных конфигурации для целевой среды.</span><span class="sxs-lookup"><span data-stu-id="50f6e-148">To deploy to the different environments, you can invoke `Start-DscConfiguration` with the correct configuration data for the environment you want to target.</span></span> 

## <a name="see-also"></a><span data-ttu-id="50f6e-149">См. также</span><span class="sxs-lookup"><span data-stu-id="50f6e-149">See Also</span></span>

[<span data-ttu-id="50f6e-150">Конфигурации</span><span class="sxs-lookup"><span data-stu-id="50f6e-150">Configurations</span></span>](configurations.md)

[<span data-ttu-id="50f6e-151">Данные конфигурации</span><span class="sxs-lookup"><span data-stu-id="50f6e-151">Configuration Data</span></span>](configData.md)

[<span data-ttu-id="50f6e-152">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="50f6e-152">Resources</span></span>](resources.md)

