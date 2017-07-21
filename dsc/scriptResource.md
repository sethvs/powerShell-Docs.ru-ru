---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс Script в DSC"
ms.openlocfilehash: 81718de0b0c8463189e33e565dc9ff39692dbe8b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-script-resource"></a><span data-ttu-id="16e49-103">Ресурс Script в DSC</span><span class="sxs-lookup"><span data-stu-id="16e49-103">DSC Script Resource</span></span>

 
> <span data-ttu-id="16e49-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="16e49-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="16e49-105">Ресурс **Script** в DSC Windows PowerShell предоставляет механизм запуска блоков сценариев на целевых узлах.</span><span class="sxs-lookup"><span data-stu-id="16e49-105">The **Script** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to run Windows PowerShell script blocks on target nodes.</span></span> <span data-ttu-id="16e49-106">Ресурс `Script` имеет свойства `GetScript`, `SetScript` и `TestScript`.</span><span class="sxs-lookup"><span data-stu-id="16e49-106">The `Script` resource has `GetScript`, `SetScript`, and `TestScript` properties.</span></span> <span data-ttu-id="16e49-107">Эти свойства должны быть заданы для блоков сценария, выполняемых на каждом целевом узле.</span><span class="sxs-lookup"><span data-stu-id="16e49-107">These properties should be set to script blocks that will run on each target node.</span></span> 

<span data-ttu-id="16e49-108">Блок сценария `GetScript` должен возвращать хэш-таблицу, представляющую состояние текущего узла.</span><span class="sxs-lookup"><span data-stu-id="16e49-108">The `GetScript` script block should return a hashtable representing the state of the current node.</span></span> <span data-ttu-id="16e49-109">Хэш-таблица должна содержать только один ключ `Result`, а значение должно иметь тип `String`.</span><span class="sxs-lookup"><span data-stu-id="16e49-109">The hashtable must only contain one key `Result` and the value must be of type `String`.</span></span> <span data-ttu-id="16e49-110">Выходные значения этого блока необязательны.</span><span class="sxs-lookup"><span data-stu-id="16e49-110">It is not required to return anything.</span></span> <span data-ttu-id="16e49-111">DSC не выполняет никаких действий с выходными данными этого блока сценария.</span><span class="sxs-lookup"><span data-stu-id="16e49-111">DSC doesn't do anything with the output of this script block.</span></span>

<span data-ttu-id="16e49-112">Блок сценария `TestScript` должен определять, требуется ли изменение текущего узла.</span><span class="sxs-lookup"><span data-stu-id="16e49-112">The `TestScript` script block should determine if the current node needs to be modified.</span></span> <span data-ttu-id="16e49-113">Он должен возвращать значение `$true`, если состояние узла актуально.</span><span class="sxs-lookup"><span data-stu-id="16e49-113">It should return `$true` if the node is up-to-date.</span></span> <span data-ttu-id="16e49-114">Он должен возвращать значение `$false`, если конфигурация узла устарела и должна быть обновлена блоком сценария `SetScript`.</span><span class="sxs-lookup"><span data-stu-id="16e49-114">It should return `$false` if the node's configuration is out-of-date and should be updated by the `SetScript` script block.</span></span> <span data-ttu-id="16e49-115">Блок сценария `TestScript` вызывается DSC.</span><span class="sxs-lookup"><span data-stu-id="16e49-115">The `TestScript` script block is called by DSC.</span></span>

<span data-ttu-id="16e49-116">Блок сценария `SetScript` должен изменить узел.</span><span class="sxs-lookup"><span data-stu-id="16e49-116">The `SetScript` script block should modify the node.</span></span> <span data-ttu-id="16e49-117">Он вызывается DSC, если блок `TestScript` возвращает значение `$false`.</span><span class="sxs-lookup"><span data-stu-id="16e49-117">It is called by DSC if the `TestScript` block return `$false`.</span></span>

