# Создание командлетов PowerShell на основе конечной точки OData
Создание командлетов Windows PowerShell на основе конечной точки OData
--------------------------------------------------------------

Командлет **Export-ODataEndpointProxy** создает набор командлетов Windows PowerShell в зависимости от функциональности, предоставляемой заданной конечной точкой OData.

В следующем примере показано, как использовать этот новый командлет:

\# Базовый вариант использования Export-ODataEndpointProxy

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

Ключевые компоненты вариантов использования для этой функции по-прежнему находятся в разработке, включая следующее:
-   Сопоставления
-   Передача потоков

Создание командлетов Windows PowerShell на основе конечной точки OData с помощью ODataUtils
------------------------------------------------------------------------------
Модуль ODataUtils позволяет создавать командлеты Windows PowerShell на базе конечных точек REST, которые поддерживают OData. В модуль Microsoft.PowerShell.ODataUtils Windows PowerShell внесены следующие дополнительные усовершенствования:
-   Передача дополнительных сведений с серверной конечной точки на сторону клиента
-   Поддержки разбивки на страницы на стороне клиента
-   Фильтрация на стороне сервера с помощью параметра Select
-   Поддержка заголовков веб-запросов

Командлеты прокси-сервера, созданные с помощью командлета Export-ODataEndPointProxy, предоставляют дополнительные сведения (которая не упоминается в $metadata, используемом во время создания прокси на стороне клиента) с серверной конечной точки OData в потоке информации (новая функция Windows PowerShell 5.0). Ниже приведен пример того, как получить эту информацию.
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

Записи со стороны сервера можно получить в пакетах, используя поддержку разбивки на страницы на стороне клиента. Это удобно, когда требуется получить большой объем данных с сервера по сети.
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

Созданные командлеты прокси-сервера поддерживают параметр –Select, который можно использовать в качестве фильтра, чтобы получить только свойства записей, необходимые клиенту. Это уменьшает объем передаваемых по сети данных, поскольку фильтрация выполняется на стороне сервера.
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

Командлет Export-ODataEndpointProxy и созданные им командлеты прокси-сервера теперь поддерживают параметр Headers (предоставление значений в виде хэш-таблицы), который можно использовать для передачи любых дополнительных сведений, ожидаемых серверной конечной точкой OData. В следующем примере можно передать ключ Subscription через параметр Headers для служб, которые ожидают этот ключ для проверки подлинности.
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```


<!--HONumber=Jun16_HO4-->


