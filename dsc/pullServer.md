---
title: "Настройка опрашивающего веб-сервера DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: a5f3025ff222d4a27c0da074df9e84d82c51a46f
ms.openlocfilehash: 7bbfc31fdebdde83ac1784373b51af40b1dc9492

---

# Настройка опрашивающего веб-сервера DSC

> Область применения: Windows PowerShell 5.0

Опрашивающий веб-сервер DSC — это веб-служба в IIS, которая использует интерфейс OData для создания файлов конфигурации DSC, доступных на целевых узлах при запросе.

Требования к использованию опрашивающего сервера:

* Сервер под управлением:
  - WMF/PowerShell 5.0 или более поздней версии
  - Роль сервера служб IIS
  - Служба DSC
* Рекомендуется использовать средства создания сертификата для защиты учетных данных, передаваемых в локальный диспетчер конфигураций (LCM) на целевых узлах

Вы можете добавить роль сервера служб IIS и службу DSC с помощью мастера добавления ролей и компонентов в диспетчере сервера или PowerShell. В примерах сценариев в этом разделе также охватываются оба шага.

## Использование ресурса xWebService
Самый простой способ настроить опрашивающий веб-сервер — использовать ресурс xWebService, включенный в модуль xPSDesiredStateConfiguration. В следующих действиях показано, как использовать ресурс в конфигурации, которая настраивает веб-службу.

