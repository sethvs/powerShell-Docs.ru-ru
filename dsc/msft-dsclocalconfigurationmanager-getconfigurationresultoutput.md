---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 09862fd3c19e1e517c9bf5df878113ba3f10d8a6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="52801-103">Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="52801-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="52801-104">Получает выходные данные агента конфигурации, относящиеся к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="52801-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="52801-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="52801-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="52801-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="52801-106">Parameters</span></span>
----------

<span data-ttu-id="52801-107">*jobId* \[in\]</span><span class="sxs-lookup"><span data-stu-id="52801-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="52801-108">Идентификатор задания, для которого необходимо получить выходные данные.</span><span class="sxs-lookup"><span data-stu-id="52801-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="52801-109">*resumeOutputBookmark* \[in\]</span><span class="sxs-lookup"><span data-stu-id="52801-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="52801-110">Указывает, что выходные данные должны быть продолжением от предыдущей закладки.</span><span class="sxs-lookup"><span data-stu-id="52801-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="52801-111">*output* \[out\]</span><span class="sxs-lookup"><span data-stu-id="52801-111">*output* \[out\]</span></span>  
<span data-ttu-id="52801-112">Выходные данные для указанного задания.</span><span class="sxs-lookup"><span data-stu-id="52801-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="52801-113">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="52801-113">Return value</span></span>
------------

<span data-ttu-id="52801-114">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="52801-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="52801-115">Замечания</span><span class="sxs-lookup"><span data-stu-id="52801-115">Remarks</span></span>

<span data-ttu-id="52801-116">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="52801-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="52801-117">Требования</span><span class="sxs-lookup"><span data-stu-id="52801-117">Requirements</span></span>
------------
><span data-ttu-id="52801-118">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="52801-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="52801-119">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="52801-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="52801-120">См. также:</span><span class="sxs-lookup"><span data-stu-id="52801-120">See also</span></span>


[<span data-ttu-id="52801-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="52801-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



