---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Конфигурации DSC"
ms.openlocfilehash: b0868a276dbf5cdb566ce1f35a96b3372cf49be1
ms.sourcegitcommit: 60c6f9d8cf316e6d5b285854e6e5641ac7648f3f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="dsc-configurations"></a><span data-ttu-id="90e7d-103">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="90e7d-103">DSC Configurations</span></span>

><span data-ttu-id="90e7d-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="90e7d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="90e7d-105">Конфигурации DSC — это сценарии PowerShell, определяющие особый тип функции.</span><span class="sxs-lookup"><span data-stu-id="90e7d-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span> <span data-ttu-id="90e7d-106">Для определения конфигурации используйте ключевое слово PowerShell **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="90e7d-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
} 

```

<span data-ttu-id="90e7d-107">Сохраните сценарий как PS1-файл.</span><span class="sxs-lookup"><span data-stu-id="90e7d-107">Save the script as a .ps1 file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="90e7d-108">Синтаксис конфигурации</span><span class="sxs-lookup"><span data-stu-id="90e7d-108">Configuration syntax</span></span>

<span data-ttu-id="90e7d-109">Сценарий конфигурации состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="90e7d-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="90e7d-110">Блок **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="90e7d-110">The **Configuration** block.</span></span> <span data-ttu-id="90e7d-111">Это основной блок сценария.</span><span class="sxs-lookup"><span data-stu-id="90e7d-111">This is the outermost script block.</span></span> <span data-ttu-id="90e7d-112">Для его определения необходимо использовать ключевое слово **Configuration** и указать имя.</span><span class="sxs-lookup"><span data-stu-id="90e7d-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="90e7d-113">В этом случае имя конфигурации — MyDscConfiguration.</span><span class="sxs-lookup"><span data-stu-id="90e7d-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="90e7d-114">Один блок **Node** или несколько.</span><span class="sxs-lookup"><span data-stu-id="90e7d-114">One or more **Node** blocks.</span></span> <span data-ttu-id="90e7d-115">Определяют настраиваемые вами узлы (компьютеры или виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="90e7d-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="90e7d-116">В представленной выше конфигурации присутствует один блок **Node**, соответствующий компьютеру с именем TEST-PC1.</span><span class="sxs-lookup"><span data-stu-id="90e7d-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span>
- <span data-ttu-id="90e7d-117">Один блок ресурсов или несколько.</span><span class="sxs-lookup"><span data-stu-id="90e7d-117">One or more resource blocks.</span></span> <span data-ttu-id="90e7d-118">В этих блоках конфигурация определяет свойства настраиваемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90e7d-118">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="90e7d-119">В данном случае используются два блока ресурсов, каждый из которых вызывает ресурс WindowsFeature.</span><span class="sxs-lookup"><span data-stu-id="90e7d-119">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="90e7d-120">В блоке **Configuration** можно делать все то же самое, что и в функции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90e7d-120">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="90e7d-121">Например, в предыдущем примере вместо того, чтобы прописывать имя целевого компьютера конфигурации в коде, можно добавить в имя узла соответствующий параметр:</span><span class="sxs-lookup"><span data-stu-id="90e7d-121">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}

```

<span data-ttu-id="90e7d-122">В этом примере вы указываете имя узла, передавая его как параметр **ComputerName** при компиляции конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90e7d-122">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuraton.</span></span> <span data-ttu-id="90e7d-123">По умолчанию используется имя localhost.</span><span class="sxs-lookup"><span data-stu-id="90e7d-123">The name defaults to "localhost".</span></span>

## <a name="compiling-the-configuration"></a><span data-ttu-id="90e7d-124">Компиляция конфигурации</span><span class="sxs-lookup"><span data-stu-id="90e7d-124">Compiling the configuration</span></span>

