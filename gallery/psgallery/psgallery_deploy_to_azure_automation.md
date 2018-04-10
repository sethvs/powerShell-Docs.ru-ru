---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: psgallery_развертывание_в_службу_автоматизации_azure
ms.openlocfilehash: 8da4eabead6a419dc0c01c74335c06bf8be25d0c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
<a name="deploy-to-azure-automation"></a><span data-ttu-id="f860a-103">Развертывание в службу автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f860a-103">Deploy to Azure Automation</span></span>
===========================

<span data-ttu-id="f860a-104">Кнопкой "Развернуть в службе автоматизации Azure" на странице подробностей об элементе можно развернуть элемент из коллекции PowerShell в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f860a-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Кнопка "Развернуть в службе автоматизации Azure"](Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="f860a-106">При нажатии этой кнопки вы будете перенаправлены на портал управления Azure, на который нужно войти с использованием учетных данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="f860a-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="f860a-107">Если элемент имеет зависимости, все они будут также развернуты в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f860a-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

<span data-ttu-id="f860a-108">ВНИМАНИЕ! Если в вашей учетной записи службы автоматизации уже существует такой элемент с той же версией, его повторное развертывание из коллекции PowerShell приведет к перезаписи существующего элемента в учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="f860a-108">WARNING:  If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="f860a-109">При развертывании модуля он будет отображаться в разделе модулей службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f860a-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="f860a-110">При развертывании скрипта он будет отображаться в разделе модулей Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="f860a-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="f860a-111">Кнопку "Развернуть в службу автоматизации Azure" можно отключить, добавив тег AzureAutomationNotSupported в метаданные элемента.</span><span class="sxs-lookup"><span data-stu-id="f860a-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

<span data-ttu-id="f860a-112">Подробности о службе автоматизации Azure см. на [сайте службы автоматизации Azure](http://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="f860a-112">To learn more about Azure Automation, see the Azure Automation website [Azure Automation website](http://azure.microsoft.com/services/automation/).</span></span>