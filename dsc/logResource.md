---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Log в DSC
ms.openlocfilehash: f1a528767508d4a0e7f0ea2e58fd27a6a4d7ec75
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-log-resource"></a><span data-ttu-id="b7070-103">Ресурс Log в DSC</span><span class="sxs-lookup"><span data-stu-id="b7070-103">DSC Log Resource</span></span>

> <span data-ttu-id="b7070-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b7070-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b7070-105">Ресурс __Log__ в DSC Windows PowerShell предоставляет механизм записи сообщений в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="b7070-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

<span data-ttu-id="b7070-106">ПРИМЕЧАНИЕ. По умолчанию включены только операционные журналы DSC.</span><span class="sxs-lookup"><span data-stu-id="b7070-106">NOTE: By default only the Operational logs for DSC are enabled.</span></span>
<span data-ttu-id="b7070-107">Чтобы журнал аналитики стал доступным или видимым, его необходимо включить.</span><span class="sxs-lookup"><span data-stu-id="b7070-107">Before the Analytic log will be available or visible, it must be enabled.</span></span>
<span data-ttu-id="b7070-108">См. следующую статью.</span><span class="sxs-lookup"><span data-stu-id="b7070-108">See the following article.</span></span>

[<span data-ttu-id="b7070-109">Где находятся журналы событий DSC?</span><span class="sxs-lookup"><span data-stu-id="b7070-109">Where are DSC Event Logs?</span></span>](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a><span data-ttu-id="b7070-110">Свойства</span><span class="sxs-lookup"><span data-stu-id="b7070-110">Properties</span></span>
|  <span data-ttu-id="b7070-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="b7070-111">Property</span></span>  |  <span data-ttu-id="b7070-112">Описание</span><span class="sxs-lookup"><span data-stu-id="b7070-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="b7070-113">Сообщение</span><span class="sxs-lookup"><span data-stu-id="b7070-113">Message</span></span>| <span data-ttu-id="b7070-114">Указывает сообщение для записи в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="b7070-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>|
| <span data-ttu-id="b7070-115">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b7070-115">DependsOn</span></span> | <span data-ttu-id="b7070-116">Указывает, что перед записью этого сообщения в журнал необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b7070-116">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="b7070-117">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b7070-117">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="b7070-118">Пример</span><span class="sxs-lookup"><span data-stu-id="b7070-118">Example</span></span>

<span data-ttu-id="b7070-119">В следующем примере показано, как добавить сообщение в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="b7070-119">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> <span data-ttu-id="b7070-120">**Примечание**. Если этот ресурс настроен, при выполнении командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) всегда возвращается значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="b7070-120">**Note**: if you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```