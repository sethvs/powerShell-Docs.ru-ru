---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 96676a76a0302543e5e4a214c82ed952d7f52a71
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="bc3c1-103">Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="bc3c1-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="bc3c1-104">Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bc3c1-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="bc3c1-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="bc3c1-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="bc3c1-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="bc3c1-106">Parameters</span></span>
----------

<span data-ttu-id="bc3c1-107">*configurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="bc3c1-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="bc3c1-108">Указывает передаваемые данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bc3c1-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="bc3c1-109">*configurations* \[out\]</span><span class="sxs-lookup"><span data-stu-id="bc3c1-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="bc3c1-110">Выходные данные содержат встроенный экземпляр конфигураций.</span><span class="sxs-lookup"><span data-stu-id="bc3c1-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="bc3c1-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="bc3c1-111">Return value</span></span>
------------

<span data-ttu-id="bc3c1-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="bc3c1-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="bc3c1-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="bc3c1-113">Remarks</span></span>

<span data-ttu-id="bc3c1-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="bc3c1-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="bc3c1-115">Требования</span><span class="sxs-lookup"><span data-stu-id="bc3c1-115">Requirements</span></span>
------------
><span data-ttu-id="bc3c1-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="bc3c1-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="bc3c1-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="bc3c1-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="bc3c1-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="bc3c1-118">See also</span></span>


[<span data-ttu-id="bc3c1-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="bc3c1-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 



