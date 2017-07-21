---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: faa113c442b80eea3ac474220b098b7d80ec50a8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5aa1d-103">Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="5aa1d-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5aa1d-104">Удаляет файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5aa1d-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="5aa1d-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5aa1d-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="5aa1d-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="5aa1d-106">Parameters</span></span>
----------

<span data-ttu-id="5aa1d-107">*Stage* \[in\]</span><span class="sxs-lookup"><span data-stu-id="5aa1d-107">*Stage* \[in\]</span></span>  
<span data-ttu-id="5aa1d-108">Указывает, какой документ конфигурации необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="5aa1d-108">Specifies which configuration document to remove.</span></span> <span data-ttu-id="5aa1d-109">Допустимы следующие значения:</span><span class="sxs-lookup"><span data-stu-id="5aa1d-109">The following values are valid:</span></span>

|<span data-ttu-id="5aa1d-110">Значение</span><span class="sxs-lookup"><span data-stu-id="5aa1d-110">Value</span></span> |<span data-ttu-id="5aa1d-111">Описание</span><span class="sxs-lookup"><span data-stu-id="5aa1d-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="5aa1d-112">**1**</span><span class="sxs-lookup"><span data-stu-id="5aa1d-112">**1**</span></span> | <span data-ttu-id="5aa1d-113">Документ **текущей** конфигурации (current.mof).</span><span class="sxs-lookup"><span data-stu-id="5aa1d-113">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="5aa1d-114">**2**</span><span class="sxs-lookup"><span data-stu-id="5aa1d-114">**2**</span></span> | <span data-ttu-id="5aa1d-115">Документ **ожидающей** конфигурации (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="5aa1d-115">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="5aa1d-116">**4**</span><span class="sxs-lookup"><span data-stu-id="5aa1d-116">**4**</span></span> | <span data-ttu-id="5aa1d-117">Документ **предыдущей** конфигурации (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="5aa1d-117">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="5aa1d-118">*Force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="5aa1d-118">*Force* \[in\]</span></span>  
<span data-ttu-id="5aa1d-119">Значение **true** для принудительного удаления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5aa1d-119">**true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="5aa1d-120">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="5aa1d-120">Return value</span></span>
------------

<span data-ttu-id="5aa1d-121">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="5aa1d-121">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5aa1d-122">Замечания</span><span class="sxs-lookup"><span data-stu-id="5aa1d-122">Remarks</span></span>

<span data-ttu-id="5aa1d-123">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="5aa1d-123">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5aa1d-124">Требования</span><span class="sxs-lookup"><span data-stu-id="5aa1d-124">Requirements</span></span>
------------
><span data-ttu-id="5aa1d-125">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5aa1d-125">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5aa1d-126">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5aa1d-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5aa1d-127">См. также:</span><span class="sxs-lookup"><span data-stu-id="5aa1d-127">See also</span></span>


[<span data-ttu-id="5aa1d-128">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5aa1d-128">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



