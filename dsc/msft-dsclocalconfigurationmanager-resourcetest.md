---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ResourceTest класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 3c88f74c5f623502e8cbe0d7aa7390fca75569a9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b1375-103">Метод ResourceTest класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="b1375-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b1375-104">Напрямую вызывает метод **Test** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="b1375-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="b1375-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b1375-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="b1375-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="b1375-106">Parameters</span></span>
----------

<span data-ttu-id="b1375-107">*ResourceType* \[in\]</span><span class="sxs-lookup"><span data-stu-id="b1375-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="b1375-108">Имя вызываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b1375-108">The name of the resource to call.</span></span>

<span data-ttu-id="b1375-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="b1375-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="b1375-110">Имя модуля, содержащего вызываемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="b1375-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="b1375-111">*resourceProperty* \[in\]</span><span class="sxs-lookup"><span data-stu-id="b1375-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="b1375-112">Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно.</span><span class="sxs-lookup"><span data-stu-id="b1375-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="b1375-113">Используйте командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.</span><span class="sxs-lookup"><span data-stu-id="b1375-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="b1375-114">*InDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="b1375-114">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="b1375-115">В выходных данных это свойство имеет значение **true**, если целевой узел находится в нужном состоянии.</span><span class="sxs-lookup"><span data-stu-id="b1375-115">On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="b1375-116">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="b1375-116">Return value</span></span>
------------

<span data-ttu-id="b1375-117">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="b1375-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b1375-118">Замечания</span><span class="sxs-lookup"><span data-stu-id="b1375-118">Remarks</span></span>

<span data-ttu-id="b1375-119">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="b1375-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b1375-120">Требования</span><span class="sxs-lookup"><span data-stu-id="b1375-120">Requirements</span></span>
------------
><span data-ttu-id="b1375-121">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b1375-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="b1375-122">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b1375-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="b1375-123">См. также:</span><span class="sxs-lookup"><span data-stu-id="b1375-123">See also</span></span>


[<span data-ttu-id="b1375-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b1375-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



