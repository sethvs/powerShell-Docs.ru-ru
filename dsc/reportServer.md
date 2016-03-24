# Использование сервера отчетов DSC

> Область применения: Windows PowerShell 5.0

> **Примечание**. Сервер отчетов, описанный в этом разделе, недоступен в PowerShell 4.0. Сведения о создании отчетов в PowerShell 4.0 см. в разделе "Использование сервера соответствия DSC".

В локальном диспетчере конфигураций (LCM) узла можно настроить отправку отчетов о состоянии конфигурации на опрашивающий сервер, которые затем можно запросить для извлечения содержащихся в них данных. Каждый раз при проверке и применении
конфигурации узел отправляет отчет на сервер отчетов. Эти отчеты хранятся в базе данных на сервере, и их можно извлечь, вызвав веб-службу отчетов. Каждый отчет содержит
сведения, например перечень примененных конфигураций и данные о том, успешно ли они были выполнены, использованные ресурсы, любые произошедшие ошибки, а также время начала и окончания.

## Настройка узла для отправки отчетов

Запросить на узле отправку отчетов на сервер можно с помощью блока **ReportServerWeb** в конфигурации LCM узла (сведения о настройке LCM
 см. в разделе [Настройка локального диспетчера конфигураций](metaConfig.md)). Сервер, на который узел отправляет отчеты, необходимо настроить как опрашивающий веб-сервер (отправлять отчеты
 в общую папку SMB невозможно). Сведения о настройке опрашивающего сервера см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md). Сервер отчетов может быть той же службой, в которой
 узел извлекает конфигурации и получает ресурсы, или другой службой.
 
 В блоке **ReportServerWeb** укажите URL-адрес опрашивающей службы
 и ключ регистрации, известный серверу.
 
  Следующая конфигурация настраивает на узле извлечение конфигураций из службы и отправку отчетов
 в службу на другом сервере. 
 
```powershell
[DSCLocalConfigurationManager()]
configuration ReportClientConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode          = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded   = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = 'https://CONTOSO-PULL:8080/PSDSCPullServer.svc'
            RegistrationKey    = 'bbb9778f-43f2-47de-b61e-a0daff474c6d'
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL               = 'http://CONTOSO-REPORT:8080/PSDSCReportServer.svc'
            RegistrationKey         = 'ba39daaa-96c5-4f2f-9149-f95c46460faa'
            AllowUnsecureConnection = $true
        }
    }
}
PullClientConfigID
```

## Получение данных из отчетов

Отчеты, отправляемые на опрашивающий сервер, добавляются в базу данных на сервере. Отчеты доступны путем вызовов веб-службы. Чтобы извлечь отчеты с указанного узла, 
отправьте HTTP-запрос в веб-службу отчетов в следующем формате:
`http://CONTOSO-REPORT:8080/PSDSCReportServer.svc/Nodes(AgentID = MyNodeAgentId)/Reports` 
где `MyNodeAgentId` — это AgentId узла, с которого вы хотите получать отчеты. Вы можете получить AgentID узла, вызвав [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx)
на этом узле.

Отчеты возвращаются в виде массива объектов JSON.

Следующий сценарий возвращает отчеты для узла, на котором он выполняется:

```powershell
function GetReport
{
    param($AgentId = "$((glcm).AgentId)", $serviceURL = "http://CONTOSO-REPORT:8080/PSDSCReportServer.svc")
    $requestUri = "$serviceURL/Nodes(AgentId= '$AgentId')/Reports"
    $request = Invoke-WebRequest -Uri $requestUri  -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" `
               -UseBasicParsing -Headers @{Accept = "application/json";ProtocolVersion = "2.0"} `
               -ErrorAction SilentlyContinue -ErrorVariable ev
    $object = ConvertFrom-Json $request.content
    return $object.value
}
```
    
## Просмотр данных из отчетов

