---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: dadb6912af2e4450381958ed465799056da49946
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9baae-103">Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="9baae-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9baae-104">Останавливает выполняемое изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9baae-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="9baae-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="9baae-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="9baae-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="9baae-106">Parameters</span></span>
----------

<span data-ttu-id="9baae-107">*force* \[in\] **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9baae-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="9baae-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="9baae-108">Return value</span></span>
------------

<span data-ttu-id="9baae-109">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="9baae-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9baae-110">Замечания</span><span class="sxs-lookup"><span data-stu-id="9baae-110">Remarks</span></span>

<span data-ttu-id="9baae-111">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="9baae-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9baae-112">Требования</span><span class="sxs-lookup"><span data-stu-id="9baae-112">Requirements</span></span>
------------
><span data-ttu-id="9baae-113">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9baae-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9baae-114">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9baae-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="9baae-115">См. также:</span><span class="sxs-lookup"><span data-stu-id="9baae-115">See also</span></span>


[<span data-ttu-id="9baae-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9baae-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)