<span data-ttu-id="90e7d-125">Прежде чем активировать конфигурацию, необходимо скомпилировать ее в MOF-документ.</span><span class="sxs-lookup"><span data-stu-id="90e7d-125">Before you can enact a configuration, you have to compile it into a MOF document.</span></span> <span data-ttu-id="90e7d-126">Для этого нужно вызвать конфигурацию так же, как функцию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90e7d-126">You do this by calling the configuration like you would a PowerShell function.</span></span>  
<span data-ttu-id="90e7d-127">Последняя строка примера, содержащего только имя конфигурации, вызывает конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="90e7d-127">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

><span data-ttu-id="90e7d-128">**Примечание**. Для вызова конфигурация функция должна находиться в глобальной области видимости (как и любая другая функция PowerShell).</span><span class="sxs-lookup"><span data-stu-id="90e7d-128">**Note:** To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span> 
><span data-ttu-id="90e7d-129">Для этого нужно либо использовать вызов сценария с точкой, либо выполнить сценарий конфигурации, нажав клавишу F5 или кнопку **Выполнить сценарий** в интегрированной среде сценариев.</span><span class="sxs-lookup"><span data-stu-id="90e7d-129">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span> 
><span data-ttu-id="90e7d-130">Чтобы использовать вызов сценария с точкой, выполните команду `. .\myConfig.ps1`, где `myConfig.ps1` — это имя файла сценария, который содержит конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="90e7d-130">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="90e7d-131">При вызове конфигурации она выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="90e7d-131">When you call the configuration, it:</span></span>

- <span data-ttu-id="90e7d-132">разрешает все переменные;</span><span class="sxs-lookup"><span data-stu-id="90e7d-132">Resolves all variables</span></span> 
- <span data-ttu-id="90e7d-133">создает папку в текущем каталоге с тем же именем, что и у конфигурации;</span><span class="sxs-lookup"><span data-stu-id="90e7d-133">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="90e7d-134">создает файл с именем _имя_узла_.mof в новой папке, где _имя_узла_ — это имя целевого узла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90e7d-134">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span> 
    <span data-ttu-id="90e7d-135">Если узлов несколько, MOF-файл создается для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="90e7d-135">If there are more than one nodes, a MOF file will be created for each node.</span></span>

><span data-ttu-id="90e7d-136">**Примечание**. MOF-файл содержит все сведения о конфигурации целевого узла.</span><span class="sxs-lookup"><span data-stu-id="90e7d-136">**Note**: The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="90e7d-137">Поэтому его необходимо хранить в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="90e7d-137">Because of this, it’s important to keep it secure.</span></span> 
><span data-ttu-id="90e7d-138">Дополнительные сведения см. в статье [Защита MOF-файла](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="90e7d-138">For more information, see [Securing the MOF file](secureMOF.md).</span></span>

<span data-ttu-id="90e7d-139">При компиляции первой приведенной конфигурации создается следующая структура папок:</span><span class="sxs-lookup"><span data-stu-id="90e7d-139">Compiling the first configuration above results in the following folder structure:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```  

<span data-ttu-id="90e7d-140">Если конфигурация принимает какой-либо параметр, как во втором примере, его необходимо указывать во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="90e7d-140">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="90e7d-141">Вот как это выглядит:</span><span class="sxs-lookup"><span data-stu-id="90e7d-141">Here's how that would look:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```      

## <a name="using-dependson"></a><span data-ttu-id="90e7d-142">Использование ключевого слова DependsOn</span><span class="sxs-lookup"><span data-stu-id="90e7d-142">Using DependsOn</span></span>

<span data-ttu-id="90e7d-143">Одно из полезных ключевых слов DSC — это **DependsOn**.</span><span class="sxs-lookup"><span data-stu-id="90e7d-143">A useful DSC keyword is **DependsOn**.</span></span> <span data-ttu-id="90e7d-144">Как правило (хоть и не всегда), DSC применяет ресурсы в порядке их появления в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90e7d-144">Typically (though not necessarily always), DSC applies the resources in the order that they appear within the configuration.</span></span> <span data-ttu-id="90e7d-145">Ключевое слово **DependsOn** определяет, какие ресурсы зависят от других ресурсов, а LCM следит за тем, чтобы они применялись в правильном порядке независимо от того, в каком порядке определены экземпляры ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90e7d-145">However, **DependsOn** specifies which resources depend on other resources, and the LCM ensures that they are applied in the correct order, regardless of the order in which resource instances are defined.</span></span> <span data-ttu-id="90e7d-146">Например, в конфигурации может быть указано, что экземпляр ресурса **User** зависит от наличия ресурса **Group**:</span><span class="sxs-lookup"><span data-stu-id="90e7d-146">For example, a configuration might specify that an instance of the **User** resource depends on the existence of a **Group** instance:</span></span>

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}