Если задать для переменной результат функции **GetReport**, можно просмотреть отдельные поля в элементе возвращаемого массива:

```powershell
$reports = GetReport
$reports[1]

JobId                : 71515ae8-7294-40a3-8137-fc85bf4b678f
OperationType        : Consistency
RefreshMode          : 
Status               : 
ReportFormatVersion  : 1.0
ConfigurationVersion : 2.0.0
StartTime            : 02/08/2016 01:28:54
EndTime              : 02/08/2016 01:28:57
RebootRequested      : False
Errors               : {}
StatusData           : {{"NumberOfResources":"2","Locale":"en-US","ResourcesInDesiredState":[{"ResourceId":"[WindowsFeature]MyFeatureInstance","SourceI
                       nfo":"C:\\ReportTest\\ClientConfig.ps1::4::9::WindowsFeature","ModuleName":"PsDesiredStateConfiguration","ModuleVersion":"1.0","
                       ConfigurationName":"ClientConfig","ResourceName":"WindowsFeature"},{"ResourceId":"[WindowsFeature]My2ndFeatureInstance","SourceI
                       nfo":"C:\\ReportTest\\ClientConfig.ps1::8::9::WindowsFeature","ModuleName":"PsDesiredStateConfiguration","ModuleVersion":"1.0","
                       ConfigurationName":"ClientConfig","ResourceName":"WindowsFeature"}]}}
```

Обратите внимание, что поле **StatusData** является объектом с тремя свойствами: **NumberOfResources**, **Locale** и **ResourcesInDesiredState**. Свойство **ResourcesInDesiredState**
является массивом объектов, каждый из который содержит ряд свойств. Следующий сценарий получает отчет в виде параметра, выполняет итерацию по массиву **ResourcesInDesiredState**
и выводит данные на консоль:
 
```powershell
function GetStatusData
{
    param ($Report)
    $statusData = $Report.StatusData | ConvertFrom-Json

    $Resources = $statusData.ResourcesInDesiredState

    Foreach ($Resource in $Resources)
    {
        Write-Host 'ResourceId: ' $Resource.ResourceId
        Write-Host 'SourceInfo: ' $Resource.SourceInfo
        Write-Host 'ModuleName: ' $Resource.ModuleName
        Write-Host 'ModuleVersion: ' $Resource.ModuleVersion
        Write-Host 'ConfigurationName: ' $Resource.ConfigurationName
        Write-Host 'ResourceName: ' $Resource.ResourceName
        Write-Host
    }
}
```

Ниже приведен пример выходных данных после вызова функции **GetStatusData**:

```powershell
GetStatusData -Report $report[1]

ResourceId:  [WindowsFeature]MyFeatureInstance
SourceInfo:  C:\ReportTest\ClientConfig.ps1::4::9::WindowsFeature
ModuleName:  PsDesiredStateConfiguration
ModuleVersion:  1.0
ConfigurationName:  ClientConfig
ResourceName:  WindowsFeature

ResourceId:  [WindowsFeature]My2ndFeatureInstance
SourceInfo:  C:\ReportTest\ClientConfig.ps1::8::9::WindowsFeature
ModuleName:  PsDesiredStateConfiguration
ModuleVersion:  1.0
ConfigurationName:  ClientConfig
ResourceName:  WindowsFeature
```

Обратите внимание, что эти примеры призваны дать представление о том, что вы можете сделать с данными из отчетов. Общие сведения о работе с JSON в PowerShell см. в разделе
[Работа с JSON и PowerShell](https://blogs.technet.microsoft.com/heyscriptingguy/2015/10/08/playing-with-json-and-powershell/).

## См. также
>[Настройка локального диспетчера конфигураций](metaConfig.md)
>[Настройка опрашивающего веб-сервера DSC](pullServer.md)
>[Настройка опрашивающего клиента с помощью имен конфигураций](pullClientConfigNames.md)
<!--HONumber=Feb16_HO4-->
