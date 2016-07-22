---
title: "Усовершенствования DSC в WMF 5.1 (предварительная версия)"
ms.date: 2016-07-13
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
translationtype: Human Translation
ms.sourcegitcommit: 57049ff138604b0e13c8fd949ae14da05cb03a4b
ms.openlocfilehash: 1f00f2706f3c3ece783590f3a2b0bdb6734402b0

---

#Усовершенствования в настройке требуемого состояния (DSC) в WMF 5.1

## Усовершенствования в ресурсах класса DSC

В WMF 5.1 были устранены следующие известные проблемы.
* Командлет Get-DscConfiguration может возвращать пустые значения (NULL) или ошибки, если функция Get() ресурса DSC на основе класса возвращает сложный тип или хэш-таблицу.
* Командлет Get-DscConfiguration возвращает ошибку, если в конфигурации DSC используются учетные данные для запуска от имени.
* Ресурсы на основе класса не могут использоваться в составной конфигурации.
* Командлет Start-DscConfiguration зависает, если ресурс на основе класса имеет свойство с собственным типом.
* Ресурсы на основе класса не могут использоваться в качестве монопольных ресурсов.


## Усовершенствования в отладке ресурсов DSC

В WMF 5.0 отладчик PowerShell не останавливался непосредственно в методах для работы с ресурсами класса (Get, Set, Test).
В WMF 5.1 отладчик будет останавливаться в методах для работы с ресурсами класса точно так же, как в методах для работы с ресурсами на основе MOF.

## Опрашивающий клиент DSC поддерживает TLS 1.1 и TLS 1.2 
Ранее опрашивающий клиент DSC поддерживал только SSL3.0 и TLS1.0 через подключения по протоколу HTTPS. При принудительном использовании более безопасных протоколов опрашивающий клиент прекращал работу. В WMF 5.1 опрашивающий клиент DSC больше не поддерживает SSL 3.0, но поддерживает более безопасные протоколы TLS 1.1 и TLS 1.2.  

## Улучшенная регистрация опрашивающего сервера ##

В более ранних версиях WMF одновременные запросы регистрации или отчетов к опрашивающему серверу DSC при использовании базы данных ESENT привели бы к ошибке LCM в регистрации или получении отчета. В журналах событий на опрашивающем сервере в таких случаях появилась бы ошибка "Имя экземпляра уже используется".
Эта ошибка вызывалась тем, что для доступа к базе данных ESENT в сценарии с несколькими потоками использовался неправильный шаблон. В WMF 5.1 эта проблема устранена. Одновременные запросы регистрации или отчетов (с использованием базы данных ESENT) будут выполняться корректно в WMF 5.1. Эта проблема относится только к базе данных ESENT и не касается базы данных OLEDB. 

##Соглашение об именовании для частичной конфигурации
В предыдущем выпуске соглашение об именовании для частичной конфигурации было таким, что имя MOF-файла в опрашивающем сервере или службе должно было соответствовать имени частичной конфигурации, указанному в параметрах локального диспетчера конфигурации, которое, в свою очередь, должно соответствовать имени конфигурации, включенному в MOF-файл. 

См. моментальные снимки ниже.- •   Параметры локальной конфигурации, определяющие частичную конфигурацию, которую разрешено получать узлу.

![Пример метаконфигурации](../../images/MetaConfigPartialOne.png)

•   Пример определения частичной конфигурации 

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

•   "Имя конфигурации", включенное в созданный MOF-файл.

![Пример созданного MOF-файла](../../images/PartialGeneratedMof.png)

•   Имя файла в репозитории конфигураций 

![Имя файла в репозитории конфигураций](../../images/PartialInConfigRepository.png)

Служба автоматизации Azure создала MOF-файлы с именами <ConfigurationName>.<NodeName>.mof. Поэтому следующая конфигурация будет скомпилирована в файл PartialOne.Localhost.mof.

Это делало невозможным запрос к одной из частичных конфигураций в службе автоматизации Azure.

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

В WMF 5.1 частичная конфигурация в опрашивающем сервере или службе может иметь имя <ConfigurationName>.<NodeName>.mof. Кроме того, если компьютер запрашивает одну конфигурацию с опрашивающего сервера или службы, то файл конфигурации в репозитории конфигураций опрашивающего сервера может иметь любое имя. Эта гибкость в именовании позволяет управлять узлами, которые находятся под частичным управлением службы автоматизации Azure. В этом случае часть конфигурации узла поступает из DSC службы автоматизации Azure, а другой частью конфигурации вы управляете локально.

В следующей метаконфигурации узел находится как под локальным управлением, так и под управлением службы автоматизации Azure.

```Powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30;
            RefreshMode = "PULL";            
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation Service.
        PartialConfiguration PartialCOnfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"   
        }
    
        # This partial configuration is managed locally.
        PartialConfiguration OnPremConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   slcm -Path .\RegistrationMetaConfig -Verbose
 ```

# Использование параметра PsDscRunAsCredential с составными ресурсами DSC   

Добавлена поддержка использования параметра [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) с [составными](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) ресурсами DSC.    

Теперь пользователь может указать значение параметра PsDscRunAsCredential при использовании составных ресурсов в конфигурации. Если значение задано, все ресурсы, включенные в составной ресурс, также будут запущены от имени этого пользователя. Если составной ресурс вызывает другой составной ресурс, то все входящие в него ресурсы также будут запущены от имени этого пользователя.  Учетные данные запуска от имени распространяются на любой уровень иерархии составных ресурсов. Если для одного из ресурсов, входящих в составной ресурс, указано собственное значение параметра PsDscRunAsCredential, то при компиляции конфигурации будет выдана ошибка слияния.