<span data-ttu-id="16e49-118">Если необходимо использовать переменные из сценария конфигурации в блоках сценария `GetScript`, `TestScript` или `SetScript`, используйте область `$using:` (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="16e49-118">If you need to use variables from your configuration script in the `GetScript`, `TestScript`, or `SetScript` script blocks, use the `$using:` scope (see below for an example).</span></span>


## <a name="syntax"></a><span data-ttu-id="16e49-119">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="16e49-119">Syntax</span></span>

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="16e49-120">Свойства</span><span class="sxs-lookup"><span data-stu-id="16e49-120">Properties</span></span>

|  <span data-ttu-id="16e49-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="16e49-121">Property</span></span>  |  <span data-ttu-id="16e49-122">Описание</span><span class="sxs-lookup"><span data-stu-id="16e49-122">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="16e49-123">GetScript</span><span class="sxs-lookup"><span data-stu-id="16e49-123">GetScript</span></span>| <span data-ttu-id="16e49-124">Предоставляет блок сценария Windows PowerShell, который выполняется при вызове командлета [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e49-124">Provides a block of Windows PowerShell script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) cmdlet.</span></span> <span data-ttu-id="16e49-125">Этот блок должен возвращать хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="16e49-125">This block must return a hashtable.</span></span> <span data-ttu-id="16e49-126">Хэш-таблица должна содержать только один ключ **Result**, а значение должно иметь тип **String**.</span><span class="sxs-lookup"><span data-stu-id="16e49-126">The hashtable must only contain one key **Result** and the value must be of type **String**.</span></span>| 
| <span data-ttu-id="16e49-127">SetScript</span><span class="sxs-lookup"><span data-stu-id="16e49-127">SetScript</span></span>| <span data-ttu-id="16e49-128">Предоставляет блок сценария Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16e49-128">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="16e49-129">При вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) в первую очередь выполняется блок **TestScript**.</span><span class="sxs-lookup"><span data-stu-id="16e49-129">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** block runs first.</span></span> <span data-ttu-id="16e49-130">Если блок **TestScript** возвращает **$false**, будет запущен блок **SetScript**.</span><span class="sxs-lookup"><span data-stu-id="16e49-130">If the **TestScript** block returns **$false**, the **SetScript** block will run.</span></span> <span data-ttu-id="16e49-131">Если блок **TestScript** возвращает **$true**, то блок **SetScript** запущен не будет.</span><span class="sxs-lookup"><span data-stu-id="16e49-131">If the **TestScript** block returns **$true**, the **SetScript** block will not run.</span></span>| 
| <span data-ttu-id="16e49-132">TestScript</span><span class="sxs-lookup"><span data-stu-id="16e49-132">TestScript</span></span>| <span data-ttu-id="16e49-133">Предоставляет блок сценария Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16e49-133">Provides a block of Windows PowerShell script.</span></span> <span data-ttu-id="16e49-134">Этот блок запускается при вызове командлета[Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e49-134">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this block runs.</span></span> <span data-ttu-id="16e49-135">Если он возвращает **$false**, будет запущен блок SetScript.</span><span class="sxs-lookup"><span data-stu-id="16e49-135">If it returns **$false**, the SetScript block will run.</span></span> <span data-ttu-id="16e49-136">Если он возвращает **$true**, блок SetScript запущен не будет.</span><span class="sxs-lookup"><span data-stu-id="16e49-136">If it returns **$true**, the SetScript block will not run.</span></span> <span data-ttu-id="16e49-137">Кроме того, блок **TestScript** запускается при вызове командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx).</span><span class="sxs-lookup"><span data-stu-id="16e49-137">The **TestScript** block also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="16e49-138">Однако в этом случае блок **SetScript** не будет запущен независимо от того, какое значение возвращает блок TestScript.</span><span class="sxs-lookup"><span data-stu-id="16e49-138">However, in this case, the **SetScript** block will not run, no matter what value the TestScript block returns.</span></span> <span data-ttu-id="16e49-139">Блок **TestScript** должен вернуть True, если фактическая конфигурация соответствует текущей конфигурации требуемого состояния, и False в противном случае.</span><span class="sxs-lookup"><span data-stu-id="16e49-139">The **TestScript** block must return True if the actual configuration matches the current desired state configuration, and False if it does not match.</span></span> <span data-ttu-id="16e49-140">(Текущей конфигурацией требуемого состояния является последняя конфигурация, активированная на узле, который использует DSC.)</span><span class="sxs-lookup"><span data-stu-id="16e49-140">(The current desired state configuration is the last configuration enacted on the node that is using DSC.)</span></span>| 
| <span data-ttu-id="16e49-141">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="16e49-141">Credential</span></span>| <span data-ttu-id="16e49-142">Указывает учетные данные, используемые для запуска этого сценария, если они необходимы.</span><span class="sxs-lookup"><span data-stu-id="16e49-142">Indicates the credentials to use for running this script, if credentials are required.</span></span>| 
| <span data-ttu-id="16e49-143">DependsOn</span><span class="sxs-lookup"><span data-stu-id="16e49-143">DependsOn</span></span>| <span data-ttu-id="16e49-144">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="16e49-144">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="16e49-145">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="16e49-145">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>

## <a name="example-1"></a><span data-ttu-id="16e49-146">Пример 1</span><span class="sxs-lookup"><span data-stu-id="16e49-146">Example 1</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript = 
        { 
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
    }
}
```

## <a name="example-2"></a><span data-ttu-id="16e49-147">Пример 2.</span><span class="sxs-lookup"><span data-stu-id="16e49-147">Example 2</span></span>
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Version' = "$currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
            if( $state['Version'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Version'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = { 
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

<span data-ttu-id="16e49-148">Этот ресурс записывает версию конфигурации в текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="16e49-148">This resource is writing the configuration's version to a text file.</span></span> <span data-ttu-id="16e49-149">Эта версия доступна на клиентском компьютере, но не на узлах, поэтому ее необходимо передать во все блоки сценария ресурса `Script` с помощью области PowerShell `using`.</span><span class="sxs-lookup"><span data-stu-id="16e49-149">This version is available on the client computer, but isn't on any of the nodes, so it has to be passed to each of the `Script` resource's script blocks with PowerShell's `using` scope.</span></span> <span data-ttu-id="16e49-150">При создании MOF-файла узла значение переменной `$version` считывается из текстового файла на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="16e49-150">When generating the node's MOF file, the value of the `$version` variable is read from a text file on the client computer.</span></span> <span data-ttu-id="16e49-151">DSC заменяет переменные `$using:version` в каждом блоке сценария значением переменной `$version`.</span><span class="sxs-lookup"><span data-stu-id="16e49-151">DSC replaces the `$using:version` variables in each script block with the value of the `$version` variable.</span></span>

