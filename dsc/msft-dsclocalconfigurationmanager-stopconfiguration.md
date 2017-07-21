---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: f0b550615b20f07f99c8ed7009805c45794bfe22
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e2650-103">Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e2650-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e2650-104">Останавливает выполняемое изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2650-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="e2650-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="e2650-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="e2650-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="e2650-106">Parameters</span></span>
----------

<span data-ttu-id="e2650-107">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="e2650-107">*force* \[in\]</span></span>  
<span data-ttu-id="e2650-108">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2650-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="e2650-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="e2650-109">Return value</span></span>
------------

<span data-ttu-id="e2650-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="e2650-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e2650-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="e2650-111">Remarks</span></span>

<span data-ttu-id="e2650-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="e2650-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e2650-113">Требования</span><span class="sxs-lookup"><span data-stu-id="e2650-113">Requirements</span></span>
------------
><span data-ttu-id="e2650-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e2650-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e2650-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e2650-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e2650-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="e2650-116">See also</span></span>


[<span data-ttu-id="e2650-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e2650-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



