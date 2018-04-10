---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Раздел реестра DSCAutomationHostEnabled
ms.openlocfilehash: 9fd71120b4959a7b14094922b453b05b217f3736
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
><span data-ttu-id="f914a-103">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f914a-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="f914a-104">Раздел реестра DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="f914a-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="f914a-105">DSC использует раздел реестра **DSCAutomationHostEnabled** в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** для включения конфигурации компьютера при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="f914a-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="f914a-106">DSCAutomationHostEnabled поддерживает три режима:</span><span class="sxs-lookup"><span data-stu-id="f914a-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="f914a-107">Значение DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="f914a-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="f914a-108">Описание</span><span class="sxs-lookup"><span data-stu-id="f914a-108">Description</span></span>   |
|---|---|
<span data-ttu-id="f914a-109">0</span><span class="sxs-lookup"><span data-stu-id="f914a-109">0</span></span> | <span data-ttu-id="f914a-110">Отключение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="f914a-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="f914a-111">1</span><span class="sxs-lookup"><span data-stu-id="f914a-111">1</span></span> | <span data-ttu-id="f914a-112">Включение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="f914a-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="f914a-113">2</span><span class="sxs-lookup"><span data-stu-id="f914a-113">2</span></span> | <span data-ttu-id="f914a-114">Включение настройки компьютера, только если DSC находится в состоянии ожидания или в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="f914a-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="f914a-115">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f914a-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="f914a-116">См. также</span><span class="sxs-lookup"><span data-stu-id="f914a-116">See Also</span></span>

<span data-ttu-id="f914a-117">Пример использования этой функции для запуска конфигураций при начальной загрузке системы см. в разделе [Настройка виртуальных машин при начальной загрузке с помощью DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="f914a-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>