---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс Log в DSC"
ms.openlocfilehash: 72c9c5a9b8e2a4ed4ce43cfd792572ce95b502b3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-log-resource"></a><span data-ttu-id="bccb7-103">Ресурс Log в DSC</span><span class="sxs-lookup"><span data-stu-id="bccb7-103">DSC Log Resource</span></span> 

> <span data-ttu-id="bccb7-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bccb7-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="bccb7-105">Ресурс __Log__ в DSC Windows PowerShell предоставляет механизм записи сообщений в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="bccb7-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

<span data-ttu-id="bccb7-106">ПРИМЕЧАНИЕ. По умолчанию включены только операционные журналы DSC.</span><span class="sxs-lookup"><span data-stu-id="bccb7-106">NOTE: By default only the Operational logs for DSC are enabled.</span></span>
<span data-ttu-id="bccb7-107">Чтобы журнал аналитики стал доступным или видимым, его необходимо включить.</span><span class="sxs-lookup"><span data-stu-id="bccb7-107">Before the Analytic log will be available or visible, it must be enabled.</span></span>
<span data-ttu-id="bccb7-108">См. следующую статью.</span><span class="sxs-lookup"><span data-stu-id="bccb7-108">See the following article.</span></span>

[<span data-ttu-id="bccb7-109">Где находятся журналы событий DSC?</span><span class="sxs-lookup"><span data-stu-id="bccb7-109">Where are DSC Event Logs?</span></span>](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a><span data-ttu-id="bccb7-110">Свойства</span><span class="sxs-lookup"><span data-stu-id="bccb7-110">Properties</span></span>
|  <span data-ttu-id="bccb7-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="bccb7-111">Property</span></span>  |  <span data-ttu-id="bccb7-112">Описание</span><span class="sxs-lookup"><span data-stu-id="bccb7-112">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="bccb7-113">Сообщение</span><span class="sxs-lookup"><span data-stu-id="bccb7-113">Message</span></span>| <span data-ttu-id="bccb7-114">Указывает сообщение для записи в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="bccb7-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>| 
| <span data-ttu-id="bccb7-115">DependsOn</span><span class="sxs-lookup"><span data-stu-id="bccb7-115">DependsOn</span></span> | <span data-ttu-id="bccb7-116">Указывает, что перед записью этого сообщения в журнал необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bccb7-116">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="bccb7-117">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="bccb7-117">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="bccb7-118">Пример</span><span class="sxs-lookup"><span data-stu-id="bccb7-118">Example</span></span>

<span data-ttu-id="bccb7-119">В следующем примере показано, как добавить сообщение в журнал событий Microsoft-Windows-Desired State Configuration/Analytic.</span><span class="sxs-lookup"><span data-stu-id="bccb7-119">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> <span data-ttu-id="bccb7-120">**Примечание**. Если этот ресурс настроен, при выполнении командлета [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) всегда возвращается значение **$false**.</span><span class="sxs-lookup"><span data-stu-id="bccb7-120">**Note**: if you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

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

