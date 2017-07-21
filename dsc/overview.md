---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Общие сведения о службе настройки требуемого состояния Windows PowerShell"
ms.openlocfilehash: 154a3c78a9bf2a029577ca6862f333b6bfe69878
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="fc2e2-103">Общие сведения о службе настройки требуемого состояния Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc2e2-103">Windows PowerShell Desired State Configuration Overview</span></span> 

> <span data-ttu-id="fc2e2-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="fc2e2-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="fc2e2-105">DSC — это платформа управления в PowerShell, которая позволяет управлять ИТ-инфраструктурой и инфраструктурой разработки с помощью конфигурации в виде кода.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="fc2e2-106">Обзор преимуществ использования DSC для компаний см. в статье [Общие сведения о настройке требуемого состояния Windows PowerShell для руководителей](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="fc2e2-107">Обзор преимуществ использования DSC для инженеров см. в статье [Общие сведения о настройке требуемого состояния для инженеров](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="fc2e2-108">Чтобы начать использовать DSC, см. [Краткое руководство по DSC](quickStart.md).</span><span class="sxs-lookup"><span data-stu-id="fc2e2-108">To start using DSC quickly, see [DSC quick start](quickStart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="fc2e2-109">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="fc2e2-109">Key Concepts</span></span>

<span data-ttu-id="fc2e2-110">DSC — это декларативная платформа, которая используется для настройки, развертывания и администрирования систем.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="fc2e2-111">Она состоит из трех основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="fc2e2-111">It consists of three primary components:</span></span>

- <span data-ttu-id="fc2e2-112">[Конфигурации](configurations.md) — это декларативные сценарии PowerShell, которые определяют и настраивают экземпляры ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-112">[Configurations](configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="fc2e2-113">После выполнения конфигурации DSC (а также вызываемые этой конфигурацией ресурсы) принимает ее в исходном виде и обеспечивает существование системы в состоянии, заданном этой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span> 
    <span data-ttu-id="fc2e2-114">Конфигурации DSC также идемпотентны: локальный диспетчер конфигураций (LCM) следит за тем, чтобы компьютеры находились в состоянии, объявленном конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="fc2e2-115">[Ресурсы](resources.md) — это часть DSC.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-115">[Resources](resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="fc2e2-116">Они содержат код, который приводит целевой объект конфигурации в указанное состояние и сохраняет это состояние.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span> 
    <span data-ttu-id="fc2e2-117">Ресурсы находятся в модулях PowerShell и могут записываться для моделирования обычных объектов, таких как файл или процесс Windows, и специфических элементов, таких как сервер служб IIS или виртуальная машина, работающая в Azure.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="fc2e2-118">[Локальный диспетчер конфигураций (LCM)](metaConfig.md) — это механизм, с помощью которого DSC упрощает взаимодействие между ресурсами и конфигурациями.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-118">The [Local Configuration Manager (LCM)](metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span> 
    <span data-ttu-id="fc2e2-119">LCM регулярно опрашивает систему, используя реализуемую ресурсами последовательность управления, и следит за сохранением состояния, определенного конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span> 
    <span data-ttu-id="fc2e2-120">Если система выходит из этого состояния, LCM вызывает код в ресурсах для сохранения заданного конфигурацией состояния.</span><span class="sxs-lookup"><span data-stu-id="fc2e2-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span> 

## <a name="see-also"></a><span data-ttu-id="fc2e2-121">См. также</span><span class="sxs-lookup"><span data-stu-id="fc2e2-121">See Also</span></span>

- [<span data-ttu-id="fc2e2-122">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="fc2e2-122">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="fc2e2-123">Ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="fc2e2-123">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="fc2e2-124">Настройка локального диспетчера конфигураций</span><span class="sxs-lookup"><span data-stu-id="fc2e2-124">Configuring The Local Configuration Manager</span></span>](metaConfig.md)

