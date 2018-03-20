---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс DSC ServiceSet"
ms.openlocfilehash: 2488dda5212ccb717f7fd5d59ad62ec135ad13d5
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="5d5f5-103">Ресурс DSC ServiceSet</span><span class="sxs-lookup"><span data-stu-id="5d5f5-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="5d5f5-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5d5f5-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="5d5f5-105">Ресурс **ServiceSet** в DSC Windows PowerShell предоставляет механизм управления службами на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="5d5f5-106">Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс Service](serviceResource.md) для каждой службы, указанной в свойстве `Name`.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="5d5f5-107">Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких служб.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="5d5f5-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5d5f5-108">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="5d5f5-109">Свойства</span><span class="sxs-lookup"><span data-stu-id="5d5f5-109">Properties</span></span>

|  <span data-ttu-id="5d5f5-110">Свойство</span><span class="sxs-lookup"><span data-stu-id="5d5f5-110">Property</span></span>  |  <span data-ttu-id="5d5f5-111">Описание</span><span class="sxs-lookup"><span data-stu-id="5d5f5-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="5d5f5-112">Name</span><span class="sxs-lookup"><span data-stu-id="5d5f5-112">Name</span></span>| <span data-ttu-id="5d5f5-113">Указывает имена служб.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-113">Indicates the service names.</span></span> <span data-ttu-id="5d5f5-114">Обратите внимание на то, что иногда они отличаются от отображаемых имен.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="5d5f5-115">Список служб и их текущее состояние можно получить с помощью командлета [Get-Service](https://technet.microsoft.com/library/hh849804.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d5f5-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="5d5f5-116">StartupType</span><span class="sxs-lookup"><span data-stu-id="5d5f5-116">StartupType</span></span>| <span data-ttu-id="5d5f5-117">Указывает тип запуска службы.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="5d5f5-118">Допустимые значения этого свойства: **Automatic**, **Disabled** и **Manual**.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|  
| <span data-ttu-id="5d5f5-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="5d5f5-119">BuiltInAccount</span></span>| <span data-ttu-id="5d5f5-120">Указывает учетную запись, используемую службами для входа.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="5d5f5-121">Допустимые значения этого свойства: **LocalService**, **LocalSystem** и **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>| 
| <span data-ttu-id="5d5f5-122">State</span><span class="sxs-lookup"><span data-stu-id="5d5f5-122">State</span></span>| <span data-ttu-id="5d5f5-123">Указывает состояние, в котором должны находиться службы: **Stopped** или **Running**.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>| 
| <span data-ttu-id="5d5f5-124">Ensure</span><span class="sxs-lookup"><span data-stu-id="5d5f5-124">Ensure</span></span>| <span data-ttu-id="5d5f5-125">Указывает, имеются ли службы в системе.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="5d5f5-126">Если службы не должны существовать, присвойте этому свойству значение **Absent**.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="5d5f5-127">Если целевые службы должны существовать, укажите значение **Present** (используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5d5f5-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="5d5f5-128">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="5d5f5-128">Credential</span></span>| <span data-ttu-id="5d5f5-129">Указывает учетные данные для учетной записи, от имени которой будет запускаться ресурс службы.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="5d5f5-130">Это свойство нельзя использовать одновременно со свойством **BuiltinAccount**.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>| 
| <span data-ttu-id="5d5f5-131">DependsOn</span><span class="sxs-lookup"><span data-stu-id="5d5f5-131">DependsOn</span></span>| <span data-ttu-id="5d5f5-132">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5d5f5-133">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — *ResourceName*, а его тип — *ResourceType*, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5d5f5-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 



## <a name="example"></a><span data-ttu-id="5d5f5-134">Пример</span><span class="sxs-lookup"><span data-stu-id="5d5f5-134">Example</span></span>

<span data-ttu-id="5d5f5-135">Приведенная ниже конфигурация запускает службы "Windows Audio" и "Службы удаленных рабочих столов".</span><span class="sxs-lookup"><span data-stu-id="5d5f5-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```

