---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: fed45836293adedbce18f01cfe53cdfa1a474975
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="2f8f4-103">Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="2f8f4-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="2f8f4-104">Удаляет файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="2f8f4-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="2f8f4-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="2f8f4-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="2f8f4-106">Parameters</span></span>
----------

<span data-ttu-id="2f8f4-107">*Stage* \[in\]</span><span class="sxs-lookup"><span data-stu-id="2f8f4-107">*Stage* \[in\]</span></span>  
<span data-ttu-id="2f8f4-108">Указывает, какой документ конфигурации необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-108">Specifies which configuration document to remove.</span></span> <span data-ttu-id="2f8f4-109">Допустимы следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2f8f4-109">The following values are valid:</span></span>

|<span data-ttu-id="2f8f4-110">Значение</span><span class="sxs-lookup"><span data-stu-id="2f8f4-110">Value</span></span> |<span data-ttu-id="2f8f4-111">Описание</span><span class="sxs-lookup"><span data-stu-id="2f8f4-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="2f8f4-112">**1**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-112">**1**</span></span> | <span data-ttu-id="2f8f4-113">Документ **текущей** конфигурации (current.mof).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-113">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="2f8f4-114">**2**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-114">**2**</span></span> | <span data-ttu-id="2f8f4-115">Документ **ожидающей** конфигурации (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-115">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="2f8f4-116">**4**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-116">**4**</span></span> | <span data-ttu-id="2f8f4-117">Документ **предыдущей** конфигурации (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="2f8f4-117">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="2f8f4-118">*Force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="2f8f4-118">*Force* \[in\]</span></span>  
<span data-ttu-id="2f8f4-119">Значение **true** для принудительного удаления конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-119">**true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="2f8f4-120">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="2f8f4-120">Return value</span></span>
------------

<span data-ttu-id="2f8f4-121">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-121">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2f8f4-122">Замечания</span><span class="sxs-lookup"><span data-stu-id="2f8f4-122">Remarks</span></span>

<span data-ttu-id="2f8f4-123">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="2f8f4-123">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2f8f4-124">Требования</span><span class="sxs-lookup"><span data-stu-id="2f8f4-124">Requirements</span></span>
------------
><span data-ttu-id="2f8f4-125">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2f8f4-125">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="2f8f4-126">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2f8f4-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="2f8f4-127">См. также:</span><span class="sxs-lookup"><span data-stu-id="2f8f4-127">See also</span></span>


[<span data-ttu-id="2f8f4-128">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2f8f4-128">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



