---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Прямой вызов методов ресурсов DSC
ms.openlocfilehash: dbf0a4ada4c6cc2e7d65698b87a5a29a2ea84781
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="94305-103">Прямой вызов методов ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="94305-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="94305-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="94305-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="94305-105">Командлет [Invoke-DscResource](https://technet.microsoft.com/library/mt517869.aspx) можно использовать для прямого вызова функций или методов ресурса DSC (функций **Get-TargetResource**, **Set-TargetResource** и **Test-TargetResource** ресурса на основе MOF-файла или методов **Get**, **Set** и **Test** ресурса на основе класса).</span><span class="sxs-lookup"><span data-stu-id="94305-105">You can use the [Invoke-DscResource](https://technet.microsoft.com/library/mt517869.aspx) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span>
<span data-ttu-id="94305-106">Этот командлет могут использовать сторонние разработчики, которым требуется использовать ресурсы DSC, кроме того, он удобен для разработки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="94305-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span>

<span data-ttu-id="94305-107">Командлет обычно используется в сочетании со свойством метаконфигурации `refreshMode = 'Disabled'`, однако он доступен независимо от значения **refreshMode**.</span><span class="sxs-lookup"><span data-stu-id="94305-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="94305-108">При вызове командлета **Invoke-DscResource** указать, какой метод или функцию необходимо вызвать, можно с помощью параметра **Method**.</span><span class="sxs-lookup"><span data-stu-id="94305-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="94305-109">Свойства ресурса указываются путем передачи хэш-таблицы в качестве значения параметра **Property**.</span><span class="sxs-lookup"><span data-stu-id="94305-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="94305-110">Ниже приведены примеры прямого вызова методов ресурсов:</span><span class="sxs-lookup"><span data-stu-id="94305-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="94305-111">Проверка наличия файла</span><span class="sxs-lookup"><span data-stu-id="94305-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="94305-112">Тестирование наличия файла</span><span class="sxs-lookup"><span data-stu-id="94305-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="94305-113">Получение содержимого файла</span><span class="sxs-lookup"><span data-stu-id="94305-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="94305-114">**Примечание**. Прямой вызов методов составного ресурса не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="94305-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="94305-115">Вместо этого вызывайте методы базовых ресурсов, входящих в составной ресурс.</span><span class="sxs-lookup"><span data-stu-id="94305-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="94305-116">См. также</span><span class="sxs-lookup"><span data-stu-id="94305-116">See Also</span></span>
- [<span data-ttu-id="94305-117">Написание пользовательских ресурсов DSC с использованием MOF</span><span class="sxs-lookup"><span data-stu-id="94305-117">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md)
- [<span data-ttu-id="94305-118">Написание пользовательских ресурсов DSC с использованием классов PowerShell</span><span class="sxs-lookup"><span data-stu-id="94305-118">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="94305-119">Отладка ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="94305-119">Debugging DSC resources</span></span>](debugResource.md)