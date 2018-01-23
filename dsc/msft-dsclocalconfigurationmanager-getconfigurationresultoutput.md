---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: f6106bb28dc20004b5bbb6df2d8e719cf0c453f0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4f923-103">Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4f923-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4f923-104">Получает выходные данные агента конфигурации, относящиеся к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="4f923-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="4f923-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4f923-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="4f923-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="4f923-106">Parameters</span></span>
----------

<span data-ttu-id="4f923-107">*jobId* \[in\]</span><span class="sxs-lookup"><span data-stu-id="4f923-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="4f923-108">Идентификатор задания, для которого необходимо получить выходные данные.</span><span class="sxs-lookup"><span data-stu-id="4f923-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="4f923-109">*resumeOutputBookmark* \[in\]</span><span class="sxs-lookup"><span data-stu-id="4f923-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="4f923-110">Указывает, что выходные данные должны быть продолжением от предыдущей закладки.</span><span class="sxs-lookup"><span data-stu-id="4f923-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="4f923-111">*output* \[out\]</span><span class="sxs-lookup"><span data-stu-id="4f923-111">*output* \[out\]</span></span>  
<span data-ttu-id="4f923-112">Выходные данные для указанного задания.</span><span class="sxs-lookup"><span data-stu-id="4f923-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="4f923-113">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="4f923-113">Return value</span></span>
------------

<span data-ttu-id="4f923-114">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="4f923-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4f923-115">Замечания</span><span class="sxs-lookup"><span data-stu-id="4f923-115">Remarks</span></span>

<span data-ttu-id="4f923-116">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="4f923-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4f923-117">Требования</span><span class="sxs-lookup"><span data-stu-id="4f923-117">Requirements</span></span>
------------
><span data-ttu-id="4f923-118">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4f923-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4f923-119">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4f923-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4f923-120">См. также:</span><span class="sxs-lookup"><span data-stu-id="4f923-120">See also</span></span>


[<span data-ttu-id="4f923-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4f923-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



