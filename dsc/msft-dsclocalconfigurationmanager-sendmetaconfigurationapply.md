---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 350555220757b1939b1de34ab423e963635eb53c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="58a2d-103">Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="58a2d-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="58a2d-104">Задает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="58a2d-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="58a2d-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="58a2d-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="58a2d-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="58a2d-106">Parameters</span></span>
----------

<span data-ttu-id="58a2d-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="58a2d-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="58a2d-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="58a2d-108">The environment data for the configuration.</span></span>

<span data-ttu-id="58a2d-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="58a2d-109">*force* \[in\]</span></span>  
<span data-ttu-id="58a2d-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="58a2d-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="58a2d-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="58a2d-111">Return value</span></span>
------------

<span data-ttu-id="58a2d-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="58a2d-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="58a2d-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="58a2d-113">Remarks</span></span>

<span data-ttu-id="58a2d-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="58a2d-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="58a2d-115">Требования</span><span class="sxs-lookup"><span data-stu-id="58a2d-115">Requirements</span></span>
------------
><span data-ttu-id="58a2d-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="58a2d-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="58a2d-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="58a2d-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="58a2d-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="58a2d-118">See also</span></span>


[<span data-ttu-id="58a2d-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="58a2d-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



