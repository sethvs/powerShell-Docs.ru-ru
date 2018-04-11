---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 2844e354e0d054b13b92267ce314536d88a1c33e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="afa90-103">Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="afa90-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="afa90-104">Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="afa90-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="afa90-105">Если нет ожидающих конфигураций, этот метод повторно применяет текущую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="afa90-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="afa90-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="afa90-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="afa90-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="afa90-107">Parameters</span></span>
----------

<span data-ttu-id="afa90-108">*force* \[in\] Если параметр имеет значение **true**, текущая конфигурация применяется повторно даже при наличии конфигурации в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="afa90-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="afa90-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="afa90-109">Return value</span></span>
------------

<span data-ttu-id="afa90-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="afa90-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="afa90-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="afa90-111">Remarks</span></span>

<span data-ttu-id="afa90-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="afa90-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="afa90-113">Требования</span><span class="sxs-lookup"><span data-stu-id="afa90-113">Requirements</span></span>
------------
><span data-ttu-id="afa90-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="afa90-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="afa90-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="afa90-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="afa90-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="afa90-116">See also</span></span>


[<span data-ttu-id="afa90-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="afa90-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)