---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: febaf972a2a452eb9aaf3ec7fbc5e41f3f463a58
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="44f85-103">Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="44f85-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="44f85-104">Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="44f85-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span> 

<span data-ttu-id="44f85-105">Если нет ожидающих конфигураций, этот метод повторно применяет текущую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="44f85-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="44f85-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="44f85-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="44f85-107">Параметры</span><span class="sxs-lookup"><span data-stu-id="44f85-107">Parameters</span></span>
----------

<span data-ttu-id="44f85-108">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="44f85-108">*force* \[in\]</span></span>  
<span data-ttu-id="44f85-109">Если параметр имеет значение **true**, текущая конфигурация применяется повторно даже при наличии конфигурации в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="44f85-109">If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="44f85-110">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="44f85-110">Return value</span></span>
------------

<span data-ttu-id="44f85-111">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="44f85-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="44f85-112">Замечания</span><span class="sxs-lookup"><span data-stu-id="44f85-112">Remarks</span></span>

<span data-ttu-id="44f85-113">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="44f85-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="44f85-114">Требования</span><span class="sxs-lookup"><span data-stu-id="44f85-114">Requirements</span></span>
------------
><span data-ttu-id="44f85-115">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="44f85-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="44f85-116">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="44f85-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="44f85-117">См. также:</span><span class="sxs-lookup"><span data-stu-id="44f85-117">See also</span></span>


[<span data-ttu-id="44f85-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="44f85-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



