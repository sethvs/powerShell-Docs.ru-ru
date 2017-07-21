---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC WaitForAll"
ms.openlocfilehash: dcc23ad4e6905bc277ad39348350d5425fc90ad7
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="58101-103">Ресурс DSC WaitForAll</span><span class="sxs-lookup"><span data-stu-id="58101-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="58101-104">Область применения: Windows PowerShell 5.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="58101-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="58101-105">Ресурс настройки требуемого состояния **WaitForAll** можно использовать в блоке узла в [конфигурации DSC](configurations.md) для определения зависимостей от конфигураций на других узлах.</span><span class="sxs-lookup"><span data-stu-id="58101-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="58101-106">Этот ресурс выполняется успешно, если ресурс, указанный свойством **ResourceName**, находится в требуемом состоянии на всех целевых узлах, определенных в свойстве **NodeName**.</span><span class="sxs-lookup"><span data-stu-id="58101-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="58101-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="58101-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="58101-108">Свойства</span><span class="sxs-lookup"><span data-stu-id="58101-108">Properties</span></span>

|  <span data-ttu-id="58101-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="58101-109">Property</span></span>  |  <span data-ttu-id="58101-110">Описание</span><span class="sxs-lookup"><span data-stu-id="58101-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="58101-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="58101-111">ResourceName</span></span>| <span data-ttu-id="58101-112">Имя ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="58101-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="58101-113">NodeName</span><span class="sxs-lookup"><span data-stu-id="58101-113">NodeName</span></span>| <span data-ttu-id="58101-114">Целевые узлы ресурса, с которым настраивается отношение зависимости.</span><span class="sxs-lookup"><span data-stu-id="58101-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="58101-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="58101-115">RetryIntervalSec</span></span>| <span data-ttu-id="58101-116">Количество секунд перед повторной попыткой.</span><span class="sxs-lookup"><span data-stu-id="58101-116">The number of seconds before retrying.</span></span> <span data-ttu-id="58101-117">Минимальное значение — 1.</span><span class="sxs-lookup"><span data-stu-id="58101-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="58101-118">RetryCount</span><span class="sxs-lookup"><span data-stu-id="58101-118">RetryCount</span></span>| <span data-ttu-id="58101-119">Максимальное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="58101-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="58101-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="58101-120">ThrottleLimit</span></span>| <span data-ttu-id="58101-121">Количество одновременно подключаемых компьютеров.</span><span class="sxs-lookup"><span data-stu-id="58101-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="58101-122">Значение по умолчанию — New-CimSession.</span><span class="sxs-lookup"><span data-stu-id="58101-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="58101-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="58101-123">DependsOn</span></span> | <span data-ttu-id="58101-124">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="58101-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="58101-125">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="58101-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="58101-126">Пример</span><span class="sxs-lookup"><span data-stu-id="58101-126">Example</span></span>

<span data-ttu-id="58101-127">Пример использования этого ресурса см. в статье [Указание межузловых зависимостей](crossNodeDependencies.md).</span><span class="sxs-lookup"><span data-stu-id="58101-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>

