---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: d8ddc9d99f0d74ad907a6e39ae0e8ac14159be16
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0d4df-103">Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="0d4df-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0d4df-104">Задает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0d4df-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="0d4df-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0d4df-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="0d4df-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="0d4df-106">Parameters</span></span>
----------

<span data-ttu-id="0d4df-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="0d4df-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="0d4df-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0d4df-108">The environment data for the configuration.</span></span>

<span data-ttu-id="0d4df-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="0d4df-109">*force* \[in\]</span></span>  
<span data-ttu-id="0d4df-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0d4df-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="0d4df-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="0d4df-111">Return value</span></span>
------------

<span data-ttu-id="0d4df-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="0d4df-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0d4df-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="0d4df-113">Remarks</span></span>

<span data-ttu-id="0d4df-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="0d4df-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0d4df-115">Требования</span><span class="sxs-lookup"><span data-stu-id="0d4df-115">Requirements</span></span>
------------
><span data-ttu-id="0d4df-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0d4df-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0d4df-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0d4df-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="0d4df-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="0d4df-118">See also</span></span>


[<span data-ttu-id="0d4df-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0d4df-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



