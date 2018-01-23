---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 72c59b5aad293fa561146e5ad6822f27f40f321f
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c14fa-103">Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c14fa-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c14fa-104">Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.</span><span class="sxs-lookup"><span data-stu-id="c14fa-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="c14fa-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c14fa-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="c14fa-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="c14fa-106">Parameters</span></span>
----------

<span data-ttu-id="c14fa-107">*ConfigurationData* \[in\]</span><span class="sxs-lookup"><span data-stu-id="c14fa-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="c14fa-108">Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c14fa-108">The environment data for the configuration.</span></span>

<span data-ttu-id="c14fa-109">*force* \[in\]</span><span class="sxs-lookup"><span data-stu-id="c14fa-109">*force* \[in\]</span></span>  
<span data-ttu-id="c14fa-110">Значение **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c14fa-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="c14fa-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="c14fa-111">Return value</span></span>
------------

<span data-ttu-id="c14fa-112">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="c14fa-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c14fa-113">Замечания</span><span class="sxs-lookup"><span data-stu-id="c14fa-113">Remarks</span></span>

<span data-ttu-id="c14fa-114">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="c14fa-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c14fa-115">Требования</span><span class="sxs-lookup"><span data-stu-id="c14fa-115">Requirements</span></span>
------------
><span data-ttu-id="c14fa-116">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c14fa-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="c14fa-117">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c14fa-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="c14fa-118">См. также:</span><span class="sxs-lookup"><span data-stu-id="c14fa-118">See also</span></span>


[<span data-ttu-id="c14fa-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c14fa-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



