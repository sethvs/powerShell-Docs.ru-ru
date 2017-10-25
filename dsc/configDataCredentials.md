---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Параметры учетных данных в данных конфигурации"
ms.openlocfilehash: ec4eeb8e519158b2bf929b949e381cdba54f8928
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2017
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="e9165-103">Параметры учетных данных в данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="e9165-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="e9165-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e9165-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="e9165-105">Пароли в виде простого текста и пользователи домена</span><span class="sxs-lookup"><span data-stu-id="e9165-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="e9165-106">Конфигурации DSC, содержащие незашифрованные учетные данные, приводят к сообщениям об ошибке в связи с указанием паролей в виде простого текста.</span><span class="sxs-lookup"><span data-stu-id="e9165-106">DSC configurations containing a credential without encryption will generate an error messages about plain text passwords.</span></span>
<span data-ttu-id="e9165-107">Кроме того, DSC выдает предупреждение при использовании учетных данных домена.</span><span class="sxs-lookup"><span data-stu-id="e9165-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="e9165-108">Чтобы не получать такие ошибки и предупреждения, используйте следующие ключевые слова в данных конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="e9165-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="e9165-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="e9165-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="e9165-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="e9165-110">**PsDscAllowDomainUser**</span></span>

><span data-ttu-id="e9165-111">**Примечание.** Использование паролей в формате открытого текста не является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e9165-111">**Note:** Using plaintext passwords is not secure.</span></span> <span data-ttu-id="e9165-112">Рекомендуется использовать методы защиты учетных данных, описанные далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e9165-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>

<span data-ttu-id="e9165-113">Ниже приведен пример передачи учетных данных в виде открытого текста:</span><span class="sxs-lookup"><span data-stu-id="e9165-113">The following is an example of passing plain text credentials:</span></span>

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

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="e9165-114">Обработка учетных данных в DSC</span><span class="sxs-lookup"><span data-stu-id="e9165-114">Handling Credentials in DSC</span></span>

<span data-ttu-id="e9165-115">По умолчанию ресурсы DSC запускаются от имени `Local System`.</span><span class="sxs-lookup"><span data-stu-id="e9165-115">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="e9165-116">При этом некоторые ресурсы требуют учетных данных, например, если ресурсу `Package` необходимо установить программное обеспечение с помощью учетной записи определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9165-116">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="e9165-117">В более ранних ресурсах для этого использовалось прописываемое в коде свойство `Credential`.</span><span class="sxs-lookup"><span data-stu-id="e9165-117">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="e9165-118">В WMF 5.0 для всех ресурсов было добавлено автоматическое свойство `PsDscRunAsCredential`.</span><span class="sxs-lookup"><span data-stu-id="e9165-118">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span> <span data-ttu-id="e9165-119">Дополнительные сведения об использовании `PsDscRunAsCredential` см. в разделе [Запуск DSC с учетными данными пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="e9165-119">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="e9165-120">Новые и настраиваемые ресурсы позволяют использовать это автоматическое свойство вместо создания отдельного свойства для учетных данных.</span><span class="sxs-lookup"><span data-stu-id="e9165-120">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

<span data-ttu-id="e9165-121">*Обратите внимание, что некоторые ресурсы по определенной причине предполагают использование нескольких учетных данных. Такие ресурсы имеют собственные свойства учетных данных.*</span><span class="sxs-lookup"><span data-stu-id="e9165-121">*Note that the design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.*</span></span>

<span data-ttu-id="e9165-122">Чтобы найти доступные свойства учетных данных ресурса, используйте `Get-DscResource -Name ResourceName -Syntax` или Intellisense в интегрированной среде сценариев (`CTRL+SPACE`).</span><span class="sxs-lookup"><span data-stu-id="e9165-122">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

