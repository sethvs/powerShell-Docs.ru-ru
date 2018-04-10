---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Написание пользовательских ресурсов DSC с использованием MOF
ms.openlocfilehash: 4e336e837d2153fecab8325cb8714ffed85a6175
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a><span data-ttu-id="9d2d6-103">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="9d2d6-103">Writing a custom DSC resource with MOF</span></span>

> <span data-ttu-id="9d2d6-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="9d2d6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="9d2d6-105">В этом разделе мы определим схему для настраиваемого ресурса настройки требуемого состояния (DSC) Windows PowerShell в MOF-файле и реализуем этот ресурс в файле сценария Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-105">In this topic, we will define the schema for a Windows PowerShell Desired State Configuration (DSC) custom resource in a MOF file, and implement the resource in a Windows PowerShell script file.</span></span> <span data-ttu-id="9d2d6-106">Этот ресурс применяется для создания и обслуживания веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-106">This custom resource is for creating and maintaining a web site.</span></span>

## <a name="creating-the-mof-schema"></a><span data-ttu-id="9d2d6-107">Создание схемы MOF</span><span class="sxs-lookup"><span data-stu-id="9d2d6-107">Creating the MOF schema</span></span>

<span data-ttu-id="9d2d6-108">Схема определяет свойства ресурса, которые можно настроить с помощью сценария DSC.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-108">The schema defines the properties of your resource that can be configured by a DSC configuration script.</span></span>

### <a name="folder-structure-for-a-mof-resource"></a><span data-ttu-id="9d2d6-109">Структура папок для ресурса MOF</span><span class="sxs-lookup"><span data-stu-id="9d2d6-109">Folder structure for a MOF resource</span></span>

<span data-ttu-id="9d2d6-110">Для реализации настраиваемого ресурса DSC в схеме MOF создайте указанную ниже структуру папок.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-110">To implement a DSC custom resource with a MOF schema, create the following folder structure.</span></span> <span data-ttu-id="9d2d6-111">Схема MOF определяется в файле Demo_IISWebsite.schema.mof, а сценарий ресурса — в файле Demo_IISWebsite.psm1.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-111">The MOF schema is defined in the file Demo_IISWebsite.schema.mof, and the resource script is defined in Demo_IISWebsite.psm1.</span></span> <span data-ttu-id="9d2d6-112">При необходимости можно создать файл манифеста (PSD1) для модуля.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-112">Optionally, you can create a module manifest (psd1) file.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

<span data-ttu-id="9d2d6-113">Обратите внимание, что папку DSCResources необходимо создать в папке верхнего уровня, а имя папки для каждого ресурса должно совпадать с именем ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-113">Note that it is necessary to create a folder named DSCResources under the top-level folder, and that the folder for each resource must have the same name as the resource.</span></span>

### <a name="the-contents-of-the-mof-file"></a><span data-ttu-id="9d2d6-114">Содержание MOF-файла</span><span class="sxs-lookup"><span data-stu-id="9d2d6-114">The contents of the MOF file</span></span>

<span data-ttu-id="9d2d6-115">Приведем пример файла MOF, который можно использовать как настраиваемый ресурс веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-115">Following is an example MOF file that can be used for a custom website resource.</span></span> <span data-ttu-id="9d2d6-116">Чтобы воспользоваться этим примером, сохраните данную схему в файле с именем *Demo_IISWebsite.schema.mof*.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-116">To follow this example, save this schema to a file, and call the file *Demo_IISWebsite.schema.mof*.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("Website")]
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

<span data-ttu-id="9d2d6-117">В представленном выше коде обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-117">Note the following about the previous code:</span></span>

