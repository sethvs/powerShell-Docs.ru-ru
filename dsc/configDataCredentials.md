---
title:   Параметры учетных данных в данных конфигурации
ms.date:  2016-05-16
keywords:  powershell,DSC
description:  
ms.topic:  article
author:  eslesar
manager:  dongill
ms.prod:  powershell
---

# Параметры учетных данных в данных конфигурации
>Область применения: Windows PowerShell 5.0

## Пароли в виде простого текста и пользователи домена

Конфигурации DSC, содержащие незашифрованные учетные данные, приводят к сообщениям об ошибке в связи с указанием паролей в виде простого текста.
Кроме того, DSC выдает предупреждение при использовании учетных данных домена.
Чтобы не получать такие ошибки и предупреждения, используйте следующие ключевые слова в данных конфигурации DSC.
* **PsDscAllowPlainTextPassword**
* **PsDscAllowDomainUser**

## Обработка учетных данных в DSC

По умолчанию ресурсы DSC запускаются от имени `Local System`.
При этом некоторые ресурсы требуют учетных данных, например, если ресурсу `Package` необходимо установить программное обеспечение с помощью учетной записи определенного пользователя.

В более ранних ресурсах для этого использовалось прописываемое в коде свойство `Credential`.
В WMF 5.0 для всех ресурсов было добавлено автоматическое свойство `PsDscRunAsCredential`. Дополнительные сведения об использовании `PsDscRunAsCredential` см. в разделе [Запуск DSC с учетными данными пользователя](runAsUser.md).
Новые и настраиваемые ресурсы позволяют использовать это автоматическое свойство вместо создания отдельного свойства для учетных данных.

*Обратите внимание, что структура некоторых ресурсов рассчитана на использование нескольких учетных данных по определенной причине и такие ресурсы имеют собственные свойства учетных данных.*

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

## Пример: свойство учетных данных для ресурса Group

DSC выполняется в качестве `Local System`, поэтому уже имеет разрешения на изменение локальных пользователей и групп.
Если в локальную учетную группу добавляется новый пользователь, учетные данные не требуются.
Но если ресурс `Group` добавляет учетную запись домена в локальную группу, учетные данные необходимы.

Анонимные запросы к Active Directory не допускаются.
Свойство `Credential` ресурса `Group` — это учетная запись домена, которая используется для запросов к Active Directory.
В большинстве случаев это может быть универсальная учетная запись пользователя, поскольку пользователи по умолчанию могут *читать* большинство объектов в Active Directory.

## Пример конфигурации

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

## PsDscAllowPlainTextPassword

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

*Обратите внимание, что `NodeName` не может быть звездочкой — необходимо указать определенное имя узла.*

**Корпорация Майкрософт не рекомендует использовать пароли в виде простого текста из-за серьезной угрозы безопасности.**

## Доменные учетные данные

Выполнив сценарий конфигурации из примера еще раз (с шифрованием или без), вы снова получите предупреждение о том, что использовать доменную учетную запись в качестве учетных данных не рекомендуется.
Пользуясь для этой цели локальной учетной записью, вы защитите от риска доменные учетные данные, которые можно использовать на других серверах.

**Используя учетные данные с ресурсами DSC, по возможности отдавайте предпочтение локальной учетной записи, а не доменной.**

Если свойство `Username` учетных данных содержит \' или @, DSC будет рассматривать их как доменную учетную запись.
Исключение составляют значения localhost, 127.0.0.1 и ::1 в доменной части имени пользователя.

## PSDscAllowDomainUser

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



<!--HONumber=May16_HO3-->


