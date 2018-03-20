---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ResourceGet класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 2c055b3fab468f85c9e2f91cf1eaf1a4353b4660
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="88267-103">Метод ResourceGet класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="88267-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="88267-104">Напрямую вызывает метод **Get** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="88267-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="88267-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="88267-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="88267-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="88267-106">Parameters</span></span>
----------

<span data-ttu-id="88267-107">*ResourceType* \[in\]</span><span class="sxs-lookup"><span data-stu-id="88267-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="88267-108">Имя вызываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="88267-108">The name of the resource to call.</span></span>

<span data-ttu-id="88267-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="88267-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="88267-110">Имя модуля, содержащего вызываемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="88267-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="88267-111">*resourceProperty* \[in\]</span><span class="sxs-lookup"><span data-stu-id="88267-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="88267-112">Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно.</span><span class="sxs-lookup"><span data-stu-id="88267-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="88267-113">Используйте командлет [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.</span><span class="sxs-lookup"><span data-stu-id="88267-113">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="88267-114">*configurations* \[out\]</span><span class="sxs-lookup"><span data-stu-id="88267-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="88267-115">Выходные данные содержат встроенный экземпляр конфигураций.</span><span class="sxs-lookup"><span data-stu-id="88267-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="88267-116">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="88267-116">Return value</span></span>
------------

<span data-ttu-id="88267-117">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="88267-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="88267-118">Замечания</span><span class="sxs-lookup"><span data-stu-id="88267-118">Remarks</span></span>

<span data-ttu-id="88267-119">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="88267-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="88267-120">Требования</span><span class="sxs-lookup"><span data-stu-id="88267-120">Requirements</span></span>
------------
><span data-ttu-id="88267-121">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="88267-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="88267-122">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="88267-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="88267-123">См. также:</span><span class="sxs-lookup"><span data-stu-id="88267-123">See also</span></span>


[<span data-ttu-id="88267-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="88267-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



