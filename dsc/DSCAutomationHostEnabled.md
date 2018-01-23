---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Раздел реестра DSCAutomationHostEnabled"
ms.openlocfilehash: c58b7a8f2485ff02f09763749a3de8a75f882d19
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
><span data-ttu-id="e6832-103">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e6832-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="e6832-104">Раздел реестра DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="e6832-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="e6832-105">DSC использует раздел реестра **DSCAutomationHostEnabled** в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** для включения конфигурации компьютера при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="e6832-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="e6832-106">DSCAutomationHostEnabled поддерживает три режима:</span><span class="sxs-lookup"><span data-stu-id="e6832-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="e6832-107">Значение DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="e6832-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="e6832-108">Описание</span><span class="sxs-lookup"><span data-stu-id="e6832-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="e6832-109">0</span><span class="sxs-lookup"><span data-stu-id="e6832-109">0</span></span> | <span data-ttu-id="e6832-110">Отключение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="e6832-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="e6832-111">1</span><span class="sxs-lookup"><span data-stu-id="e6832-111">1</span></span> | <span data-ttu-id="e6832-112">Включение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="e6832-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="e6832-113">2</span><span class="sxs-lookup"><span data-stu-id="e6832-113">2</span></span> | <span data-ttu-id="e6832-114">Включение настройки компьютера, только если DSC находится в состоянии ожидания или в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="e6832-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="e6832-115">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e6832-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="e6832-116">См. также</span><span class="sxs-lookup"><span data-stu-id="e6832-116">See Also</span></span>

<span data-ttu-id="e6832-117">Пример использования этой функции для запуска конфигураций при начальной загрузке системы см. в разделе [Настройка виртуальных машин при начальной загрузке с помощью DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="e6832-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>


