---
ms.date: 04/11/2018
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Опрашивающая служба DSC
ms.openlocfilehash: 61b4c0e9cfe1d1d7539cd32da35d2fe50da4b0e3
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="desired-state-configuration-pull-service"></a>Опрашивающая служба Desired State Configuration

> Область применения: Windows PowerShell 5.0

> [!IMPORTANT]
> Опрашивающий сервер (компонент Windows *служба DSC*) — поддерживаемый компонент Windows Server, но реализация новых функций и возможностей для него не планируется. Рекомендуется начать перенос управляемых клиентов на [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (включает возможности опрашивающего сервера в Windows Server) или на одно из решений сообщества, указанных [в следующем списке](pullserver.md#community-solutions-for-pull-service).

Управление локальным диспетчером конфигураций можно централизировать с помощью опрашивающей службы.
При использовании такого подхода управляемый узел регистрируется в службе, и ему в параметрах локального диспетчера конфигураций назначается конфигурация.
Конфигурация и все ресурсы DSC, которые необходимы в качестве зависимостей конфигурации, загружаются на компьютер и используются локальным диспетчером конфигураций для управления конфигурацией.
Сведения о состоянии управляемого компьютера отправляются в службу для отчетности.
Эта концепция называется "опрашивающей службой".

Текущие варианты опрашивающей службы:

- служба Desired State Configuration в службе автоматизации Azure;
- Опрашивающая служба в Windows Server
- Решения с открытым исходным кодом, поддерживаемые сообществом
- Общий ресурс SMB

**Рекомендуемое решение** и вариант с наибольшим числом доступных функций — [DSC в службе автоматизации Azure](/azure/automation/automation-dsc-getting-started).

Служба Azure может управлять узлами в локальных частных центрах обработки данных или в общедоступных облаках, таких как Azure и AWS.
Для частных сред, где серверы не могут напрямую подключаться к Интернету, рекомендуем ограничить исходящий трафик только опубликованным диапазоном IP-адресов Azure (см. сведения о [диапазонах IP-адресов для центров обработки данных Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Функции веб-службы, которые сейчас недоступны в опрашивающей службе в Windows Server:
- Шифрование всех данных при передаче и хранении.
- Автоматическое создание и обслуживание клиентских сертификатов.
- Хранение секретов с централизованным управлением [паролями и учетными данными](/azure/automation/automation-credentials) или [переменными](/azure/automation/automation-variables), такими как имена серверов или строки подключения.
- Централизованное управление [конфигурацией LCM](metaConfig.md#basic-settings) в узле.
- Централизованное назначение конфигураций клиентским узлам.
- Выпуск изменений конфигурации для небольших групп пользователей, позволяющий протестировать решение перед реализацией в рабочей среде.
- Графические отчеты:
  - сведения о состоянии на уровне ресурсов DSC;
  - подробные сообщения об ошибках с клиентских компьютеров для устранения неполадок.
- [Интеграция с Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) для отправки предупреждений, автоматизации задач, а также выполнения приложений Android или iOS для создания отчетов и оповещений.

## <a name="dsc-pull-service-in-windows-server"></a>Опрашивающая служба DSC в Windows Server

Опрашивающую службу можно настроить для работы в Windows Server.
Учтите, что опрашивающая служба в составе Windows Server включает только возможности сохранения конфигураций и модулей для скачивания и записи данных отчетов в базу данных.
Она не включает многих функций, предоставляемых службой в Azure, и поэтому не слишком хорошо подходит для оценки потенциального использования службы.

Опрашивающая служба в Windows Server — это веб-служба в составе IIS, которая использует интерфейс OData для создания файлов конфигурации DSC, доступных целевым узлам по запросу.

Требования к использованию опрашивающего сервера:

- Сервер под управлением:
  - WMF/PowerShell 5.0 или более поздней версии
  - Роль сервера служб IIS
  - Служба DSC
- Рекомендуется использовать средства создания сертификата для защиты учетных данных, передаваемых в локальный диспетчер конфигураций (LCM) на целевых узлах

Для настройки размещения опрашивающей службы в Windows Server лучше всего воспользоваться конфигурацией DSC.
Пример сценария приведен ниже.

### <a name="supported-database-systems"></a>Поддерживаемые системы баз данных

|WMF 4.0   |WMF 5.0  |WMF 5.1 |WMF 5.1 (Windows Server Insider Preview версии 17090)|
|---------|---------|---------|---------|
|MDB     |ESENT (по умолчанию), MDB |ESENT (по умолчанию), MDB|ESENT (по умолчанию), SQL Server, MDB

Начиная с выпуска 17090 [Windows Server Insider Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), в опрашивающей службе (компонент Windows *служба DSC*) поддерживается SQL Server.  Это новый вариант масштабирования крупных сред DSC, которые не были перенесены в [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> **Примечание**. Поддержка SQL Server не будет добавлена в предыдущие версии WMF 5.1 (или более ранней версии) и будет доступна только в Windows Server версии 17090 и более поздних версиях.

Чтобы настроить на опрашивающем сервере использование SQL Server, установите значение `$true` для параметра **SqlProvider** и допустимую строку подключения SQL Server для параметра **SqlConnectionString**.  Дополнительные сведения см. в разделе [Строки подключения SqlClient](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Чтобы ознакомиться с настройкой SQL Server с помощью **xDscWebService**, прочтите статью [Использование ресурса xDscWebService](#using-the-xdscwebservice-resource) и просмотрите файл [Sample_xDscWebServiceRegistration_UseSQLProvider.ps1 в GitHub](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>Использование ресурса xDSCWebService

Самый простой способ настроить опрашивающий веб-сервер — использовать ресурс **xDscWebService**, включенный в модуль **xPSDesiredStateConfiguration**.
В следующих действиях показано, как использовать ресурс в конфигурации, которая настраивает веб-службу.

1. Вызовите командлет [Install-Module](/powershell/module/PowershellGet/Install-Module), чтобы установить модуль **xPSDesiredStateConfiguration**. **Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
1. Получите SSL-сертификат для опрашивающего сервера DSC из доверенного центра сертификации (общедоступного или входящего в состав вашей организации). Полученный из центра сертификат обычно имеет формат PFX. Установите сертификат на узле, который должен стать опрашивающим сервером DSC, в расположении по умолчанию (CERT:\LocalMachine\My). Запишите отпечаток сертификата.
1. Выберите идентификатор GUID для использования в качестве ключа регистрации. Для его создания с помощью PowerShell введите следующие команды в командной строке PS и нажмите клавишу ВВОД: "``` [guid]::newGuid()```" или "```New-Guid```". Этот ключ будет использоваться клиентскими узлами в качестве общего ключа для проверки подлинности во время регистрации. Дополнительные сведения см. в разделе "Ключ регистрации" ниже.
1. В PowerShell ISE запустите (нажав клавишу F5) следующий сценарий конфигурации (находящийся в папке "Примеры" модуля **xPSDesiredStateConfiguration** в файле Sample_xDscWebServiceRegistration.ps1). Этот сценарий настраивает опрашивающий сервер.

```powershell
configuration Sample_xDscWebServiceRegistration
{
    param
    (
        [string[]]$NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $certificateThumbPrint,

        [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
    )

    Import-DSCResource -ModuleName xPSDesiredStateConfiguration

    Node $NodeName
    {
        WindowsFeature DSCServiceFeature
        {
            Ensure = "Present"
            Name   = "DSC-Service"
        }

        xDscWebService PSDSCPullServer
        {
            Ensure                  = "Present"
            EndpointName            = "PSDSCPullServer"
            Port                    = 8080
            PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
            CertificateThumbPrint   = $certificateThumbPrint
            ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
            ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
            State                   = "Started"
            DependsOn               = "[WindowsFeature]DSCServiceFeature"
            RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
            AcceptSelfSignedCertificates = $true
            Enable32BitAppOnWin64   = $false
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
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

#### <a name="registration-key"></a>Ключ регистрации

Чтобы разрешить клиентским узлам регистрироваться на сервере для использования имен конфигурации вместо идентификаторов конфигурации, созданный конфигурацией ключ сохраняется в файле `RegistrationKeys.txt` в `C:\Program Files\WindowsPowerShell\DscService`. Ключ регистрации работает как общий секрет, используемый во время первоначальной регистрации клиента с опрашивающим сервером. Клиент создает самозаверяющий сертификат, который используется для уникальной проверки подлинности на опрашивающем сервере после успешного завершения регистрации. Отпечаток этого сертификата сохраняется локально и связывается с URL-адресом опрашивающего сервера.
> **Примечание**. Ключи регистрации не поддерживаются в PowerShell 4.0.

Для настройки проверки подлинности узла на опрашивающем сервере необходимо поместить ключ регистрации в метаконфигурацию всех целевых узлов, которые будут регистрироваться на этом опрашивающем сервере. Обратите внимание, что **RegistrationKey** в метаконфигурации ниже удаляется после успешной регистрации целевого компьютера и значение "140a952b-b9d6-406b-b416-e0f759c9c0e4" должно соответствовать значению в файле RegistrationKeys.txt на опрашивающем сервере. Значение ключа регистрации должно оставаться конфиденциальным, так как с ним любой целевой компьютер сможет зарегистрироваться на опрашивающем сервере.

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to setup pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> **Примечание**. Раздел **ReportServerWeb** позволяет отправлять данные отчетов на опрашивающий сервер.

Отсутствие свойства **ConfigurationID** в файле метаконфигурации неявно означает, что опрашивающий сервер поддерживает версию 2 протокола опрашивающего сервера и требуется начальная регистрация.
Наоборот, наличие свойства **ConfigurationID** означает, что используется версия 1 протокола опрашивающего сервера и регистрация не выполняется.

>**Примечание**. В сценарии PUSH в текущем выпуске есть ошибка, из-за которой необходимо определять свойство ConfigurationID в файле метаконфигурации для узлов, которые никогда не регистрировались на опрашивающем сервере. Это приведет к принудительному использованию версии 1 протокола опрашивающего сервера и позволит избежать сообщений об ошибках регистрации.

## <a name="placing-configurations-and-resources"></a>Размещение конфигураций и ресурсов

После завершения установки опрашивающего сервера папки для размещения модулей и конфигурации, которые будут доступны целевым узлам, задаются свойствами **ConfigurationPath** и **ModulePath** в конфигурации опрашивающего сервера.
Для правильной обработки опрашивающим сервером эти файлы должны иметь специальный формат.

### <a name="dsc-resource-module-package-format"></a>Формат пакета модуля для ресурсов DSC

Каждый модуль ресурса необходимо упаковать в ZIP-архив и переименовать согласно следующему шаблону: `{Module Name}_{Module Version}.zip`.
Например, модуль с именем xWebAdminstration с версией модуля 3.1.2.0 будет иметь имя "xWebAdministration_3.2.1.0.zip".
Каждая версия модуля должна находиться в собственном ZIP-файле.
Так как в каждом ZIP-файле существует только одна версия ресурса, формат модулей с поддержкой нескольких версий модуля в одном каталоге, который появился в WMF 5.0, не поддерживается.
Это означает, что перед упаковкой модулей ресурсов DSC для опрашивающего сервера необходимо внести небольшое изменение в структуру каталогов.
Формат модулей, содержащих ресурсы DSC, в WMF 5.0 по умолчанию таков: "{папка_модуля}\{{версия_модуля}\DscResources\{{папка_ресурса_DSC}\'.
Перед упаковкой для опрашивающего сервера удалите папку **{версия_модуля}**, чтобы путь стал таким: "{папка_модуля}\DscResources\{{папка_ресурса_DSC}\'.
Выполнив это изменение, упакуйте папку в ZIP-архив, как описано выше, и поместите ZIP-архивы в папку **ModulePath**.

Используйте `New-DscChecksum {module zip file}`, чтобы создать файл контрольной суммы для только что добавленного модуля.

### <a name="configuration-mof-format"></a>Формат файлов конфигурации MOF

MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию.
Чтобы создать контрольную сумму, вызовите командлет [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum).
Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации.
Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации.
Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.
Поместите файлы MOF и их файлы контрольных сумм в папку **ConfigurationPath**.

>**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

### <a name="tooling"></a>Инструменты

Для упрощения настройки, проверки опрашивающего сервера и управления им в последнюю версию модуля xPSDesiredStateConfiguration в качестве примеров включены следующие инструменты:

1. Модуль, который помогает упаковывать модули ресурсов и конфигурационные файлы DSC для использования на опрашивающем сервере. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Примеры ниже:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Сценарий, который проверяет, что опрашивающий сервер настроен правильно. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Решения сообщества для опрашивающей службы

Сообщество DSC разработало несколько решений для реализации протокола опрашивающей службы.
Для локальных сред эти решения предоставляют функции опрашивающей службы и дают возможность поделиться с сообществом своими улучшениями.

- [Tug](https://github.com/powershellorg/tug)
- [DSC-TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Настройка опрашивающего клиента

В следующих разделах настройка опрашивающих клиентов описывается более подробно:

- [Настройка опрашивающего клиента DSC с помощью идентификатора конфигурации](pullClientConfigID.md)
- [Настройка опрашивающего клиента DSC с помощью имен конфигурации](pullClientConfigNames.md)
- [Частичные конфигурации](partialConfigs.md)

## <a name="see-also"></a>См. также:

- [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
- [Активированные конфигурации](enactingConfigurations.md)
- [Использование сервера отчетов DSC](reportServer.md)