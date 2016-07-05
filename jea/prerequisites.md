---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "предварительные требования"
ms.technology: powershell
ms.sourcegitcommit: 7504fe496a8913718847e45115d126caf4049bef
ms.openlocfilehash: ac9231a475ba84e9051bbd06a65f3f20c9e49846

---

# Необходимые компоненты

## Начальное состояние
Прежде чем приступать к этому разделу, убедитесь в следующем.

1. В вашей системе доступна функция JEA. Проверьте список поддерживаемых операционных систем и необходимые скачиваемые компоненты в файле [README](./README.md).
2. У вас есть права администратора на компьютере, где используется JEA.
3. Компьютер присоединен к домену.
Инструкции по быстрой настройке нового домена на сервере см. в статье [Создание контроллера домена](#creating-a-domain-controller).

## Включение удаленного взаимодействия PowerShell
Управление с помощью функции JEA осуществляется через удаленное взаимодействие PowerShell.
Чтобы убедиться, что оно включено и правильно настроено, выполните в окне администратора PowerShell следующую команду:

```PowerShell
Enable-PSRemoting
```

Если вы не знакомы с работой удаленного взаимодействия PowerShell, запустите `Get-Help about_Remote` и ознакомьтесь с этой важной фундаментальной концепцией.

## Идентификация пользователей или групп
Чтобы показать JEA в действии, необходимо определить пользователей и группы без прав администратора, которые будут использоваться в этом руководстве.

Если используется существующий домен, определите или создайте учетные записи непривилегированных пользователей и группы.
Им будет предоставлен доступ к JEA без прав администратора.
Каждый раз, когда вы видите переменную `$NonAdministrator` в верхней части сценария, необходимо записать в нее выбранных пользователей или группы без прав администратора.

При создании нового домена с нуля все происходит гораздо проще.
Для создания учетных записей пользователей и групп без прав администратора воспользуйтесь сведениями в разделе [Настройка пользователей и групп](creating-a-domain-controller.md#set-up-users-and-groups) в приложении.
Значениями переменной `$NonAdministrator` по умолчанию будут группы, созданные в указанном разделе.

## Настройка файла возможности для роли обслуживания
Чтобы создать демонстрационный файл возможностей роли, который понадобится нам в следующем разделе, выполните в PowerShell следующие команды:
Для чего нужен этот файл, вы узнаете далее в этом разделе.

```PowerShell
# Fields in the role capability
$MaintenanceRoleCapabilityCreationParams = @{
    Author = 'Contoso Admin'
    CompanyName = 'Contoso'
    VisibleCmdlets = 'Restart-Service'
    FunctionDefinitions =
            @{ Name = 'Get-UserInfo'; ScriptBlock = { $PSSenderInfo } }
}

# Create the demo module, which will contain the maintenance Role Capability File
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module" -ItemType Directory
New-ModuleManifest -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\Demo_Module.psd1"
New-Item -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities" -ItemType Directory

# Create the Role Capability file
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\Demo_Module\RoleCapabilities\Maintenance.psrc" @MaintenanceRoleCapabilityCreationParams
```

## Создание и регистрация демонстрационного файла конфигурации сеанса
Чтобы создать и зарегистрировать демонстрационный файл конфигурации сеанса, который понадобится нам в следующем разделе, выполните следующие команды:
Для чего нужен этот файл, вы узнаете далее в этом разделе.

```PowerShell
# Determine domain
$domain = (Get-CimInstance -ClassName Win32_ComputerSystem).Domain

# Replace with your non-admin group name
$NonAdministrator = "$domain\JEA_NonAdmin_Operator"

# Specify the settings for this JEA endpoint
# Note: You will not be able to use a virtual account if you are using WMF 5.0 on Windows 7 or Windows Server 2008 R2
$JEAConfigParams = @{
    SessionType = 'RestrictedRemoteServer'
    RunAsVirtualAccount = $true
    RoleDefinitions = @{
        $NonAdministrator = @{ RoleCapabilities = 'Maintenance' }
    }
    TranscriptDirectory = "$env:ProgramData\JEAConfiguration\Transcripts"
}

# Set up a folder for the Session Configuration files
if (-not (Test-Path "$env:ProgramData\JEAConfiguration"))
{
    New-Item -Path "$env:ProgramData\JEAConfiguration" -ItemType Directory
}

# Specify the name of the JEA endpoint
$sessionName = 'JEA_Demo'

if (Get-PSSessionConfiguration -Name $sessionName -ErrorAction SilentlyContinue)
{
    Unregister-PSSessionConfiguration -Name $sessionName -ErrorAction Stop
}

New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc" @JEAConfigParams

# Register the session configuration
Register-PSSessionConfiguration -Name $sessionName -Path "$env:ProgramData\JEAConfiguration\JEADemo.pssc"
```

## Включение ведения журнала модуля PowerShell (необязательно)
Указанные ниже действия позволят включить ведение журнала действий PowerShell в вашей системе.
Это не обязательно для работы с JEA, но пригодится при работе с разделом [Отчеты о JEA](reporting-on-jea.md).

1. Откройте редактор локальных групповых политик
2. Откройте папку "Конфигурация компьютера\Административные шаблоны\Компоненты Windows\Windows PowerShell".
3. Дважды щелкните пункт "Включить модуль ведения журнала".
4. Нажмите кнопку "Включено".
5. В разделе "Параметры" нажмите кнопку "Показать" рядом с именами модулей.
6. Введите "\*" во всплывающем окне. Это означает, что PowerShell будет регистрировать в журнале команды из всех модулей.
7. Нажмите кнопку "ОК" и примените политику.

Примечание. Вы можете также включить при помощи групповой политики запись действий PowerShell в масштабе всей системы.

**Итак, вы настроили на компьютере демонстрационную конечную точку и готовы приступить к работе с JEA.**




<!--HONumber=Jun16_HO4-->


