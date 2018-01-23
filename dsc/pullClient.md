---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка опрашивающего клиента DSC"
ms.openlocfilehash: 98a67b8d27eeb445bb70f75253ca31e12207d5bd
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="5812d-103">Настройка опрашивающего клиента DSC</span><span class="sxs-lookup"><span data-stu-id="5812d-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="5812d-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5812d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5812d-105">Для каждого целевого узла нужно включить опрашивающий режим и указать URL-адрес или расположение файла для подключения к опрашивающему серверу, чтобы получать конфигурации и ресурсы, а также отправлять данные отчетов.</span><span class="sxs-lookup"><span data-stu-id="5812d-105">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>


<span data-ttu-id="5812d-106">В следующих разделах показано, как настроить опрашивающие клиенты.</span><span class="sxs-lookup"><span data-stu-id="5812d-106">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="5812d-107">Настройка опрашивающего клиента с помощью имени конфигурации</span><span class="sxs-lookup"><span data-stu-id="5812d-107">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="5812d-108">Настройка опрашивающего клиента с помощью идентификатора конфигурации</span><span class="sxs-lookup"><span data-stu-id="5812d-108">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="5812d-109">**Примечание**. Эти разделы относятся к PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="5812d-109">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="5812d-110">Сведения о настройке опрашивающего клиента в PowerShell 4.0 см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации в PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="5812d-110">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>