В этом примере показано, как использовать этот параметр с составным ресурсом [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources), включенным в модуль PSDesiredStateConfiguration. 



```powershell

Configuration InstallWindowsFeature     
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features 
        {  
            Name = @("Telnet-Client","SNMP-Service")  
            Ensure = "Present"  
            IncludeAllSubFeature = $true  
            PsDscRunAsCredential = Get-Credential   
        }  
    }

}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost';
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData 

```

##Модуль DSC и проверка подписи конфигурации
В DSC конфигурации и модули распространяются на управляемые компьютеры с опрашивающего сервера. При компрометации опрашивающего сервера злоумышленник может изменить конфигурации и модули на опрашивающем сервере и распространить их на все управляемые узлы, что также приведет к их компрометации. 

 В WMF 5.1 DSC поддерживает проверку цифровых подписей файлов каталогов и конфигурации (MOF-файлов). Эта функция предотвращает выполнение конфигураций или файлов модулей, которые не были подписаны доверенным лицом или которые были изменены после подписания доверенным лицом. 



###Подписывание конфигурации и модулей 
***
* Файлы конфигурации (MOF-файлы): поддержка подписывания MOF-файлов была добавлена к функциям существующего командлета PowerShell [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).  
* Модули: для подписывания модулей необходимо подписать каталог соответствующего модуля, выполнив следующие действия. 
    1. Создайте файл каталога: файл каталога содержит коллекцию криптографических хэшей или отпечатков. Каждый отпечаток соответствует файлу, включенному в модуль. Был добавлен новый командлет [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), благодаря которому пользователи могут создавать файлы каталогов для своих модулей.
    2. Подпишите файл каталога: подпишите файл каталога с помощью командлета [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).
    3. Поместите файл каталога в папку модуля.
По соглашению файл каталога модуля должен находиться в папке модуля и имя файла каталога модуля должно совпадать с именем модуля.

###Параметры локального диспетчера конфигураций для включения проверки подписи

####По запросу
Локальный диспетчер конфигураций узла выполняет проверку подписи модулей и конфигураций в соответствии со своими текущими параметрами. По умолчанию проверка подписи отключена. Проверку подписи можно включить, добавив блок "SignatureValidation" в определение метаконфигурации узла, как показано ниже.

```PowerShell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'        
    } 
    
    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # By default,LCM will use default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM will use this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'            
        SignedItemType =  'Configuration','Module'         # Those are list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.       
    }
 
}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose 
 ```

Установка приведенной выше метаконфигурации для узла включает проверку подписи для загруженных конфигураций и модулей. Для проверки цифровых подписей локальный диспетчер конфигураций выполнит следующие действия.
1. Проверьте подпись в файле конфигурации (MOF-файл). Для проверки подписи диспетчер использует командлет PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), в котором в версии 5.1 была добавлена поддержка проверки подписей MOF.
2. Проверьте центр сертификации, который авторизовал доверенное лицо.
3. Скачайте зависимости модуля или ресурса конфигурации во временный каталог.
4. Проверьте подпись каталога, включенного в модуль.
    * Найдите файл <moduleName>.cat и проверьте его подпись с помощью командлета [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).
    * Проверьте центр сертификации, который проверил подлинность доверенного лица.
    * Проверьте, что содержимое модулей не было изменено, с помощью нового командлета [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).
5. Установите модуль в папку $env:ProgramFiles\WindowsPowerShell\Modules\
6. Выполните конфигурацию.

> Примечание. Проверка подписи каталога модуля и конфигурации выполняется только при первом применении конфигурации к системе или при скачивании и установке модуля. При проверке на согласованность не проверяется подпись файла Current.mof и зависимости для его модулей.
Если проверка на любом этапе завершается неудачно, например если конфигурация, полученная с опрашивающего сервера, не подписана, то обработка конфигурации будет завершена с ошибкой, показанной ниже, и все временные файлы будут удалены.

![Пример ошибки конфигурации](../../images/PullUnsignedConfigFail.png)

Аналогично при попытке получения модуля, каталог для которого не подписан, появится следующая ошибка.

![Пример ошибки модуля](../../images/PullUnisgnedCatalog.png)

####Принудительная отправка
Конфигурация, переданная на узел с помощью принудительной отправки, может быть изменена злоумышленником в месте ее отправки. Локальный диспетчер конфигураций выполняет похожие действия для проверки подписи для принудительно отправленных и опубликованных конфигураций.
Ниже приведен полный пример проверки подписи для принудительной отправки.

* Включите проверку подписи на узле.

```Powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'        
    } 
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'   
        SignedItemType =  'Configuration','Module'             
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
``` 
* Создайте пример файла конфигурации.

```Powershell
# Sample configuration
Configuration Test{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* Попробуйте принудительно отправить не подписанный файл конфигурации на узел. 

```Powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
``` 
![Ошибка "MOF-файл не подписан"](../../images/PushUnsignedMof.png)

* Подпишите конфигурационный файл с помощью сертификата подписи кода.

![Подписанный MOF-файл](../../images/SignMofFile.png)

* Попробуйте отправить подписанный MOF-файл.

![Подписанный MOF-файл](../../images/PushSignedMof.png)




<!--HONumber=Jul16_HO3-->


