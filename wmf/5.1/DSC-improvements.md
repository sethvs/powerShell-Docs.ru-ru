---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: Усовершенствования DSC в WMF 5.1
ms.openlocfilehash: 04bf8ed820d24f1062e05d19c8f3b0c041298979
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="3c25a-103">Усовершенствования в настройке требуемого состояния (DSC) в WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="3c25a-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="3c25a-104">Усовершенствования в ресурсах классов DSC</span><span class="sxs-lookup"><span data-stu-id="3c25a-104">DSC class resource improvements</span></span>

<span data-ttu-id="3c25a-105">В WMF 5.1 были устранены следующие известные проблемы.</span><span class="sxs-lookup"><span data-stu-id="3c25a-105">In WMF 5.1, we have fixed the following known issues:</span></span>
* <span data-ttu-id="3c25a-106">Командлет Get-DscConfiguration может возвращать пустые значения (NULL) или ошибки, если функция Get() ресурса DSC на основе классов возвращает сложный тип или хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="3c25a-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
* <span data-ttu-id="3c25a-107">Командлет Get-DscConfiguration возвращает ошибку, если в конфигурации DSC используются учетные данные запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="3c25a-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
* <span data-ttu-id="3c25a-108">Ресурсы на основе классов не могут использоваться в составной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3c25a-108">Class-based resource cannot be used in a composite configuration.</span></span>
* <span data-ttu-id="3c25a-109">Командлет Start-DscConfiguration зависает, если ресурс на основе классов имеет свойство со своим собственным типом.</span><span class="sxs-lookup"><span data-stu-id="3c25a-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
* <span data-ttu-id="3c25a-110">Ресурсы на основе класса не могут использоваться в качестве монопольных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3c25a-110">Class-based resource cannot be used as an exclusive resource.</span></span>


## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="3c25a-111">Усовершенствования в отладке ресурсов DSC</span><span class="sxs-lookup"><span data-stu-id="3c25a-111">DSC resource debugging improvements</span></span>
<span data-ttu-id="3c25a-112">В WMF 5.0 отладчик PowerShell не останавливался непосредственно в методах для работы с ресурсами, основанными на классах (Get, Set, Test).</span><span class="sxs-lookup"><span data-stu-id="3c25a-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span>
<span data-ttu-id="3c25a-113">В WMF 5.1 отладчик останавливается в методах для работы с ресурсами, основанными на классах, точно так же, как в методах для работы с ресурсами на основе MOF.</span><span class="sxs-lookup"><span data-stu-id="3c25a-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="3c25a-114">Опрашивающий клиент DSC поддерживает TLS 1.1 и TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="3c25a-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>
<span data-ttu-id="3c25a-115">Ранее опрашивающий клиент DSC поддерживал только SSL3.0 и TLS1.0 через подключения по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3c25a-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span>
<span data-ttu-id="3c25a-116">При принудительном использовании более безопасных протоколов опрашивающий клиент прекращал работу.</span><span class="sxs-lookup"><span data-stu-id="3c25a-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span>
<span data-ttu-id="3c25a-117">В WMF 5.1 опрашивающий клиент DSC больше не поддерживает SSL 3.0, но поддерживает более безопасные протоколы TLS 1.1 и TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="3c25a-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="3c25a-118">Улучшенная регистрация опрашивающего сервера</span><span class="sxs-lookup"><span data-stu-id="3c25a-118">Improved pull server registration</span></span> ##

