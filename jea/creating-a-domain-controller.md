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
ms.openlocfilehash: 80b957ed666ca626c6083041cf99c263e2e0dc27
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
### <a name="creating-a-domain-controller"></a><span data-ttu-id="b0777-103">Создание контроллера домена</span><span class="sxs-lookup"><span data-stu-id="b0777-103">Creating a Domain Controller</span></span>

<span data-ttu-id="b0777-104">В этом документе предполагается, что компьютер уже присоединен к домену.</span><span class="sxs-lookup"><span data-stu-id="b0777-104">This document assumes that your machine is domain joined.</span></span>
<span data-ttu-id="b0777-105">Если сейчас у вас нет домена для присоединения, этот раздел поможет вам быстро настроить контроллер домена с помощью DSC.</span><span class="sxs-lookup"><span data-stu-id="b0777-105">If you currently don't have a domain to join, this section can help you quickly stand up a domain controller using DSC.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="b0777-106">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="b0777-106">Prerequisites</span></span>

1.  <span data-ttu-id="b0777-107">Компьютер находится во внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="b0777-107">The machine is on an internal network</span></span>
2.  <span data-ttu-id="b0777-108">Компьютер не присоединен к существующему домену.</span><span class="sxs-lookup"><span data-stu-id="b0777-108">The machine is not joined to an existing domain</span></span>
3.  <span data-ttu-id="b0777-109">Компьютер работает под управлением Windows Server 2016 или на нем установлена платформа WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="b0777-109">The machine is running Windows Server 2016 or has WMF 5.0 installed</span></span>

#### <a name="install-xactivedirectory"></a><span data-ttu-id="b0777-110">Установка xActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="b0777-110">Install xActiveDirectory</span></span>
<span data-ttu-id="b0777-111">Если компьютер имеет активное подключение к Интернету, выполните следующую команду в окне PowerShell с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="b0777-111">If your machine has an active internet connection, run the following command in an elevated PowerShell window:</span></span>
```PowerShell
Install-Module xActiveDirectory -Force
```
<span data-ttu-id="b0777-112">Если подключения к Интернету нет, установите xActiveDirectory на другой компьютер и скопируйте папку xActiveDirectory в папку "C:\Program Files\WindowsPowerShell\Modules" на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b0777-112">If you do not have an internet connection, install xActiveDirectory to another machine and then copy the xActiveDirectory folder to the "C:\Program Files\WindowsPowerShell\Modules" folder on your machine.</span></span>

<span data-ttu-id="b0777-113">Чтобы проверить успешность установки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b0777-113">To confirm the installation succeeded, run the following command:</span></span>
```PowerShell
Get-Module xActiveDirectory -ListAvailable
```

#### <a name="set-up-a-domain-with-dsc"></a><span data-ttu-id="b0777-114">Настройка имени домена</span><span class="sxs-lookup"><span data-stu-id="b0777-114">Set up a domain with DSC</span></span>
<span data-ttu-id="b0777-115">Скопируйте приведенный ниже сценарий в PowerShell, чтобы сделать компьютер контроллером нового домена.</span><span class="sxs-lookup"><span data-stu-id="b0777-115">Copy the following script in PowerShell to make your machine a Domain Controller in a new domain.</span></span>
<span data-ttu-id="b0777-116">**ПРИМЕЧАНИЕ АВТОРА: ИЗВЕСТНО, ЧТО СУЩЕСТВУЕТ ПРОБЛЕМА, ПРИ КОТОРОЙ УКАЗАННЫЕ УЧЕТНЫЕ ДАННЫЕ НЕ ИСПОЛЬЗУЮТСЯ.  В ЦЕЛЯХ БЕЗОПАСНОСТИ НЕ ЗАБЫВАЙТЕ СВОЙ ПАРОЛЬ ЛОКАЛЬНОГО АДМИНИСТРАТОРА.**</span><span class="sxs-lookup"><span data-stu-id="b0777-116">**AUTHOR'S NOTE: THERE IS A KNOWN ISSUE WITH THE CREDENTIALS PROVIDED NOT BEING USED.  TO BE SAFE, DON'T FORGET YOUR LOCAL ADMIN PASSWORD.**</span></span>

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
<span data-ttu-id="b0777-117">Компьютер перезагрузится несколько раз.</span><span class="sxs-lookup"><span data-stu-id="b0777-117">Your machine will restart a few times.</span></span>
<span data-ttu-id="b0777-118">Вы узнаете, что процесс завершен, как только будет создан файл с именем "C:\temp.txt", содержащий текст "Domain has been created" (Домен создан).</span><span class="sxs-lookup"><span data-stu-id="b0777-118">You will know the process is complete once you see a file called "C:\temp.txt" containing "Domain has been created."</span></span>

#### <a name="set-up-users-and-groups"></a><span data-ttu-id="b0777-119">Настройка пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="b0777-119">Set up Users and Groups</span></span>
<span data-ttu-id="b0777-120">Следующие команды настроят группы операторов и службы поддержки в вашем домене и учетную запись соответствующего пользователя без прав администратора, входящего в эту группу.</span><span class="sxs-lookup"><span data-stu-id="b0777-120">The following commands will set up an Operator and Helpdesk group in your domain and a corresponding non-administrator user who is a member of that group.</span></span>
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

