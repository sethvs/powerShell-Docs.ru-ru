# Отправка отчета о состоянии конфигурации в центральное расположение

Подробные сведения о состоянии конфигурации DSC можно отправить на сервер, где выполняется служба DSC. В эту службу отправляются те же сведения, которые возвращает командлет Get-DscConfigurationStatus. После определения сервера отчетов в метаконфигурации это состояние отправляется на него при возникновении ошибки или успешном выполнении конфигурации. Отправка производится, если для узла настроен режим извлечения или принудительной отправки. Сведения о состоянии хранятся в базе данных службы DSC.

## Пример метаконфигурации для отправки отчетов о состоянии
```PowerShell
[DscLocalConfigurationManager()]
Configuration ReportingClientMetaConfig
{
    Settings
        {
            RefreshFrequencyMins = 30
            RefreshMode = "PUSH"
            ConfigurationModeFrequencyMins = 15
            AllowModuleOverwrite = $true
        }

        ReportServerWeb ReportManager
        {
            ServerUrL = "http://localhost:8080/PSDSCPullServer/PSDSCPullserver.svc"
            AllowUnsecureConnection  = $true
        }           
}
```
Службой DSC создается новая конечная точка OData, предоставляющая сведения о состоянии. Передав идентификатор конфигурации или агента {$guid} на конечную точку, можно выполнить сбор и анализ всех данных о состоянии для узла.

## Пример веб-запроса для сбора данных о состоянии конфигурации 
```PowerShell
$statusReports = Invoke-WebRequest -Uri "[http://localhost:8080/PSDSCPullserver/PSDSCPullserver.svc/Node(ConfigurationId='$guid')/StatusReport](http://localhost:8080/PSDSCPullserver/psdscpullserver.svc/Node(ConfigurationId='$guid')/StatusReport)s" -UseBasicParsing -UseDefaultCredentials -ContentType "application/json;odata=minimalmetadata;streaming=true;charset=utf-8" -Headers @{Accept = "application/json"; ProtocolVersion = “1.1”}
```<!--HONumber=Mar16_HO2-->
