---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс WindowsProcess в DSC"
ms.openlocfilehash: c34d3cb1d4d9b899b45fba7b4b148a7c977f5365
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="24503-103">Ресурс WindowsProcess в DSC</span><span class="sxs-lookup"><span data-stu-id="24503-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="24503-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="24503-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="24503-105">Ресурс **WindowsProcess** в DSC Windows PowerShell предоставляет механизм настройки процессов на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="24503-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="24503-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="24503-106">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="24503-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="24503-107">Properties</span></span>
|  <span data-ttu-id="24503-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="24503-108">Property</span></span>  |  <span data-ttu-id="24503-109">Описание</span><span class="sxs-lookup"><span data-stu-id="24503-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="24503-110">Аргументы</span><span class="sxs-lookup"><span data-stu-id="24503-110">Arguments</span></span>| <span data-ttu-id="24503-111">Указывает строку аргументов, которая будет передана процессу "как есть".</span><span class="sxs-lookup"><span data-stu-id="24503-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="24503-112">Если необходимо передать несколько аргументов, поместите их все в эту строку.</span><span class="sxs-lookup"><span data-stu-id="24503-112">If you need to pass several arguments, put them all in this string.</span></span>| 
| <span data-ttu-id="24503-113">путь</span><span class="sxs-lookup"><span data-stu-id="24503-113">Path</span></span>| <span data-ttu-id="24503-114">Путь к исполняемому файлу процесса.</span><span class="sxs-lookup"><span data-stu-id="24503-114">The path to the process executable.</span></span> <span data-ttu-id="24503-115">Если это имя исполняемого файла (а не полный путь к нему), ресурс DSC будет искать переменную среды **Path** (`$env:Path`), чтобы найти исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="24503-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="24503-116">Если значение этого свойства — полный путь, ресурс DSC не будет использовать переменную среды **Path** для поиска файла и вызовет ошибку в случае отсутствия пути.</span><span class="sxs-lookup"><span data-stu-id="24503-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="24503-117">Относительные пути не допускаются.</span><span class="sxs-lookup"><span data-stu-id="24503-117">Relative paths are not allowed.</span></span>| 
| <span data-ttu-id="24503-118">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="24503-118">Credential</span></span>| <span data-ttu-id="24503-119">Указывает учетные данные для запуска процесса.</span><span class="sxs-lookup"><span data-stu-id="24503-119">Indicates the credentials for starting the process.</span></span>| 
| <span data-ttu-id="24503-120">Ensure</span><span class="sxs-lookup"><span data-stu-id="24503-120">Ensure</span></span>| <span data-ttu-id="24503-121">Указывает, существует ли процесс.</span><span class="sxs-lookup"><span data-stu-id="24503-121">Indicates if the process exists.</span></span> <span data-ttu-id="24503-122">Если процесс существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="24503-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="24503-123">В противном случае укажите значение Absent.</span><span class="sxs-lookup"><span data-stu-id="24503-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="24503-124">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="24503-124">The default is "Present".</span></span>| 
| <span data-ttu-id="24503-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="24503-125">DependsOn</span></span> | <span data-ttu-id="24503-126">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="24503-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="24503-127">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: 'DependsOn = "[ResourceType]ResourceName"''.</span><span class="sxs-lookup"><span data-stu-id="24503-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\` .</span></span>| 
| <span data-ttu-id="24503-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="24503-128">StandardErrorPath</span></span>| <span data-ttu-id="24503-129">Указывает путь к каталогу для записи стандартных ошибок.</span><span class="sxs-lookup"><span data-stu-id="24503-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="24503-130">Все существующие файлы в этом каталоге будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="24503-130">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="24503-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="24503-131">StandardInputPath</span></span>| <span data-ttu-id="24503-132">Указывает расположение стандартного ввода.</span><span class="sxs-lookup"><span data-stu-id="24503-132">Indicates the standard input location.</span></span>| 
| <span data-ttu-id="24503-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="24503-133">StandardOutputPath</span></span>| <span data-ttu-id="24503-134">Указывает расположение стандартного вывода.</span><span class="sxs-lookup"><span data-stu-id="24503-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="24503-135">Все существующие файлы в этом каталоге будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="24503-135">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="24503-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="24503-136">WorkingDirectory</span></span>| <span data-ttu-id="24503-137">Указывает расположение, которое будет использоваться в качестве текущего рабочего каталога для процесса.</span><span class="sxs-lookup"><span data-stu-id="24503-137">Indicates the location that will be used as the current working directory for the process.</span></span>| 

