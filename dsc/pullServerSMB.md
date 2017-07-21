---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка опрашивающего SMB-сервера DSC"
ms.openlocfilehash: 5efd8a822e4420484391f7a5a9832d5d51883e8d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-dsc-smb-pull-server"></a><span data-ttu-id="13ed4-103">Настройка опрашивающего SMB-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="13ed4-103">Setting up a DSC SMB pull server</span></span>

><span data-ttu-id="13ed4-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="13ed4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="13ed4-105">Опрашивающий [SMB-сервер](https://technet.microsoft.com/en-us/library/hh831795.aspx) DSC — это, компьютер, размещающий файловый ресурс SMB, который делает конфигурации DSC или ресурсы DSC доступными для целевых узлов, когда эти узлы запрашивают их.</span><span class="sxs-lookup"><span data-stu-id="13ed4-105">A DSC [SMB](https://technet.microsoft.com/en-us/library/hh831795.aspx) pull server is a computer hosting SMB file shares that make DSC configuration files and DSC resources available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="13ed4-106">Для использования опрашивающего SMB-сервера DSC необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="13ed4-106">To use an SMB pull server for DSC, you have to:</span></span>
- <span data-ttu-id="13ed4-107">Настроить файловый SMB-ресурс на сервере, с PowerShell 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="13ed4-107">Set up an SMB file share on a server running PowerShell 4.0 or higher</span></span>
- <span data-ttu-id="13ed4-108">Настроить клиент с PowerShell 4.0 или более поздней версии для получения данных с этого файлового SMB-ресурса.</span><span class="sxs-lookup"><span data-stu-id="13ed4-108">Configure a client running PowerShell 4.0 or higher to pull from that SMB share</span></span>

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a><span data-ttu-id="13ed4-109">Использование ресурса xSmbShare для создания файлового SMB-ресурса</span><span class="sxs-lookup"><span data-stu-id="13ed4-109">Using the xSmbShare resource to create an SMB file share</span></span>

<span data-ttu-id="13ed4-110">Существует несколько способов настройки файлового SMB-ресурса. Давайте рассмотрим, как это можно сделать с помощью DSC.</span><span class="sxs-lookup"><span data-stu-id="13ed4-110">There are a number of ways to set up an SMB file share, but let's look at how you can do this by using DSC.</span></span>

### <a name="install-the-xsmbshare-resource"></a><span data-ttu-id="13ed4-111">Установка ресурса xSmbShare</span><span class="sxs-lookup"><span data-stu-id="13ed4-111">Install the xSmbShare resource</span></span>

<span data-ttu-id="13ed4-112">Для установки модуля **xSmbShare** используйте командлет [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx).</span><span class="sxs-lookup"><span data-stu-id="13ed4-112">Call the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xSmbShare** module.</span></span>
><span data-ttu-id="13ed4-113">**Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="13ed4-113">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="13ed4-114">Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="13ed4-114">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> <span data-ttu-id="13ed4-115">**xSmbShare** содержит ресурс DSC **xSmbShare**, с помощью которого можно создать файловый ресурс SMB.</span><span class="sxs-lookup"><span data-stu-id="13ed4-115">The **xSmbShare** contains the DSC resource **xSmbShare**, which can be used to create an SMB file share.</span></span>

### <a name="create-the-directory-and-file-share"></a><span data-ttu-id="13ed4-116">Создание файлового ресурса и каталога</span><span class="sxs-lookup"><span data-stu-id="13ed4-116">Create the directory and file share</span></span>

<span data-ttu-id="13ed4-117">В следующей конфигурации ресурс [File](fileResource.md) используется для создания каталога для ресурса, а ресурс **xSmbShare** — для настройки ресурса SMB:</span><span class="sxs-lookup"><span data-stu-id="13ed4-117">The following configuration uses the [File](fileResource.md) resource to create the directory for the share and the **xSmbShare** resource to set up the SMB share:</span></span>

```powershell
Configuration SmbShare {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'C:\DscSmbShare'
            FullAccess = 'admininstrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }
        
    }
 
}
```

<span data-ttu-id="13ed4-118">Конфигурация создает каталог `C:\DscSmbShare`, если его еще не существует, и затем использует этот каталог в качестве файлового SMB-ресурса.</span><span class="sxs-lookup"><span data-stu-id="13ed4-118">The configuration creates the directory `C:\DscSmbShare` if it doesn't already exists, and then uses that directory as an SMB file share.</span></span> <span data-ttu-id="13ed4-119">Разрешение **FullAccess** необходимо предоставить всем учетным записям, которым нужно записывать или удалять данные из файлового ресурса, а разрешение **ReadAccess** — всем узлам клиента, которые получают конфигурации и (или) ресурсы DSC из общего ресурса. Это связано с тем, что DSC по умолчанию выполняется с системной учетной записью, чтобы у самого компьютера был доступ к общему ресурсу.</span><span class="sxs-lookup"><span data-stu-id="13ed4-119">**FullAccess** should be given to any account that needs to write to or delete from the file share, and **ReadAccess** must be given to any client nodes that get configurations and/or DSC resources from the share ( this is because DSC runs as the system account by default, so the computer itself has to have access to the share).</span></span>


### <a name="give-file-system-access-to-the-pull-client"></a><span data-ttu-id="13ed4-120">Предоставление файловой системе доступа к опрашивающему клиенту</span><span class="sxs-lookup"><span data-stu-id="13ed4-120">Give file system access to the pull client</span></span>

<span data-ttu-id="13ed4-121">Предоставление разрешения **ReadAccess** клиенту узла позволяет этому узлу обращаться к ресурсу SMB, но не к файлам или папкам в этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="13ed4-121">Giving **ReadAccess** to a client node allows that node to access the SMB share, but not to files or folders within that share.</span></span> <span data-ttu-id="13ed4-122">Следует явно предоставить узлам клиента доступ к папке и вложенным папкам ресурса SMB.</span><span class="sxs-lookup"><span data-stu-id="13ed4-122">You have to explicitly grant client nodes access to the SMB share folder and sub-folders.</span></span> <span data-ttu-id="13ed4-123">Сделать это можно с помощью DSC, используя ресурс **cNtfsPermissionEntry**, который содержится в модуле [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0).</span><span class="sxs-lookup"><span data-stu-id="13ed4-123">We can do this with DSC by adding using the **cNtfsPermissionEntry** resource, which is contained in the [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) module.</span></span> <span data-ttu-id="13ed4-124">Следующая конфигурация добавляет блок **cNtfsPermissionEntry**, который предоставляет разрешение ReadAndExecute опрашивающему клиенту.</span><span class="sxs-lookup"><span data-stu-id="13ed4-124">The following configuration adds a **cNtfsPermissionEntry** block that grants ReadAndExecute access to the pull client:</span></span>

```powershell
Configuration DSCSMB {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
Import-DscResource -ModuleName cNtfsAccessControl
 
    Node localhost {
 
        File CreateFolder {
 
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
 
        }
 
        xSMBShare CreateShare {
 
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
 
        }

        cNtfsPermissionEntry PermissionSet1 {
            
        Ensure = 'Present'
        Path = 'C:\DSCSMB'
        Principal = 'myDomain\Contoso-Server$'
        AccessControlInformation = @(
            cNtfsAccessControlInformation
            {
                AccessControlType = 'Allow'
                FileSystemRights = 'ReadAndExecute'
                Inheritance = 'ThisFolderSubfoldersAndFiles'
                NoPropagateInherit = $false
            }
        )
        DependsOn = '[File]CreateFolder'
        
        }
 
        
    }
 
}
```

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="13ed4-125">Размещение конфигураций и ресурсов</span><span class="sxs-lookup"><span data-stu-id="13ed4-125">Placing configurations and resources</span></span>

<span data-ttu-id="13ed4-126">Сохраните все MOF-файлы конфигурации и ресурсы DSC, к которым должны обращаться клиентские узлы, в общей папке SMB.</span><span class="sxs-lookup"><span data-stu-id="13ed4-126">Save any configuration MOF files and/or DSC resources that you want client nodes to pull in the SMB share folder.</span></span>

<span data-ttu-id="13ed4-127">Все MOF-файлы конфигурации должны иметь имена вида _ConfigurationID_.mof, где _ConfigurationID_ — значение свойства **ConfigurationID** LCM целевого узла.</span><span class="sxs-lookup"><span data-stu-id="13ed4-127">Any configuration MOF file must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="13ed4-128">Дополнительные сведения о настройке опрашивающих клиентов см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="13ed4-128">For more information about setting up pull clients, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="13ed4-129">**Примечание**. При использовании опрашивающего SMB-сервера необходимо использовать идентификаторы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13ed4-129">**Note:** You must use configuration IDs if you are using an SMB pull server.</span></span> <span data-ttu-id="13ed4-130">Имена конфигураций не поддерживаются SMB.</span><span class="sxs-lookup"><span data-stu-id="13ed4-130">Configuration names are not supported for SMB.</span></span>

<span data-ttu-id="13ed4-131">Каждый модуль ресурса необходимо упаковать в ZIP-архив и переименовать по шаблону `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="13ed4-131">Each resource module needs to be zipped and named according the the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="13ed4-132">Например, модуль с именем xWebAdminstration с версией модуля 3.1.2.0 будет иметь имя "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="13ed4-132">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="13ed4-133">Каждая версия модуля должна находиться в собственном ZIP-файле.</span><span class="sxs-lookup"><span data-stu-id="13ed4-133">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="13ed4-134">Поскольку в каждом ZIP-файле существует только одна версия ресурса, формат модулей с поддержкой нескольких версий модуля в одном каталоге, который появился в WMF 5.0, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="13ed4-134">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="13ed4-135">Это означает, что перед упаковкой модулей ресурсов DSC для опрашивающего сервера необходимо внести небольшое изменение в структуру каталогов.</span><span class="sxs-lookup"><span data-stu-id="13ed4-135">This means that before packaging up DSC resource modules for use with pull server you need to make a small change to the directory structure.</span></span> <span data-ttu-id="13ed4-136">Формат модулей, содержащих ресурсы DSC, в WMF 5.0 по умолчанию таков: "{папка_модуля}\{{версия_модуля}\DscResources\{{папка_ресурса_DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="13ed4-136">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="13ed4-137">Перед упаковкой для опрашивающего сервера просто удалите папку **{версия_модуля}**, чтобы путь стал таким: "{папка_модуля}\DscResources\{{папка_ресурса_DSC}\'.</span><span class="sxs-lookup"><span data-stu-id="13ed4-137">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="13ed4-138">Выполнив это изменение, упакуйте папку в ZIP-архив, как описано выше, и поместите ZIP-архивы в папку общего ресурса SMB.</span><span class="sxs-lookup"><span data-stu-id="13ed4-138">With this change, zip the folder as described above and place these zip files in the SMB share folder.</span></span> 

## <a name="creating-the-mof-checksum"></a><span data-ttu-id="13ed4-139">Создание контрольной суммы MOF</span><span class="sxs-lookup"><span data-stu-id="13ed4-139">Creating the MOF checksum</span></span>
<span data-ttu-id="13ed4-140">MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="13ed4-140">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span> <span data-ttu-id="13ed4-141">Чтобы создать контрольную сумму, вызовите командлет [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx).</span><span class="sxs-lookup"><span data-stu-id="13ed4-141">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span> <span data-ttu-id="13ed4-142">Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13ed4-142">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="13ed4-143">Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13ed4-143">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span> <span data-ttu-id="13ed4-144">Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.</span><span class="sxs-lookup"><span data-stu-id="13ed4-144">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>

<span data-ttu-id="13ed4-145">Файл контрольной суммы должен находиться в том же каталоге, что и MOF-файл конфигурации (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` по умолчанию), и иметь то же имя, что и у добавленного расширения `.checksum`.</span><span class="sxs-lookup"><span data-stu-id="13ed4-145">The checksum file must be present in the same directory as the configuration MOF file (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` by default), and have the same name with the `.checksum` extension appended.</span></span>

><span data-ttu-id="13ed4-146">**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.</span><span class="sxs-lookup"><span data-stu-id="13ed4-146">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="setting-up-a-pull-client-for-smb"></a><span data-ttu-id="13ed4-147">Настройка опрашивающего клиента для SMB</span><span class="sxs-lookup"><span data-stu-id="13ed4-147">Setting up a pull client for SMB</span></span>

<span data-ttu-id="13ed4-148">Чтобы определить клиент, запрашивающий конфигурации и (или) ресурсы из общей папки SMB, настройте для локального диспетчера конфигураций (LCM) клиента блоки **ConfigurationRepositoryShare** и **ResourceRepositoryShare**, указывающие общую папку для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="13ed4-148">To set up a client that pulls configurations and/or resources from an SMB share, you configure the client's Local Configuration Manager (LCM) with **ConfigurationRepositoryShare** and **ResourceRepositoryShare** blocks that specify the share from which to pull configurations and DSC resources.</span></span>

<span data-ttu-id="13ed4-149">Дополнительные сведения о настройке LCM см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="13ed4-149">For more information about configuring the LCM, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="13ed4-150">**Примечание.** Для простоты в этом примере используется **PSDscAllowPlainTextPassword**, чтобы разрешить передачу пароля в формате открытого текста в параметр **Credential**.</span><span class="sxs-lookup"><span data-stu-id="13ed4-150">**Note:** For simplicity, this example uses the **PSDscAllowPlainTextPassword** to allow passing a plaintext password to the **Credential** parameter.</span></span> <span data-ttu-id="13ed4-151">Сведения о более безопасной передачи учетных данных см. в разделе [Параметры учетных данных в данных конфигурации](configDataCredentials.md).</span><span class="sxs-lookup"><span data-stu-id="13ed4-151">For information about passing credentials more securely, see [Credentials Options in Configuration Data](configDataCredentials.md).</span></span>

><span data-ttu-id="13ed4-152">**Примечание.** Следует указать **ConfigurationID** в блоке **Settings** метаконфигурации опрашивающего сервера SMB, даже если вы просто извлекаете ресурсы.</span><span class="sxs-lookup"><span data-stu-id="13ed4-152">**Note:** You must specify a **ConfigurationID** in the **Settings** block of a metaconfiguration for an SMB pull server, even if you are only pulling resources.</span></span>

```powershell
$secpasswd = ConvertTo-SecureString “Pass1Word” -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential (“TestUser”, $secpasswd)

[DSCLocalConfigurationManager()]
configuration SmbCredTest
{
    Node $AllNodes.NodeName
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
            ConfigurationID    = '16db7357-9083-4806-a80c-ebbaf4acd6c1'
        }
         
         ConfigurationRepositoryShare SmbConfigShare      
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
        }

        ResourceRepositoryShare SmbResourceShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
            
        }      
    }
}

