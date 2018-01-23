---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: e680d510aaac097f4f0de80660274230e028ed45
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="76034-103">Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="76034-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="76034-104">Асинхронно отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76034-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="76034-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="76034-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="76034-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="76034-106">Parameters</span></span>
----------

<span data-ttu-id="76034-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="76034-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="76034-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76034-108">The environment data for the configuration.</span></span>

<span data-ttu-id="76034-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="76034-109">*force* \[in\]</span></span>  
<span data-ttu-id="76034-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76034-110">**true** to force the configuration to stop.</span></span>

<span data-ttu-id="76034-111">*jobId* \[in\]</span><span class="sxs-lookup"><span data-stu-id="76034-111">*jobId* \[in\]</span></span>  
<span data-ttu-id="76034-112">Идентификатор задания, для которого отправляется конфигурация.</span><span class="sxs-lookup"><span data-stu-id="76034-112">The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="76034-113">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="76034-113">Return value</span></span>
------------

<span data-ttu-id="76034-114">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="76034-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="76034-115">Замечания</span><span class="sxs-lookup"><span data-stu-id="76034-115">Remarks</span></span>

<span data-ttu-id="76034-116">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="76034-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="76034-117">Требования</span><span class="sxs-lookup"><span data-stu-id="76034-117">Requirements</span></span>
------------
><span data-ttu-id="76034-118">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="76034-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="76034-119">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="76034-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="76034-120">См. также:</span><span class="sxs-lookup"><span data-stu-id="76034-120">See also</span></span>


[<span data-ttu-id="76034-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="76034-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



