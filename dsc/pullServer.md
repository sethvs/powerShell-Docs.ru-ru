# Настройка опрашивающего веб-сервера DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Опрашивающий веб-сервер DSC — это веб-служба в IIS, которая использует интерфейс OData для создания файлов конфигурации DSC, доступных на целевых узлах при запросе.

Требования к использованию опрашивающего сервера:

* Сервер под управлением:
  - WMF/PowerShell 4.0 или более поздней версии
  - Роль сервера служб IIS
  - Служба DSC
* Рекомендуется использовать средства создания сертификата для защиты учетных данных, передаваемых в локальный диспетчер конфигураций (LCM) на целевых узлах

Вы можете добавить роль сервера служб IIS и службу DSC с помощью мастера добавления ролей и компонентов в диспетчере сервера или PowerShell. В примерах сценариев в этом разделе также охватываются оба шага.

## Использование ресурса xWebService
Самый простой способ настроить опрашивающий веб-сервер — использовать ресурс xWebService, включенный в модуль xPSDesiredStateConfiguration. В следующих действиях показано, как использовать ресурс в конфигурации, которая настраивает веб-службу.

1. Вызовите командлет [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx), чтобы установить модуль **xPSDesiredStateConfiguration**. **Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186). 
1. Создайте самозаверяющий сертификат с субъектом `"CN=PSDSCPullServerCert"` в хранилище `CERT:\LocalMachine\MY\`. Это можно сделать с помощью команды `New-SelfSignedCertificate  -CertStoreLocation 'CERT:\LocalMachine\MY' -DnsName "PSDSCPullServerCert"`.
1. В PowerShell ISE запустите (нажав клавишу F5) следующий сценарий конфигурации (включенный в пример папки модуля **xPSDesiredStateConfiguration** в качестве Sample_xDscWebService.ps1). Этот сценарий настраивает опрашивающий сервер и сервер соответствия.
  
```powershell
configuration Sample_xDscWebService 
6 { 
7     param  
8     ( 
9         [string[]]$NodeName = 'localhost', 
10 
 
11         [ValidateNotNullOrEmpty()] 
12         [string] $certificateThumbPrint 
13     ) 
14 
 
15     Import-DSCResource -ModuleName xPSDesiredStateConfiguration 
16 
 
17     Node $NodeName 
18     { 
19         WindowsFeature DSCServiceFeature 
20         { 
21             Ensure = "Present" 
22             Name   = "DSC-Service"             
23         } 
24 
 
25         xDscWebService PSDSCPullServer 
26         { 
27             Ensure                  = "Present" 
28             EndpointName            = "PSDSCPullServer" 
29             Port                    = 8080 
30             PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer" 
31             CertificateThumbPrint   = $certificateThumbPrint          
32             ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules" 
33             ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"             
34             State                   = "Started" 
35             DependsOn               = "[WindowsFeature]DSCServiceFeature"                         
36         } 
```

1. Запустите конфигурацию, передав отпечаток созданного самозаверяющего сертификата в параметре **certificateThumbPrint**:

```powershell
PS:\>$myCert = Get-ChildItem CERT: | Where-Object {$_.Subject -eq 'CN=PSDSCPullServerCert'}
PS:\>Sample_xDSCService -certificateThumbprint $myCert.Thumbprint 
```

## Ключ регистрации
Чтобы разрешить клиентским узлам регистрироваться на сервере для использования имен конфигурации вместо идентификатора, необходимо разместить ключ регистрации (GUID, известный как на узле сервера, так и на узле клиента) в файле `RegistrationKeys.txt`. По умолчанию опрашивающий сервер, созданный в этом примере, ожидает, что файл будет расположен в `C:\Program Files\WindowsPowerShell\DscService`. Создайте текстовый файл с одной строкой, состоящей из ключа регистрации, и сохраните его в папке.
> **Примечание**. Ключи регистрации не поддерживаются в PowerShell 4.0. 

## Размещение конфигураций и ресурсов
После завершения установки опрашивающего сервера в `$env:PROGRAMFILES\WindowsPowerShell` появилась новая папка с именем DscService. В этой папке содержатся две папки: Modules и Configuration. В папке Modules разместите все ресурсы, необходимые конфигурациям, которые узлы будут запрашивать с сервера. В папке Configuration разместите MOF-файлы конфигурации для любых конфигураций, которые будут запрошены с узлов. Имена MOF-файлов зависят от типа опрашивающего клиента. В следующих разделах настройка опрашивающих клиентов описывается более подробно:

* [Настройка опрашивающего клиента DSC с помощью идентификатора конфигурации](pullClientConfigID.md)
* [Настройка опрашивающего клиента DSC с помощью имен конфигурации](pullClientConfigNames.md)
* [Частичные конфигурации](partialConfigs.md)

## Создание контрольной суммы MOF
MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. Чтобы создать контрольную сумму, вызовите командлет [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx). Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.

Файл контрольной суммы должен находиться в том же каталоге, что и MOF-файл конфигурации (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` по умолчанию), и иметь то же имя, что и у добавленного расширения `.checksum`.

>**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

## См. также:
* [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
* [Активированные конфигурации](enactingConfigurations.md)
* [Извлечение сведений об узле с опрашивающего сервера DSC](retrieveNodeInfo.md)
<!--HONumber=Feb16_HO4-->
