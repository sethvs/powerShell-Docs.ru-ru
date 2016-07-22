---
title: "Контрольный список для создания ресурсов"
ms.date: 2016-07-11
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 4a7c9bfa0f22930732776b510d5cc4b0275424ff
ms.openlocfilehash: b2900987b1102cf41880e5af0a0cc44bc6499ef5

---

# Контрольный список для создания ресурсов
Это список рекомендаций, которых нужно придерживаться при создании нового ресурса DSC.
## Модуль ресурсов содержит PSD1-файл и SCHEMA.MOF-файл для каждого ресурса 
Убедитесь, что ресурс имеет правильную структуру и содержит все необходимые файлы. Каждый модуль ресурсов должен содержать PSD1-файл, а каждый несоставной ресурс должен иметь SCHEMA.MOF-файл. Ресурсы, которые не содержат схему, не выводятся **Get-DscResource**, и пользователи не смогут использовать IntelliSense при написании кода для этих модулей в интегрированной среде сценариев. Структура каталогов для ресурса xRemoteFile, который является частью [модуля ресурсов xPSDesiredStateConfiguration](https://github.com/PowerShell/xPSDesiredStateConfiguration), выглядит следующим образом.


```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## Ресурс и схема верны##
Проверьте файл схемы ресурса (*.schema.mof). Для разработки и проверки схемы можно использовать [Конструктор ресурсов DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/). Убедитесь в следующем.
- Типы свойств являются правильными (например, не используйте String для свойств, принимающих числовые значения, в таких случаях следует использовать UInt32 или другие числовые типы).
- Атрибуты свойств указаны правильно: ([key], [required], [write], [read]).
- По меньшей мере один параметр в схеме должен быть помечен как [key].
- Свойство [read] невозможно использовать совместно с любым из следующих свойств: [required], [key], [write].
- Если указано несколько квалификаторов кроме [read], то [key] имеет приоритет.
- Если указаны [write] and [required], то приоритет имеет [required].
- Где необходимо, указан ValueMap.

Пример:
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- Понятное имя указано и соответствует соглашениям об именовании DSC.

Пример:
```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```

- Каждое поле имеет осмысленное описание. В репозитории GitHub PowerShell есть хорошие примеры, такие как [схема .schema.mof для xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof).

Кроме того, следует использовать командлеты **Test-xDscResource** и **Test-xDscSchema** из [Конструктора ресурсов DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) для автоматической проверки ресурса и схемы.
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
Например:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## Ресурс загружается без ошибок ##
Проверьте, загружен ли модуль ресурсов.
Это можно сделать вручную, выполнив команду `Import-Module <resource_module> -force ` и убедившись в отсутствии ошибок, или создав средства автоматизированного тестирования. В последнем случае вы можете применить для тестового случая приведенную ниже структуру:
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## В положительном случае ресурс является идемпотентным. 
Одной из фундаментальных характеристик ресурсов DSC является идемпотентность. Это означает, что при каждом применении конфигурации DSC, содержащей этот ресурс, результаты будут одинаковыми. Например, если мы создадим конфигурацию со следующим файлом ресурсов.
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
} 
```
После первого ее применения файл test.txt должен появится в папке C:\test. Однако последующие запуски с такой же конфигурацией не должны изменять состояние компьютера (например, не должны создаваться копии файла test.txt).
Для подтверждения идемпотентности ресурса можно несколько раз вызвать командлет **Set-TargetResource** при тестировании ресурса напрямую или командлет **Start-DscConfiguration** при комплексном тестировании. Результат должен быть идентичным после каждого запуска. 


## Проверка сценария с изменением пользователя ##
Изменив состояние компьютера и повторно запустив DSC, можно убедиться, что командлеты **Set-TargetResource** и **Test-TargetResource** работают правильно. Выполните следующие действия.
1.  Используйте ресурс, состояние которого отличается от нужного.
2.  Запустите конфигурацию с этим ресурсом.
3.  Проверьте, что **Test-DscConfiguration** возвращает значение true.
4.  Измените настроенный элемент так, чтобы он находился не в требуемом состоянии.
5.  Проверьте, возвращает ли **Test-DscConfiguration** значение false. Вот более конкретный пример для ресурса Registry.
1.  Используйте раздел реестра, состояние которого отличается от нужного.
2.  Запустите **Start-DscConfiguration** с конфигурацией, чтобы переключить его в нужное состоянии, и убедитесь в прохождении проверки.
3.  Запустите **Test-DscConfiguration** и подтвердите, что возвращается значение true.
4.  Измените значение раздела, чтобы он находился не в требуемом состоянии.
5.  Запустите **Test-DscConfiguration** и подтвердите, что возвращается значение false.
6.  Функциональность Get-TargetResource была проверена с помощью Get-DscConfiguration

Get-TargetResource должен возвращать сведения о текущем состоянии ресурса. Обязательно проверьте результат, вызвав командлет Get-DscConfiguration после применения конфигурации и убедившись, что выходные данные правильно отражают текущее состояние компьютера. Очень важно тестировать его отдельно, поскольку все проблемы в этой области не проявляются при вызове Start-DscConfiguration.

## Вызов функций **Get/Set/Test-TargetResource** напрямую ##

Убедитесь, что функции **Get/Set/Test-TargetResource**, реализованные в ресурсе, протестированы (вызваны напрямую и проверены на предмет правильной работы).

## Комплексная проверка с помощью командлета **Start-DscConfiguration** ##

Тестирование функций **Get/Set и тест-TargetResource** посредством вызова их напрямую имеет важное значение, однако не позволяет выявить все проблемы. Значительная часть тестирования должна быть направлена на использование **Start-DscConfiguration** или опрашивающего сервера. На самом деле, именно так пользователи и будут использовать ресурс, поэтому не стоит недооценивать важность таких тестов. Возможные типы проблем.
- Учетные данные или сеанса могут работать по-разному, так как агент DSC выполняется как служба.  Обязательно выполните комплексное тестирование всех этих функций.
- Ошибки, выдаваемые командлетом **Start-DscConfiguration**, могут отличаться от ошибок, отображаемых при вызове функции **Set-TargetResource** напрямую.

## Проверка совместимости на всех платформах, поддерживаемых DSC ##
Ресурс должен работать на всех платформах, поддерживаемых DSC (Windows Server 2008 R2 и более поздней версии). Для получения последней версии DSC установите последнюю версию WMF (Windows Management Framework) в своей операционной системе. Если ресурс по своей природе не поддерживает некоторые из этих платформ, должно быть возвращено сообщение об ошибке. Кроме того, убедитесь, что ресурс проверяет, присутствуют ли вызываемые командлеты на конкретном компьютере. В Windows Server 2012 было добавлено большое количество новых командлетов, которые недоступны в Windows Server 2008 R2 даже при установленном WMF. 

## Проверка на клиенте Windows (если применимо) ##
При тестировании довольно часто допускается упущение, заключающееся в проверке ресурса только в серверных версиях Windows. Многие ресурсы также предназначены для работы в клиентских SKU. Если это характерно для вашего случая, не забудьте проверить ресурс и на этих платформах также. 
## Get-DSCResource указывает ресурс ##
При вызове командлета Get-DscResource после развертывания модуля ваш ресурс должен отображаться вместе с другими в списке результатов. Если ресурс отсутствует в списке, убедитесь, что для этого ресурса существует SCHEMA.MOF-файл. 
## Модуль ресурсов содержит примеры ##
Создавайте качественные примеры, которые помогут другим пользователям понять, как работать с модулем ресурсов. Это особенно важно, потому что многие пользователи рассматривают пример кода в качестве документации. 
- Во-первых, необходимо определить примеры, которые будут включены в модуль; они по меньшей мере должны охватывать наиболее важные варианты использования ресурса:
- Если модуль содержит несколько ресурсов, которые должны работать вместе в рамках комплексного сценария, в качестве первого оптимально подойдет простой комплексный пример.
- Начальные примеры должны быть очень простыми — начало работы с ресурсами в небольших управляемых фрагментах (например, создание нового виртуального жесткого диска).
- Последующие примеры должны основываться на начальных (например, создание виртуальной машины из виртуального жесткого диска, ее удаление и изменение) и демонстрировать расширенные функциональные возможности (например, создание виртуальной машины с динамической памятью).
- Примеры конфигурации должны быть параметризованными (все значения должны передаваться конфигурации в качестве параметров, а жестко закодированные значения должны отсутствовать):
```powershell
configuration Sample_xRemoteFile_DownloadFile
{
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
} 
```
- Рекомендуется включить (закомментировать) в конце примера сценария образец вызова конфигурации с фактическими значениями. Например, в приведенной выше конфигурации не совсем очевидно, что лучше всего указать UserAgent следующим образом.

`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer`  
В этом случае можно пояснить, как будет выполнена конфигурация, с помощью следующего комментария.
```
<# 
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>  
```
- Для каждого примера укажите краткое описание его назначение и параметров. 
- Убедитесь, что примеры охватывают большинство важных сценариев для ресурса, а если все нужное присутствует, убедитесь, что они выполняют и переводят компьютер в нужное состояние.  

## Сообщения об ошибках просты для понимания и помогают пользователям устранять проблемы ##
Грамотный подход к сообщениям об ошибках должен отвечать следующим условиям.
- Наличие: самым большим недостатком сообщений об ошибках является их частое отсутствие, поэтому убедитесь, что они существуют. 
- Простота для восприятия: естественный язык без малопонятных кодов.
- Точность: объясните, в чем именно заключается проблема.
- Конструктивность: приведите советы по устранению.
- Вежливость: не обвиняйте пользователя и не заставляйте его чувствовать себя некомфортно. Обязательно проверяйте ошибки в комплексных сценариях (с помощью **Start-DscConfiguration**), так как они могут отличаться от тех ошибок, которые возвращаются при выполнении функций ресурсов напрямую. 

## Сообщения журнала просты для понимания и информативны (включая журналы –verbose, –debug и трассировки событий Windows) ##
Убедитесь, что выводимые ресурсом журналы просты для понимания и представляют ценность для пользователя. Ресурсы должны выводить все сведения, которые могут оказаться полезными для пользователя, однако ведение максимального числа всевозможных журналов не всегда является лучшим решением. Следует избегать избыточности и вывода данных, которые не представляют никакой ценности. Не заставляйте людей просматривать сотни записей в журналах для поиска необходимых сведений. Конечно же, полное отсутствие журналов также не является допустимым. 

При тестировании следует проанализировать журналы подробных сведений и отладки (запустив **Start-DscConfiguration** с параметрами –verbose и –debug), а также журналы трассировки событий Windows. Чтобы просмотреть журналы трассировки событий Windows для DSC, перейдите в средство просмотра событий и откройте следующую папку: "Приложения и службы" — "Microsoft" — "Windows" — "Desired State Configuration".  По умолчанию будет доступен операционный канал; также включите каналы аналитики и отладки (это необходимо сделать перед запуском конфигурации). Чтобы включить каналы аналитики и отладки, можно выполнить следующий сценарий:
```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug" 
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}     
Invoke-Expression $commandToExecute 
```
## Реализация ресурса не содержит жестко заданные пути ##
Убедитесь, в реализации ресурса нет ни одного жестко заданного пути, особенно в том случае, если они предполагают язык (en-us) или имеются системные переменные, которые могут использоваться.
Если ресурсу требуется доступ к определенным путям, используйте переменные среды вместо жесткого задания пути, так как на других компьютерах он может отличаться.

Пример:

Вместо этого:
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
Можно написать:
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)} 
```
## Реализация ресурса не содержит сведения о пользователе ##
Убедитесь, что в коде отсутствуют адреса электронной почты, сведения об учетной записи или имена людей.
## Ресурс был протестирован с допустимыми и недопустимыми учетными данными ##
Если ресурс принимает учетные данные в качестве параметра:
- Проверьте работу ресурса при отсутствии доступа у учетной записи Local System (или учетной записи компьютера для удаленных ресурсов).
- Убедитесь, что ресурс работает с учетными данными, указанными для Get, Set и Test 
- Если ресурс обращается к общим ресурсам, протестируйте все варианты, которые должны поддерживаться, например следующие.
  - Стандартные общие ресурсы Windows.
  - Общие ресурсы DFS.
  - Общие ресурсы SAMBA (если требуется поддержка Linux).

## Ресурс не требует интерактивного ввода ##
Функции **Get/Set/Test-TargetResource** должны выполняться автоматически и не ожидать ввода данных пользователем на любом этапе выполнения (например, не следует использовать **Get-Credential** внутри этих функций). Если необходимо предоставить вводимые пользователем данные, их следует передать в конфигурацию в качестве параметра на этапе компиляции. 
## Функциональность ресурса была тщательно протестирована ##
Этот контрольный список содержит элементы, которые важны для тестирования и/или часто пропускаются. Будет проведено несколько тестов, главным образом функциональных, которые предназначены для тестируемого вами ресурса и здесь не упомянуты. Не забывайте об отрицательных тестовых случаях. 
## Рекомендация: модуль ресурсов содержит папку Tests со сценарием ResourceDesignerTests.ps1 ##
Рекомендуется создать папку Tests внутри модуля ресурсов, создать файл ResourceDesignerTests.ps1 и с помощью **Test-xDscResource** и **Test-xDscSchema** добавить тесты для всех ресурсов в заданном модуле. Так можно быстро проверить все ресурсы из заданных модулей, а также проверить их работоспособность перед публикацией.
Для xRemoteFile файл ResourceTests.ps1 может иметь просто вид:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof 
```
##Рекомендация: папка Resource содержит сценарий конструктора ресурсов для создания схемы##
Каждый ресурс должен содержать сценарий конструктора ресурсов, создающий MOF-схему для данного ресурса. Этот файл следует поместить в каталог <ResourceName>\ResourceDesignerScripts and be named Generate<ResourceName>Schema.ps1. Для ресурса xRemoteFile этот файл будет называться GenerateXRemoteFileSchema.ps1 и содержать следующее.
```powershell 
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.' 
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile 
```
## Рекомендация: ресурс поддерживает -whatif ##
Если ресурс выполняет "небезопасные" операции, рекомендуется реализовать функциональность -whatif. После этого убедитесь в том, что выходные данные whatif правильно описывают операции, которые могут быть выполнены при запуске команды без параметра whatif.
Кроме того, убедитесь, что при наличии параметра -whatif операции не выполняются (не изменяется состояние узла). Например, предположим, что мы тестируем ресурс File. Ниже приведена простая конфигурации, которая создает файл test.txt с содержимым test:
```powershell
configuration config
{
    node localhost 
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config 
```
Если скомпилировать и выполнить эту конфигурацию с параметром –whatif, выходные данные сообщают, что именно произойдет при запуске конфигурации. При этом сама конфигурация не выполняется (файл test.txt не создается).
```powershell 
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

Этот список не является исчерпывающим, однако он охватывает множество важных проблем, которые могут возникнуть при проектировании, разработке и тестировании ресурсов DSC.



<!--HONumber=Jul16_HO2-->


