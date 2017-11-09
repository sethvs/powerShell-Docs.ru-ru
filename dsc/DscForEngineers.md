---
ms.date: 2017-10-13
author: eslesar;mgreenegit
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Обзор платформы Desired State Configuration для руководителей"
ms.openlocfilehash: 66822d9a60f98aab3d4f27d14b27ebc6ec90b2c9
ms.sourcegitcommit: 9a5da3f739b1eebb81ede58bd4fc8037bad87224
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2017
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="6f9e1-103">Обзор платформы Desired State Configuration для инженеров</span><span class="sxs-lookup"><span data-stu-id="6f9e1-103">Desired State Configuration Overview for Engineers</span></span>

<span data-ttu-id="6f9e1-104">В этом документе, предназначенном для групп разработки и эксплуатации, описаны преимущества использования платформы Desired State Configuration (DSC) в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="6f9e1-105">C более высокой точкой зрения о преимуществах DSC вы можете ознакомиться в [обзоре платформы Desired State Configuration для руководителей](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="6f9e1-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="6f9e1-106">Преимущества Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="6f9e1-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="6f9e1-107">Настройка требуемого состояния обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6f9e1-107">DSC exists to:</span></span>

- <span data-ttu-id="6f9e1-108">упрощение написания скриптов для Windows;</span><span class="sxs-lookup"><span data-stu-id="6f9e1-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="6f9e1-109">повышение скорости итерации.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-109">Increase the speed of iteration</span></span>

<span data-ttu-id="6f9e1-110">Понятие непрерывного развертывания становится все более важным.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-110">The concept of "continuous deployment" is becoming more important.</span></span>
<span data-ttu-id="6f9e1-111">Непрерывное развертывание означает возможность выполнять развертывание часто (возможно, несколько раз в день).</span><span class="sxs-lookup"><span data-stu-id="6f9e1-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="6f9e1-112">Эти развертывания предназначены не для исправления ошибок, а для быстрой публикации компонентов.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="6f9e1-113">Разрабатывая новые компоненты и вводя их в эксплуатацию с максимальной простотой и надежностью, можно сократить время окупаемости новой бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="6f9e1-114">При переходе к облачным вычислениям требуется решение для развертывания, в котором используется модель декларативного шаблона. При этом данные среды конечного состояния объявляются как текст и публикуются в подсистеме развертывания.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-114">The move towards cloud computing implies a deployment solution that utilizes a "declarative" template model, where an end state environment is declared as text and published to a deployment engine.</span></span>
<span data-ttu-id="6f9e1-115">Такой метод развертывания позволяет быстро вносить изменения, а также обеспечивает масштабируемость и устойчивость к сбоям. Развертывание можно в любой момент последовательно повторить для обеспечения надлежащего конечного состояния.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-115">This deployment technique allows for rapid change, at scale, with resilience against threat of failure because at any time the deployment can be consistently repeated to guarantee an end state.</span></span>
<span data-ttu-id="6f9e1-116">Для работы с такой моделью создаются специальные автоматизированные средства и службы.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-116">The creation of tools and services that support this style of operations through automation is a response to these changes.</span></span>

<span data-ttu-id="6f9e1-117">DSC — это платформа, которая обеспечивает декларативное и идемпотентное (повторяемое) развертывание, настройку и соответствие требованиям.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-117">DSC is a platform that provides declarative and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="6f9e1-118">Платформа DSC гарантирует, что компоненты центра обработки данных имеют правильные настройки, что позволяет избежать ошибок и затратных сбоев при развертывании.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-118">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="6f9e1-119">Рассматривая конфигурации DSC как часть кода приложения, DSC обеспечивает непрерывное развертывание.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-119">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="6f9e1-120">Конфигурации DSC должны обновляться в составе приложения. Это является гарантией того, что сведения, необходимые для развертывания приложения, всегда актуальны и готовы к использованию.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-120">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="6f9e1-121">"Я использую PowerShell. Зачем мне платформа Desired State Configuration?"</span><span class="sxs-lookup"><span data-stu-id="6f9e1-121">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="6f9e1-122">Конфигурации DSC отделяют намерение ("что мне нужно") от его реализации ("каким образом это сделать").</span><span class="sxs-lookup"><span data-stu-id="6f9e1-122">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="6f9e1-123">Это означает, что логика выполнения содержится внутри ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-123">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="6f9e1-124">Пользователи не должны знать, как реализовать или развернуть тот или иной компонент, если для него доступен ресурс DSC.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-124">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="6f9e1-125">Это позволяет пользователям сосредоточиться на структуре развертывания.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-125">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="6f9e1-126">Например, сценарий PowerShell должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6f9e1-126">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="6f9e1-127">Это простой и понятный скрипт.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-127">This script is simple, comprehensible, and straightforward.</span></span>
<span data-ttu-id="6f9e1-128">Тем не менее при попытке использовать этот скрипт в рабочей среде возникнет ряд проблем.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-128">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="6f9e1-129">Что произойдет, если выполнить этот скрипт два раза подряд?</span><span class="sxs-lookup"><span data-stu-id="6f9e1-129">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="6f9e1-130">Что произойдет, если у Боба раньше был полный доступ к общей папке?</span><span class="sxs-lookup"><span data-stu-id="6f9e1-130">What happens if Bob previously had Full Access to the share?</span></span>

<span data-ttu-id="6f9e1-131">Чтобы компенсировать эти проблемы, "реальная" версия этого скрипта будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="6f9e1-131">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
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

<span data-ttu-id="6f9e1-132">Это более сложный скрипт с множеством выражений логики и обработкой ошибок.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-132">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="6f9e1-133">Он сложнее, так как на этот раз вы указываете не что нужно сделать, а *как это сделать*.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-133">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="6f9e1-134">DSC позволяет указать, что нужно сделать, абстрагируясь от базовой логики.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-134">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

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

<span data-ttu-id="6f9e1-135">Этот скрипт четко отформатирован и удобен для чтения.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-135">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="6f9e1-136">Логические пути и обработка ошибок по-прежнему присутствуют в реализации [ресурсов](resources.md), но они невидимы для автора скрипта.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-136">The logic paths and error handling are still present in the [resource](resources.md) implementation, but invisible to the script author.</span></span>

## <a name="separating-environment-from-structure"></a><span data-ttu-id="6f9e1-137">Разделение среды и структуры</span><span class="sxs-lookup"><span data-stu-id="6f9e1-137">Separating Environment from Structure</span></span>

<span data-ttu-id="6f9e1-138">Обычно в DevOps используется несколько сред развертывания.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-138">A common pattern in DevOps is to have multiple environments for deployment.</span></span>
<span data-ttu-id="6f9e1-139">Например, у вас может быть среда разработки, используемая для быстрого создания прототипа нового кода.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-139">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="6f9e1-140">Из среды разработки код переходит в среду тестирования, где другие пользователи могут проверить новые функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-140">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="6f9e1-141">Наконец код переходит в рабочую среду активного сайта.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-141">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="6f9e1-142">Конфигурации DSC включают конвейер "разработка — тестирование — производство", который реализуется в ходе использования [данных конфигурации](configData.md).</span><span class="sxs-lookup"><span data-stu-id="6f9e1-142">DSC configurations accommodate this dev-test-prod pipeline through the use of [configuration data](configData.md).</span></span>
<span data-ttu-id="6f9e1-143">Это позволяет отвлеченно рассматривать различия между структурой конфигурации и управляемыми узлами.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-143">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="6f9e1-144">Например, вы можете определить конфигурацию, для которой требуется SQL Server, сервер IIS и сервер среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-144">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span>
<span data-ttu-id="6f9e1-145">Независимо от того, к каким узлам относятся различные части этой конфигурации, эти три элемента всегда будет присутствовать.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-145">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="6f9e1-146">С помощью данных конфигурации можно указать все три элемента на одном компьютере в среде разработки, разделить три элемента на трех разных компьютерах в тестовой среде и, наконец, на всех рабочих серверах в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-146">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="6f9e1-147">Чтобы выполнить развертывание в различных средах, можно вызвать **Start-DscConfiguration** с помощью правильных данных конфигурации для целевой среды.</span><span class="sxs-lookup"><span data-stu-id="6f9e1-147">To deploy to the different environments, you can invoke **Start-DscConfiguration** with the correct configuration data for the environment you want to target.</span></span>

## <a name="see-also"></a><span data-ttu-id="6f9e1-148">См. также</span><span class="sxs-lookup"><span data-stu-id="6f9e1-148">See Also</span></span>

[<span data-ttu-id="6f9e1-149">Конфигурации</span><span class="sxs-lookup"><span data-stu-id="6f9e1-149">Configurations</span></span>](configurations.md)

[<span data-ttu-id="6f9e1-150">Данные конфигурации</span><span class="sxs-lookup"><span data-stu-id="6f9e1-150">Configuration Data</span></span>](configData.md)

[<span data-ttu-id="6f9e1-151">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="6f9e1-151">Resources</span></span>](resources.md)
