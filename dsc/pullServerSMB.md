---
title: "Настройка опрашивающего SMB-сервера DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: f16af7664ac5d07b5884070534bed20e8cf2fcd9
ms.sourcegitcommit: 6057e6d22ef8a2095af610e0d681e751366a9773
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2017
---
# <a name="setting-up-a-dsc-smb-pull-server"></a>Настройка опрашивающего SMB-сервера DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Опрашивающий [SMB-сервер](https://technet.microsoft.com/en-us/library/hh831795.aspx) DSC — это, компьютер, размещающий файловый ресурс SMB, который делает конфигурации DSC или ресурсы DSC доступными для целевых узлов, когда эти узлы запрашивают их.

Для использования опрашивающего SMB-сервера DSC необходимо выполнить следующее:
- Настроить файловый SMB-ресурс на сервере, с PowerShell 4.0 или более поздней версии.
- Настроить клиент с PowerShell 4.0 или более поздней версии для получения данных с этого файлового SMB-ресурса.

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a>Использование ресурса xSmbShare для создания файлового SMB-ресурса

Существует несколько способов настройки файлового SMB-ресурса. Давайте рассмотрим, как это можно сделать с помощью DSC.

### <a name="install-the-xsmbshare-resource"></a>Установка ресурса xSmbShare

Для установки модуля **xSmbShare** используйте командлет [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx).
>**Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186). **xSmbShare** содержит ресурс DSC **xSmbShare**, с помощью которого можно создать файловый ресурс SMB.

### <a name="create-the-directory-and-file-share"></a>Создание файлового ресурса и каталога

В следующей конфигурации ресурс [File](fileResource.md) используется для создания каталога для ресурса, а ресурс **xSmbShare** — для настройки ресурса SMB:

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

Конфигурация создает каталог `C:\DscSmbShare`, если его еще не существует, и затем использует этот каталог в качестве файлового SMB-ресурса. Разрешение **FullAccess** необходимо предоставить всем учетным записям, которым нужно записывать или удалять данные из файлового ресурса, а разрешение **ReadAccess** — всем узлам клиента, которые получают конфигурации и (или) ресурсы DSC из общего ресурса. Это связано с тем, что DSC по умолчанию выполняется с системной учетной записью, чтобы у самого компьютера был доступ к общему ресурсу.


### <a name="give-file-system-access-to-the-pull-client"></a>Предоставление файловой системе доступа к опрашивающему клиенту

Предоставление разрешения **ReadAccess** клиенту узла позволяет этому узлу обращаться к ресурсу SMB, но не к файлам или папкам в этом ресурсе. Следует явно предоставить узлам клиента доступ к папке и вложенным папкам ресурса SMB. Сделать это можно с помощью DSC, используя ресурс **cNtfsPermissionEntry**, который содержится в модуле [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0). Следующая конфигурация добавляет блок **cNtfsPermissionEntry**, который предоставляет разрешение ReadAndExecute опрашивающему клиенту.

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

## <a name="placing-configurations-and-resources"></a>Размещение конфигураций и ресурсов

Сохраните все MOF-файлы конфигурации и ресурсы DSC, к которым должны обращаться клиентские узлы, в общей папке SMB.

Все MOF-файлы конфигурации должны иметь имена вида _ConfigurationID_.mof, где _ConfigurationID_ — значение свойства **ConfigurationID** LCM целевого узла. Дополнительные сведения о настройке опрашивающих клиентов см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).

>**Примечание**. При использовании опрашивающего SMB-сервера необходимо использовать идентификаторы конфигурации. Имена конфигураций не поддерживаются SMB.

Каждый модуль ресурса необходимо упаковать в ZIP-архив и переименовать по шаблону `{Module Name}_{Module Version}.zip`. Например, модуль с именем xWebAdminstration с версией модуля 3.1.2.0 будет иметь имя "xWebAdministration_3.2.1.0.zip". Каждая версия модуля должна находиться в собственном ZIP-файле. Поскольку в каждом ZIP-файле существует только одна версия ресурса, формат модулей с поддержкой нескольких версий модуля в одном каталоге, который появился в WMF 5.0, не поддерживается. Это означает, что перед упаковкой модулей ресурсов DSC для опрашивающего сервера необходимо внести небольшое изменение в структуру каталогов. Формат модулей, содержащих ресурсы DSC, в WMF 5.0 по умолчанию таков: "{папка_модуля}\{{версия_модуля}\DscResources\{{папка_ресурса_DSC}\'. Перед упаковкой для опрашивающего сервера просто удалите папку **{версия_модуля}**, чтобы путь стал таким: "{папка_модуля}\DscResources\{{папка_ресурса_DSC}\'. Выполнив это изменение, упакуйте папку в ZIP-архив, как описано выше, и поместите ZIP-архивы в папку общего ресурса SMB. 

## <a name="creating-the-mof-checksum"></a>Создание контрольной суммы MOF
MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. Чтобы создать контрольную сумму, вызовите командлет [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx). Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.

Файл контрольной суммы должен находиться в том же каталоге, что и MOF-файл конфигурации (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` по умолчанию), и иметь то же имя, что и у добавленного расширения `.checksum`.

>**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

## <a name="setting-up-a-pull-client-for-smb"></a>Настройка опрашивающего клиента для SMB

Чтобы определить клиент, запрашивающий конфигурации и (или) ресурсы из общей папки SMB, настройте для локального диспетчера конфигураций (LCM) клиента блоки **ConfigurationRepositoryShare** и **ResourceRepositoryShare**, указывающие общую папку для извлечения данных.

Дополнительные сведения о настройке LCM см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).

>**Примечание.** Для простоты в этом примере используется **PSDscAllowPlainTextPassword**, чтобы разрешить передачу пароля в формате открытого текста в параметр **Credential**. Сведения о более безопасной передачи учетных данных см. в разделе [Параметры учетных данных в данных конфигурации](configDataCredentials.md).

>**Примечание.** Следует указать **ConfigurationID** в блоке **Settings** метаконфигурации опрашивающего сервера SMB, даже если вы просто извлекаете ресурсы.

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

## <a name="acknowledgements"></a>Благодарности

Выражаю особую благодарность:

- Майку Ф. Роббинсу, чьи записи об использовании SMB для DSC помогли в составлении этой статьи. Ссылка на его блог — [Майк Ф. Роббинс](http://mikefrobbins.com/).
- Сергею Николайчуку, который создал модуль **cNtfsAccessControl**. Исходный код этого модуля доступен по ссылке https://github.com/SNikalaichyk/cNtfsAccessControl.

## <a name="see-also"></a>См. также:
- [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
- [Активированные конфигурации](enactingConfigurations.md)
- [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md)

 
