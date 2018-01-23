---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 72fbedf30e5058d8003ed620400d6b443d50dff6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="82b6a-103">Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="82b6a-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="82b6a-104">Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="82b6a-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span> 

<span data-ttu-id="82b6a-105">Если нет ожидающих конфигураций, этот метод повторно применяет текущую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="82b6a-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="82b6a-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="82b6a-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="82b6a-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="82b6a-107">Parameters</span></span>
----------

<span data-ttu-id="82b6a-108">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="82b6a-108">*force* \[in\]</span></span>  
<span data-ttu-id="82b6a-109">Если параметр имеет значение **true**, текущая конфигурация применяется повторно даже при наличии конфигурации в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="82b6a-109">If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="82b6a-110">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="82b6a-110">Return value</span></span>
------------

<span data-ttu-id="82b6a-111">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="82b6a-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="82b6a-112">Замечания</span><span class="sxs-lookup"><span data-stu-id="82b6a-112">Remarks</span></span>

<span data-ttu-id="82b6a-113">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="82b6a-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="82b6a-114">Требования</span><span class="sxs-lookup"><span data-stu-id="82b6a-114">Requirements</span></span>
------------
><span data-ttu-id="82b6a-115">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="82b6a-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="82b6a-116">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="82b6a-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="82b6a-117">См. также:</span><span class="sxs-lookup"><span data-stu-id="82b6a-117">See also</span></span>


[<span data-ttu-id="82b6a-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="82b6a-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