* <span data-ttu-id="9d2d6-118">`FriendlyName` определяет имя, которое можно использовать для ссылки на этот настраиваемый ресурс в сценариях DSC.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-118">`FriendlyName` defines the name you can use to refer to this custom resource in DSC configuration scripts.</span></span> <span data-ttu-id="9d2d6-119">В этом примере `Website` — эквивалент понятного имени `Archive` для встроенного ресурса архива.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-119">In this example, `Website` is equivalent to the friendly name `Archive` for the built-in Archive resource.</span></span>
* <span data-ttu-id="9d2d6-120">Класс, определяемый для настраиваемого ресурса, должен быть производным от `OMI_BaseResource`.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-120">The class you define for your custom resource must derive from `OMI_BaseResource`.</span></span>
* <span data-ttu-id="9d2d6-121">Квалификатор типа `[Key]` в свойстве означает, что это свойство служит для уникальной идентификации экземпляра ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-121">The type qualifier, `[Key]`, on a property indicates that this property will uniquely identify the resource instance.</span></span> <span data-ttu-id="9d2d6-122">Необходимо указать по крайней мере одно свойство `[Key]`.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-122">At least one `[Key]` property is required.</span></span>
* <span data-ttu-id="9d2d6-123">Квалификатор `[Required]` означает, что свойство является обязательным (значение необходимо указывать в любом сценарии настройки, где используется ресурс).</span><span class="sxs-lookup"><span data-stu-id="9d2d6-123">The `[Required]` qualifier indicates that the property is required (a value must be specified in any configuration script that uses this resource).</span></span>
* <span data-ttu-id="9d2d6-124">Квалификатор `[write]` означает, что свойство не является обязательным при использовании настраиваемого ресурса в сценарии настройки.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-124">The `[write]` qualifier indicates that this property is optional when using the custom resource in a configuration script.</span></span> <span data-ttu-id="9d2d6-125">Квалификатор `[read]` означает, что свойство не может задаваться конфигурацией и предназначено только для целей отчетности.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-125">The `[read]` qualifier indicates that a property cannot be set by a configuration, and is for reporting purposes only.</span></span>
* <span data-ttu-id="9d2d6-126">`Values` ограничивает значения, которые могут быть присвоены свойству, списком значений, определенных в `ValueMap`.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-126">`Values` restricts the values that can be assigned to the property to the list of values defined in `ValueMap`.</span></span> <span data-ttu-id="9d2d6-127">Дополнительные сведения см. в статье [ValueMap и квалификаторы значений](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d2d6-127">For more information, see [ValueMap and Value Qualifiers](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span></span>
* <span data-ttu-id="9d2d6-128">Для сохранения единообразия встроенных ресурсов DSC рекомендуется включать в ресурс свойство `Ensure` с значениями `Present` и `Absent`.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-128">Including a property called `Ensure` with values `Present` and `Absent` in your resource is recommended as a way to maintain a consistent style with built-in DSC resources.</span></span>
* <span data-ttu-id="9d2d6-129">Имя настраиваемого ресурса должно иметь формат `classname.schema.mof`, где `classname` — это идентификатор, следующий за ключевым словом `class` в определении схемы.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-129">Name the schema file for your custom resource as follows: `classname.schema.mof`, where `classname` is the identifier that follows the `class` keyword in your schema definition.</span></span>

### <a name="writing-the-resource-script"></a><span data-ttu-id="9d2d6-130">Создание сценария ресурсов</span><span class="sxs-lookup"><span data-stu-id="9d2d6-130">Writing the resource script</span></span>

<span data-ttu-id="9d2d6-131">Сценарий ресурса реализует логику ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-131">The resource script implements the logic of the resource.</span></span> <span data-ttu-id="9d2d6-132">В этот модуль необходимо включить три функции: **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-132">In this module, you must include three functions called **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource**.</span></span> <span data-ttu-id="9d2d6-133">Все три функции должны принимать набор параметров, идентичный набору свойств, заданных в схеме MOF для вашего ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-133">All three functions must take a parameter set that is identical to the set of properties defined in the MOF schema that you created for your resource.</span></span> <span data-ttu-id="9d2d6-134">В этом документе такой набор свойств называется "свойства ресурса".</span><span class="sxs-lookup"><span data-stu-id="9d2d6-134">In this document, this set of properties is referred to as the “resource properties.”</span></span> <span data-ttu-id="9d2d6-135">Сохраните эти три функции в файл <ResourceName>.psm1.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-135">Store these three functions in a file called <ResourceName>.psm1.</span></span> <span data-ttu-id="9d2d6-136">В следующем примере функции сохраняются в файл с именем Demo_IISWebsite.psm1.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-136">In the following example, the functions are stored in a file called Demo_IISWebsite.psm1.</span></span>

> <span data-ttu-id="9d2d6-137">**Примечание**. Многократное выполнение одного и того же сценария настройки для ресурса не вызывает ошибок, а состояние ресурса остается таким же, как при однократном выполнении.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-137">**Note**: When you run the same configuration script on your resource more than once, you should receive no errors and the resource should remain in the same state as running the script once.</span></span> <span data-ttu-id="9d2d6-138">Для этого функции **Get-TargetResource** и **Test-TargetResource** не должны изменять ресурс, а вызов функции **Set-TargetResource** с одними и теми же параметрами больше одного раза подряд должен быть эквивалентен однократному вызову этой функции.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-138">To accomplish this, ensure that your **Get-TargetResource** and **Test-TargetResource** functions leave the resource unchanged, and that invoking the **Set-TargetResource** function more than once in a sequence with the same parameter values is always equivalent to invoking it once.</span></span>

<span data-ttu-id="9d2d6-139">В реализации функции **Get-TargetResource** используйте значения свойств основных ресурсов, предоставляемых в качестве параметров, для проверки состояния указанного экземпляра ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-139">In the **Get-TargetResource** function implementation, use the key resource property values that are provided as parameters to check the status of the specified resource instance.</span></span> <span data-ttu-id="9d2d6-140">Эта функция должна возвращать хэш-таблицу со списком всех свойств ресурса в виде ключей и фактических значений этих свойств в виде соответствующих значений.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-140">This function must return a hash table that lists all the resource properties as keys and the actual values of these properties as the corresponding values.</span></span> <span data-ttu-id="9d2d6-141">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-141">The following code provides an example.</span></span>

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource
{
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name;
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }

        $getTargetResourceResult;
}
```

<span data-ttu-id="9d2d6-142">В зависимости от того, какие значения заданы для свойств ресурса в сценарии конфигурации, **Set-TargetResource** должен выполнять одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-142">Depending on the values that are specified for the resource properties in the configuration script, the **Set-TargetResource** must do one of the following:</span></span>

* <span data-ttu-id="9d2d6-143">Создание веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9d2d6-143">Create a new website</span></span>
* <span data-ttu-id="9d2d6-144">Обновление существующего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9d2d6-144">Update an existing website</span></span>
* <span data-ttu-id="9d2d6-145">Удаление существующего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9d2d6-145">Delete an existing website</span></span>

<span data-ttu-id="9d2d6-146">Это демонстрируется в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-146">The following example illustrates this.</span></span>

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine.
function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

<span data-ttu-id="9d2d6-147">И наконец, функция **Test-TargetResource** должна принимать тот же набор параметров, что и функции **Get-TargetResource** и **Set-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-147">Finally, the **Test-TargetResource** function must take the same parameter set as **Get-TargetResource** and **Set-TargetResource**.</span></span> <span data-ttu-id="9d2d6-148">В собственной реализации функции **Test-TargetResource** проверьте состояние экземпляра ресурса, заданное основными параметрами.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-148">In your implementation of **Test-TargetResource**, check the status of the resource instance that is specified in the key parameters.</span></span> <span data-ttu-id="9d2d6-149">Если фактическое состояние экземпляра ресурса не соответствует значениям, указанным в наборе параметров, возвращается **$false**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-149">If the actual status of the resource instance does not match the values specified in the parameter set, return **$false**.</span></span> <span data-ttu-id="9d2d6-150">В противном случае возвращается **$true**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-150">Otherwise, return **$true**.</span></span>

<span data-ttu-id="9d2d6-151">Следующий код реализует функцию **Test-TargetResource**:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-151">The following code implements the **Test-TargetResource** function.</span></span>

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result
}
```

