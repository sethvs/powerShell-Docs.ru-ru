---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 66d00cb40750e91e4b369a2e8cebb449697406d9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="06242-103">Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="06242-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="06242-104">Останавливает выполняемое изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="06242-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="06242-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="06242-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="06242-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="06242-106">Parameters</span></span>
----------

<span data-ttu-id="06242-107">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="06242-107">*force* \[in\]</span></span>  
<span data-ttu-id="06242-108">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="06242-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="06242-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="06242-109">Return value</span></span>
------------

<span data-ttu-id="06242-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="06242-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="06242-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="06242-111">Remarks</span></span>

<span data-ttu-id="06242-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="06242-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="06242-113">Требования</span><span class="sxs-lookup"><span data-stu-id="06242-113">Requirements</span></span>
------------
><span data-ttu-id="06242-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="06242-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="06242-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="06242-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="06242-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="06242-116">See also</span></span>


[<span data-ttu-id="06242-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="06242-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



