---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Начало работы с настройкой требуемого состояния (DSC) для Linux"
ms.openlocfilehash: f88167cd039077574c3a84aa07ba78186adfa181
ms.sourcegitcommit: 9a5da3f739b1eebb81ede58bd4fc8037bad87224
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2017
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>Начало работы с настройкой требуемого состояния (DSC) для Linux

В этом разделе объясняется, как приступить к работе с настройкой требуемого состояния PowerShell (DSC) для Linux. Общие сведения о службе настройки требуемого состояния см. в разделе [Начало работы со службой настройки требуемого состояния Windows PowerShell](overview.md).

## <a name="supported-linux-operation-system-versions"></a>Поддерживаемые версии операционной системы Linux

DSC для Linux поддерживает следующие версии операционной системы Linux:
- CentOS 5, 6 и 7 (x86 и x64)
- Debian GNU/Linux 6 и 7 (x86 и x64)
- Oracle Linux 5, 6 и 7 (x86 и x64)
- Red Hat Enterprise Linux Server 5, 6 и 7 (x86 и x64)
- SUSE Linux Enterprise Server 10, 11 и 12 (x86 и x64)
- Ubuntu Server 12.04 LTS и 14.04 LTS (x86 и x64)

Ниже указано, какие зависимости пакетов необходимы DSC для Linux.

|  Требуемый пакет |  Описание |  Минимальная версия | 
|---|---|---|
| glibc| Библиотека GNU| 2…4 — 31.30| 
| python| Python| 2.4 — 3.4| 
| omiserver| Открытая инфраструктура управления| 1.0.8.1| 
| openssl| Библиотеки OpenSSL| 0.9.8 или 1.0| 
| ctypes| Библиотека Python CTypes| Должна соответствовать версии Python| 
| libcurl| Библиотека HTTP-клиентов cURL| 7.15.1| 

## <a name="installing-dsc-for-linux"></a>Установка DSC для Linux