<span data-ttu-id="9d2d6-152">**Примечание**. Чтобы упростить отладку, используйте в реализации трех предыдущих функций командлет **Write-Verbose**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-152">**Note**: For easier debugging, use the **Write-Verbose** cmdlet in your implementation of the previous three functions.</span></span>
><span data-ttu-id="9d2d6-153">Он записывает текст в поток подробных сообщений.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-153">This cmdlet writes text to the verbose message stream.</span></span>
><span data-ttu-id="9d2d6-154">По умолчанию поток подробных сообщений не отображается, однако его можно вывести на экран, изменив значение переменной **$VerbosePreference** или применив в командлетах DSC параметр **Verbose** со значением new.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-154">By default, the verbose message stream is not displayed, but you can display it by changing the value of the **$VerbosePreference** variable or by using the **Verbose** parameter in the DSC cmdlets = new.</span></span>

### <a name="creating-the-module-manifest"></a><span data-ttu-id="9d2d6-155">Создание манифеста модуля</span><span class="sxs-lookup"><span data-stu-id="9d2d6-155">Creating the module manifest</span></span>

<span data-ttu-id="9d2d6-156">Командлет **New-ModuleManifest** позволяет определить файл <ResourceName>.psd1 для модуля настраиваемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-156">Finally, use the **New-ModuleManifest** cmdlet to define a <ResourceName>.psd1 file for your custom resource module.</span></span> <span data-ttu-id="9d2d6-157">При вызове этого командлета необходимо сослаться на модуль сценария (PSM1-файл), описанный в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-157">When you invoke this cmdlet, reference the script module (.psm1) file described in the previous section.</span></span> <span data-ttu-id="9d2d6-158">Включите в список функций для экспорта функции **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-158">Include **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** in the list of functions to export.</span></span> <span data-ttu-id="9d2d6-159">Пример файла манифеста:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-159">Following is an example manifest file.</span></span>

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="9d2d6-160">Поддержка PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="9d2d6-160">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="9d2d6-161">**Примечание.** **PsDscRunAsCredential** поддерживается в PowerShell 5.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-161">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="9d2d6-162">Свойство **PsDscRunAsCredential** может использоваться в блоке ресурса [конфигураций DSC](configurations.md), чтобы указать, что ресурс должен выполняться с указанным набором учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-162">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="9d2d6-163">Дополнительные сведения см. в разделе [Запуск DSC с учетными данными пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="9d2d6-163">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

<span data-ttu-id="9d2d6-164">Чтобы получить доступ к пользовательскому контексту из настраиваемого ресурса, можно использовать автоматическую переменную `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="9d2d6-164">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="9d2d6-165">Например, следующий код пропишет пользовательский контекст, по которому выполняется ресурс, в подробный выходной поток:</span><span class="sxs-lookup"><span data-stu-id="9d2d6-165">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```