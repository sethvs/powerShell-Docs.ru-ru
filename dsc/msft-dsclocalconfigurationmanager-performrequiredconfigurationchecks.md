---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 26110b3920104da7343b8d55cf63440c12accbbc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6dc62-103">Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="6dc62-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6dc62-104">Запускает проверку согласованности с помощью планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="6dc62-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="6dc62-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6dc62-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="6dc62-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="6dc62-106">Parameters</span></span>
----------

<span data-ttu-id="6dc62-107">*Flags* \[in\]</span><span class="sxs-lookup"><span data-stu-id="6dc62-107">*Flags* \[in\]</span></span>  
<span data-ttu-id="6dc62-108">Битовая маска, определяющая тип выполняемой проверки согласованности.</span><span class="sxs-lookup"><span data-stu-id="6dc62-108">A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="6dc62-109">Допустимы следующие значения, которые можно объединить с помощью битовой операции **OR**:</span><span class="sxs-lookup"><span data-stu-id="6dc62-109">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="6dc62-110">Значение</span><span class="sxs-lookup"><span data-stu-id="6dc62-110">Value</span></span> |<span data-ttu-id="6dc62-111">Описание</span><span class="sxs-lookup"><span data-stu-id="6dc62-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="6dc62-112">**1**</span><span class="sxs-lookup"><span data-stu-id="6dc62-112">**1**</span></span> | <span data-ttu-id="6dc62-113">Обычная проверка согласованности.</span><span class="sxs-lookup"><span data-stu-id="6dc62-113">A normal consistency check.</span></span> |
|<span data-ttu-id="6dc62-114">**2**</span><span class="sxs-lookup"><span data-stu-id="6dc62-114">**2**</span></span> | <span data-ttu-id="6dc62-115">Продолжение проверки согласованности после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="6dc62-115">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="6dc62-116">Это значение не следует использовать в сочетании с другими значениями.</span><span class="sxs-lookup"><span data-stu-id="6dc62-116">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="6dc62-117">**4**</span><span class="sxs-lookup"><span data-stu-id="6dc62-117">**4**</span></span> | <span data-ttu-id="6dc62-118">Конфигурация должна извлекаться с запрашивающего сервера, указанного в метаконфигурации для узла.</span><span class="sxs-lookup"><span data-stu-id="6dc62-118">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="6dc62-119">Это значение следует всегда использовать в сочетании с **1**, если указано значение **5**.</span><span class="sxs-lookup"><span data-stu-id="6dc62-119">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="6dc62-120">**8**</span><span class="sxs-lookup"><span data-stu-id="6dc62-120">**8**</span></span> | <span data-ttu-id="6dc62-121">Состояние отправки на сервер отчетов.</span><span class="sxs-lookup"><span data-stu-id="6dc62-121">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="6dc62-122">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6dc62-122">Return value</span></span>
------------

<span data-ttu-id="6dc62-123">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="6dc62-123">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6dc62-124">Замечания</span><span class="sxs-lookup"><span data-stu-id="6dc62-124">Remarks</span></span>

<span data-ttu-id="6dc62-125">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="6dc62-125">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6dc62-126">Требования</span><span class="sxs-lookup"><span data-stu-id="6dc62-126">Requirements</span></span>
------------
><span data-ttu-id="6dc62-127">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6dc62-127">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="6dc62-128">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6dc62-128">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="6dc62-129">См. также:</span><span class="sxs-lookup"><span data-stu-id="6dc62-129">See also</span></span>


[<span data-ttu-id="6dc62-130">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6dc62-130">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



