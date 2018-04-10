---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: a8947844df0da167961c64e1e09d5075960c95de
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a><span data-ttu-id="337bc-102">Создание командлетов PowerShell на основе конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="337bc-102">Generate PowerShell Cmdlets based on OData Endpoint</span></span>
<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a><span data-ttu-id="337bc-103">Создание командлетов Windows PowerShell на основе конечной точки OData</span><span class="sxs-lookup"><span data-stu-id="337bc-103">Generate Windows PowerShell cmdlets based on an OData endpoint</span></span>
--------------------------------------------------------------

<span data-ttu-id="337bc-104">Командлет **Export-ODataEndpointProxy** создает набор командлетов Windows PowerShell в зависимости от функциональности, предоставляемой заданной конечной точкой OData.</span><span class="sxs-lookup"><span data-stu-id="337bc-104">**Export-ODataEndpointProxy** is a cmdlet that generates a set of Windows PowerShell cmdlets based on the functionality exposed by a given OData endpoint.</span></span>

<span data-ttu-id="337bc-105">В следующем примере показано, как использовать этот новый командлет:</span><span class="sxs-lookup"><span data-stu-id="337bc-105">The following example shows how to use this new cmdlet:</span></span>

<span data-ttu-id="337bc-106">\# Базовый вариант использования Export-ODataEndpointProxy</span><span class="sxs-lookup"><span data-stu-id="337bc-106">\# Basic use case of Export-ODataEndpointProxy</span></span>

```powershell
Export-ODataEndpointProxy -Uri 'http://services.odata.org/v3/(S(snyobsk1hhutkb2yulwldgf1))/odata/odata.svc' -OutputModule C:\Users\user\Generated.psd1

ipmo 'C:\Users\user\Generated.psd1'
# Cmdlets are created based on the following heuristics
# New-<EntityType> -<Key> [-<Other Attributes>]
#
# Get-<EntityType> [-<Key> -Top –Skip –Filter -OrderBy]
# # If there is a complex key, the keys will actually be -<Key1> -<Key2>…
# # Note this rule applies to any other instances of the key
#
# Set-<EntityType> -<Key> [-<Other Attributes>]
#
# Remove-<EntityType> -<Key>
#
# Invoke-<EntityType><Action> [-<Key> -<Other Parameters>]
#
#
# Cmdlets from associations (Note: Get and Remove get additional parameter sets)
# Get-<EntityType> -<AssociatedEntity>
# New-<EntityType> -<AssociatedEntity> -<Key>
# Remove-<EntityType> -<AssociatedEntity> -<Key>
#
#
# Note: Every cmdlet has the –ConnectionURI parameter for explicitly setting the URI of the endpoint. This normally uses the same address that you gave the Export-ODataEndpointProxy cmdlet, but can be overridden in this fashion for the sake of similar endpoints.
#
```

<span data-ttu-id="337bc-107">Ключевые компоненты вариантов использования для этой функции по-прежнему находятся в разработке, включая следующее:</span><span class="sxs-lookup"><span data-stu-id="337bc-107">There are still parts of key use cases in development for this functionality, including, but not limited to:</span></span>
-   <span data-ttu-id="337bc-108">Сопоставления</span><span class="sxs-lookup"><span data-stu-id="337bc-108">Associations</span></span>
-   <span data-ttu-id="337bc-109">Передача потоков</span><span class="sxs-lookup"><span data-stu-id="337bc-109">Passing streams</span></span>

<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a><span data-ttu-id="337bc-110">Создание командлетов Windows PowerShell на основе конечной точки OData с помощью ODataUtils</span><span class="sxs-lookup"><span data-stu-id="337bc-110">Generate Windows PowerShell cmdlets based on an OData endpoint with ODataUtils</span></span>
------------------------------------------------------------------------------
<span data-ttu-id="337bc-111">Модуль ODataUtils позволяет создавать командлеты Windows PowerShell на базе конечных точек REST, которые поддерживают OData.</span><span class="sxs-lookup"><span data-stu-id="337bc-111">The ODataUtils module allows generation of Windows PowerShell cmdlets from REST endpoints that support OData.</span></span> <span data-ttu-id="337bc-112">В модуль Microsoft.PowerShell.ODataUtils Windows PowerShell внесены следующие дополнительные усовершенствования:</span><span class="sxs-lookup"><span data-stu-id="337bc-112">The following incremental enhancements are in the Microsoft.PowerShell.ODataUtils Windows PowerShell module.</span></span>
-   <span data-ttu-id="337bc-113">Передача дополнительных сведений с серверной конечной точки на сторону клиента</span><span class="sxs-lookup"><span data-stu-id="337bc-113">Channel additional information from server-side endpoint to client side.</span></span>
-   <span data-ttu-id="337bc-114">Поддержки разбивки на страницы на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="337bc-114">Client-side paging support</span></span>
-   <span data-ttu-id="337bc-115">Фильтрация на стороне сервера с помощью параметра Select</span><span class="sxs-lookup"><span data-stu-id="337bc-115">Server-side filtering by using the -Select parameter</span></span>
-   <span data-ttu-id="337bc-116">Поддержка заголовков веб-запросов</span><span class="sxs-lookup"><span data-stu-id="337bc-116">Support for web request headers</span></span>

