---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetConfigurationStatus класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: a41e7a15fc935c2cd5fd4cb66d0ab13509d5d4e0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d6ca7-103">Метод GetConfigurationStatus класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d6ca7-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d6ca7-104">Получает журнал состояния конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6ca7-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="d6ca7-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="d6ca7-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="d6ca7-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="d6ca7-106">Parameters</span></span>
----------

<span data-ttu-id="d6ca7-107">*All* \[in\]</span><span class="sxs-lookup"><span data-stu-id="d6ca7-107">*All* \[in\]</span></span>  
<span data-ttu-id="d6ca7-108">Значение **true**, если этот метод должен возвращать сведения обо всех запусках конфигурации на компьютере, включая применение конфигурации и проверку согласованности.</span><span class="sxs-lookup"><span data-stu-id="d6ca7-108">**true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="d6ca7-109">*configurationStatus* \[out\]</span><span class="sxs-lookup"><span data-stu-id="d6ca7-109">*configurationStatus* \[out\]</span></span>  
<span data-ttu-id="d6ca7-110">Выходные данные содержат встроенный экземпляр класса **MSFT_DSCConfigurationStatus**, который определяет параметры.</span><span class="sxs-lookup"><span data-stu-id="d6ca7-110">On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="d6ca7-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="d6ca7-111">Return value</span></span>
------------

<span data-ttu-id="d6ca7-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="d6ca7-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d6ca7-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="d6ca7-113">Remarks</span></span>

<span data-ttu-id="d6ca7-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="d6ca7-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d6ca7-115">Требования</span><span class="sxs-lookup"><span data-stu-id="d6ca7-115">Requirements</span></span>
------------
><span data-ttu-id="d6ca7-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d6ca7-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d6ca7-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6ca7-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d6ca7-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="d6ca7-118">See also</span></span>


[<span data-ttu-id="d6ca7-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d6ca7-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



