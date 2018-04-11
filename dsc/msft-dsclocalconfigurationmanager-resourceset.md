---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод ResourceSet класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b5f437a123bd38df21f30d11e71d2c3b36bc9f3a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c3bd6-103">Метод ResourceSet класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c3bd6-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c3bd6-104">Напрямую вызывает метод **Set** ресурса DSC.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="c3bd6-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c3bd6-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="c3bd6-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="c3bd6-106">Parameters</span></span>
----------

<span data-ttu-id="c3bd6-107">*ResourceType* \[in\] Имя вызываемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="c3bd6-108">*ModuleName* \[in\] Имя модуля, содержащего вызываемый ресурс.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="c3bd6-109">*resourceProperty* \[in\] Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="c3bd6-110">Используйте командлет [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="c3bd6-111">*RebootRequired* \[out\] В выходных данных это свойство имеет значение **true**, если целевой узел необходимо перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="c3bd6-112">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="c3bd6-112">Return value</span></span>
------------

<span data-ttu-id="c3bd6-113">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c3bd6-114">Замечания</span><span class="sxs-lookup"><span data-stu-id="c3bd6-114">Remarks</span></span>

<span data-ttu-id="c3bd6-115">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="c3bd6-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c3bd6-116">Требования</span><span class="sxs-lookup"><span data-stu-id="c3bd6-116">Requirements</span></span>
------------
><span data-ttu-id="c3bd6-117">**MOF-файл:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c3bd6-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="c3bd6-118">**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c3bd6-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="c3bd6-119">См. также:</span><span class="sxs-lookup"><span data-stu-id="c3bd6-119">See also</span></span>


[<span data-ttu-id="c3bd6-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c3bd6-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)