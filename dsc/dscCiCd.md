---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Создание конвейера непрерывной интеграции и непрерывного развертывания с помощью DSC"
ms.openlocfilehash: 6d21faef6e58068456c6c454b4d50b7a9415850b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="building-a-continuous-integration-and-continuous-deplyoment-pipeline-with-dsc"></a>Создание конвейера непрерывной интеграции и непрерывного развертывания с помощью DSC

В этом примере показано, как создать конвейер непрерывной интеграции и непрерывного развертывания с помощью PowerShell, DSC, Pester и Visual Studio Team Foundation Server.

После создания и настройки конвейера его можно использовать для полного развертывания, настройки и проверки DNS-сервера и связанных записей узла. Этот процесс имитирует первую часть конвейера, которая будет использоваться в среде разработки.

Автоматический конвейер непрерывной интеграции и развертывания помогает быстро и надежно обновлять программное обеспечение, следя за тем, чтоб весь код проверялся и чтобы текущая сборка была доступна в любое время.

## <a name="prerequisites"></a>Необходимые компоненты

Чтобы использовать этот пример, следует ознакомиться со следующим:

- Основные понятия непрерывной интеграции и развертывания. Хороший справочник можно найти в документе [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf) (Модель конвейера выпуска).
- Система управления версиями [Git](https://git-scm.com/).
- Платформа тестирования [Pester](https://github.com/pester/Pester).
- [Team Foundation Server](https://www.visualstudio.com/tfs/).

## <a name="what-you-will-need"></a>Что вам понадобится

Чтобы собрать и запустить этот пример, необходима среда из нескольких компьютеров или виртуальных машин.

### <a name="client"></a>клиент

Это компьютер, на котором вы будете выполнять всю работу по настройке и запуску примера.

Это должен быть компьютер Windows, на котором установлены следующие компоненты:
- [Git](https://git-scm.com/).
- Локальный репозиторий Git, клонированный из https://github.com/PowerShell/Demo_CI.
- Текстовый редактор, такой как [Visual Studio Code](https://code.visualstudio.com/).

### <a name="tfssrv1"></a>TFSSrv1

Компьютер, на котором размещен сервер TFS и где определяется сборка и выпуск.
На этом компьютере должен быть установлен [Team Foundation Server 2017](https://www.visualstudio.com/tfs/).

### <a name="buildagent"></a>BuildAgent

Компьютер, на котором запущен агент сборки Windows, создающий проект.
На этом компьютере должен быть установлен и запущен агент сборки Windows.
Дополнительные сведения о том, как устанавливать и запускать агент сборки Windows, см. в статье [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) (Развертывание агента в Windows).

Кроме того, необходимо установить модули DSC `xDnsServer` и `xNetworking` на этом компьютере.

### <a name="testagent1"></a>TestAgent1

В этом примере это компьютер, настроенный как DNS-сервер с помощью конфигурации DSC.
На компьютере должен быть запущен [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).

### <a name="testagent2"></a>TestAgent2

Это компьютер, на котором размещается веб-сайт, настраиваемый в этом примере.
На компьютере должен быть запущен [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). 

## <a name="add-the-code-to-tfs"></a>Добавление кода в TFS

Начнем с создания репозитория Git в TFS и импорта кода из локального репозитория на клиентском компьютере.
Если вы еще не клонировали репозиторий Demo_CI на клиентский компьютер, сделайте это сейчас, выполнив следующую команду Git:

`git clone https://github.com/PowerShell/Demo_CI`

1. На клиентском компьютере перейдите к серверу TFS в веб-браузере.
1. На сервере TFS [создайте командный проект](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) с именем Demo_CI.

    Убедитесь, что для **управления версиями** задано значение **Git**.
1. На клиентском компьютере сделайте удаленным репозиторий, созданный в TFS, с помощью следующей команды:

    `git remote add tfs <YourTFSRepoURL>`

    Где `<YourTFSRepoURL>` — это URL-адрес клона репозитория TFS, созданного на предыдущем шаге.

    Если вы не знаете, где можно найти этот URL-адрес, см. в статье [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone) (Клонирование имеющегося репозитория Git).
1. Отправьте код из локального репозитория в репозиторий TFS с помощью следующей команды:

    `git push tfs --all`
1. Репозиторий TFS будет заполнен кодом из Demo_CI.

>**Примечание.** В этом примере используется код ветви `ci-cd-example` из репозитория Git.
>Задайте эту ветвь как ветвь по умолчанию в проекте TFS и для создаваемых триггеров непрерывной интеграции и развертывания.

## <a name="understanding-the-code"></a>Общие сведения о коде

Прежде чем создать сборку и конвейеры развертывания, давайте взглянем на часть кода, чтобы понять, что происходит.
На клиентском компьютере откройте любой удобный текстовый редактор и перейдите в корневую папку своего репозитория Git Demo_CI.

### <a name="the-dsc-configuration"></a>Конфигурация DSC

Откройте файл `DNSServer.ps1` (из корня локального репозитория Demo_CI, `./InfraDNS/Configs/DNSServer.ps1`).

Этот файл содержит конфигурации DSC, которые настраивают DNS-сервер. Ниже они приведены в полном объеме:

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

Обратите внимание на инструкцию `Node`:

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

Она находит все узлы, определенные как имеющие роль `DNSServer` в [данных конфигурации](configData.md), которые создаются с помощью скрипта `DevEnv.ps1`.

При выполнении непрерывной интеграции важно использовать данные конфигурации для определения узлов, так как сведения об узле, скорее всего, изменятся между средами. Использование данных конфигурации позволит вам легко вносить изменения в сведения об узле без изменения кода конфигурации.

В первом блоке ресурсов конфигурация вызывает [WindowsFeature](windowsFeatureResource.md), чтобы убедиться, что функция DNS включена. Следующие блоки ресурсов вызывают ресурсы из модуля [xDnsServer ](https://github.com/PowerShell/xDnsServer), чтобы настроить основную зону и записи DNS.

Обратите внимание, что два блока `xDnsRecord` упаковываются в циклы `foreach`, которые проходят через массивы данных конфигурации.
При этом данные конфигурации создаются скриптом `DevEnv.ps1`, который мы рассмотрим далее.

### <a name="configuration-data"></a>Данные конфигурации

Файл `DevEnv.ps1` (из корня локального репозитория Demo_CI, `./InfraDNS/DevEnv.ps1`) указывает данные конфигурации среды в хэш-таблице, а затем передает эту хэш-таблицу вызову к функции `New-DscConfigurationDataDocument`, которая определяется в `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).

Файл `DevEnv.ps1`:

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

Функция `New-DscConfigurationDataDocument` (определяется в `\Assets\DscPipelineTools\DscPipelineTools.psm1`) программным образом создает документ данных конфигурации из хэш-таблицы (данные узла) и массива (данные, отличные от данных узла), которые передаются как параметры `RawEnvData` и `OtherEnvData`.

В нашем случае используется только параметр `RawEnvData`.

### <a name="the-psake-build-script"></a>Скрипт сборки psake

Скрипт сборки [psake](https://github.com/psake/psake), определенный в `Build.ps1` (из корня репозитория Demo_CI, `./InfraDNS/Build.ps1`), указывает задачи, которые являются частью сборки.
Он также определяет, от каких задач зависят другие задачи. При вызове скрипт psake проверяет выполнение указанной задачи (или задачи с именем `Default`, если она не указана) и всех ее зависимостей (рекурсивно, т. е. выполняются зависимости зависимостей и т. д.).

В этом примере задача `Default` определяется как:

```powershell
Task Default -depends UnitTests
```

В задаче `Default` нет самостоятельной реализации задачи, но есть зависимость от задачи `CompileConfigs`.
Полученная цепочка зависимостей обеспечивает выполнение всех задач в скрипте сборки.

В этом примере скрипт psake вызывается путем вызова `Invoke-PSake` в файле `Initiate.ps1` (находится в корне репозитория Demo_CI):

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

При создании определения сборки для нашего примера в TFS мы предоставим наш файл скрипта psake в качестве параметра `fileName` для этого скрипта.

Скрипт сборки определяет следующие задачи:

#### <a name="generateenvironmentfiles"></a>GenerateEnvironmentFiles

Выполняет файл `DevEnv.ps1`, создает конфигурационный файл данных.

#### <a name="installmodules"></a>InstallModules

Устанавливает модули, необходимые в конфигурации `DNSServer.ps1`.

#### <a name="scriptanalysis"></a>ScriptAnalysis

Вызывает [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).

#### <a name="unittests"></a>UnitTests

Выполняет модульные тесты [Pester](https://github.com/pester/Pester/wiki).

#### <a name="compileconfigs"></a>CompileConfigs

Компилирует конфигурацию (`DNSServer.ps1`) в файл типа MOF, используя данные конфигурации, созданные задачей `GenerateEnvironmentFiles`.

#### <a name="clean"></a>Clean

Создает папки, используемые в примере, и удаляет все результаты тестирования, файлы данных конфигурации и модули из предыдущих выполнений.

### <a name="the-psake-deploy-script"></a>Развертывание скрипта psake

Скрипт развертывания [psake](https://github.com/psake/psake), определяемый в `Deploy.ps1` (находится в корне репозитория Demo_CI, `./InfraDNS/Deploy.ps1`), указывает задачи, которые развертывают и запускают конфигурацию.

`Deploy.ps1` определяет следующие задачи:

#### <a name="deploymodules"></a>DeployModules

Запускает сеанс PowerShell на `TestAgent1` и устанавливает модули, содержащие ресурсы DSC, которые необходимы для конфигурации.

#### <a name="deployconfigs"></a>DeployConfigs

Вызывает командлет [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) для выполнения конфигурации на `TestAgent1`.

#### <a name="integrationtests"></a>IntegrationTests

Выполняет интеграционные тесты [Pester](https://github.com/pester/Pester/wiki).

#### <a name="acceptancetests"></a>AcceptanceTests

Выполняет приемочные тесты [Pester](https://github.com/pester/Pester/wiki).

#### <a name="clean"></a>Clean

Удаляет все модули, установленные при предыдущих выполнениях, и проверяет существование папки с результатами теста.

### <a name="test-scripts"></a>Скрипты тестирования

Приемочные, интеграционные и модульные тесты определяются в скриптах в папке `Tests` (из корня репозитория Demo_CI, `./InfraDNS/Tests`), каждый в файлах с именем `DNSServer.tests.ps1` в соответствующих папках.

Скрипты тестирования используют синтаксис [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).

#### <a name="unit-tests"></a>Модульные тесты

Модульные тесты проверяют конфигурации DSC самостоятельно, чтобы убедиться, что конфигурации будут делать то, что ожидается при их запуске.
Скрипт модульных тестов использует [Pester](https://github.com/pester/Pester/wiki).

#### <a name="integration-tests"></a>Интеграционные тесты

Интеграционные тесты проверяют конфигурацию системы, чтобы убедиться, что при интеграции с другими компонентами система настроена должным образом. Эти тесты выполняются на целевом узле после его настройки с помощью DSC.
Скрипт интеграционного теста использует сочетание синтаксиса [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).

#### <a name="acceptance-tests"></a>Приемочные тесты

Приемочные тесты проверяют систему, чтобы убедиться, что она правильно работает.
Например, они проверяют, правильную ли информацию возвращает веб-страница при запросе.
Эти тесты выполняются удаленно с целевого узла, чтобы протестировать реальные сценарии.
Скрипт интеграционного теста использует сочетание синтаксиса [Pester](https://github.com/pester/Pester/wiki) и [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction).

## <a name="define-the-build"></a>Определение сборки

Теперь, когда мы передали свой код в TFS и просмотрели, что он делает, определим нашу сборку.

Здесь мы расскажем только о шагах сборки, которые вы добавите к ней. Инструкции о том, как создать определение сборки в TFS и поместить его в очередь, см. в [этой статье](https://www.visualstudio.com/en-us/docs/build/define/create).

Создайте определение сборки (выберите шаблон **Пусто**) с именем InfraDNS.
Добавьте следующие шаги к своему определению сборки:

- Сценарий PowerShell.
- Публикация результатов тестирования.
- Копирование файлов.
- Публикация артефакта.

После добавления этих шагов сборки измените свойства каждого шага следующим образом.

### <a name="powershell-script"></a>Сценарий PowerShell

1. Задайте для свойства **Тип** значение `File Path`.
1. Задайте для свойства **Путь к скрипту** значение `initiate.ps1`.
1. Добавьте параметр `-fileName build` к свойству **Аргументы**.

Этот шаг сборки запускает файл `initiate.ps1`, вызывающий скрипт сборки psake.

### <a name="publish-test-results"></a>Публикация результатов тестирования

1. Задайте для свойства **Формат результатов теста** значение `NUnit`.
1. Задайте для свойства **Файлы результатов тестов** значение `InfraDNS/Tests/Results/*.xml`.
1. Задайте для свойства **Название тестового запуска** значение `Unit`.
1. Убедитесь, что выбраны **параметры управления** **Включен** и **Всегда запускать**.

На этом этапе сборки запускаются модульные тесты в скрипте Pester, рассмотренном ранее, и результаты сохраняются в папке `InfraDNS/Tests/Results/*.xml`.

### <a name="copy-files"></a>Копирование файлов

1. Добавьте следующие строки в раздел **Содержание**:

    ```
    initiate.ps1
    **\deploy.ps1
    **\Acceptance\**
    **\Integration\**
    ```

1. Задайте для параметра **TargetFolder** значение `$(BuildArtifactStagingDirectory)\`.

На этом шаге копируются сборка и скрипты тестирования в промежуточный каталог, чтобы их можно было опубликовать как артефакты сборки на следующем шаге.

### <a name="publish-artifact"></a>Публикация артефакта

1. Задайте для параметра **Путь к публикации** значение `$(Build.ArtifactStagingDirectory)\`.
1. Задайте для параметра **Имя артефакта** значение `Deploy`.
1. Задайте для параметра **Тип артефакта** значение `Server`.
1. Выберите `Enabled` в **параметрах управления**.

## <a name="enable-continuous-integration"></a>Включение непрерывной интеграции

Теперь мы создадим триггер, который активирует новую сборку проекта каждый раз, когда в ветке `ci-cd-example` репозитория Git отмечено изменение.

1. В TFS откройте вкладку **Сборка и выпуск**.
1. Выберите определение сборки `DNS Infra` и щелкните **Изменить**.
1. Откройте вкладку **Триггеры**.
1. Щелкните **Непрерывная интеграция (CI)** и в раскрывающемся списке ветви выберите `refs/heads/ci-cd-example`.
1. Щелкните **Сохранить**, а потом **ОК**.

Теперь любые изменения в репозитории Git TFS запускают автоматическую сборку.

## <a name="create-the-release-definition"></a>Создание определения выпуска

Создадим определение выпуска, чтобы проект развертывался в среду разработки с записью каждого кода после изменения.

Для этого добавьте новые определения выпуска, связанные с созданным определением сборки `InfraDNS`.
Установите **непрерывное развертывание**, чтобы новый выпуск запускался при каждом завершении новой сборки
([How to: Work with release definitions ](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions) (Как работать с определениями выпуска)), и настройте его следующим образом:

Добавьте следующие шаги к своему определению выпуска:

- Сценарий PowerShell.
- Публикация результатов тестирования.
- Публикация результатов тестирования.

Измените шаги следующим образом.

### <a name="powershell-script"></a>Сценарий PowerShell

1. Задайте для **пути к скрипту** значение `$(Build.DefinitionName)\Deploy\initiate.ps1"`.
1. Задайте для **аргументов** значение `-fileName Deploy`.

### <a name="first-publish-test-results"></a>Первая публикация результатов тестирования

1. Выберите `NUnit` для поля **Формат результатов теста**.
1. Задайте в качестве **файлов результатов тестов** значение `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`.
1. Задайте в качестве **название тестового запуска** значение `Integration`.
1. В разделе **Параметры управления** установите параметр **Всегда запускать**.

### <a name="second-publish-test-results"></a>Вторая публикация результатов тестирования

1. Выберите `NUnit` для поля **Формат результатов теста**.
1. Задайте в качестве **файлов результатов тестов** значение `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`.
1. Задайте в качестве **название тестового запуска** значение `Acceptance`.
1. В разделе **Параметры управления** установите параметр **Всегда запускать**.

## <a name="verify-your-results"></a>Проверка результатов

Теперь всякий раз, когда вы вносите изменения в ветку `ci-cd-example` ​​в TFS, запускается новая сборка.
Если создание сборки успешно, запускается новое развертывание.

Результаты развертывания можно проверить, открыв браузер на клиентском компьютере и перейдя на сайт `www.contoso.com`.

## <a name="next-steps"></a>Дальнейшие действия

В этом примере настраивается DNS-сервер `TestAgent1`, чтобы URL-адрес `www.contoso.com` разрешался в `TestAgent2`, но на самом деле веб-сайт не развертывается.
Структура для этого предоставляется в репозитории в папке `WebApp`.
Заглушки для создания скриптов psake, тестов Pester и конфигурации DSC можно использовать для развертывания собственных веб-сайтов.







