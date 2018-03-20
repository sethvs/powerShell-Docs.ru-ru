---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "Заметки о выпуске WMF 5.1"
ms.openlocfilehash: fa3d9a3563ecf1bfc76d82b027641d19c9a4ff4e
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="b6050-103">Заметки о выпуске Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="b6050-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span> #

<span data-ttu-id="b6050-104">WMF 5.1 включает компоненты PowerShell, WMI, WinRM и Software Inventory Logging (SIL), которые были выпущены с Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b6050-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="b6050-105">Службу WMF 5.1 можно установить на Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 и 2012 R2; она предоставляет ряд улучшений в WMF 5.0 RTM, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="b6050-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="b6050-106">Новые командлеты: локальные пользователи и группы; Get-ComputerInfo.</span><span class="sxs-lookup"><span data-stu-id="b6050-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="b6050-107">Улучшения PowerShellGet включают принудительное подписание модулей и установку модулей JEA.</span><span class="sxs-lookup"><span data-stu-id="b6050-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="b6050-108">Дополнительная поддержка PackageManagement для контейнеров, установка CBS, установка на основе EXE, пакеты CAB.</span><span class="sxs-lookup"><span data-stu-id="b6050-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="b6050-109">Улучшения отладки для классов DSC и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6050-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="b6050-110">Улучшения для системы безопасности, включая принудительное использование модулей, подписанных каталогом и полученных от опрашивающего сервера, а также при использовании командлетов PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="b6050-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="b6050-111">Ответы на разные запросы пользователей и решение проблем.</span><span class="sxs-lookup"><span data-stu-id="b6050-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="b6050-112">**Важные примечания.**</span><span class="sxs-lookup"><span data-stu-id="b6050-112">**Important notes:**</span></span>

- <span data-ttu-id="b6050-113">**Для WMF 5.1 требуется .NET Framework 4.5.2** (или более поздняя версия).</span><span class="sxs-lookup"><span data-stu-id="b6050-113">**WMF 5.1 requires the .NET Framework 4.5.2** (or above).</span></span> <span data-ttu-id="b6050-114">Если платформа .NET 4.5.2 (или более поздняя версия) не установлена, установка WMF 5.1 будет выполнена, но основные функции работать не будут.</span><span class="sxs-lookup"><span data-stu-id="b6050-114">Installation will succeed, but key features will fail if .NET 4.5.2 (or above) is not installed.</span></span> <span data-ttu-id="b6050-115">Инструкции см. в разделе [Установка и настройка WMF 5.1](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure).</span><span class="sxs-lookup"><span data-stu-id="b6050-115">Instructions are available in the [Install and Configure WMF 5.1 ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="b6050-116">Перед установкой WMF 5.1 RTM нужно удалить предварительную версию WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="b6050-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="b6050-117">WMF 5.1 можно установить непосредственно на WMF 5.0 или WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="b6050-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="b6050-118">Устанавливать WMF 4.0 перед установкой WMF 5.1 в Windows 7 и Windows Server 2008 R2 __не требуется__.</span><span class="sxs-lookup"><span data-stu-id="b6050-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="b6050-119">Эта проблема имела место для предварительной версии WMF 5.1 и была устранена.</span><span class="sxs-lookup"><span data-stu-id="b6050-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>  


