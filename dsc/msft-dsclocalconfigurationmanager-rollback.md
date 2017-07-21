---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод RollBack класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: b8597e3eb7872d9894863fb02d927c9f475da44c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="02e3c-103">Метод RollBack класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="02e3c-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="02e3c-104">Выполняет откат конфигурации к предыдущей версии.</span><span class="sxs-lookup"><span data-stu-id="02e3c-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="02e3c-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="02e3c-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="02e3c-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="02e3c-106">Parameters</span></span>
----------

<span data-ttu-id="02e3c-107">*configurationNumber* \[in\]</span><span class="sxs-lookup"><span data-stu-id="02e3c-107">*configurationNumber* \[in\]</span></span>  
<span data-ttu-id="02e3c-108">Указывает запрошенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="02e3c-108">Specifies the requested configuration.</span></span> 

## <a name="return-value"></a><span data-ttu-id="02e3c-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="02e3c-109">Return value</span></span>
------------

<span data-ttu-id="02e3c-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="02e3c-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="02e3c-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="02e3c-111">Remarks</span></span>

<span data-ttu-id="02e3c-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="02e3c-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="02e3c-113">Требования</span><span class="sxs-lookup"><span data-stu-id="02e3c-113">Requirements</span></span>
------------
><span data-ttu-id="02e3c-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="02e3c-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="02e3c-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="02e3c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="02e3c-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="02e3c-116">See also</span></span>


[<span data-ttu-id="02e3c-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="02e3c-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