1. Вызовите командлет [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx), чтобы установить модуль **xPSDesiredStateConfiguration**. **Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186). 
1. Получите SSL-сертификат для опрашивающего сервера DSC из доверенного центра сертификации (публичного или входящего в состав вашей организации). Сертификат, полученный от центра сертификации, обычно имеет формат PFX. Установите сертификат на узле, который должен стать опрашивающим сервером DSC, в расположении по умолчанию (CERT:\LocalMachine\My). Запишите отпечаток сертификата.
1. Выберите идентификатор GUID для использования в качестве ключа регистрации. Для его создания с помощью PowerShell введите следующую команду в командной строке PS и нажмите клавишу ВВОД: "``` [guid]::newGuid()```". Этот ключ будет использоваться клиентскими узлами в качестве общего ключа для проверки подлинности во время регистрации. Дополнительные сведения см. в разделе [Ключ регистрации](#RegKey) ниже.
1. В PowerShell ISE запустите (нажав клавишу F5) следующий сценарий конфигурации (включенный в пример папки модуля **xPSDesiredStateConfiguration** в качестве Sample_xDscWebService.ps1). Этот сценарий настраивает опрашивающий сервер.
  
```powershell
configuration Sample_xDscPullServer
{ 
    param  
    ( 
            [string[]]$NodeName = 'localhost', 
            
            [ValidateNotNullOrEmpty()] 
            [string] $certificateThumbPrint,
            
            [Parameter(Mandatory)]
            [ValidateNotNullOrEmpty()]
            [string] $RegistrationKey 
     ) 
 
 
     Import-DSCResource -ModuleName xPSDesiredStateConfiguration 

     Node $NodeName 
     { 
         WindowsFeature DSCServiceFeature 
         { 
             Ensure = 'Present'
             Name   = 'DSC-Service'             
         } 
 
         xDscWebService PSDSCPullServer 
         { 
             Ensure                  = 'Present' 
             EndpointName            = 'PSDSCPullServer' 
             Port                    = 8080 
             PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer" 
             CertificateThumbPrint   = $certificateThumbPrint          
             ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules" 
             ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration" 
             State                   = 'Started'
             DependsOn               = '[WindowsFeature]DSCServiceFeature'                         
         } 

        File RegistrationKeyFile
        {
            Ensure          = 'Present'
            Type            = 'File'
            DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
            Contents        = $RegistrationKey
        }
    }
}

```

1. Запустите конфигурацию, передав отпечаток SSL-сертификата в виде параметра **certificateThumbPrint** и ключ регистрации GUID в виде параметра **RegistrationKey**:

```powershell
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certifcates in your local store 
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

## Ключ регистрации
Чтобы разрешить клиентским узлам регистрироваться на сервере для использования имен конфигурации вместо идентификаторов конфигурации, созданный конфигурацией ключ конфигурации сохраняется в файле `RegistrationKeys.txt` и `C:\Program Files\WindowsPowerShell\DscService`. Ключ регистрации работает как общий секрет, используемый во время первоначальной регистрации клиента с опрашивающим сервером. Клиент создает самозаверяющий сертификат, который используется для уникальной проверки подлинности на опрашивающем сервере после успешного завершения регистрации. Отпечаток этого сертификата хранится локально и связывается с URL-адресом опрашивающего сервера.
> **Примечание**. Ключи регистрации не поддерживаются в PowerShell 4.0. 

Для настройки проверки подлинности узла на опрашивающем сервере необходимо поместить ключ регистрации в метаконфигурацию всех целевых узлов, которые будут регистрироваться на этом опрашивающем сервере. Обратите внимание, что **RegistrationKey** в метаконфигурации ниже удаляется после успешной регистрации целевого компьютера и значение "140a952b-b9d6-406b-b416-e0f759c9c0e4" должно соответствовать значению в файле RegistrationKeys.txt на опрашивающем сервере. Значение ключа регистрации должно оставаться конфиденциальным, так как с ним любой целевой компьютер сможет зарегистрироваться на опрашивающем сервере.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
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
            ServerURL          = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey    = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }   
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
        }
    }
}

PullClientConfigID -OutputPath c:\Configs\TargetNodes
```
> **Примечание**. Раздел **ReportServerWeb** позволяет отправлять данные отчетов на опрашивающий сервер. 

Отсутствие свойства **ConfigurationID** в файле метаконфигурации неявно означает, что опрашивающий сервер поддерживает версию 2 протокола опрашивающего сервера и требуется начальная регистрация. Наоборот, наличие свойства **ConfigurationID** означает, что используется версия 1 протокола опрашивающего сервера и регистрация не выполняется.

>**Примечание**. В сценарии PUSH в текущем выпуске есть ошибка, из-за которой необходимо определять свойство ConfigurationID в файле метаконфигурации для узлов, которые никогда не регистрировались на опрашивающем сервере. Это приведет к принудительному использованию версии 1 протокола опрашивающего сервера и позволит избежать сообщений об ошибках регистрации.

## Размещение конфигураций и ресурсов
После завершения установки опрашивающего сервера папки для размещения модулей и конфигурации, которые будут доступны целевым узлам, задаются свойствами **ConfigurationPath** и **ModulePath** в конфигурации опрашивающего сервера. Для правильной обработки опрашивающим сервером эти файлы должны иметь специальный формат. 

### Формат пакета модуля для ресурсов DSC
Каждый модуль ресурса необходимо упаковать в ZIP-архив и переименовать по шаблону **{название_модуля}_{версия_модуля}.zip**. Например, модуль с именем xWebAdminstration с версией модуля 3.1.2.0 будет иметь имя "xWebAdministration_3.2.1.0.zip". Каждая версия модуля должна находиться в собственном ZIP-файле. Поскольку в каждом ZIP-файле существует только одна версия ресурса, формат модулей с поддержкой нескольких версий модуля в одном каталоге, который появился в WMF 5.0, не поддерживается. Это означает, что перед упаковкой модулей ресурсов DSC для опрашивающего сервера необходимо внести небольшое изменение в структуру каталогов. Формат модулей, содержащих ресурсы DSC, в WMF 5.0 по умолчанию таков: "{папка_модуля}\{{версия_модуля}\DscResources\{{папка_ресурса_DSC}\'. Перед упаковкой для опрашивающего сервера просто удалите папку **{версия_модуля}**, чтобы путь стал таким: "{папка_модуля}\DscResources\{{папка_ресурса_DSC}\'. Выполнив это изменение, упакуйте папку в ZIP-архив, как описано выше, и поместите ZIP-архивы в папку **ModulePath**.

### Формат файлов конфигурации MOF 
MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. Чтобы создать контрольную сумму, вызовите командлет [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx). Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке. Поместите файлы MOF и их файлы контрольной суммы в папку **ConfigurationPath**.

>**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

## Инструменты
Для упрощения настройки, проверки опрашивающего сервера и управления им в последнюю версию модуля xPSDesiredStateConfiguration в качестве примеров включены следующие инструменты:
1. Модуль, который помогает упаковывать модули ресурсов и конфигурационные файлы DSC для использования на опрашивающем сервере. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Примеры ниже:

```powershell
    # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
     $moduleList = @("xWebAdministration", "xPhp") 
     Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList 
     
     # Example 2 - Package modules and mof documents from c:\LocalDepot
     Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
```

1. Сценарий, который проверяет, что опрашивающий сервер настроен правильно. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/Examples/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).


## Настройка опрашивающего клиента 
В следующих разделах настройка опрашивающих клиентов описывается более подробно:

* [Настройка опрашивающего клиента DSC с помощью идентификатора конфигурации](pullClientConfigID.md)
* [Настройка опрашивающего клиента DSC с помощью имен конфигурации](pullClientConfigNames.md)
* [Частичные конфигурации](partialConfigs.md)


## См. также:
* [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
* [Применение конфигураций](enactingConfigurations.md)
* [Использование сервера отчетов DSC](reportServer.md)




<!--HONumber=Jun16_HO4-->


