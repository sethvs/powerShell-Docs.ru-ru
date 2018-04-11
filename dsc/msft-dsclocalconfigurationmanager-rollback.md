---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод RollBack класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c0a801c4037921e700e447d1434e246df0a63a4f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f5a82-103">Метод RollBack класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f5a82-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f5a82-104">Выполняет откат конфигурации к предыдущей версии.</span><span class="sxs-lookup"><span data-stu-id="f5a82-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="f5a82-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="f5a82-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="f5a82-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="f5a82-106">Parameters</span></span>
----------

<span data-ttu-id="f5a82-107">*configurationNumber* \[in\] Указывает запрошенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f5a82-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="f5a82-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="f5a82-108">Return value</span></span>
------------

<span data-ttu-id="f5a82-109">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="f5a82-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f5a82-110">Замечания</span><span class="sxs-lookup"><span data-stu-id="f5a82-110">Remarks</span></span>

<span data-ttu-id="f5a82-111">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="f5a82-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f5a82-112">Требования</span><span class="sxs-lookup"><span data-stu-id="f5a82-112">Requirements</span></span>
------------
><span data-ttu-id="f5a82-113">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f5a82-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="f5a82-114">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f5a82-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="f5a82-115">См. также:</span><span class="sxs-lookup"><span data-stu-id="f5a82-115">See also</span></span>


[<span data-ttu-id="f5a82-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f5a82-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)