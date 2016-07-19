---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "возможности ролей"
ms.technology: powershell
translationtype: Human Translation
ms.sourcegitcommit: 81fd386d58576a8930093b4f18ce36a4ff6cecd0
ms.openlocfilehash: a3dd4a217f5b1fd80e97adf802c65073ca015bbc

---

# Возможности ролей

## Обзор
В предыдущем разделе вы узнали, что поле RoleDefinitions определяет, какие группы имеют доступ к отдельным возможностям ролей.
Вероятно, вы задумались о том, что такое возможности ролей?
Ответ находится в этом разделе.  

## Введение в возможности ролей PowerShell
Возможности ролей PowerShell определяют, что именно сможет делать пользователь в конечной точке JEA.
Они содержат подробный список таких вещей, как видимые команды, видимые приложения и многое другое.
Возможности ролей определяются файлами с расширением PSRC.

## Содержимое возможностей роли
Начнем с изучения и изменения демонстрационного файла возможностей роли, который мы использовали раньше.
Допустим, вы развернули конфигурацию сеанса в своей среде, но получили указание изменить предоставляемые пользователям возможности.
У операторов должна быть возможность перезапускать компьютеры, а также получать информацию о параметрах их сетей.
Кроме того, группа, отвечающая за безопасность, сообщила вам, что разрешать пользователям выполнять команду Restart-Service без ограничений недопустимо.
Список служб, которые может перезапускать оператор, необходимо ограничить.

Для внесения этих изменений запустите интегрированную среду сценариев PowerShell и откройте следующий файл:

```
C:\Program Files\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc
```

Теперь найдите и измените в этом файле следующие строки:

```PowerShell
# OLD: VisibleCmdlets = 'Restart-Service'
VisibleCmdlets = 'Restart-Computer',
                 @{
                     Name = 'Restart-Service'
                     Parameters = @{ Name = 'Name'; ValidateSet = 'Spooler' }
                 },
                 'NetTCPIP\Get-*'

# OLD: VisibleExternalCommands = 'Item1', 'Item2'
VisibleExternalCommands = 'C:\Windows\system32\ipconfig.exe'
```

Здесь есть несколько интересных примеров:

1.  Вы ограничили выполнение команды Restart-Service таким образом, что операторы могут выполнять ее только с параметром -Name и использовать для этого параметра только аргумент "Spooler".
При желании доступные аргументы можно ограничить с помощью регулярного выражения, указав "ValidatePattern" вместо "ValidateSet".

2.  Вы предоставили доступ ко всем командам с глаголом "Get" из модуля NetTCPIP.
Так как команды "Get" обычно не изменяют системные данные, это относительно безопасное действие.
С другой стороны, настоятельно рекомендуется тщательно изучать все команды, предоставляемые через JEA.

3.  Вы предоставили доступ к исполняемому файлу (ipconfig), используя VisibleExternalCommands.
С помощью этого поля можно также предоставить доступ ко всем сценариям PowerShell.
Очень важно всегда указывать полный путь ко внешним командам, чтобы вместо нужной программы не была выполнена одноименная (и, возможно, вредоносная) программа, указанная в пути пользователя.

Сохраните файл, а затем еще раз подключитесь к демонстрационной конечной точке, чтобы убедиться в том, что изменения сработали.

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
Get-Command
```
Так как вы изменили только файл возможностей роли, регистрировать конфигурацию сеанса заново не нужно.
При подключении пользователя PowerShell автоматически находит обновленные возможности роли.
Так как возможности роли загружаются при запуске сеанса, изменения в файлах возможностей ролей не влияют на существующие сеансы.

Теперь убедитесь, что вы можете перезапустить компьютер, выполнив команду Restart-Computer с параметром -WhatIf (если только перезагрузка компьютера не требуется вам на самом деле).

```PowerShell
Restart-Computer -WhatIf
```

Убедитесь, что вы можете выполнить команду "ipconfig".

```PowerShell
ipconfig
```

Наконец, убедитесь, что команда Restart-Service работает только со службой Spooler.

```PowerShell
Restart-Service Spooler # This should work
Restart-Service WSearch # This should fail
```

Закончив, выйдите из сеанса.

```PowerShell
Exit-PSSession
```

## Создание возможностей роли
В следующем разделе мы создадим конечную точку JEA для пользователей службы поддержки AD.
Для подготовки создадим пустой файл возможностей роли, который заполним в этом разделе.
Возможности роли должны создаваться в папке "RoleCapabilities" в допустимом модуле PowerShell, чтобы их можно было использовать при запуске сеанса.

По сути модули PowerShell — это пакеты функциональных возможностей PowerShell.
Они могут содержать функции PowerShell, командлеты, ресурсы DSC, возможности ролей и многое другое.
Чтобы получить сведения о модулях, выполните команду `Get-Help about_Modules` в консоли PowerShell.

Чтобы создать новый модуль PowerShell с пустым файлом возможностей роли, выполните следующие команды:  

```PowerShell
# Create a new folder for the module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module' -ItemType Directory

# Add a module manifest to contain metadata for this module.
New-ModuleManifest -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psd1' -RootModule Contoso_AD_Module.psm1

# Create a blank script module. You'll use this for custom functions in the next section.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1' -ItemType File

# Create a RoleCapabilities folder in the Contoso_AD_Module folder. PowerShell expects Role Capabilities to be located in a "RoleCapabilities" folder within a module.
New-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities' -ItemType Directory

# Create a blank Role Capability in your RoleCapabilities folder. Running this command without any additional parameters just creates a blank template.
New-PSRoleCapabilityFile -Path 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc'
```

Поздравляем, вы создали пустой файл возможностей роли.
Он будет использоваться в следующем разделе.

## Основные понятия
**Возможности роли PowerShell (PSRC)**: файл, определяющий, что именно может делать пользователь в конечной точке JEA.
Он содержит подробный список таких вещей, как видимые команды, видимые приложения консоли и многое другое.
Чтобы среда PowerShell обнаруживала возможности ролей, необходимо поместить их в папку RoleCapabilities в допустимом модуле PowerShell.

**Модуль PowerShell**: пакет функциональных возможностей PowerShell.
Может содержать функции PowerShell, командлеты, ресурсы DSC, возможности ролей и многое другое.
Для автоматической загрузки модули PowerShell должны находиться в папке `$env:PSModulePath`.




<!--HONumber=Jul16_HO1-->


