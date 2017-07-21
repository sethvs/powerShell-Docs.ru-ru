---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForSome"
ms.openlocfilehash: 5d67a9111f6358240590b651e627ffb96abc0896
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="b596a-103">Ресурс DSC WaitForSome</span><span class="sxs-lookup"><span data-stu-id="b596a-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="b596a-104">Область применения: Windows PowerShell 5.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="b596a-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="b596a-105">Ресурс настройки требуемого состояния **WaitForAny** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.</span><span class="sxs-lookup"><span data-stu-id="b596a-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="b596a-106">Ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на минимальном числе узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="b596a-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span> 


## <a name="syntax"></a><span data-ttu-id="b596a-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="b596a-107">Syntax</span></span>

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    NodeCount = [Uint32]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="b596a-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="b596a-108">Properties</span></span>

|  <span data-ttu-id="b596a-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="b596a-109">Property</span></span>  |  <span data-ttu-id="b596a-110">Описание</span><span class="sxs-lookup"><span data-stu-id="b596a-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="b596a-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="b596a-111">ResourceName</span></span>| <span data-ttu-id="b596a-112">Имя ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="b596a-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="b596a-113">NodeName</span><span class="sxs-lookup"><span data-stu-id="b596a-113">NodeName</span></span>| <span data-ttu-id="b596a-114">Целевые узлы ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="b596a-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="b596a-115">NodeCount</span><span class="sxs-lookup"><span data-stu-id="b596a-115">NodeCount</span></span>| <span data-ttu-id="b596a-116">Минимальное количество узлов, которые должны быть в требуемом состоянии для успешного выполнения этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b596a-116">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="b596a-117">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="b596a-117">RetryIntervalSec</span></span>| <span data-ttu-id="b596a-118">Количество секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="b596a-118">The number of seconds before retrying.</span></span> <span data-ttu-id="b596a-119">Минимальное значение — 1.</span><span class="sxs-lookup"><span data-stu-id="b596a-119">Minimum is 1.</span></span>| 
| <span data-ttu-id="b596a-120">RetryCount</span><span class="sxs-lookup"><span data-stu-id="b596a-120">RetryCount</span></span>| <span data-ttu-id="b596a-121">Максимальное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="b596a-121">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="b596a-122">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="b596a-122">ThrottleLimit</span></span>| <span data-ttu-id="b596a-123">Количество одновременно подключаемых компьютеров.</span><span class="sxs-lookup"><span data-stu-id="b596a-123">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="b596a-124">Значение по умолчанию — New-CimSession.</span><span class="sxs-lookup"><span data-stu-id="b596a-124">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="b596a-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b596a-125">DependsOn</span></span> | <span data-ttu-id="b596a-126">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b596a-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b596a-127">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b596a-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="b596a-128">Пример</span><span class="sxs-lookup"><span data-stu-id="b596a-128">Example</span></span>

<span data-ttu-id="b596a-129">Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).</span><span class="sxs-lookup"><span data-stu-id="b596a-129">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

