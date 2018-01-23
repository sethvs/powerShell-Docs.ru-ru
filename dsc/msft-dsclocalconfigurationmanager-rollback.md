---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод RollBack класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: a219703389405c0dd457d0b2e0b1c54b9c28f559
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4eb29-103">Метод RollBack класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4eb29-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4eb29-104">Выполняет откат конфигурации к предыдущей версии.</span><span class="sxs-lookup"><span data-stu-id="4eb29-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="4eb29-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4eb29-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="4eb29-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="4eb29-106">Parameters</span></span>
----------

<span data-ttu-id="4eb29-107">*configurationNumber* \[in\]</span><span class="sxs-lookup"><span data-stu-id="4eb29-107">*configurationNumber* \[in\]</span></span>  
<span data-ttu-id="4eb29-108">Указывает запрошенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="4eb29-108">Specifies the requested configuration.</span></span> 

## <a name="return-value"></a><span data-ttu-id="4eb29-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="4eb29-109">Return value</span></span>
------------

<span data-ttu-id="4eb29-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="4eb29-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4eb29-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="4eb29-111">Remarks</span></span>

<span data-ttu-id="4eb29-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="4eb29-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4eb29-113">Требования</span><span class="sxs-lookup"><span data-stu-id="4eb29-113">Requirements</span></span>
------------
><span data-ttu-id="4eb29-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4eb29-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4eb29-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4eb29-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4eb29-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="4eb29-116">See also</span></span>


[<span data-ttu-id="4eb29-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4eb29-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