<span data-ttu-id="337bc-117">Командлеты прокси-сервера, созданные с помощью командлета Export-ODataEndPointProxy, предоставляют дополнительные сведения (которая не упоминается в $metadata, используемом во время создания прокси на стороне клиента) с серверной конечной точки OData в потоке информации (новая функция Windows PowerShell 5.0).</span><span class="sxs-lookup"><span data-stu-id="337bc-117">The proxy cmdlets generated by the Export-ODataEndPointProxy cmdlet provide additional information (not mentioned in the $metadata used during the client-side proxy generation) from the server side OData endpoint on the Information stream (a new Windows PowerShell 5.0 feature).</span></span> <span data-ttu-id="337bc-118">Ниже приведен пример того, как получить эту информацию.</span><span class="sxs-lookup"><span data-stu-id="337bc-118">Here is an example of how to get that information.</span></span>
```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
Import-Module $generatedProxyModuleDir -Force

# In the below command, we are retrieving top 1 product.
# By specifying -IncludeTotalResponseCount parameter,
# we are getting the total count of all the Product records
# available on the server side. This information
# is surfaced on the client side through the Information stream.
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
# The Information stream contains the additional
# information sent from the server side.
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
# 'Odata.Count' indicates the total product records
# available on the server side Odata endpoint.
$additionalInfo['odata.count']
```

<span data-ttu-id="337bc-119">Записи со стороны сервера можно получить в пакетах, используя поддержку разбивки на страницы на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="337bc-119">You can get the records from the server side in batches by using client-side paging support.</span></span> <span data-ttu-id="337bc-120">Это удобно, когда требуется получить большой объем данных с сервера по сети.</span><span class="sxs-lookup"><span data-stu-id="337bc-120">This is useful when you must get a large amount of data from the server over the network.</span></span>
```powershell
$skipCount = 0
$batchSize = 3
# Client-Side Paging Support: The records from the server side
# are retrieved in batches of $batchSize
while($skipCount -le $additionalInfo['odata.count'])
{
Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
$skipCount += $batchSize
}
```

<span data-ttu-id="337bc-121">Созданные командлеты прокси-сервера поддерживают параметр –Select, который можно использовать в качестве фильтра, чтобы получить только свойства записей, необходимые клиенту.</span><span class="sxs-lookup"><span data-stu-id="337bc-121">The generated proxy cmdlets support the –Select parameter which you can use as a filter to receive only the record properties that the client needs.</span></span> <span data-ttu-id="337bc-122">Это уменьшает объем передаваемых по сети данных, поскольку фильтрация выполняется на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="337bc-122">This reduces the amount of data that is transferred over the network, because the filtering occurs on the server side.</span></span>
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

<span data-ttu-id="337bc-123">Командлет Export-ODataEndpointProxy и созданные им командлеты прокси-сервера теперь поддерживают параметр Headers (предоставление значений в виде хэш-таблицы), который можно использовать для передачи любых дополнительных сведений, ожидаемых серверной конечной точкой OData.</span><span class="sxs-lookup"><span data-stu-id="337bc-123">The Export-ODataEndpointProxy cmdlet, and the proxy cmdlets generated by it, now support the Headers parameter (supply values as a hash table), which you can use to channel any additional information that is expected by the server-side OData endpoint.</span></span> <span data-ttu-id="337bc-124">В следующем примере можно передать ключ Subscription через параметр Headers для служб, которые ожидают этот ключ для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="337bc-124">In the following example, you can channel a Subscription key through Headers for services that are expecting a Subscription key for authentication.</span></span>
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```