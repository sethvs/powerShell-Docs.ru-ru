---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Environment в DSC
ms.openlocfilehash: 4f024afe2d70c13e19406745ec7fd69821ab229b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-environment-resource"></a><span data-ttu-id="bf411-103">Ресурс Environment в DSC</span><span class="sxs-lookup"><span data-stu-id="bf411-103">DSC Environment Resource</span></span>

> <span data-ttu-id="bf411-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bf411-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="bf411-105">Ресурс __Environment__ в DSC Windows PowerShell предоставляет механизм управления системными переменными среды.</span><span class="sxs-lookup"><span data-stu-id="bf411-105">The __Environment__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables.</span></span>

## <a name="syntax"></a><span data-ttu-id="bf411-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="bf411-106">Syntax</span></span>
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="bf411-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="bf411-107">Properties</span></span>

|  <span data-ttu-id="bf411-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="bf411-108">Property</span></span>  |  <span data-ttu-id="bf411-109">Описание</span><span class="sxs-lookup"><span data-stu-id="bf411-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="bf411-110">Name</span><span class="sxs-lookup"><span data-stu-id="bf411-110">Name</span></span>| <span data-ttu-id="bf411-111">Указывает имя переменной среды, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="bf411-111">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="bf411-112">Ensure</span><span class="sxs-lookup"><span data-stu-id="bf411-112">Ensure</span></span>| <span data-ttu-id="bf411-113">Указывает, существует ли переменная.</span><span class="sxs-lookup"><span data-stu-id="bf411-113">Indicates if a variable exists.</span></span> <span data-ttu-id="bf411-114">Присвойте этому свойству значение __Present__, чтобы создать переменную среды, если она отсутствует, или убедиться, что ее значение соответствует значению свойства __Value__, если переменная уже существует.</span><span class="sxs-lookup"><span data-stu-id="bf411-114">Set this property to __Present__ to create the environment variable if it does not exist or to ensure that its value matches what is provided through the __Value__ property if the variable already exists.</span></span> <span data-ttu-id="bf411-115">Задайте значение __Absent__, чтобы удалить переменную, если она существует.</span><span class="sxs-lookup"><span data-stu-id="bf411-115">Set it to __Absent__ to delete the variable if it exists.</span></span>|
| <span data-ttu-id="bf411-116">путь</span><span class="sxs-lookup"><span data-stu-id="bf411-116">Path</span></span>| <span data-ttu-id="bf411-117">Определяет настраиваемую переменную среды.</span><span class="sxs-lookup"><span data-stu-id="bf411-117">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="bf411-118">Для переменной __Path__ присвойте этому свойству значение __$true__; для остальных переменных используйте значение __$false__.</span><span class="sxs-lookup"><span data-stu-id="bf411-118">Set this property to __$true__ if the variable is the __Path__ variable; otherwise, set it to __$false__.</span></span> <span data-ttu-id="bf411-119">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="bf411-119">The default is __$false__.</span></span> <span data-ttu-id="bf411-120">Если настраивается переменная __Path__, к существующему значению прикрепляется значение свойства __Value__.</span><span class="sxs-lookup"><span data-stu-id="bf411-120">If the variable being configured is the __Path__ variable, the value provided through the __Value__ property will be appended to the existing value.</span></span>|
| <span data-ttu-id="bf411-121">DependsOn</span><span class="sxs-lookup"><span data-stu-id="bf411-121">DependsOn</span></span> | <span data-ttu-id="bf411-122">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bf411-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="bf411-123">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="bf411-123">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="bf411-124">Значение</span><span class="sxs-lookup"><span data-stu-id="bf411-124">Value</span></span>| <span data-ttu-id="bf411-125">Значение, которое нужно присвоить переменной среды.</span><span class="sxs-lookup"><span data-stu-id="bf411-125">The value to assign to the environment variable.</span></span>|

## <a name="example"></a><span data-ttu-id="bf411-126">Пример</span><span class="sxs-lookup"><span data-stu-id="bf411-126">Example</span></span>

<span data-ttu-id="bf411-127">В следующем примере проверяется, существует ли переменная __TestEnvironmentVariable__ и имеет ли она значение __TestValue__.</span><span class="sxs-lookup"><span data-stu-id="bf411-127">The following example ensures that __TestEnvironmentVariable__ is present and it has the value __TestValue__.</span></span> <span data-ttu-id="bf411-128">Если переменная не существует, она создается.</span><span class="sxs-lookup"><span data-stu-id="bf411-128">If it is not present, it creates it.</span></span>

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```