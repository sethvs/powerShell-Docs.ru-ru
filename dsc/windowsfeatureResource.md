---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс WindowsFeature в DSC"
ms.openlocfilehash: a3433577a122f6c7e31360e094a089f6ceef77c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="32d58-103">Ресурс WindowsFeature в DSC</span><span class="sxs-lookup"><span data-stu-id="32d58-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="32d58-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="32d58-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="32d58-105">Ресурс **WindowsFeature** в DSC Windows PowerShell предоставляет механизм добавления и удаления ролей и компонентов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="32d58-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="32d58-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="32d58-106">Syntax</span></span>

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="32d58-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="32d58-107">Properties</span></span>

|  <span data-ttu-id="32d58-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="32d58-108">Property</span></span>  |  <span data-ttu-id="32d58-109">Описание</span><span class="sxs-lookup"><span data-stu-id="32d58-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="32d58-110">Название</span><span class="sxs-lookup"><span data-stu-id="32d58-110">Name</span></span>| <span data-ttu-id="32d58-111">Указывает имя роли или компонента, которые необходимо добавить или удалить.</span><span class="sxs-lookup"><span data-stu-id="32d58-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="32d58-112">Это свойство аналогично свойству __Name__ командлета [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) и не является отображаемым именем роли или компонента.</span><span class="sxs-lookup"><span data-stu-id="32d58-112">This is the same as the __Name__ property from the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the role or feature.</span></span>| 
| <span data-ttu-id="32d58-113">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="32d58-113">Credential</span></span>| <span data-ttu-id="32d58-114">Указывает учетные данные для добавления или удаления роли или компонента.</span><span class="sxs-lookup"><span data-stu-id="32d58-114">Indicates the credentials to use to add or remove the role or feature.</span></span>| 
| <span data-ttu-id="32d58-115">Ensure</span><span class="sxs-lookup"><span data-stu-id="32d58-115">Ensure</span></span>| <span data-ttu-id="32d58-116">Указывает, добавляется или удаляется роль или компонент.</span><span class="sxs-lookup"><span data-stu-id="32d58-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="32d58-117">Чтобы добавить роль или компонент, установите это свойство равным Present, чтобы удалить — равным Absent.</span><span class="sxs-lookup"><span data-stu-id="32d58-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>| 
| <span data-ttu-id="32d58-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="32d58-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="32d58-119">Присвойте этому свойству значение __$true__ для синхронизации состояния всех необходимых дополнительных компонентов с состоянием компонента, указанного в свойстве __Name__.</span><span class="sxs-lookup"><span data-stu-id="32d58-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>| 
| <span data-ttu-id="32d58-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="32d58-120">LogPath</span></span>| <span data-ttu-id="32d58-121">Указывает путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.</span><span class="sxs-lookup"><span data-stu-id="32d58-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="32d58-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="32d58-122">DependsOn</span></span>| <span data-ttu-id="32d58-123">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="32d58-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="32d58-124">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="32d58-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="32d58-125">Источник</span><span class="sxs-lookup"><span data-stu-id="32d58-125">Source</span></span>| <span data-ttu-id="32d58-126">Указывает расположение исходного файла для установки, если он необходим.</span><span class="sxs-lookup"><span data-stu-id="32d58-126">Indicates the location of the source file to use for installation, if necessary.</span></span>| 

## <a name="example"></a><span data-ttu-id="32d58-127">Пример</span><span class="sxs-lookup"><span data-stu-id="32d58-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```

