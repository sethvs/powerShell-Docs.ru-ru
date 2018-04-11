---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: f4c2ddaa37cdafeff1a442f3f1fa656788a1c6c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="36867-103">Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="36867-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="36867-104">Получает выходные данные агента конфигурации, относящиеся к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="36867-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="36867-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="36867-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="36867-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="36867-106">Parameters</span></span>
----------

<span data-ttu-id="36867-107">*jobId* \[in\] Идентификатор задания, для которого необходимо получить выходные данные.</span><span class="sxs-lookup"><span data-stu-id="36867-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="36867-108">*resumeOutputBookmark* \[in\] Указывает, что выходные данные должны быть продолжением от предыдущей закладки.</span><span class="sxs-lookup"><span data-stu-id="36867-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="36867-109">*output* \[out\] Выходные данные для указанного задания.</span><span class="sxs-lookup"><span data-stu-id="36867-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="36867-110">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="36867-110">Return value</span></span>
------------

<span data-ttu-id="36867-111">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="36867-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="36867-112">Замечания</span><span class="sxs-lookup"><span data-stu-id="36867-112">Remarks</span></span>

<span data-ttu-id="36867-113">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="36867-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="36867-114">Требования</span><span class="sxs-lookup"><span data-stu-id="36867-114">Requirements</span></span>
------------
><span data-ttu-id="36867-115">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="36867-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="36867-116">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="36867-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="36867-117">См. также:</span><span class="sxs-lookup"><span data-stu-id="36867-117">See also</span></span>


[<span data-ttu-id="36867-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="36867-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)