<span data-ttu-id="3c25a-119">В более ранних версиях WMF одновременные запросы регистрации или отчетов к опрашивающему серверу DSC при использовании базы данных ESENT привели бы к ошибке в LCM при регистрации или получении отчета.</span><span class="sxs-lookup"><span data-stu-id="3c25a-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span>
<span data-ttu-id="3c25a-120">В журналах событий на опрашивающем сервере в таких случаях появляется ошибка "Имя экземпляра уже используется".</span><span class="sxs-lookup"><span data-stu-id="3c25a-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span>
<span data-ttu-id="3c25a-121">Эта ошибка вызывалась тем, что для доступа к базе данных ESENT в сценарии с несколькими потоками использовался неправильный шаблон.</span><span class="sxs-lookup"><span data-stu-id="3c25a-121">This was due to an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span>
<span data-ttu-id="3c25a-122">В WMF 5.1 эта проблема устранена.</span><span class="sxs-lookup"><span data-stu-id="3c25a-122">In WMF 5.1, this issue has been fixed.</span></span>
<span data-ttu-id="3c25a-123">Одновременные запросы регистрации или отчетов (с использованием базы данных ESENT) выполняются корректно в WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="3c25a-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span>
<span data-ttu-id="3c25a-124">Эта проблема относится только к базе данных ESENT и не касается базы данных OLEDB.</span><span class="sxs-lookup"><span data-stu-id="3c25a-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="3c25a-125">Включить циклический журнал в экземпляре базы данных ESENT</span><span class="sxs-lookup"><span data-stu-id="3c25a-125">Enable Circular log on ESENT database instance</span></span>
<span data-ttu-id="3c25a-126">В более ранней версии DSC-PullServer файлы журнала базы данных ESENT заполняли дисковое пространство опрашивающего сервера, так как экземпляр базы данных был создан без циклического ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="3c25a-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver becouse the database instance was being created without circular logging.</span></span> <span data-ttu-id="3c25a-127">В этом выпуске можно управлять поведением циклического ведения журнала экземпляра с помощью web.config опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="3c25a-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="3c25a-128">По умолчанию значение CircularLogging равно TRUE.</span><span class="sxs-lookup"><span data-stu-id="3c25a-128">By default CircularLogging is set to TRUE.</span></span>
```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```
## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="3c25a-129">Соглашение об именовании для частичной опрашивающей конфигурации</span><span class="sxs-lookup"><span data-stu-id="3c25a-129">Pull partial configuration naming convention</span></span>
<span data-ttu-id="3c25a-130">В предыдущем выпуске соглашение об именовании для частичной конфигурации было таким, что имя MOF-файла в опрашивающем сервере или службе должно было соответствовать имени частичной конфигурации, указанному в параметрах локального диспетчера конфигурации, которое, в свою очередь, должно соответствовать имени конфигурации, включенному в MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="3c25a-130">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="3c25a-131">См. моментальные снимки ниже.</span><span class="sxs-lookup"><span data-stu-id="3c25a-131">See the snapshots below:</span></span>

<span data-ttu-id="3c25a-132">•   Параметры локальной конфигурации, определяющие частичную конфигурацию, которую разрешено получать узлу.</span><span class="sxs-lookup"><span data-stu-id="3c25a-132">•   Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

![Пример метаконфигурации](../images/MetaConfigPartialOne.png)

<span data-ttu-id="3c25a-134">•   Пример определения частичной конфигурации</span><span class="sxs-lookup"><span data-stu-id="3c25a-134">•   Sample partial configuration definition</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

<span data-ttu-id="3c25a-135">•   Имя конфигурации (ConfigurationName), включенное в созданный MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="3c25a-135">•   'ConfigurationName' embedded in the generated MOF file.</span></span>

![Пример созданного MOF-файла](../images/PartialGeneratedMof.png)

<span data-ttu-id="3c25a-137">•   Имя файла в репозитории конфигураций</span><span class="sxs-lookup"><span data-stu-id="3c25a-137">•   FileName in the pull configuration repository</span></span>

![Имя файла в репозитории конфигураций](../images/PartialInConfigRepository.png)

<span data-ttu-id="3c25a-139">Служба автоматизации Azure создавала MOF-файлы с именами `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="3c25a-139">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="3c25a-140">Поэтому следующая конфигурация компилируется в файл PartialOne.Localhost.mof.</span><span class="sxs-lookup"><span data-stu-id="3c25a-140">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

<span data-ttu-id="3c25a-141">Это делало невозможным запрос к одной из частичных конфигураций из службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3c25a-141">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

<span data-ttu-id="3c25a-142">В WMF 5.1 частичная конфигурация на опрашивающем сервере или в службе может иметь имя `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="3c25a-142">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="3c25a-143">Кроме того, если компьютер запрашивает одну конфигурацию с опрашивающего сервера или службы, то файл конфигурации в репозитории конфигураций опрашивающего сервера может иметь любое имя.</span><span class="sxs-lookup"><span data-stu-id="3c25a-143">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span>
<span data-ttu-id="3c25a-144">Эта гибкость в именовании позволяет управлять узлами, которые находятся под частичным управлением службы автоматизации Azure. В этом случае часть конфигурации узла поступает из DSC службы автоматизации Azure, а другой частью конфигурации вы управляете локально.</span><span class="sxs-lookup"><span data-stu-id="3c25a-144">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