```powershell
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

<span data-ttu-id="e9165-123">В этом примере используется ресурс [Group](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) из встроенного модуля ресурсов DSC `PSDesiredStateConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="e9165-123">This example uses a [Group](https://msdn.microsoft.com/en-us/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="e9165-124">Он может создавать локальные группы, а также добавлять и удалять члены.</span><span class="sxs-lookup"><span data-stu-id="e9165-124">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="e9165-125">Этот ресурс принимает как свойство `Credential`, так и автоматическое свойство `PsDscRunAsCredential`,</span><span class="sxs-lookup"><span data-stu-id="e9165-125">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="e9165-126">но использует только свойство `Credential`.</span><span class="sxs-lookup"><span data-stu-id="e9165-126">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="e9165-127">См. дополнительные сведения о свойстве `PsDscRunAsCredential` и [запуске DSC с учетными данными пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="e9165-127">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="e9165-128">Пример: свойство учетных данных для ресурса Group</span><span class="sxs-lookup"><span data-stu-id="e9165-128">Example: The Group resource Credential property</span></span>

<span data-ttu-id="e9165-129">DSC выполняется в качестве `Local System`, поэтому уже имеет разрешения на изменение локальных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="e9165-129">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="e9165-130">Если в локальную учетную группу добавляется новый пользователь, учетные данные не требуются.</span><span class="sxs-lookup"><span data-stu-id="e9165-130">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="e9165-131">Но если ресурс `Group` добавляет учетную запись домена в локальную группу, учетные данные необходимы.</span><span class="sxs-lookup"><span data-stu-id="e9165-131">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="e9165-132">Анонимные запросы к Active Directory не допускаются.</span><span class="sxs-lookup"><span data-stu-id="e9165-132">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="e9165-133">Свойство `Credential` ресурса `Group` — это учетная запись домена, которая используется для запросов к Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9165-133">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="e9165-134">В большинстве случаев это может быть универсальная учетная запись пользователя, поскольку пользователи по умолчанию могут *читать* большинство объектов в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9165-134">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="e9165-135">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="e9165-135">Example Configuration</span></span>

<span data-ttu-id="e9165-136">В следующем примере кода DSC используется для добавления пользователя домена в локальную группу:</span><span class="sxs-lookup"><span data-stu-id="e9165-136">The following example code uses DSC to populate a local group with a domain user:</span></span>

```powershell
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

<span data-ttu-id="e9165-137">Этот код вызывает ошибку и предупреждение:</span><span class="sxs-lookup"><span data-stu-id="e9165-137">This code generates both an error and warning message:</span></span>

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

<span data-ttu-id="e9165-138">В этом примере есть две проблемы:</span><span class="sxs-lookup"><span data-stu-id="e9165-138">This example has two issues:</span></span>
1.  <span data-ttu-id="e9165-139">Ошибка с указанием на то, что использовать пароли в виде простого текста не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="e9165-139">An error explains that plain text passwords are not recommended</span></span>
2.  <span data-ttu-id="e9165-140">Предупреждение с рекомендацией не использовать доменные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e9165-140">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="e9165-141">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="e9165-141">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="e9165-142">В первом сообщении об ошибке находится URL-адрес документации.</span><span class="sxs-lookup"><span data-stu-id="e9165-142">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="e9165-143">Он содержит инструкции по шифрованию паролей с использованием структуры [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) и сертификата.</span><span class="sxs-lookup"><span data-stu-id="e9165-143">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/en-us/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="e9165-144">Дополнительные сведения о сертификатах в DSC см. в [этой записи](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="e9165-144">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="e9165-145">Чтобы принудительно использовать пароль в виде простого текста, необходимо добавить в раздел данных конфигурации ресурса ключ `PsDscAllowPlainTextPassword` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9165-145">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

```powershell
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

<span data-ttu-id="e9165-146">*Обратите внимание, что `NodeName` не может быть выражен звездочкой — необходимо указать конкретное имя узла.*</span><span class="sxs-lookup"><span data-stu-id="e9165-146">*Note that `NodeName` cannot equal asterisk, a specific node name is mandatory.*</span></span>

<span data-ttu-id="e9165-147">**Корпорация Майкрософт не рекомендует использовать пароли в виде простого текста из-за серьезной угрозы безопасности.**</span><span class="sxs-lookup"><span data-stu-id="e9165-147">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="e9165-148">Доменные учетные данные</span><span class="sxs-lookup"><span data-stu-id="e9165-148">Domain Credentials</span></span>

<span data-ttu-id="e9165-149">Выполнив сценарий конфигурации из примера еще раз (с шифрованием или без), вы снова получите предупреждение о том, что использовать доменную учетную запись в качестве учетных данных не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="e9165-149">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="e9165-150">Пользуясь для этой цели локальной учетной записью, вы защитите от риска доменные учетные данные, которые можно использовать на других серверах.</span><span class="sxs-lookup"><span data-stu-id="e9165-150">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="e9165-151">**Используя учетные данные с ресурсами DSC, по возможности отдавайте предпочтение локальной учетной записи, а не доменной.**</span><span class="sxs-lookup"><span data-stu-id="e9165-151">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="e9165-152">Если свойство `Username` учетных данных содержит \' или @, DSC будет рассматривать их как доменную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="e9165-152">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="e9165-153">Исключение составляют значения localhost, 127.0.0.1 и ::1 в доменной части имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9165-153">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="e9165-154">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="e9165-154">PSDscAllowDomainUser</span></span>

<span data-ttu-id="e9165-155">В приведенном выше примере ресурса `Group` DSC для запроса к домену Active Directory *требуется* доменная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="e9165-155">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="e9165-156">В этом случае добавьте свойство `PSDscAllowDomainUser` в блок `ConfigurationData` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e9165-156">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

```powershell
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

<span data-ttu-id="e9165-157">После этого сценарий конфигурации создаст MOF-файл без ошибок или предупреждений.</span><span class="sxs-lookup"><span data-stu-id="e9165-157">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>

