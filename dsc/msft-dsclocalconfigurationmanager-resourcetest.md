---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод ResourceTest класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: f03a034329a9cde5cd44dbaf42ba1789c2b8f4f9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cc61c-103">Метод ResourceTest класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="cc61c-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cc61c-104">Напрямую вызывает метод **Test** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="cc61c-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="cc61c-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="cc61c-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="cc61c-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc61c-106">Parameters</span></span>
----------

<span data-ttu-id="cc61c-107">*ResourceType* \[in\] Имя вызываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="cc61c-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="cc61c-108">*ModuleName* \[in\] Имя модуля, содержащего вызываемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="cc61c-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="cc61c-109">*resourceProperty* \[in\] Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно.</span><span class="sxs-lookup"><span data-stu-id="cc61c-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="cc61c-110">Используйте командлет [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.</span><span class="sxs-lookup"><span data-stu-id="cc61c-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="cc61c-111">*InDesiredState* \[out\] В выходных данных это свойство имеет значение **true**, если целевой узел находится в нужном состоянии.</span><span class="sxs-lookup"><span data-stu-id="cc61c-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="cc61c-112">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="cc61c-112">Return value</span></span>
------------

<span data-ttu-id="cc61c-113">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="cc61c-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cc61c-114">Замечания</span><span class="sxs-lookup"><span data-stu-id="cc61c-114">Remarks</span></span>

<span data-ttu-id="cc61c-115">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="cc61c-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cc61c-116">Требования</span><span class="sxs-lookup"><span data-stu-id="cc61c-116">Requirements</span></span>
------------
><span data-ttu-id="cc61c-117">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cc61c-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="cc61c-118">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cc61c-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="cc61c-119">См. также:</span><span class="sxs-lookup"><span data-stu-id="cc61c-119">See also</span></span>


[<span data-ttu-id="cc61c-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cc61c-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)