<span data-ttu-id="3c25a-145">В следующей метаконфигурации узел находится как под локальным управлением, так и под управлением службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3c25a-145">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

```powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30
            RefreshMode = "PULL"
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation service.
        PartialConfiguration PartialConfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
        }

        # This partial configuration is managed locally.
        PartialConfiguration OnPremisesConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
 ```

# <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="3c25a-146">Использование параметра PsDscRunAsCredential с составными ресурсами DSC</span><span class="sxs-lookup"><span data-stu-id="3c25a-146">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="3c25a-147">Добавлена поддержка использования параметра [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) с [составными](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) ресурсами DSC.</span><span class="sxs-lookup"><span data-stu-id="3c25a-147">We have added support for using [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) with DSC [Composite](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="3c25a-148">Теперь можно указать значение параметра PsDscRunAsCredential при использовании составных ресурсов в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3c25a-148">You can now specify a value for PsDscRunAsCredential when using composite resources inside configurations.</span></span>
<span data-ttu-id="3c25a-149">Если значение задано, все ресурсы, включенные в составной ресурс, будут запущены от имени этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3c25a-149">When specified, all resources run inside a composite resource as a RunAs user.</span></span>
<span data-ttu-id="3c25a-150">Если составной ресурс вызывает другой составной ресурс, то все входящие в него ресурсы также будут запущены от имени этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="3c25a-150">If a composite resource calls another composite resource, all of its resources are also executed as RunAs user.</span></span>
<span data-ttu-id="3c25a-151">Учетные данные запуска от имени распространяются на любой уровень иерархии составных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3c25a-151">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span>
<span data-ttu-id="3c25a-152">Если для одного из ресурсов, входящих в составной ресурс, указано собственное значение параметра PsDscRunAsCredential, при компиляции конфигурации появляется ошибка слияния.</span><span class="sxs-lookup"><span data-stu-id="3c25a-152">If any resource inside a composite resource specifies its own value for PsDscRunAsCredential, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="3c25a-153">В этом примере показано, как использовать этот параметр с составным ресурсом [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources), включенным в модуль PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="3c25a-153">This example shows usage with [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) composite resource included in PSDesiredStateConfiguration module.</span></span>



```powershell

Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }

}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData

```

##<a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="3c25a-154">Модуль DSC и проверка подписи конфигурации</span><span class="sxs-lookup"><span data-stu-id="3c25a-154">DSC module and configuration signing validations</span></span>
<span data-ttu-id="3c25a-155">В DSC конфигурации и модули распространяются на управляемые компьютеры с опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="3c25a-155">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span>
<span data-ttu-id="3c25a-156">При компрометации опрашивающего сервера злоумышленник может изменить конфигурации и модули на опрашивающем сервере и распространить их на все управляемые узлы, что также приведет к их компрометации.</span><span class="sxs-lookup"><span data-stu-id="3c25a-156">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes, compromising all of them.</span></span>

 <span data-ttu-id="3c25a-157">В WMF 5.1 DSC поддерживает проверку цифровых подписей файлов каталогов и конфигурации (MOF-файлов).</span><span class="sxs-lookup"><span data-stu-id="3c25a-157">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span>
<span data-ttu-id="3c25a-158">Эта функция предотвращает выполнение на узлах конфигураций или файлов модулей, которые не подписаны доверенным лицом или изменены после подписания доверенным лицом.</span><span class="sxs-lookup"><span data-stu-id="3c25a-158">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>



