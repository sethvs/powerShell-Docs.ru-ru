---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс nxEnvironment в DSC для Linux"
ms.openlocfilehash: 61e0c7e77e486cea878351f1929d73f1f80710d8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxenvironment-resource"></a><span data-ttu-id="504e4-103">Ресурс nxEnvironment в DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="504e4-103">DSC for Linux nxEnvironment Resource</span></span>

<span data-ttu-id="504e4-104">Ресурс **nxEnvironment** в DSC PowerShell предоставляет механизм управления системными переменными среды на узле Linux.</span><span class="sxs-lookup"><span data-stu-id="504e4-104">The **nxEnvironment** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage system environment variables on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="504e4-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="504e4-105">Syntax</span></span>

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="504e4-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="504e4-106">Properties</span></span>

|  <span data-ttu-id="504e4-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="504e4-107">Property</span></span> |  <span data-ttu-id="504e4-108">Описание</span><span class="sxs-lookup"><span data-stu-id="504e4-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="504e4-109">Name</span><span class="sxs-lookup"><span data-stu-id="504e4-109">Name</span></span>| <span data-ttu-id="504e4-110">Указывает имя переменной среды, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="504e4-110">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="504e4-111">Значение</span><span class="sxs-lookup"><span data-stu-id="504e4-111">Value</span></span>| <span data-ttu-id="504e4-112">Значение, которое нужно присвоить переменной среды.</span><span class="sxs-lookup"><span data-stu-id="504e4-112">The value to assign to the environment variable.</span></span>| 
| <span data-ttu-id="504e4-113">Ensure</span><span class="sxs-lookup"><span data-stu-id="504e4-113">Ensure</span></span>| <span data-ttu-id="504e4-114">Определяет, нужно ли проверять существование переменной.</span><span class="sxs-lookup"><span data-stu-id="504e4-114">Determines whether to check if the variable exists.</span></span> <span data-ttu-id="504e4-115">Чтобы убедиться, что переменная существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="504e4-115">Set this property to "Present" to ensure the variable exists.</span></span> <span data-ttu-id="504e4-116">Чтобы убедиться, что переменная не существует, укажите для этого свойства значение Absent.</span><span class="sxs-lookup"><span data-stu-id="504e4-116">Set it to "Absent" to ensure the variable does not exist.</span></span> <span data-ttu-id="504e4-117">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="504e4-117">The default value is "Present".</span></span>| 
| <span data-ttu-id="504e4-118">путь</span><span class="sxs-lookup"><span data-stu-id="504e4-118">Path</span></span>| <span data-ttu-id="504e4-119">Определяет настраиваемую переменную среды.</span><span class="sxs-lookup"><span data-stu-id="504e4-119">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="504e4-120">Для переменной **Path** присвойте этому свойству значение **$true**; для остальных переменных используйте значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="504e4-120">Set this property to **$true** if the variable is the **Path** variable; otherwise, set it to **$false**.</span></span> <span data-ttu-id="504e4-121">Значение по умолчанию — **$false**.</span><span class="sxs-lookup"><span data-stu-id="504e4-121">The default is **$false**.</span></span> <span data-ttu-id="504e4-122">Если настраивается переменная **Path**, к существующему значению прикрепляется значение свойства **Value**.</span><span class="sxs-lookup"><span data-stu-id="504e4-122">If the variable being configured is the **Path** variable, the value provided through the **Value** property will be appended to the existing value.</span></span>| 
| <span data-ttu-id="504e4-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="504e4-123">DependsOn</span></span> | <span data-ttu-id="504e4-124">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="504e4-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="504e4-125">Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="504e4-125">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="additional-information"></a><span data-ttu-id="504e4-126">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="504e4-126">Additional Information</span></span>

* <span data-ttu-id="504e4-127">Если свойство **Path** не задано или имеет значение **$false**, управление переменными среды осуществляется в файле `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="504e4-127">If **Path** is absent or set to **$false**, environment variables are managed in `/etc/environment`.</span></span> <span data-ttu-id="504e4-128">Для доступа к управляемым переменным среды может потребоваться настроить файл `/etc/environment` в качестве источника для программ или сценариев.</span><span class="sxs-lookup"><span data-stu-id="504e4-128">Your programs or scripts may require configuration to source the `/etc/environment` file to access the managed environment variables.</span></span>
* <span data-ttu-id="504e4-129">Если свойство **Path** имеет значение **$true**, управление переменными среды осуществляется в файле `/etc/profile.d/DSCenvironment.sh`.</span><span class="sxs-lookup"><span data-stu-id="504e4-129">If **Path** is set to **$true**, the environment variable is managed in the file `/etc/profile.d/DSCenvironment.sh`.</span></span> <span data-ttu-id="504e4-130">Если этот файл не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="504e4-130">This file will be created if it does not exist.</span></span> <span data-ttu-id="504e4-131">Если свойство **Ensure** имеет значение Absent, а свойство **Path** — значение **$true**, существующая переменная среды будет удалена только из файла `/etc/profile.d/DSCenvironment.sh`; остальные файлы затронуты не будут.</span><span class="sxs-lookup"><span data-stu-id="504e4-131">If **Ensure** is set to "Absent" and **Path** is set to **$true**, an existing environment variable will only be removed from `/etc/profile.d/DSCenvironment.sh` and not from other files.</span></span>

## <a name="example"></a><span data-ttu-id="504e4-132">Пример</span><span class="sxs-lookup"><span data-stu-id="504e4-132">Example</span></span>

<span data-ttu-id="504e4-133">В следующем примере показано, как использовать ресурс **nxEnvironment**, чтобы убедиться, что переменная **TestEnvironmentVariable** существует и имеет значение Test-Value.</span><span class="sxs-lookup"><span data-stu-id="504e4-133">The following example shows how to use the **nxEnvironment** resource to ensure that **TestEnvironmentVariable** is present and has the value "Test-Value".</span></span> <span data-ttu-id="504e4-134">Если переменная **TestEnvironmentVariable** не существует, она будет создана.</span><span class="sxs-lookup"><span data-stu-id="504e4-134">If **TestEnvironmentVariable** is not present, it will be created.</span></span>

```
Import-DSCResource -Module nx 


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```


