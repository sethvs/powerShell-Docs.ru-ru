---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Использование DSC на сервере Nano Server"
ms.openlocfilehash: 7427d6bb7644f513b9b523f284109f5ae0f8ef27
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="using-dsc-on-nano-server"></a>Использование DSC на сервере Nano Server

> Область применения: Windows PowerShell 5.0

**DSC для Nano Server** — это дополнительный пакет в папке `NanoServer\Packages` носителей Windows Server 2016. Пакет можно установить при создании виртуального жесткого диска для сервера Nano Server, указав значение **Microsoft-NanoServer-DSC-Package** для параметра **Packages** функции **New-NanoServerImage**. Например, при создании виртуального жесткого диска для виртуальной машины команда будет выглядеть следующим образом.

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

Сведения об установке и использовании сервера Nano Server, а также об управлении этим сервером с помощью удаленного взаимодействия PowerShell см. в статье [Getting Started with Nano Server](https://technet.microsoft.com/en-us/library/mt126167.aspx) (Приступая к работе с сервером Nano Server).


## <a name="dsc-features-available-on-nano-server"></a>Функции DSC, доступные на сервере Nano Server

 Так как сервер Nano Server поддерживает только ограниченный набор API по сравнению с полной версией Windows Server, набор функций DSC в системе Nano Server на данный момент несравним с DSC в полнофункциональных SKU. DSC для Nano Server в настоящее время активно разрабатывается и не является законченным компонентом.
 
 Следующие функции DSC в настоящее время доступны для Nano Server: 


* Режимы опроса и принудительной отправки

* Все командлеты DSC, которые существуют в полной версии Windows Server, включая следующие: 
  * [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx)
  * [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx)   
  * [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [Stop-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [Publish-DscConfiguraiton](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [Restore-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [Remove-DscConfigurationDocument](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [Find-DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [New-DscChecksum](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* Компиляция конфигураций (см. раздел [Конфигурации DSC](configurations.md)).

  **Проблема**. Не работает шифрование паролей (см. раздел [Защита MOF-файла](securemof.md)) во время компиляции конфигурации.

* Компиляция метаконфигураций (см. раздел [Настройка локального диспетчера конфигураций](metaConfig.md)).

* Выполнение ресурса в контексте пользователя (см. раздел [Запуск DSC с учетными данными пользователя (запуск от имени)](runAsUser.md)).

* Ресурсы на основе класса (см. раздел [Написание пользовательских ресурсов DSC с использованием классов PowerShell](authoringResourceClass.md)).

* Отладка ресурсов DSC (см. раздел [Отладка ресурсов DSC](debugresource.md)).
  
  **Проблема**. Отладка не работает, если ресурс использует PsDscRunAsCredential (см. раздел [Запуск DSC с учетными данными пользователя](runAsUser.md)).

* [Указание межузловых зависимостей](crossNodeDependencies.md) 

* [Управление версиями ресурсов](sxsResource.md)

* Опрашивающий клиент (конфигурации и ресурсы) (см. раздел [Настройка опрашивающего клиента с помощью имен конфигураций](pullClientConfigNames.md)).

* [Частичные конфигурации (по запросу и принудительная отправка)](partialConfigs.md)

* [Передача отчетов на опрашивающий сервер](reportServer.md) 

* Шифрование MOF-файлов

* Ведение журналов событий

* Отчеты DSC службы автоматизации Azure

* Полнофункциональные ресурсы.
  * [Archive](archiveResource.md)
  * [Environment](environmentResource.md)
  * [File](fileResource.md)
  * [Log](logResource.md)
  * ProcessSet
  * [Registry](registryResource.md)
  * [Script](scriptResource.md)
  * WindowsPackageCab
  * [WindowsProcess](windowsProcessResource.md)
  * WaitForAll (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).
  * WaitForAny (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).
  * WaitForSome (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).

* Ресурсы, функциональность которых не полная.
  * [Группа](groupResource.md)
  * GroupSet
  
  **Проблема**. Приведенные выше ресурсы не работают, если определенный экземпляр вызывается дважды (дважды запускается одна и та же конфигурация).
  
  * [Служба](serviceResource.md)
  * ServiceSet
  
  **Проблема**. Работает только для запуска или остановки службы (атрибут status). Не работает при попытке изменить другие атрибуты службы, например startuptype, credentials, description и т. д. Возникает ошибка такого вида.
  
  *Не удается найти тип [management.managementobject]: убедитесь в том, что сборка, содержащая этот тип, загружена.*
  
* Нефункционирующие ресурсы.
  * [User](userResource.md)
  

## <a name="dsc-features-not-available-on-nano-server"></a>Функции DSC, недоступные на сервере Nano Server

Следующие функции DSC в настоящее время недоступны для Nano Server:

* Расшифровка документа MOF с помощью зашифрованных паролей. 
* Опрашивающий сервер — в настоящее время опрашивающий сервер нельзя настроить на сервере Nano Server.
* Все компоненты, не указанные в списке функций, работают.

## <a name="using-custom-dsc-resources-on-nano-server"></a>Использование настраиваемых ресурсов DSC на сервере Nano Server
 
Поскольку набор API Windows и библиотек CLR, доступный на сервере Nano Server, ограничен, ресурсы DSC, работающие в полной версии среды выполнения Windows, не всегда работают в Nano Server. Перед развертыванием каких-либо настраиваемых ресурсов DSC в рабочей среде рекомендуется выполнять их полное и всестороннее тестирование.

## <a name="see-also"></a>См. также
- [Начало работы с сервером Nano Server](https://technet.microsoft.com/en-us/library/mt126167.aspx)

