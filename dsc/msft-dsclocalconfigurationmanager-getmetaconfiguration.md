---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 695be4ee6490567295fda0cc44635870362d24b8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4db66-103">Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4db66-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4db66-104">Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4db66-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="4db66-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4db66-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="4db66-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="4db66-106">Parameters</span></span>
----------

<span data-ttu-id="4db66-107">*MetaConfiguration* \[out\]</span><span class="sxs-lookup"><span data-stu-id="4db66-107">*MetaConfiguration* \[out\]</span></span>  
<span data-ttu-id="4db66-108">Выходные данные содержат встроенный экземпляр класса **MSFT_DSCMetaConfiguration**, который определяет параметры.</span><span class="sxs-lookup"><span data-stu-id="4db66-108">On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="4db66-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="4db66-109">Return value</span></span>
------------

<span data-ttu-id="4db66-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="4db66-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4db66-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="4db66-111">Remarks</span></span>

<span data-ttu-id="4db66-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="4db66-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4db66-113">Требования</span><span class="sxs-lookup"><span data-stu-id="4db66-113">Requirements</span></span>
------------
><span data-ttu-id="4db66-114">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4db66-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4db66-115">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4db66-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4db66-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="4db66-116">See also</span></span>


[<span data-ttu-id="4db66-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4db66-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



