---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Использование DSC в Microsoft Azure"
ms.openlocfilehash: 9b7d301c3e011b8933b9ee49219e7f0949a5c886
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="072e6-103">Использование DSC в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="072e6-104">Настройка требуемого состояния (DSC) поддерживается в Microsoft Azure при помощи [обработчика расширений настройки требуемого состояния Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) и [DSC в службе автоматизации Azure](https://docs.microsoft.com/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="072e6-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) and through [Azure Automation DSC](https://docs.microsoft.com/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="072e6-105">Обработчик расширения настройки требуемого состояния Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="072e6-106">Расширение Azure DSC позволяет управлять виртуальными машинами, размещенным в Microsoft Azure, при помощи DSC.</span><span class="sxs-lookup"><span data-stu-id="072e6-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span> <span data-ttu-id="072e6-107">Дополнительные сведения см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="072e6-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="072e6-108">Обработчик расширения настройки требуемого состояния Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-108">Azure Desired State Configuration extension handler</span></span>](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [<span data-ttu-id="072e6-109">Windows VMSS и настройка требуемого состояния при помощи шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="072e6-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [<span data-ttu-id="072e6-110">Передача учетных данных в обработчик расширения настройки требуемого состояния Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-110">Passing credentials to the Azure DSC extension handler</span></span>](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)

## <a name="azure-automation-dsc"></a><span data-ttu-id="072e6-111">DSC в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-111">Azure Automation DSC</span></span>

<span data-ttu-id="072e6-112">[Служба автоматизации Azure](https://azure.microsoft.com/services/automation/) позволяет управлять конфигурациями DSC, ресурсами и управляемыми узлами из Azure.</span><span class="sxs-lookup"><span data-stu-id="072e6-112">The [Azure Automation service](https://azure.microsoft.com/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="072e6-113">Дополнительные сведения см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="072e6-113">For more information, see the following topics:</span></span>

- [<span data-ttu-id="072e6-114">DSC в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-114">Azure Automation DSC</span></span>](https://docs.microsoft.com/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="072e6-115">Начало работы с DSC в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-115">Getting started with Azure Automation DSC</span></span>](https://docs.microsoft.com/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="072e6-116">Подключение компьютеров для управления при помощи DSC в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="072e6-116">Onboarding machines for management by Azure Automation DSC</span></span>](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding)

