---
ms.date: 2017-08-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "Заметки о выпуске WMF 5.1"
ms.openlocfilehash: 3a6b7fb84d679d9bbe7a89e30c8c769e26f7381a
ms.sourcegitcommit: 3f49bd2e0b786e69c71393c00ad85d05a8466753
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/04/2017
---
# <a name="windows-management-framework-wmf-51"></a><span data-ttu-id="b62fe-103">Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="b62fe-103">Windows Management Framework (WMF) 5.1</span></span> #

<span data-ttu-id="b62fe-104">WMF предоставляет пользователям возможность обновить существующие системы Windows до версий PowerShell, WMI, WinRM и Software Inventory Logging (SIL), которые были выпущены с Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b62fe-104">WMF provides users with the ability to update existing Windows systems to the versions of PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span> 

<span data-ttu-id="b62fe-105">Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="b62fe-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="b62fe-106">Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.</span><span class="sxs-lookup"><span data-stu-id="b62fe-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="b62fe-107">Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.</span><span class="sxs-lookup"><span data-stu-id="b62fe-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="b62fe-108">Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.</span><span class="sxs-lookup"><span data-stu-id="b62fe-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="b62fe-109">Улучшения отладки для классов DSC и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b62fe-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="b62fe-110">Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="b62fe-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="b62fe-111">Ответы на разные запросы пользователей и решение проблем.</span><span class="sxs-lookup"><span data-stu-id="b62fe-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="b62fe-112">Дополнительные сведения о новых возможностях в этом выпуске см. в разделах, перечисленных в статье [Новые сценарии и функции](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).</span><span class="sxs-lookup"><span data-stu-id="b62fe-112">To learn about what is new in this release, browse the topics listed under [New Scenarios and Features](https://docs.microsoft.com/en-us/powershell/wmf/5.1/scenarios-features).</span></span> 

<span data-ttu-id="b62fe-113">В разделе [Установка и настройка](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) перечисляются требования и предоставляются инструкции по установке для WMF.</span><span class="sxs-lookup"><span data-stu-id="b62fe-113">The [Install and Configure](https://docs.microsoft.com/en-us/powershell/wmf/5.1/install-configure) topic lists the requirements and provides installation instructions for WMF.</span></span> 

<span data-ttu-id="b62fe-114">В разделе [Совместимость](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) перечисляются версии WMF, которые можно установить на выпуски Windows.</span><span class="sxs-lookup"><span data-stu-id="b62fe-114">The [Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/compatibility) topic lists which versions of WMF may be installed on which Windows releases.</span></span> 

<span data-ttu-id="b62fe-115">В разделе [Совместимость продуктов](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) перечисляются приложения Майкрософт, которые не утвердили использование WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="b62fe-115">[Product Compatibility](https://docs.microsoft.com/en-us/powershell/wmf/5.1/productincompat) lists the Microsoft applications that have not approved WMF 5.1 for use at this time.</span></span> 

<span data-ttu-id="b62fe-116">Сведения для компонентов WMF можно найти в документации MSDN:</span><span class="sxs-lookup"><span data-stu-id="b62fe-116">Details for the components of WMF will be found in MSDN documentation:</span></span>

- [<span data-ttu-id="b62fe-117">PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="b62fe-117">PowerShell 5.1</span></span>](https://docs.microsoft.com/en-us/powershell/) 
- [<span data-ttu-id="b62fe-118">WMI</span><span class="sxs-lookup"><span data-stu-id="b62fe-118">WMI</span></span>](https://msdn.microsoft.com/en-us/library/jj152383(v=vs.85).aspx)
- [<span data-ttu-id="b62fe-119">WinRM</span><span class="sxs-lookup"><span data-stu-id="b62fe-119">WinRM</span></span>](https://msdn.microsoft.com/en-us/library/aa384426(v=vs.85).aspx)
- [<span data-ttu-id="b62fe-120">Ведение журнала инвентаризации программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="b62fe-120">Software Inventory Logging</span></span>](https://technet.microsoft.com/en-us/library/dn383584(v=ws.11).aspx)