$ConfigurationData = @{

    AllNodes = @(

        @{

            #the "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves

            NodeName="localhost"

            PSDscAllowPlainTextPassword = $true

        })

        

}
```

## <a name="acknowledgements"></a><span data-ttu-id="13ed4-153">Благодарности</span><span class="sxs-lookup"><span data-stu-id="13ed4-153">Acknowledgements</span></span>

<span data-ttu-id="13ed4-154">Выражаю особую благодарность:</span><span class="sxs-lookup"><span data-stu-id="13ed4-154">Special thanks to the following:</span></span>

- <span data-ttu-id="13ed4-155">Майку Ф. Роббинсу, чьи записи об использовании SMB для DSC помогли в составлении этой статьи.</span><span class="sxs-lookup"><span data-stu-id="13ed4-155">Mike F. Robbins, whose posts on using SMB for DSC helped inform the content in this topic.</span></span> <span data-ttu-id="13ed4-156">Ссылка на его блог — [Майк Ф. Роббинс](http://mikefrobbins.com/).</span><span class="sxs-lookup"><span data-stu-id="13ed4-156">His blog is at [Mike F Robbins](http://mikefrobbins.com/).</span></span>
- <span data-ttu-id="13ed4-157">Сергею Николайчуку, который создал модуль **cNtfsAccessControl**.</span><span class="sxs-lookup"><span data-stu-id="13ed4-157">Serge Nikalaichyk, who authored the **cNtfsAccessControl** module.</span></span> <span data-ttu-id="13ed4-158">Исходный код этого модуля доступен по ссылке https://github.com/SNikalaichyk/cNtfsAccessControl.</span><span class="sxs-lookup"><span data-stu-id="13ed4-158">The source for this module is at https://github.com/SNikalaichyk/cNtfsAccessControl.</span></span>

## <a name="see-also"></a><span data-ttu-id="13ed4-159">См. также:</span><span class="sxs-lookup"><span data-stu-id="13ed4-159">See also</span></span>
- [<span data-ttu-id="13ed4-160">Общие сведения о службе настройки требуемого состояния Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="13ed4-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="13ed4-161">Активированные конфигурации</span><span class="sxs-lookup"><span data-stu-id="13ed4-161">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="13ed4-162">Настройка опрашивающего клиента с помощью идентификатора конфигурации</span><span class="sxs-lookup"><span data-stu-id="13ed4-162">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

 
