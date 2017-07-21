---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Раздел реестра DSCAutomationHostEnabled"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
><span data-ttu-id="24343-103">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="24343-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="24343-104">Раздел реестра DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="24343-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="24343-105">DSC использует раздел реестра **DSCAutomationHostEnabled** в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** для включения конфигурации компьютера при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="24343-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="24343-106">DSCAutomationHostEnabled поддерживает три режима:</span><span class="sxs-lookup"><span data-stu-id="24343-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="24343-107">Значение DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="24343-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="24343-108">Описание</span><span class="sxs-lookup"><span data-stu-id="24343-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="24343-109">0</span><span class="sxs-lookup"><span data-stu-id="24343-109">0</span></span> | <span data-ttu-id="24343-110">Отключение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="24343-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="24343-111">1</span><span class="sxs-lookup"><span data-stu-id="24343-111">1</span></span> | <span data-ttu-id="24343-112">Включение настройки компьютера при загрузке системы.</span><span class="sxs-lookup"><span data-stu-id="24343-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="24343-113">2</span><span class="sxs-lookup"><span data-stu-id="24343-113">2</span></span> | <span data-ttu-id="24343-114">Включение настройки компьютера, только если DSC находится в состоянии ожидания или в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="24343-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="24343-115">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="24343-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="24343-116">См. также</span><span class="sxs-lookup"><span data-stu-id="24343-116">See Also</span></span>

<span data-ttu-id="24343-117">Пример использования этой функции для запуска конфигураций при начальной загрузке системы см. в разделе [Настройка виртуальных машин при начальной загрузке с помощью DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="24343-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>


