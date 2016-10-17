---
title: "Модуль DSC и проверка подписи конфигурации"
author: jaimeo
contributor: berheabra
translationtype: Human Translation
ms.sourcegitcommit: 5c97ca6e93d31aaffc7e2207facc7658ee36dfb4
ms.openlocfilehash: 817fadb79716e41ce8cc8f4245dedc66347ac413

---

##Модуль DSC и проверка подписи конфигурации
В DSC документы и модули конфигурации распространяются на управляемые компьютеры с опрашивающего сервера или из опрашивающей службы (в случае опрашивающей службы автоматизации Azure). При компрометации опрашивающего сервера или службы злоумышленник может изменить конфигурации и модули на опрашивающем сервере и распространить их на все управляемые компьютеры, что также приведет к их компрометации. 

 В WMF 5.1 эта угроза устранена. DSC поддерживает проверку цифровых подписей файлов модулей и конфигурации (MOF-файлов). Эта возможность предотвращает выполнение файлов модулей или конфигурации, которые не были подписаны доверенным лицом или которые были изменены после подписания доверенным лицом. 



###Подписывание конфигурации и модулей 
***
1. Файлы конфигурации (MOF-файлы): поддержка подписывания MOF-файлов была добавлена к функциям существующего командлета PowerShell [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).  
2. Модули: для подписывания модулей необходимо подписать каталог соответствующего модуля, выполнив следующие действия. 
    * Создайте файл каталога: файл каталога содержит коллекцию криптографических хэшей или отпечатков. Каждый отпечаток соответствует файлу, включенному в модуль.  Был добавлен новый командлет [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), благодаря которому пользователи могут создавать файлы каталогов для своих модулей. Информацию о создании файлов каталогов с использованием командлетов для работы с каталогами см. [здесь](catalog-cmdlets.md). 
    * Подпишите файл каталога: подпишите файл каталога с помощью командлета [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).
    * Поместите файл каталога в папку модуля.
По соглашению файл каталога модуля должен находиться в папке модуля и имя файла каталога модуля должно совпадать с именем модуля.

###Параметры локального диспетчера конфигураций для включения проверки подписи.

####Получение
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
* Проверьте подпись в файле конфигурации (MOF-файл). Для проверки подписи диспетчер использует командлет PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), в котором в версии 5.1 была добавлена поддержка проверки подписей MOF.
* Убедитесь, что центр сертификации, который авторизовал подписывающую сторону, является доверенным.
* Скачайте зависимости модуля или ресурса конфигурации во временный каталог.
* Проверьте подпись каталога, включенного в модуль.
    * Найдите файл <moduleName>.cat и проверьте его подпись с помощью командлета [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).
    * Проверьте центр сертификации, который проверил подлинность доверенного лица.
    * Проверьте, чтобы содержимое модулей не было изменено, с помощью нового командлета, [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).
* Установите модуль в папку $env:ProgramFiles\WindowsPowerShell\Modules\
* Выполните конфигурацию.

Примечание. Проверка подписи каталога модуля и конфигурации выполняется только при первом применении конфигурации к системе или при скачивании и установке модуля. При проверке на согласованность не проверяется подпись файла Current.mof и зависимости для его модулей.
Если проверка на любом этапе завершается неудачно, например если конфигурация, полученная с опрашивающего сервера, не подписана, то обработка конфигурации будет прекращена с ошибкой, показанной ниже, и все временные файлы будут удалены.

![Пример ошибки конфигурации](../../images/PullUnsignedConfigFail.PNG)

Аналогично при попытке получения модуля, каталог для которого не подписан, появится следующая ошибка.

![Пример ошибки модуля](../../images/PullUnisgnedCatalog.PNG)

####Принудительная отправка
Конфигурация, переданная на узел при помощи принудительной отправки, может быть изменена злоумышленником в месте ее отправки. Локальный диспетчер конфигураций выполняет похожие действия для проверки подписи для принудительно отправленных и опубликованных конфигураций.
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
![Ошибка "MOF-файл не подписан"](../../images/PushUnsignedMof.PNG)

* Подпишите конфигурационный файл с помощью сертификата подписи кода.

![Подписанный MOF-файл](../../images/SignMofFile.PNG)

* Попробуйте отправить подписанный MOF-файл.

![Подписанный MOF-файл](../../images/PushSignedMof.PNG)




<!--HONumber=Aug16_HO3-->


