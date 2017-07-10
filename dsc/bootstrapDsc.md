---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка виртуальных машин при начальной загрузке с помощью DSC"
ms.openlocfilehash: a3592c50fa7f2232538fbec07129fac86c1d00b5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
>Область применения: Windows PowerShell 5.0

>**Примечание.** Раздел реестра **DSCAutomationHostEnabled**, описанный в этом разделе, недоступен в PowerShell 4.0.
Сведения о настройке новых виртуальных машин при начальной загрузке в PowerShell 4.0 см. в разделе [Требуется автоматически настроить машины с помощью DSC при начальной загрузке?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/).

<a id="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc" class="xliff"></a>
# Настройка виртуальных машин при начальной загрузке с помощью DSC

<a id="requirements" class="xliff"></a>
## Требования

Для выполнения этих примеров требуется следующее.

- Загрузочный VHD. ISO-файл с пробной версией Windows Server 2016 можно скачать в центре   [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). Инструкции по созданию VHD из ISO-образа см. в разделе [Создание загрузочных виртуальных жестких дисков](https://technet.microsoft.com/en-us/library/gg318049.aspx).
- Компьютер с включенным Hyper-V. Дополнительные сведения см. в статье [Обзор Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).

С помощью DSC можно автоматизировать установку и настройку программного обеспечения для компьютера при начальной загрузке.
Для этого необходимо добавить документ MOF конфигурации или метаконфигурацию на загрузочный носитель (например, VHD), чтобы они выполнялись при начальной загрузке.
Такое поведение контролируется [разделом реестра DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.
По умолчанию значение этого раздела — 2, что позволяет DSC запускаться во время загрузки.

Если запускать DSC во время загрузки не следует, задайте для [раздела реестра DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) значение 0.

- Добавление документа MOF конфигурации в VHD
- Добавление метаконфигурации DSC в VHD
- Отключение DSC при загрузке

>**Примечание.** На компьютер можно одновременно добавить `Pending.mof` и `MetaConfig.mof`.
Если присутствуют оба файла, более высокий приоритет имеют параметры, указанные в `MetaConfig.mof`.

<a id="inject-a-configuration-mof-document-into-a-vhd" class="xliff"></a>
## Добавление документа MOF конфигурации в VHD

Для применения конфигурации при начальной загрузке добавьте скомпилированный документ MOF конфигурации в VHD в качестве его файла `Pending.mof`.
Если раздел реестра **DSCAutomationHostEnabled** имеет значение 2 (значение по умолчанию), DSC применяет конфигурацию, определенную в `Pending.mof`, при первой загрузке компьютера.

В этом примере используется следующая конфигурация, которая устанавливает службы IIS на новом компьютере.

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

<a id="to-inject-the-configuration-mof-document-on-the-vhd" class="xliff"></a>
### Добавление документа MOF конфигурации в VHD

1. Подключите VHD, в который нужно добавить конфигурацию, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx). Например:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. На компьютере с PowerShell 5.0 или более поздней версией сохраните указанную выше конфигурацию (**SampleIISInstall**) как файл сценария PowerShell (.ps1).

3. В консоли PowerShell перейдите в папку, где был сохранен PS1-файл.

4. Выполните следующие команды PowerShell для компиляции документа MOF (дополнительные сведения о компиляции конфигураций DSC см. в разделе [Конфигурации DSC](configurations.md)).

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. Будет создан файл `localhost.mof` в новой папке с именем `SampleIISInstall`.
Переименуйте и переместите этот файл в нужное место на VHD как `Pending.mof` при помощи командлета [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx). Например:

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\Sytem32\Configuration\Pending.mof
    ```
6. Отключите VHD, вызвав командлет [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx). Например:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. Создайте виртуальную машину с помощью VHD, на который установлен документ MOF DSC. После первоначальной загрузки и установки операционной системы будут установлены службы IIS.
Это можно проверить, вызвав командлет [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx).

<a id="inject-a-dsc-metaconfiguration-into-a-vhd" class="xliff"></a>
## Добавление метаконфигурации DSC в VHD

Также можно настроить на компьютере извлечение конфигурации при начальной загрузке, добавив метаконфигурацию (см. раздел [Настройка локального диспетчера конфигурации [LCM]](metaConfig.md)) в VHD в качестве его файла `MetaConfig.mof`.
Если раздел реестра **DSCAutomationHostEnabled** имеет значение 2 (значение по умолчанию), DSC применяет к локальному диспетчеру конфигурации метаконфигурацию, определенную в `MetaConfig.mof` при первой загрузке компьютера.
Если в метаконфигурации указано, что локальный диспетчер конфигурации должен извлекать конфигурации с опрашивающего сервера, компьютер попытается извлечь конфигурации с этого сервера при начальной загрузке.
Сведения о настройке опрашивающего сервера DSC см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md).

В этом примере используется конфигурация, описанная в предыдущем разделе (**SampleIISInstall**), и следующая метаконфигурация.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

<a id="to-inject-the-metaconfiguration-mof-document-on-the-vhd" class="xliff"></a>
### Добавление документа MOF метаконфигурации в VHD

1. Подключите VHD, в который нужно добавить метаконфигурацию, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx). Например:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. [Настройте опрашивающий веб-сервер DSC](pullServer.md) и сохраните конфигурацию **SampleIISInistall** в соответствующую папку.

3. На компьютере с PowerShell 5.0 или более поздней версией сохраните указанную выше метаконфигурацию (**PullClientBootstrap**) как файл сценария PowerShell (.ps1).

4. В консоли PowerShell перейдите в папку, где был сохранен PS1-файл.

5. Выполните следующие команды PowerShell для компиляции документа MOF метаконфигурации (дополнительные сведения о компиляции конфигураций DSC см. в разделе [Конфигурации DSC](configurations.md)).

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. Будет создан файл `localhost.meta.mof` в новой папке с именем `PullClientBootstrap`.
Переименуйте и переместите этот файл в нужное место на VHD как `MetaConfig.mof` при помощи командлета [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx).

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. Отключите VHD, вызвав командлет [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx). Например:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. Создайте виртуальную машину с помощью VHD, на который установлен документ MOF DSC.
После первоначальной загрузки и установки операционной системы DSC извлечет конфигурацию из опрашивающего сервера и будут установлены службы IIS.
Это можно проверить, вызвав командлет [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx).

<a id="disable-dsc-at-boot-time" class="xliff"></a>
## Отключение DSC при загрузке

По умолчанию раздел **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** имеет значение 2, что позволяет запускать конфигурацию DSC, если компьютер находится в состоянии ожидания или в текущем состоянии. Если запускать конфигурацию при начальной загрузке не следует, необходимо задать для этого раздела значение 0.

1. Подключите VHD, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx). Например:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. Загрузите подраздел реестра **HKLM\Software** с VHD, вызвав `reg load`.

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. Перейдите в раздел **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*** с помощью поставщика реестра PowerShell.

    ```powershell
    Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
    ```

4. Измените значение `DSCAutomationHostEnabled` на 0.

    ```powershell
    Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
    ```

5. Выгрузите реестр, выполнив следующие команды.

    ```powershell
    [gc]::Collect()
    reg unload HKLM\Vhd
    ```

<a id="see-also" class="xliff"></a>
## См. также

- [Конфигурации DSC](configurations.md)
- [Раздел реестра DSCAutomationHostEnabled](DSCAutomationHostEnabled.md)
- [Настройка локального диспетчера конфигураций (LCM)](metaConfig.md)
- [Настройка опрашивающего веб-сервера DSC](pullServer.md)