```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="90e7d-147">Использование новых ресурсов в конфигурации</span><span class="sxs-lookup"><span data-stu-id="90e7d-147">Using new resources in Your configuration</span></span>

<span data-ttu-id="90e7d-148">Выполняя предыдущие примеры, вы могли заметить предупреждение о том, что используемый ресурс не импортирован.</span><span class="sxs-lookup"><span data-stu-id="90e7d-148">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="90e7d-149">Сейчас DSC поставляется с модулем PSDesiredStateConfiguration, в который входят 12 ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90e7d-149">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span> <span data-ttu-id="90e7d-150">Другие ресурсы во внешних модулях необходимо добавлять в `$env:PSModulePath` в том порядке, в котором LCM должен будет их распознать.</span><span class="sxs-lookup"><span data-stu-id="90e7d-150">Other resources in external modules must be placed in `$env:PSModulePath` in order to be recognized by the LCM.</span></span> <span data-ttu-id="90e7d-151">Определить, какие ресурсы установлены в системе и доступны для использования LCM, позволяет новый командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx).</span><span class="sxs-lookup"><span data-stu-id="90e7d-151">A new cmdlet, [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span> <span data-ttu-id="90e7d-152">После добавления в `$env:PSModulePath` и правильного распознавания командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) эти модули нужно будет загрузить в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="90e7d-152">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), they still need to be loaded within your configuration.</span></span> 
<span data-ttu-id="90e7d-153">**Import-DscResource** — это динамическое ключевое слово, распознаваемое только в блоке **Configuration** (т. е. оно не является командлетом).</span><span class="sxs-lookup"><span data-stu-id="90e7d-153">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block (i.e. it is not a cmdlet).</span></span> 
<span data-ttu-id="90e7d-154">**Import-DscResource** поддерживает два параметра:</span><span class="sxs-lookup"><span data-stu-id="90e7d-154">**Import-DscResource** supports two parameters:</span></span>
- <span data-ttu-id="90e7d-155">Параметр **ModuleName** — рекомендуемый способ применения **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="90e7d-155">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="90e7d-156">Он принимает имя модуля, содержащего ресурсы для импорта (а также массив строк с именами модулей).</span><span class="sxs-lookup"><span data-stu-id="90e7d-156">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span> 
- <span data-ttu-id="90e7d-157">Параметр **Name** — имя импортируемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="90e7d-157">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="90e7d-158">Это не то понятное имя, которое возвращается командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), а имя класса, используемое при определении схемы ресурса (возвращается как параметр **ResourceType** командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)).</span><span class="sxs-lookup"><span data-stu-id="90e7d-158">This is not the friendly name returned as "Name" by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)).</span></span> 

## <a name="see-also"></a><span data-ttu-id="90e7d-159">См. также</span><span class="sxs-lookup"><span data-stu-id="90e7d-159">See Also</span></span>
* [<span data-ttu-id="90e7d-160">Общие сведения о службе настройки требуемого состояния Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="90e7d-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
* [<span data-ttu-id="90e7d-161">Ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="90e7d-161">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="90e7d-162">Настройка локального диспетчера конфигураций</span><span class="sxs-lookup"><span data-stu-id="90e7d-162">Configuring The Local Configuration Manager</span></span>](metaConfig.md)

