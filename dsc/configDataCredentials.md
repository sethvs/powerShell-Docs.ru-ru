---
title: "Параметры учетных данных в данных конфигурации"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 162ae26dec67e8259661bb58c1b713818627220b
ms.sourcegitcommit: b88151841dd44c8ee9296d0855d8b322cbf16076
translationtype: HT
---
# <a name="credentials-options-in-configuration-data"></a>Параметры учетных данных в данных конфигурации
>Область применения: Windows PowerShell 5.0

## <a name="plain-text-passwords-and-domain-users"></a>Пароли в виде простого текста и пользователи домена

Конфигурации DSC, содержащие незашифрованные учетные данные, приводят к сообщениям об ошибке в связи с указанием паролей в виде простого текста.
Кроме того, DSC выдает предупреждение при использовании учетных данных домена.
Чтобы не получать такие ошибки и предупреждения, используйте следующие ключевые слова в данных конфигурации DSC.
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

>**Примечание.** Использование паролей в формате открытого текста не является безопасным. Рекомендуется использовать методы защиты учетных данных, описанные далее в этом разделе.

Ниже приведен пример передачи учетных данных в виде открытого текста:

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
        @{
            # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="*"
            PSDscAllowPlainTextPassword = $true
        },
        #however, each node still needs to be explicitly defined for "*" to have meaning
        @{
            NodeName = "TestMachine1"
        },
        #we can also use a property to define node-specific passwords, although this is no more secure
        @{
            NodeName = "TestMachine2";
            UserName = "User2"
            LocalPassword = "ThisIsYetAnotherPlaintextPassword"
        }
        )
}
configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }

    }

    
    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPass | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $domain
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
      
    }

}
# We declared the ConfigurationData in a local variable, but we need to pass it in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData
# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

## <a name="handling-credentials-in-dsc"></a>Обработка учетных данных в DSC

По умолчанию ресурсы DSC запускаются от имени `Local System`.
При этом некоторые ресурсы требуют учетных данных, например, если ресурсу `Package` необходимо установить программное обеспечение с помощью учетной записи определенного пользователя.

В более ранних ресурсах для этого использовалось прописываемое в коде свойство `Credential`.
В WMF 5.0 для всех ресурсов было добавлено автоматическое свойство `PsDscRunAsCredential`. Дополнительные сведения об использовании `PsDscRunAsCredential` см. в разделе [Запуск DSC с учетными данными пользователя](runAsUser.md).
Новые и настраиваемые ресурсы позволяют использовать это автоматическое свойство вместо создания отдельного свойства для учетных данных.

*Обратите внимание, что некоторые ресурсы по определенной причине предполагают использование нескольких учетных данных. Такие ресурсы имеют собственные свойства учетных данных.*

Чтобы найти доступные свойства учетных данных ресурса, используйте `Get-DscResource -Name ResourceName -Syntax` или Intellisense в интегрированной среде сценариев (`CTRL+SPACE`).

```PowerShell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

В этом примере используется ресурс [Group](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) из встроенного модуля ресурсов DSC `PSDesiredStateConfiguration`.
Он может создавать локальные группы, а также добавлять и удалять члены.
Этот ресурс принимает как свойство `Credential`, так и автоматическое свойство `PsDscRunAsCredential`,
но использует только свойство `Credential`.
Дополнительные сведения о `PsDscRunAsCredential` см. в [заметках о выпуске WMF](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_runas).

## <a name="example-the-group-resource-credential-property"></a>Пример: свойство учетных данных для ресурса Group

DSC выполняется в качестве `Local System`, поэтому уже имеет разрешения на изменение локальных пользователей и групп.
Если в локальную учетную группу добавляется новый пользователь, учетные данные не требуются.
Но если ресурс `Group` добавляет учетную запись домена в локальную группу, учетные данные необходимы.

Анонимные запросы к Active Directory не допускаются.
Свойство `Credential` ресурса `Group` — это учетная запись домена, которая используется для запросов к Active Directory.
В большинстве случаев это может быть универсальная учетная запись пользователя, поскольку пользователи по умолчанию могут *читать* большинство объектов в Active Directory.

## <a name="example-configuration"></a>Пример конфигурации

В следующем примере кода DSC используется для добавления пользователя домена в локальную группу:

```PowerShell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

Этот код вызывает ошибку и предупреждение:

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

В этом примере есть две проблемы:
1.  Ошибка с указанием на то, что использовать пароли в виде простого текста не рекомендуется.
2.  Предупреждение с рекомендацией не использовать доменные учетные данные.

## <a name="psdscallowplaintextpassword"></a>PsDscAllowPlainTextPassword

В первом сообщении об ошибке находится URL-адрес документации.
Он содержит инструкции по шифрованию паролей с использованием структуры [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) и сертификата.
Дополнительные сведения о сертификатах в DSC см. в [этой записи](http://aka.ms/certs4dsc).

Чтобы принудительно использовать пароль в виде простого текста, необходимо добавить в раздел данных конфигурации ресурса ключ `PsDscAllowPlainTextPassword` следующим образом:

```PowerShell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

*Обратите внимание, что `NodeName` не может быть выражен звездочкой — необходимо указать конкретное имя узла.*

**Корпорация Майкрософт не рекомендует использовать пароли в виде простого текста из-за серьезной угрозы безопасности.**

## <a name="domain-credentials"></a>Доменные учетные данные

Выполнив сценарий конфигурации из примера еще раз (с шифрованием или без), вы снова получите предупреждение о том, что использовать доменную учетную запись в качестве учетных данных не рекомендуется.
Пользуясь для этой цели локальной учетной записью, вы защитите от риска доменные учетные данные, которые можно использовать на других серверах.

**Используя учетные данные с ресурсами DSC, по возможности отдавайте предпочтение локальной учетной записи, а не доменной.**

Если свойство `Username` учетных данных содержит \' или '@', DSC будет рассматривать их как доменную учетную запись.
Исключение составляют значения localhost, 127.0.0.1 и ::1 в доменной части имени пользователя.

## <a name="psdscallowdomainuser"></a>PSDscAllowDomainUser

В приведенном выше примере ресурса `Group` DSC для запроса к домену Active Directory *требуется* доменная учетная запись.
В этом случае добавьте свойство `PSDscAllowDomainUser` в блок `ConfigurationData` следующим образом:

```PowerShell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

После этого сценарий конфигурации создаст MOF-файл без ошибок или предупреждений.

