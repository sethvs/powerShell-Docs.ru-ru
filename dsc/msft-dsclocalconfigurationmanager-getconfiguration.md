---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 60f4b49575dbb28ce74af0500e6982ec5d2e7a66
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ef1d8-103">Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ef1d8-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ef1d8-104">Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ef1d8-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="ef1d8-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ef1d8-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="ef1d8-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="ef1d8-106">Parameters</span></span>
----------

<span data-ttu-id="ef1d8-107">*configurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="ef1d8-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="ef1d8-108">Указывает передаваемые данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ef1d8-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="ef1d8-109">*configurations* \[out\]</span><span class="sxs-lookup"><span data-stu-id="ef1d8-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="ef1d8-110">Выходные данные содержат встроенный экземпляр конфигураций.</span><span class="sxs-lookup"><span data-stu-id="ef1d8-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="ef1d8-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="ef1d8-111">Return value</span></span>
------------

<span data-ttu-id="ef1d8-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="ef1d8-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ef1d8-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="ef1d8-113">Remarks</span></span>

<span data-ttu-id="ef1d8-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="ef1d8-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ef1d8-115">Требования</span><span class="sxs-lookup"><span data-stu-id="ef1d8-115">Requirements</span></span>
------------
><span data-ttu-id="ef1d8-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ef1d8-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ef1d8-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ef1d8-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="ef1d8-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="ef1d8-118">See also</span></span>


[<span data-ttu-id="ef1d8-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ef1d8-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



