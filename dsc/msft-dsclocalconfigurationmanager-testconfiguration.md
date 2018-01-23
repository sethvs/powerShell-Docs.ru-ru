---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод TestConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 04f0f3146473dc71f492086449d9dce5467c55db
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="57d14-103">Метод TestConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="57d14-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="57d14-104">Отправляет документ конфигурации на управляемый узел и проверяет соответствие текущей конфигурации документу.</span><span class="sxs-lookup"><span data-stu-id="57d14-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="57d14-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="57d14-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="57d14-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="57d14-106">Parameters</span></span>
----------

<span data-ttu-id="57d14-107">*configurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="57d14-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="57d14-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57d14-108">Environment data for the confuguration.</span></span>

<span data-ttu-id="57d14-109">*InDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="57d14-109">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="57d14-110">В выходных данных указывает, находится ли управляемый узел в состоянии, указанном в документе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57d14-110">On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="57d14-111">*ResourcesInDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="57d14-111">*ResourcesInDesiredState* \[out\]</span></span>  
<span data-ttu-id="57d14-112">Выходные данные содержат встроенный экземпляр класса **MSFT_ResourceInDesiredState**, указывающий ресурсы, которые находятся в нужном состоянии.</span><span class="sxs-lookup"><span data-stu-id="57d14-112">On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="57d14-113">*ResourcesNotInDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="57d14-113">*ResourcesNotInDesiredState* \[out\]</span></span>  
<span data-ttu-id="57d14-114">Выходные данные содержат встроенный экземпляр класса **MSFT_ResourceNotInDesiredState**, указывающий ресурсы, которые не находятся в нужном состоянии.</span><span class="sxs-lookup"><span data-stu-id="57d14-114">On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="57d14-115">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="57d14-115">Return value</span></span>
------------

<span data-ttu-id="57d14-116">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="57d14-116">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="57d14-117">Замечания</span><span class="sxs-lookup"><span data-stu-id="57d14-117">Remarks</span></span>

<span data-ttu-id="57d14-118">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="57d14-118">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="57d14-119">Требования</span><span class="sxs-lookup"><span data-stu-id="57d14-119">Requirements</span></span>
------------
><span data-ttu-id="57d14-120">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="57d14-120">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="57d14-121">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="57d14-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="57d14-122">См. также:</span><span class="sxs-lookup"><span data-stu-id="57d14-122">See also</span></span>


[<span data-ttu-id="57d14-123">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="57d14-123">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



