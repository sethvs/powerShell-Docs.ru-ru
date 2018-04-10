---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс DSC WindowsOptionalFeatureSet
ms.openlocfilehash: 3329e0d0f1988a2ee20eb848da943ff1b22bd4df
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="ceb87-103">Ресурс DSC WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="ceb87-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="ceb87-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ceb87-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="ceb87-105">Ресурс **WindowsOptionalFeatureSet** в DSC Windows PowerShell предоставляет механизм включения дополнительных компонентов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="ceb87-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>
<span data-ttu-id="ceb87-106">Он является [составным ресурсом](authoringResourceComposite.md), который вызывает [ресурс WindowsOptionalFeature](windowsOptionalFeatureResource.md) для каждого компонента, указанного в свойстве `Name`.</span><span class="sxs-lookup"><span data-stu-id="ceb87-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="ceb87-107">Используйте этот ресурс, если нужно настроить одинаковое состояние для нескольких дополнительных компонентов Windows.</span><span class="sxs-lookup"><span data-stu-id="ceb87-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="ceb87-108">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ceb87-108">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="ceb87-109">Свойства</span><span class="sxs-lookup"><span data-stu-id="ceb87-109">Properties</span></span>

|  <span data-ttu-id="ceb87-110">Свойство</span><span class="sxs-lookup"><span data-stu-id="ceb87-110">Property</span></span>  |  <span data-ttu-id="ceb87-111">Описание</span><span class="sxs-lookup"><span data-stu-id="ceb87-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="ceb87-112">Name</span><span class="sxs-lookup"><span data-stu-id="ceb87-112">Name</span></span>| <span data-ttu-id="ceb87-113">Указывает имена компонентов, которые необходимо включить или отключить.</span><span class="sxs-lookup"><span data-stu-id="ceb87-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>|
| <span data-ttu-id="ceb87-114">Ensure</span><span class="sxs-lookup"><span data-stu-id="ceb87-114">Ensure</span></span>| <span data-ttu-id="ceb87-115">Указывает, включены ли компоненты.</span><span class="sxs-lookup"><span data-stu-id="ceb87-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="ceb87-116">Чтобы включить компоненты, установите для этого свойства значение "Включить", чтобы отключить — значение "Отключить".</span><span class="sxs-lookup"><span data-stu-id="ceb87-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="ceb87-117">Источник</span><span class="sxs-lookup"><span data-stu-id="ceb87-117">Source</span></span>| <span data-ttu-id="ceb87-118">Не реализовано.</span><span class="sxs-lookup"><span data-stu-id="ceb87-118">Not implemented.</span></span>|
| <span data-ttu-id="ceb87-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="ceb87-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="ceb87-120">Указывает, обращается ли система DISM к Центру обновления Windows при поиске исходных файлов для включения компонентов.</span><span class="sxs-lookup"><span data-stu-id="ceb87-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="ceb87-121">Если задано значение $true, система DISM не обращается к Центру обновления Windows.</span><span class="sxs-lookup"><span data-stu-id="ceb87-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="ceb87-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="ceb87-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="ceb87-123">Задайте значение **$true**, чтобы удалить все файлы, связанные с компонентами, при их отключении (то есть когда свойству **Ensure** присваивается значение Absent).</span><span class="sxs-lookup"><span data-stu-id="ceb87-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="ceb87-124">Уровень журнала</span><span class="sxs-lookup"><span data-stu-id="ceb87-124">LogLevel</span></span>| <span data-ttu-id="ceb87-125">Максимальный уровень результатов, показываемый в журналах.</span><span class="sxs-lookup"><span data-stu-id="ceb87-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="ceb87-126">Допустимые значения: ErrorsOnly (в журналы записываются только ошибки), ErrorsAndWarning (в журналы записываются ошибки и предупреждения) и ErrorsAndWarningAndInformation (в журналы записываются ошибки, предупреждения и отладочные сведения).</span><span class="sxs-lookup"><span data-stu-id="ceb87-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="ceb87-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="ceb87-127">LogPath</span></span>| <span data-ttu-id="ceb87-128">Путь к файлу журнала, в котором поставщик ресурсов должен вести журнал работы.</span><span class="sxs-lookup"><span data-stu-id="ceb87-128">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="ceb87-129">DependsOn</span><span class="sxs-lookup"><span data-stu-id="ceb87-129">DependsOn</span></span>| <span data-ttu-id="ceb87-130">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="ceb87-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ceb87-131">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ceb87-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|