###<a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="3c25a-159">Подписывание конфигурации и модулей</span><span class="sxs-lookup"><span data-stu-id="3c25a-159">How to sign configuration and module</span></span>
***
* <span data-ttu-id="3c25a-160">Файлы конфигурации (MOF-файлы): поддержка подписывания MOF-файлов была добавлена к функциям существующего командлета PowerShell, [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c25a-160">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) is extended to support signing of MOF files.</span></span>
* <span data-ttu-id="3c25a-161">Модули: для подписывания модулей необходимо подписать каталог соответствующего модуля, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3c25a-161">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
    1. <span data-ttu-id="3c25a-162">Создайте файл каталога: файл каталога содержит коллекцию криптографических хэшей или отпечатков.</span><span class="sxs-lookup"><span data-stu-id="3c25a-162">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span>
       <span data-ttu-id="3c25a-163">Каждый отпечаток соответствует файлу, включенному в модуль.</span><span class="sxs-lookup"><span data-stu-id="3c25a-163">Each thumbprint corresponds to a file that is included in the module.</span></span>
       <span data-ttu-id="3c25a-164">Был добавлен новый командлет [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), благодаря которому пользователи могут создавать файлы каталогов для своих модулей.</span><span class="sxs-lookup"><span data-stu-id="3c25a-164">The new cmdlet [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), has been added to enable users to create a catalog file for their module.</span></span>
    2. <span data-ttu-id="3c25a-165">Подпишите файл каталога: подпишите файл каталога с помощью командлета [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c25a-165">Sign the catalog file: Use [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) to sign the catalog file.</span></span>
    3. <span data-ttu-id="3c25a-166">Поместите файл каталога в папку модуля.</span><span class="sxs-lookup"><span data-stu-id="3c25a-166">Place the catalog file inside the module folder.</span></span>
<span data-ttu-id="3c25a-167">По соглашению файл каталога модуля должен находиться в папке модуля и имя файла каталога модуля должно совпадать с именем модуля.</span><span class="sxs-lookup"><span data-stu-id="3c25a-167">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

###<a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="3c25a-168">Параметры локального диспетчера конфигураций для включения проверки подписи</span><span class="sxs-lookup"><span data-stu-id="3c25a-168">LocalConfigurationManager settings to enable signing validations</span></span>

####<a name="pull"></a><span data-ttu-id="3c25a-169">По запросу</span><span class="sxs-lookup"><span data-stu-id="3c25a-169">Pull</span></span>
<span data-ttu-id="3c25a-170">Локальный диспетчер конфигураций узла выполняет проверку подписи модулей и конфигураций в соответствии со своими текущими параметрами.</span><span class="sxs-lookup"><span data-stu-id="3c25a-170">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span>
<span data-ttu-id="3c25a-171">По умолчанию проверка подписи отключена.</span><span class="sxs-lookup"><span data-stu-id="3c25a-171">By default, signature validation is disabled.</span></span>
<span data-ttu-id="3c25a-172">Проверку подписи можно включить, добавив блок "SignatureValidation" в определение метаконфигурации узла, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3c25a-172">Signature validation can enabled by adding the ‘SignatureValidation’ block to the meta-configuration definition of the node as shown below:</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # By default, LCM uses the default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM uses this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
 ```

<span data-ttu-id="3c25a-173">Установка приведенной выше метаконфигурации для узла включает проверку подписи для загруженных конфигураций и модулей.</span><span class="sxs-lookup"><span data-stu-id="3c25a-173">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span>
<span data-ttu-id="3c25a-174">Для проверки цифровых подписей локальный диспетчер конфигураций выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3c25a-174">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="3c25a-175">Проверьте подпись в файле конфигурации (MOF-файл).</span><span class="sxs-lookup"><span data-stu-id="3c25a-175">Verify the signature on a configuration file (.MOF) is valid.</span></span>
   <span data-ttu-id="3c25a-176">Для проверки подписи диспетчер использует командлет PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), в котором в версии 5.1 была добавлена поддержка проверки подписи MOF.</span><span class="sxs-lookup"><span data-stu-id="3c25a-176">It uses the PowerShell cmdlet [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), which is extended in 5.1 to support MOF signature validation.</span></span>
2. <span data-ttu-id="3c25a-177">Убедитесь, что центр сертификации, который авторизовал подписывающую сторону, является доверенным.</span><span class="sxs-lookup"><span data-stu-id="3c25a-177">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="3c25a-178">Скачайте зависимости модуля или ресурса конфигурации во временный каталог.</span><span class="sxs-lookup"><span data-stu-id="3c25a-178">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="3c25a-179">Проверьте подпись каталога, включенного в модуль.</span><span class="sxs-lookup"><span data-stu-id="3c25a-179">Verify the signature of the catalog included inside the module.</span></span>
    * <span data-ttu-id="3c25a-180">Найдите файл `<moduleName>.cat` и проверьте его подпись командлетом [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c25a-180">Find a `<moduleName>.cat` file and verify its signature using the cmdlet  [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span></span>
    * <span data-ttu-id="3c25a-181">Проверьте центр сертификации, который проверил подлинность доверенного лица.</span><span class="sxs-lookup"><span data-stu-id="3c25a-181">Verify the certification authority that authenticated the signer is trusted.</span></span>
    * <span data-ttu-id="3c25a-182">Проверьте, чтобы содержимое модулей не было изменено, с помощью нового командлета, [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c25a-182">Verify the content of the modules has not been tampered using the new cmdlet [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span></span>
5. <span data-ttu-id="3c25a-183">Установите модуль (Install-Module) в папку "$env:ProgramFiles\WindowsPowerShell\Modules\".</span><span class="sxs-lookup"><span data-stu-id="3c25a-183">Install-Module to $env:ProgramFiles\WindowsPowerShell\Modules\\</span></span>
6. <span data-ttu-id="3c25a-184">Выполните конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="3c25a-184">Process configuration</span></span>

> <span data-ttu-id="3c25a-185">Примечание. Проверка подписи каталога модуля и конфигурации выполняется только при первом применении конфигурации к системе или при скачивании и установке модуля.</span><span class="sxs-lookup"><span data-stu-id="3c25a-185">Note: Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
<span data-ttu-id="3c25a-186">При проверке на согласованность не проверяется подпись файла Current.mof и зависимости для его модулей.</span><span class="sxs-lookup"><span data-stu-id="3c25a-186">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span>
<span data-ttu-id="3c25a-187">Если проверка на любом этапе завершается неудачно, например если конфигурация, полученная с опрашивающего сервера, не подписана, обработка конфигурации завершается ошибкой, показанной ниже, и все временные файлы удаляются.</span><span class="sxs-lookup"><span data-stu-id="3c25a-187">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Пример ошибки конфигурации](../images/PullUnsignedConfigFail.png)

<span data-ttu-id="3c25a-189">Точно так же при попытке получить модуль, каталог для которого не подписан, появляется следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="3c25a-189">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![Пример ошибки модуля](../images/PullUnisgnedCatalog.png)

####<a name="push"></a><span data-ttu-id="3c25a-191">Принудительная отправка</span><span class="sxs-lookup"><span data-stu-id="3c25a-191">Push</span></span>
<span data-ttu-id="3c25a-192">Конфигурация, переданная на узел с помощью принудительной отправки, может быть изменена злоумышленником в месте ее отправки.</span><span class="sxs-lookup"><span data-stu-id="3c25a-192">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span>
<span data-ttu-id="3c25a-193">Локальный диспетчер конфигураций выполняет похожие действия для проверки подписи принудительно отправленных и опубликованных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="3c25a-193">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span>
<span data-ttu-id="3c25a-194">Ниже приведен полный пример проверки подписи для принудительной отправки.</span><span class="sxs-lookup"><span data-stu-id="3c25a-194">Below is a complete example of signature validation for push.</span></span>

* <span data-ttu-id="3c25a-195">Включите проверку подписи на узле.</span><span class="sxs-lookup"><span data-stu-id="3c25a-195">Enable signature validation on the node.</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'
    }
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType =  'Configuration','Module'
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```
* <span data-ttu-id="3c25a-196">Создайте пример файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3c25a-196">Create a sample configuration file.</span></span>

```powershell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* <span data-ttu-id="3c25a-197">Попробуйте принудительно отправить не подписанный файл конфигурации на узел.</span><span class="sxs-lookup"><span data-stu-id="3c25a-197">Try pushing the unsigned configuration file in to the node.</span></span>

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```
![Ошибка "MOF-файл не подписан"](../images/PushUnsignedMof.png)

* <span data-ttu-id="3c25a-199">Подпишите файл конфигурации с помощью сертификата подписи кода.</span><span class="sxs-lookup"><span data-stu-id="3c25a-199">Sign the configuration file using code-signing certificate.</span></span>

![Подписанный MOF-файл](../images/SignMofFile.png)

* <span data-ttu-id="3c25a-201">Попробуйте отправить подписанный MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="3c25a-201">Try pushing the signed MOF file.</span></span>

![Подписанный MOF-файл](../images/PushSignedMof.png)