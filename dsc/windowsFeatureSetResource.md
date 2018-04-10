---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC WindowsFeatureSet
ms.openlocfilehash: a6fecba0397b88ce39f6f1a1be6cc366c8a983a6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="73df0-103">Ресурс DSC WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="73df0-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="73df0-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="73df0-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="73df0-105">Ресурс **WindowsFeatureSet** в DSC Windows PowerShell предоставляет механизм добавления и удаления ролей и компонентов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="73df0-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="73df0-106">Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс WindowsFeature](windowsfeatureResource.md) для каждого компонента, указанного в свойстве `Name`.</span><span class="sxs-lookup"><span data-stu-id="73df0-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="73df0-107">Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких компонентов Windows.</span><span class="sxs-lookup"><span data-stu-id="73df0-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="73df0-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="73df0-108">Syntax</span></span>

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="73df0-109">Свойства</span><span class="sxs-lookup"><span data-stu-id="73df0-109">Properties</span></span>

|  <span data-ttu-id="73df0-110">Свойство</span><span class="sxs-lookup"><span data-stu-id="73df0-110">Property</span></span>  |  <span data-ttu-id="73df0-111">Описание</span><span class="sxs-lookup"><span data-stu-id="73df0-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="73df0-112">Name</span><span class="sxs-lookup"><span data-stu-id="73df0-112">Name</span></span>| <span data-ttu-id="73df0-113">Имена ролей или компонентов, которые необходимо добавить или удалить.</span><span class="sxs-lookup"><span data-stu-id="73df0-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="73df0-114">Это свойство аналогично свойству **Name** командлета [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) и не содержит отображаемые имена ролей или компонентов.</span><span class="sxs-lookup"><span data-stu-id="73df0-114">This is the same as the **Name** property of the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the roles or features.</span></span>|
| <span data-ttu-id="73df0-115">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="73df0-115">Credential</span></span>| <span data-ttu-id="73df0-116">Учетные данные для добавления или удаления ролей или компонентов.</span><span class="sxs-lookup"><span data-stu-id="73df0-116">The credentials to use to add or remove the roles or features.</span></span>|
| <span data-ttu-id="73df0-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="73df0-117">Ensure</span></span>| <span data-ttu-id="73df0-118">Указывает, добавляются ли роли или компоненты.</span><span class="sxs-lookup"><span data-stu-id="73df0-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="73df0-119">Чтобы добавить роли или компоненты, установите это свойство равным Present, чтобы удалить — равным Absent.</span><span class="sxs-lookup"><span data-stu-id="73df0-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="73df0-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="73df0-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="73df0-121">Присвойте этому свойству значение **$true**, чтобы включить все необходимые дополнительные компоненты для компонентов, указанных в свойстве **Name**.</span><span class="sxs-lookup"><span data-stu-id="73df0-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>|
| <span data-ttu-id="73df0-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="73df0-122">LogPath</span></span>| <span data-ttu-id="73df0-123">Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.</span><span class="sxs-lookup"><span data-stu-id="73df0-123">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="73df0-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="73df0-124">DependsOn</span></span>| <span data-ttu-id="73df0-125">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="73df0-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="73df0-126">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="73df0-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="73df0-127">Источник</span><span class="sxs-lookup"><span data-stu-id="73df0-127">Source</span></span>| <span data-ttu-id="73df0-128">Указывает расположение исходного файла для установки, если он необходим.</span><span class="sxs-lookup"><span data-stu-id="73df0-128">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="73df0-129">Пример</span><span class="sxs-lookup"><span data-stu-id="73df0-129">Example</span></span>

<span data-ttu-id="73df0-130">Приведенная ниже конфигурация обеспечивает установку компонентов **Веб-сервер** (IIS) и **SMTP-сервер**, а также всех их дополнительных компонентов.</span><span class="sxs-lookup"><span data-stu-id="73df0-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```