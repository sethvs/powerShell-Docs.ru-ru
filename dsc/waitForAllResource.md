---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForAll"
ms.openlocfilehash: 2b6d9e11acd429eecb30926316d1033331524edc
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="87705-103">Ресурс DSC WaitForAll</span><span class="sxs-lookup"><span data-stu-id="87705-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="87705-104">Область применения: Windows PowerShell 5.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="87705-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="87705-105">Ресурс настройки требуемого состояния **WaitForAll** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.</span><span class="sxs-lookup"><span data-stu-id="87705-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="87705-106">Этот ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на всех целевых узлах, определенных в свойстве **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="87705-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="87705-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="87705-107">Syntax</span></span>

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="87705-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="87705-108">Properties</span></span>

|  <span data-ttu-id="87705-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="87705-109">Property</span></span>  |  <span data-ttu-id="87705-110">Описание</span><span class="sxs-lookup"><span data-stu-id="87705-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="87705-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="87705-111">ResourceName</span></span>| <span data-ttu-id="87705-112">Имя ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="87705-112">The resource name to depend on.</span></span> <span data-ttu-id="87705-113">Если этот ресурс принадлежит другой конфигурации, имя следует указать в формате "[__тип ресурса__]__имя ресурса__::[__имя конфигурации__]::[__имя конфигурации__]".</span><span class="sxs-lookup"><span data-stu-id="87705-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>| 
| <span data-ttu-id="87705-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="87705-114">NodeName</span></span>| <span data-ttu-id="87705-115">Целевые узлы ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="87705-115">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="87705-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="87705-116">RetryIntervalSec</span></span>| <span data-ttu-id="87705-117">Количество секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="87705-117">The number of seconds before retrying.</span></span> <span data-ttu-id="87705-118">Минимальное значение — 1.</span><span class="sxs-lookup"><span data-stu-id="87705-118">Minimum is 1.</span></span>| 
| <span data-ttu-id="87705-119">RetryCount</span><span class="sxs-lookup"><span data-stu-id="87705-119">RetryCount</span></span>| <span data-ttu-id="87705-120">Максимальное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="87705-120">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="87705-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="87705-121">ThrottleLimit</span></span>| <span data-ttu-id="87705-122">Количество одновременно подключаемых компьютеров.</span><span class="sxs-lookup"><span data-stu-id="87705-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="87705-123">Значение по умолчанию — New-CimSession.</span><span class="sxs-lookup"><span data-stu-id="87705-123">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="87705-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="87705-124">DependsOn</span></span> | <span data-ttu-id="87705-125">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="87705-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="87705-126">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="87705-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="87705-127">Пример</span><span class="sxs-lookup"><span data-stu-id="87705-127">Example</span></span>

<span data-ttu-id="87705-128">Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).</span><span class="sxs-lookup"><span data-stu-id="87705-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

