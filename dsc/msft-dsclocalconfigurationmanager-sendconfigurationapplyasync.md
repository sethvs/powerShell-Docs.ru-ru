---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5150b-103">Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="5150b-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5150b-104">Асинхронно отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5150b-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="5150b-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5150b-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="5150b-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="5150b-106">Parameters</span></span>
----------

<span data-ttu-id="5150b-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="5150b-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="5150b-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5150b-108">The environment data for the configuration.</span></span>

<span data-ttu-id="5150b-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="5150b-109">*force* \[in\]</span></span>  
<span data-ttu-id="5150b-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5150b-110">**true** to force the configuration to stop.</span></span>

<span data-ttu-id="5150b-111">*jobId* \[in\]</span><span class="sxs-lookup"><span data-stu-id="5150b-111">*jobId* \[in\]</span></span>  
<span data-ttu-id="5150b-112">Идентификатор задания, для которого отправляется конфигурация.</span><span class="sxs-lookup"><span data-stu-id="5150b-112">The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="5150b-113">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5150b-113">Return value</span></span>
------------

<span data-ttu-id="5150b-114">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="5150b-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5150b-115">Замечания</span><span class="sxs-lookup"><span data-stu-id="5150b-115">Remarks</span></span>

<span data-ttu-id="5150b-116">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="5150b-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5150b-117">Требования</span><span class="sxs-lookup"><span data-stu-id="5150b-117">Requirements</span></span>
------------
><span data-ttu-id="5150b-118">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5150b-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5150b-119">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5150b-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5150b-120">См. также:</span><span class="sxs-lookup"><span data-stu-id="5150b-120">See also</span></span>


[<span data-ttu-id="5150b-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5150b-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



