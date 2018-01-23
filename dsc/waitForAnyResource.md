---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForAny"
ms.openlocfilehash: 795c005c67c196ef9afb08af790fe2a1695392ec
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="529ec-103">Ресурс DSC WaitForAny</span><span class="sxs-lookup"><span data-stu-id="529ec-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="529ec-104">Область применения: Windows PowerShell 5.1 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="529ec-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="529ec-105">Ресурс настройки требуемого состояния **WaitForSome** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.</span><span class="sxs-lookup"><span data-stu-id="529ec-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="529ec-106">Этот ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на всех целевых узлах, определенных в свойстве **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="529ec-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="529ec-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="529ec-107">Syntax</span></span>

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="529ec-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="529ec-108">Properties</span></span>

|  <span data-ttu-id="529ec-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="529ec-109">Property</span></span>  |  <span data-ttu-id="529ec-110">Описание</span><span class="sxs-lookup"><span data-stu-id="529ec-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="529ec-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="529ec-111">ResourceName</span></span>| <span data-ttu-id="529ec-112">Имя ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="529ec-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="529ec-113">NodeName</span><span class="sxs-lookup"><span data-stu-id="529ec-113">NodeName</span></span>| <span data-ttu-id="529ec-114">Целевые узлы ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="529ec-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="529ec-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="529ec-115">RetryIntervalSec</span></span>| <span data-ttu-id="529ec-116">Количество секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="529ec-116">The number of seconds before retrying.</span></span> <span data-ttu-id="529ec-117">Минимальное значение — 1.</span><span class="sxs-lookup"><span data-stu-id="529ec-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="529ec-118">RetryCount</span><span class="sxs-lookup"><span data-stu-id="529ec-118">RetryCount</span></span>| <span data-ttu-id="529ec-119">Максимальное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="529ec-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="529ec-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="529ec-120">ThrottleLimit</span></span>| <span data-ttu-id="529ec-121">Количество одновременно подключаемых компьютеров.</span><span class="sxs-lookup"><span data-stu-id="529ec-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="529ec-122">Значение по умолчанию — New-CimSession.</span><span class="sxs-lookup"><span data-stu-id="529ec-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="529ec-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="529ec-123">DependsOn</span></span> | <span data-ttu-id="529ec-124">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="529ec-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="529ec-125">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="529ec-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="529ec-126">Пример</span><span class="sxs-lookup"><span data-stu-id="529ec-126">Example</span></span>

<span data-ttu-id="529ec-127">Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).</span><span class="sxs-lookup"><span data-stu-id="529ec-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

