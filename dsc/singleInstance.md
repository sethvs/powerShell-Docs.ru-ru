---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Запись ресурса DSC с одним экземпляром (рекомендуется)"
ms.openlocfilehash: fe7c50c39ba08e290076ea7a058372ce57898325
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a><span data-ttu-id="23100-103">Запись ресурса DSC с одним экземпляром (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="23100-103">Writing a single-instance DSC resource (best practice)</span></span>

><span data-ttu-id="23100-104">**Примечание.** Эта статья содержит рекомендации по определению ресурса DSC, допускающего всего один экземпляр в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23100-104">**Note:** This topic describes a best practice for defining a DSC resource that allows only a single instance in a configuration.</span></span> <span data-ttu-id="23100-105">Сейчас встроенная функция DSC для этого отсутствует.</span><span class="sxs-lookup"><span data-stu-id="23100-105">Currently, there is no built-in DSC feature to do this.</span></span> <span data-ttu-id="23100-106">Возможно, она появится в будущем.</span><span class="sxs-lookup"><span data-stu-id="23100-106">That might change in the future.</span></span>

<span data-ttu-id="23100-107">Существуют ситуации, когда требуется запретить многократное использование ресурса в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23100-107">There are situations where you don't want to allow a resource to be used multiple times in a configuration.</span></span> <span data-ttu-id="23100-108">Например, в предыдущей реализации ресурса [xTimeZone](https://github.com/PowerShell/xTimeZone) конфигурация могла вызывать ресурс несколько раз, задавая новое значение часового пояса в каждом блоке ресурсов.</span><span class="sxs-lookup"><span data-stu-id="23100-108">For example, in a previous implementation of the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource, a configuration could call the resource multiple times, setting the time zone to a different setting in each resource block:</span></span>

```powershell
Configuration SetTimeZone 
{ 
    Param 
    ( 
        [String[]]$NodeName = $env:COMPUTERNAME 

    ) 

    Import-DSCResource -ModuleName xTimeZone 
 
 
    Node $NodeName 
    { 
         xTimeZone TimeZoneExample 
         { 
        
            TimeZone = 'Eastern Standard Time' 
         } 

         xTimeZone TimeZoneExample2
         {

            TimeZone = 'Pacific Standard Time'

         }        

    } 
} 
```

<span data-ttu-id="23100-109">Это вызвано особенностями в работе ключей ресурсов DSC.</span><span class="sxs-lookup"><span data-stu-id="23100-109">This is because of the way DSC resource keys work.</span></span> <span data-ttu-id="23100-110">Ресурс должен иметь по крайней мере одно свойство ключа.</span><span class="sxs-lookup"><span data-stu-id="23100-110">A resource must have at least one key property.</span></span> <span data-ttu-id="23100-111">Экземпляр ресурса считается уникальным, если сочетание значений всех его свойств ключа является уникальным.</span><span class="sxs-lookup"><span data-stu-id="23100-111">A resource instance is considered unique if the combination of the values of all of its key properties is unique.</span></span> <span data-ttu-id="23100-112">В предыдущей реализации ресурс [xTimeZone](https://github.com/PowerShell/xTimeZone) имел только одно свойство — **TimeZone**, которое должно было быть ключом.</span><span class="sxs-lookup"><span data-stu-id="23100-112">In its previous implementation, the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource had only one property--**TimeZone**, which was required to be a key.</span></span> <span data-ttu-id="23100-113">По этой причине такая конфигурация, как приведенная выше, компилируется и выполняется без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="23100-113">Because of this, a configuration such as the one above would compile and run without warning.</span></span> <span data-ttu-id="23100-114">Каждый из блоков ресурсов **xTimeZone** считается уникальным.</span><span class="sxs-lookup"><span data-stu-id="23100-114">Each of the **xTimeZone** resource blocks is considered unique.</span></span> <span data-ttu-id="23100-115">Это приводит к многократному применению конфигурации к узлу с циклическим изменением часового пояса вперед и назад.</span><span class="sxs-lookup"><span data-stu-id="23100-115">This would cause the configuration to be repeatedly applied to the node, cycling the timezone back and forth.</span></span>

<span data-ttu-id="23100-116">Чтобы гарантировать, что конфигурация может задать часовой пояс для целевого узла всего один раз, для ресурса было добавлено второе свойство — **IsSingleInstance**, которое стало свойством ключа.</span><span class="sxs-lookup"><span data-stu-id="23100-116">To ensure that a configuration could set the time zone for a target node only once, the resource was updated to add a second property, **IsSingleInstance**, that became the key property.</span></span> <span data-ttu-id="23100-117">**IsSingleInstance** было ограничено единственным значением "Yes" с помощью **ValueMap**.</span><span class="sxs-lookup"><span data-stu-id="23100-117">The **IsSingleInstance** was limited to a single value, "Yes" by using a **ValueMap**.</span></span> <span data-ttu-id="23100-118">Старая MOF-схема для ресурса:</span><span class="sxs-lookup"><span data-stu-id="23100-118">The old MOF schema for the resource was:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="23100-119">Новая MOF-схема для ресурса:</span><span class="sxs-lookup"><span data-stu-id="23100-119">The updated MOF schema for the resource is:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="23100-120">Сценарий ресурса также был изменен для использования нового параметра.</span><span class="sxs-lookup"><span data-stu-id="23100-120">The resource script was also updated to use the new parameter.</span></span> <span data-ttu-id="23100-121">Старый сценарий ресурса:</span><span class="sxs-lookup"><span data-stu-id="23100-121">Here is the old resource script:</span></span>

```powershell
function Get-TargetResource
{
    [CmdletBinding()]
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Get the current TimeZone
    $CurrentTimeZone = Get-TimeZone

    $returnValue = @{
        TimeZone = $CurrentTimeZone
        IsSingleInstance = 'Yes'
    }

    #Output the target resource
    $returnValue
}


function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )
    
    #Output the result of Get-TargetResource function.
    $CurrentTimeZone = Get-TimeZone
    
    if($PSCmdlet.ShouldProcess("'$TimeZone'","Replace the System Time Zone"))
    {
        try
        {
            if($CurrentTimeZone -ne $TimeZone)
            {
                Write-Verbose -Verbose "Setting the TimeZone"
                Set-TimeZone -TimeZone $TimeZone}
            else
            {
                Write-Verbose -Verbose "TimeZone already set to $TimeZone"
            }
        }
        catch
        {
            $ErrorMsg = $_.Exception.Message
            Write-Verbose -Verbose $ErrorMsg
        }
    }
}


function Test-TargetResource
{
    [CmdletBinding()]
    [OutputType([Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance, 

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output from Get-TargetResource
    $CurrentTimeZone = Get-TimeZone

    if($TimeZone -eq $CurrentTimeZone)
    {
        return $true
    }
    else
    {
        return $false
    }
}

Function Get-TimeZone {
    [CmdletBinding()]
    param()

    & tzutil.exe /g
}

Function Set-TimeZone {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [System.String]
        $TimeZone
    )

    try
    {
        & tzutil.exe /s $TimeZone
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose $ErrorMsg
    }
}

Export-ModuleMember -Function *-TargetResource
```

<span data-ttu-id="23100-122">Кроме того, свойство **TimeZone** больше не является ключом.</span><span class="sxs-lookup"><span data-stu-id="23100-122">Notice that the **TimeZone** property is no longer a key.</span></span> <span data-ttu-id="23100-123">Теперь, если конфигурация дважды пытается задать часовой пояс (используя два разных блока **xTimeZone** с различными значениями **TimeZone**), при ее компиляции возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="23100-123">Now, if a configuration attempts to set the time zone twice (by using two different **xTimeZone** blocks with different **TimeZone** values), attempting to compile the configuration will cause an error:</span></span>

```powershell
Test-ConflictingResources : A conflict was detected between resources '[xTimeZone]TimeZoneExample (::15::10::xTimeZone)' and 
'[xTimeZone]TimeZoneExample2 (::22::10::xTimeZone)' in node 'CONTOSO-CLIENT'. Resources have identical key properties but there are differences in the 
following non-key properties: 'TimeZone'. Values 'Eastern Standard Time' don't match values 'Pacific Standard Time'. Please update these property 
values so that they are identical in both cases.
At line:271 char:9
+         Test-ConflictingResources $keywordName $canonicalizedValue $k ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : ConflictingDuplicateResource,Test-ConflictingResources
Errors occurred while processing configuration 'SetTimeZone'.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3705 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (SetTimeZone:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```
   
