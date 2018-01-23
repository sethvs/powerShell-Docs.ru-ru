---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 20f732d35860cccde4e507dc6916e27d0cf8c5f6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="7b32b-103">Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="7b32b-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="7b32b-104">Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7b32b-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="7b32b-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7b32b-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="7b32b-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="7b32b-106">Parameters</span></span>
----------

<span data-ttu-id="7b32b-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="7b32b-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="7b32b-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7b32b-108">The environment data for the configuration.</span></span>

<span data-ttu-id="7b32b-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="7b32b-109">*force* \[in\]</span></span>  
<span data-ttu-id="7b32b-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7b32b-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="7b32b-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7b32b-111">Return value</span></span>
------------

<span data-ttu-id="7b32b-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="7b32b-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="7b32b-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="7b32b-113">Remarks</span></span>

<span data-ttu-id="7b32b-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="7b32b-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="7b32b-115">Требования</span><span class="sxs-lookup"><span data-stu-id="7b32b-115">Requirements</span></span>
------------
><span data-ttu-id="7b32b-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="7b32b-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="7b32b-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b32b-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="7b32b-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="7b32b-118">See also</span></span>


[<span data-ttu-id="7b32b-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="7b32b-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



