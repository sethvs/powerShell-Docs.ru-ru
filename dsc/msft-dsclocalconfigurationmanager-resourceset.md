---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ResourceSet класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 7291641098578226449f8cbd360da0a3f9842598
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="2dea6-103">Метод ResourceSet класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="2dea6-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="2dea6-104">Напрямую вызывает метод **Set** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="2dea6-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="2dea6-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="2dea6-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="2dea6-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="2dea6-106">Parameters</span></span>
----------

<span data-ttu-id="2dea6-107">*ResourceType* \[in\]</span><span class="sxs-lookup"><span data-stu-id="2dea6-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="2dea6-108">Имя вызываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2dea6-108">The name of the resource to call.</span></span>

<span data-ttu-id="2dea6-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="2dea6-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="2dea6-110">Имя модуля, содержащего вызываемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="2dea6-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="2dea6-111">*resourceProperty* \[in\]</span><span class="sxs-lookup"><span data-stu-id="2dea6-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="2dea6-112">Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно.</span><span class="sxs-lookup"><span data-stu-id="2dea6-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="2dea6-113">Используйте командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.</span><span class="sxs-lookup"><span data-stu-id="2dea6-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="2dea6-114">*RebootRequired* \[out\]</span><span class="sxs-lookup"><span data-stu-id="2dea6-114">*RebootRequired* \[out\]</span></span>  
<span data-ttu-id="2dea6-115">В выходных данных это свойство имеет значение **true**, если целевой узел необходимо перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="2dea6-115">On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="2dea6-116">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="2dea6-116">Return value</span></span>
------------

<span data-ttu-id="2dea6-117">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="2dea6-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2dea6-118">Замечания</span><span class="sxs-lookup"><span data-stu-id="2dea6-118">Remarks</span></span>

<span data-ttu-id="2dea6-119">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="2dea6-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2dea6-120">Требования</span><span class="sxs-lookup"><span data-stu-id="2dea6-120">Requirements</span></span>
------------
><span data-ttu-id="2dea6-121">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2dea6-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="2dea6-122">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2dea6-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="2dea6-123">См. также:</span><span class="sxs-lookup"><span data-stu-id="2dea6-123">See also</span></span>


[<span data-ttu-id="2dea6-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2dea6-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 



