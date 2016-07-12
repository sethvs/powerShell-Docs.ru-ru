---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "создание контроллера домена"
ms.technology: powershell
translationtype: Human Translation
ms.sourcegitcommit: d4a72a7c5883b1d3ba8de3dbc9cfe016a6fb3498
ms.openlocfilehash: 8473eb668e4da5bab01c2f2b7647cbced413bd22

---

### Создание контроллера домена

В этом документе предполагается, что компьютер уже присоединен к домену.
Если сейчас у вас нет домена для присоединения, этот раздел поможет вам быстро настроить контроллер домена с помощью DSC.

#### Необходимые компоненты

1.  Компьютер находится во внутренней сети.
2.  Компьютер не присоединен к существующему домену.
3.  Компьютер работает под управлением Windows Server 2016 или на нем установлена платформа WMF 5.0.

#### Установка xActiveDirectory
Если компьютер имеет активное подключение к Интернету, выполните следующую команду в окне PowerShell с повышенными привилегиями:
```PowerShell
Install-Module xActiveDirectory -Force
```
Если подключения к Интернету нет, установите xActiveDirectory на другой компьютер и скопируйте папку xActiveDirectory в папку "C:\Program Files\WindowsPowerShell\Modules" на вашем компьютере.

Чтобы проверить успешность установки, выполните следующую команду:
```PowerShell
Get-Module xActiveDirectory -ListAvailable
```

#### Настройка имени домена
Скопируйте приведенный ниже сценарий в PowerShell, чтобы сделать компьютер контроллером нового домена.
**ПРИМЕЧАНИЕ АВТОРА: ИЗВЕСТНО, ЧТО СУЩЕСТВУЕТ ПРОБЛЕМА, ПРИ КОТОРОЙ УКАЗАННЫЕ УЧЕТНЫЕ ДАННЫЕ НЕ ИСПОЛЬЗУЮТСЯ.  В ЦЕЛЯХ БЕЗОПАСНОСТИ НЕ ЗАБЫВАЙТЕ СВОЙ ПАРОЛЬ ЛОКАЛЬНОГО АДМИНИСТРАТОРА.**

```PowerShell
Set-Item WSMan:\localhost\Client\TrustedHosts -Value $env:COMPUTERNAME -Force

# This "MetaConfiguration" sets the DSC Engine to automatically reboot if required
[DscLocalConfigurationManager()]
Configuration MetaConfiguration
{
    Node $env:Computername
    {
        Settings
        {
            RebootNodeIfNeeded = $true
        }
    }

}

MetaConfiguration
# Apply the MetaConfiguration
Set-DscLocalConfigurationManager .\MetaConfiguration

# Configure a domain controller of a new "Contoso" domain
configuration DomainController
{
    param
    (
        $node,
        $cred
    )
    Import-DscResource -ModuleName xActiveDirectory

    Node $node
    {
        WindowsFeature ADDS
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain Contoso
        {
            DomainName = 'contoso.com'
            DomainAdministratorCredential = $cred
            SafemodeAdministratorPassword = $cred
            DependsOn = '[WindowsFeature]ADDS'
        }

        file temp
        {
            DestinationPath = 'C:\temp.txt'
            Contents = 'Domain has been created'
            DependsOn = '[xADDomain]Contoso'
        }
    }
}

$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = $env:Computername
            PSDscAllowPlainTextPassword = $true
        }
    )
}

# Enter your desired password for the domain administrator (note, this will be stored as plain text)
DomainController -cred (Get-Credential -Message "Enter desired credential for domain administrator") -node $env:Computername -configurationData $ConfigData

# Apply the configuration to create the domain controller
Start-DSCConfiguration -path .\DomainController -ComputerName $env:Computername -Wait -Force -Verbose
```
Компьютер перезагрузится несколько раз.
Вы узнаете, что процесс завершен, как только будет создан файл с именем "C:\temp.txt", содержащий текст "Domain has been created" (Домен создан).

#### Настройка пользователей и групп
Следующие команды настроят группы операторов и службы поддержки в вашем домене и учетную запись соответствующего пользователя без прав администратора, входящего в эту группу.
```PowerShell
# Make Groups
$NonAdminOperatorGroup = New-ADGroup -Name "JEA_NonAdmin_Operator" -GroupScope DomainLocal -PassThru
$NonAdminHelpDeskGroup = New-ADGroup -Name "JEA_NonAdmin_HelpDesk" -GroupScope DomainLocal -PassThru
$TestGroup = New-ADGroup -Name "Test_Group" -GroupScope DomainLocal -PassThru

# Make Users
$OperatorUser = New-ADUser -Name "OperatorUser" -AccountPassword (ConvertTo-SecureString 'pa$$w0rd' -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $OperatorUser

$HelpDeskUser = New-ADUser -name "HelpDeskUser" -AccountPassword (ConvertTo-SecureString 'pa$$w0rd' -AsPlainText -Force) -PassThru
Enable-ADAccount -Identity $HelpDeskUser

# Add Users to Groups
Add-ADGroupMember -Identity $NonAdminOperatorGroup -Members $OperatorUser
Add-ADGroupMember -Identity $NonAdminHelpDeskGroup -Members $HelpDeskUser
```




<!--HONumber=Jul16_HO1-->


