---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Прямой вызов методов ресурсов DSC"
ms.openlocfilehash: 3e83984fbf31dfcfec76fa15cdd9b83d92501aa0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="74e19-103">Прямой вызов методов ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="74e19-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="74e19-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="74e19-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="74e19-105">Командлет [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) можно использовать для прямого вызова функций или методов ресурса DSC (функций **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource** ресурса на основе MOF-файла или методов **Get**, **Set** и **Test** ресурса на основе класса).</span><span class="sxs-lookup"><span data-stu-id="74e19-105">You can use the [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span> <span data-ttu-id="74e19-106">Этот командлет могут использовать сторонние разработчики, которым требуется использовать ресурсы DSC, кроме того, он удобен для разработки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="74e19-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span> 

<span data-ttu-id="74e19-107">Командлет обычно используется в сочетании со свойством метаконфигурации `refreshMode = 'Disabled'`, однако он доступен независимо от значения **refreshMode**.</span><span class="sxs-lookup"><span data-stu-id="74e19-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="74e19-108">При вызове командлета **Invoke-DscResource** указать, какой метод или функцию необходимо вызвать, можно с помощью параметра **Method**.</span><span class="sxs-lookup"><span data-stu-id="74e19-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="74e19-109">Свойства ресурса указываются путем передачи хэш-таблицы в качестве значения параметра **Property**.</span><span class="sxs-lookup"><span data-stu-id="74e19-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="74e19-110">Ниже приведены примеры прямого вызова методов ресурсов:</span><span class="sxs-lookup"><span data-stu-id="74e19-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="74e19-111">Проверка наличия файла</span><span class="sxs-lookup"><span data-stu-id="74e19-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="74e19-112">Тестирование наличия файла</span><span class="sxs-lookup"><span data-stu-id="74e19-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="74e19-113">Получение содержимого файла</span><span class="sxs-lookup"><span data-stu-id="74e19-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="74e19-114">**Примечание**. Прямой вызов методов составного ресурса не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="74e19-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="74e19-115">Вместо этого вызывайте методы базовых ресурсов, входящих в составной ресурс.</span><span class="sxs-lookup"><span data-stu-id="74e19-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="74e19-116">См. также</span><span class="sxs-lookup"><span data-stu-id="74e19-116">See Also</span></span>
- [<span data-ttu-id="74e19-117">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="74e19-117">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md) 
- [<span data-ttu-id="74e19-118">Написание пользовательских ресурсов DSC с использованием классов PowerShell</span><span class="sxs-lookup"><span data-stu-id="74e19-118">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="74e19-119">Отладка ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="74e19-119">Debugging DSC resources</span></span>](debugResource.md)