Перед установкой DSC для Linux необходимо установить [открытую инфраструктуру управления (OMI)](https://github.com/Microsoft/omi).

### <a name="installing-omi"></a>Установка OMI

Настройка требуемого состояния для Linux требует наличия CIM-сервера открытой инфраструктуры управления (OMI) версии 1.0.8.1 и выше. OMI можно загрузить из Open Group: [Открытая инфраструктура управления (OMI)](https://github.com/Microsoft/omi).

Чтобы установить OMI, установите пакет, соответствующий вашей системе Linux (RPM или DEB), а также версии OpenSSL (ssl_098 или ssl_100) и архитектуре (x64 или x86). Пакеты RPM подходят для CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server и Oracle Linux. Пакеты DEB подходят для Debian GNU/Linux и Ubuntu Server. Пакеты ssl_098 подходят для компьютеров с установленным OpenSSL 0.9.8, а пакеты ssl_100 — для компьютеров с установленным OpenSSL 1.0.

> **Примечание**. Чтобы определить установленную версию OpenSSL, выполните команду `openssl version`.

Выполните указанную ниже команду для установки OMI в системе CentOS 7 x64.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>Установка DSC

DSC для Linux можно скачать [здесь](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest). 

Чтобы установить DSC, установите пакет, соответствующий вашей системе Linux (RPM или DEB), а также версии OpenSSL (ssl_098 или ssl_100) и архитектуре (x64 или x86). Пакеты RPM подходят для CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server и Oracle Linux. Пакеты DEB подходят для Debian GNU/Linux и Ubuntu Server. Пакеты ssl_098 подходят для компьютеров с установленным OpenSSL 0.9.8, а пакеты ssl_100 — для компьютеров с установленным OpenSSL 1.0.

> **Примечание**. Чтобы определить установленную версию OpenSSL, выполните команду openssl.
 
Выполните указанную ниже команду для установки DSC в системе CentOS 7 x64.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## <a name="using-dsc-for-linux"></a>Использование DSC для Linux

В следующих разделах описывается создание и запуск конфигураций DSC на компьютерах Linux.

### <a name="creating-a-configuration-mof-document"></a>Создание MOF-документа конфигурации

На компьютерах Linux (как и на компьютерах Windows) для создания конфигурации используется ключевое слово конфигурации Windows PowerShell. Следующие шаги описывают создание документа конфигурации для компьютера Linux с использованием Windows PowerShell.

1. Импортируйте модуль nx. Модуль nx для Windows PowerShell содержит схему для встроенных ресурсов DSC в Linux, поэтому он должен быть установлен на локальном компьютере и импортирован в конфигурацию.

    Чтобы установить модуль nx, скопируйте каталог модуля nx в `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` или в `$PSHOME\Modules`. Модуль nx включается в пакет установки DSC для Linux (MSI). Чтобы импортировать модуль nx в конфигурацию, выполните команду __Import-DSCResource__:
    
```powershell
Configuration ExampleConfiguration{
   
    Import-DSCResource -Module nx

}
```
2. Определите конфигурацию и создайте документ конфигурации:

```powershell
Configuration ExampleConfiguration{
   
    Import-DscResource -Module nx
 
    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp" 
```

### <a name="push-the-configuration-to-the-linux-computer"></a>Передача конфигурации на компьютер Linux

Документы конфигурации (MOF-файлы) можно принудительно отправить на компьютер Linux с помощью командлета [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx). Чтобы выполнить этот командлет, как и командлеты [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) или [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx), удаленно на компьютере Linux, необходимо использовать CIMSession. Для создания CIMSession на компьютере Linux служит командлет [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967).

Создание CIMSession в DSC для Linux демонстрируется в следующем коде.

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true 
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90 
```

> **Примечание**.
* В режиме принудительной передачи необходимо указывать учетные данные привилегированного пользователя на компьютере Linux.
* DSC для Linux поддерживает только SSL/TLS-подключения, поэтому необходимо использовать командлет New-CimSession с параметром –UseSSL, имеющим значение $true.
* SSL-сертификат, используемый OMI (DSC), указан в файле `/opt/omi/etc/omiserver.conf` со свойствами pemfile и keyfile.
Если компьютер Windows, на котором выполняется командлет [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967), не признает этот сертификат как надежный, проверку сертификата можно пропустить, используя параметры CIMSession: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

Для принудительной отправки конфигурации DSC на узел Linux используйте следующую команду:

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>Распространение конфигурации через опрашивающий сервер

Конфигурации можно распространять на компьютер Linux через опрашивающий сервер, как и в случае компьютеров с Windows. Рекомендации по работе с опрашивающим сервером см. в статье [Опрашивающие серверы конфигурации требуемого состояния Windows PowerShell](pullServer.md). Дополнительные сведения и ограничения, связанные с использованием компьютеров Linux с опрашивающим сервером, см. в заметках о выпуске настройки требуемого состояния для Linux.

### <a name="working-with-configurations-locally"></a>Локальная работа с конфигурациями

DSC для Linux включает сценарии работы с конфигурацией на локальном компьютере Linux. Эти сценарии расположены в `/opt/microsoft/dsc/Scripts` и включают следующее:
* GetDscConfiguration.py

 Возвращает текущую конфигурацию, примененную к компьютеру. Аналог командлета Get-DscConfiguration в Windows PowerShell.

`# sudo ./GetDscConfiguration.py`

* GetDscLocalConfigurationManager.py

 Возвращает текущую метаконфигурацию, примененную к компьютеру. Аналог командлета [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx).

`# sudo ./GetDscLocalConfigurationManager.py`

* InstallModule.py

 Устанавливает пользовательский модуль ресурсов DSC. Необходим путь к ZIP-файлу, содержащему библиотеку общих объектов модуля и MOF-файлы схемы.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* RemoveModule.py

 Удаляет пользовательский модуль ресурсов DSC. Требуется имя модуля, который нужно удалить.

`# sudo ./RemoveModule.py cnx_Resource`

* StartDscLocalConfigurationManager.py 

 Применяет MOF-файл конфигурации к компьютеру. Аналог командлета [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx). Требуется путь к соответствующему MOF-файлу конфигурации.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* SetDscLocalConfigurationManager.py

 Применяет MOF-файл метаконфигурации к компьютеру. Аналог командлета [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx). Требуется путь к соответствующему MOF-файлу метаконфигурации.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>Настройка требуемого состояния Windows PowerShell для файлов журнала Linux

Для сообщений DSC для Linux формируются следующие файлы журналов:

|Файл журнала|Directory|Описание|
|---|---|---|
|omiserver.log|/var/opt/omi/log|Сообщения, относящиеся к работе сервера OMI CIM.|
|dsc.log|/var/opt/omi/log|Сообщения, относящиеся к работе локального диспетчера конфигураций (LCM) и операциям с ресурсами DSC.|

