---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 7220c972b3f43b4697cf71df54d2d43881938367
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="28ef0-103">Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="28ef0-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="28ef0-104">Включает отладку ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="28ef0-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="28ef0-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="28ef0-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="28ef0-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="28ef0-106">Parameters</span></span>
----------

<span data-ttu-id="28ef0-107">*BreakAll* \[in\]</span><span class="sxs-lookup"><span data-stu-id="28ef0-107">*BreakAll* \[in\]</span></span>  
<span data-ttu-id="28ef0-108">Устанавливает точку останова в каждой строке в сценарии ресурса.</span><span class="sxs-lookup"><span data-stu-id="28ef0-108">Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="28ef0-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="28ef0-109">Return value</span></span>
------------

<span data-ttu-id="28ef0-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="28ef0-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="28ef0-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="28ef0-111">Remarks</span></span>

<span data-ttu-id="28ef0-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="28ef0-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="28ef0-113">Требования</span><span class="sxs-lookup"><span data-stu-id="28ef0-113">Requirements</span></span>
------------
><span data-ttu-id="28ef0-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="28ef0-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="28ef0-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="28ef0-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="28ef0-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="28ef0-116">See also</span></span>


[<span data-ttu-id="28ef0-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="28ef0-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



