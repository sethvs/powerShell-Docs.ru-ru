---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Краткое руководство по настройке требуемого состояния"
ms.openlocfilehash: 295a78f3fd85464239d51d7be0defa04d2344689
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

# <a name="desired-state-configuration-quick-start"></a>Краткое руководство по настройке требуемого состояния

В этом упражнении демонстрируется создание и применение конфигурации, используемой при настройке требуемого состояния (DSC).
В нашем примере на сервере будет включен компонент `Web-Server` (IIS), а содержимое простого веб-сайта "Hello World" будет расположено на этом сервере в каталоге `intepub\wwwroot`.

См. дополнительные сведения об особенностях [настройки требуемого состояния для руководителей](decisionMaker.md).

## <a name="requirements"></a>Требования

Для выполнения этого примера вам понадобится компьютер под управлением Windows Server 2012 или более поздней версии и PowerShell 4.0 или более поздней версии.

## <a name="write-and-place-the-indexhtm-file"></a>Запись и размещение файла index.htm

Сначала мы создадим файл HTML, который будет использоваться как содержимое веб-сайта.

В корневой папке создайте папку с именем `test`.

В текстовом редакторе введите следующий текст:

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

Сохраните текст как файл `index.htm` в ранее созданной папке `test`. 

## <a name="write-the-configuration"></a>Запись конфигурации

[Конфигурация DSC](configurations.md) — это специальная функция PowerShell, которая определяет способ настройки одного или нескольких целевых компьютеров (узлов).

В среде PowerShell ISE введите следующий текст:

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

Сохраните файл как `WebsiteTest.ps1`.

Как видно, текст выглядит как функция PowerShell, перед именем которой добавлено ключевое слово **Configuration**.

Блок **Node** определяет настраиваемый целевой узел; в нашем примере это `localhost`.

Конфигурация вызывает два [ресурса](resources.md): [WindowsFeature](windowsFeatureResource.md) и [File](fileResource.md).
Ресурсы обеспечивают для целевого узла состояние, определенное в конфигурации.

## <a name="compile-the-configuration"></a>Компиляция конфигурации

Чтобы применить конфигурацию DSC к узлу, ее сначала нужно скомпилировать в MOF-файл.
Для этого запустите конфигурацию как функцию.
В консоли PowerShell перейдите к папке с сохраненным файлом конфигурации и выполните следующую команду, чтобы скомпилировать конфигурацию в MOF-файл:

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

Будут созданы следующие выходные данные:

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

Первая строка делает функцию конфигурации доступной в консоли.
Вторая строка запускает конфигурацию.
Результат — создание папки с именем `WebsiteTest`, которая вложена в текущую папку.
Папка `WebsiteTest` содержит файл с именем `localhost.mof`.
Это файл, который затем можно применить к целевому узлу.

## <a name="apply-the-configuration"></a>Применение конфигурации

Теперь, когда у вас есть скомпилированный MOF-файл, вы можете применить конфигурацию к целевому узлу (в нашем примере это локальный компьютер), вызвав командлет [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration).

Этот командлет `Start-DscConfiguration` сообщает [локальному диспетчеру конфигураций (LCM)](metaConfig.md) (ядру DSC) о необходимости применить конфигурацию.
LCM вызывает ресурсы DSC для применения конфигурации.

В консоли PowerShell перейдите к папке с сохраненным файлом конфигурации и выполните следующую команду:

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a>Тестирование конфигурации

Чтобы проверить применение конфигурации, можно вызвать командлет [Get DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus). 

Также можно проверить результаты непосредственным образом. В нашем примере для этого нужно перейти к `http://localhost/` в веб-браузере.
Вы увидите ранее созданную HTML-страницу "Hello World".

## <a name="next-steps"></a>Дальнейшие действия

- См. дополнительные сведения о [конфигурации DSC](configurations.md).
- См. дополнительные сведения о том, как создавать доступные пользовательские [ресурсы DSC](resources.md).
- Конфигурации DSC и ресурсы доступны в [коллекции PowerShell](https://www.powershellgallery.com/).



