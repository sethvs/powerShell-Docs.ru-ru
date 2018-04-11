---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9fe41fa806a6abff1d36dadd0c041a5cf0e78caf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7763e-103">Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="7763e-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7763e-104">Включает отладку ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="7763e-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="7763e-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7763e-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="7763e-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="7763e-106">Parameters</span></span>
----------

<span data-ttu-id="7763e-107">*BreakAll* \[in\] Устанавливает точку останова в каждой строке в сценарии ресурса.</span><span class="sxs-lookup"><span data-stu-id="7763e-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="7763e-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7763e-108">Return value</span></span>
------------

<span data-ttu-id="7763e-109">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="7763e-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7763e-110">Замечания</span><span class="sxs-lookup"><span data-stu-id="7763e-110">Remarks</span></span>

<span data-ttu-id="7763e-111">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="7763e-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7763e-112">Требования</span><span class="sxs-lookup"><span data-stu-id="7763e-112">Requirements</span></span>
------------
><span data-ttu-id="7763e-113">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7763e-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="7763e-114">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7763e-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="7763e-115">См. также:</span><span class="sxs-lookup"><span data-stu-id="7763e-115">See also</span></span>


[<span data-ttu-id="7763e-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7763e-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)