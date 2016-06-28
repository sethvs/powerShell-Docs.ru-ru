---
title: "Настройка опрашивающего SMB-сервера DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 6477ae8575c83fc24150f9502515ff5b82bc8198
ms.openlocfilehash: 35ac9b38086b12fb48844c56a488854f63529e21

---

# Настройка опрашивающего SMB-сервера DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Опрашивающий [SMB-сервер](https://technet.microsoft.com/en-us/library/hh831795.aspx) DSC представляет собой файловый ресурс SMB, который делает конфигурации DSC или ресурсы DSC доступными для целевых узлов, когда эти узлы запрашивают их.

Для использования опрашивающего SMB-сервера DSC необходимо выполнить следующее:
- Настроить файловый SMB-ресурс на сервере, с PowerShell 4.0 или более поздней версии.
- Настроить клиент с PowerShell 4.0 или более поздней версии для получения данных с этого файлового SMB-ресурса.

## Использование ресурса xSmbShare для создания файлового SMB-ресурса

Существует несколько способов настройки файлового SMB-ресурса. Давайте рассмотрим, как это можно сделать с помощью DSC.

### Установка ресурса xSmbShare

Для установки модуля **xSmbShare** используйте командлет [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx).
>**Примечание**. **Install-Module** включен в модуль **PowerShellGet**, содержащийся в PowerShell 5.0. Вы можете скачать модуль **PowerShellGet**для PowerShell 3.0 и 4.0 в разделе [Предварительная версия модулей PackageManagement PowerShell](https://www.microsoft.com/en-us/download/details.aspx?id=49186). **xSmbShare** содержит ресурс DSC **xSmbShare**, с помощью которого можно создать файловый ресурс SMB.

### Создание файлового ресурса и каталога

В следующей конфигурации ресурс [File](fileResource.md) используется для создания каталога для ресурса, а ресурс **xSmbShare** — для настройки ресурса SMB.

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

Конфигурация создает каталог `C:\DscSmbShare`, если его еще не существует, и затем использует этот каталог в качестве файлового SMB-ресурса. Разрешение **FullAccess** необходимо предоставить всем учетным записям, которым нужно записывать или удалять данные из файлового ресурса, а разрешение **ReadAccess** — всем узлам клиента, которые получат конфигурации и (или) ресурсы DSC из общего ресурса (это вызвано тем, что DSC по умолчанию выполняется с системной учетной записью, чтобы у самого компьютера был доступ к общему ресурсу).


### Предоставление файловой системе доступа к опрашивающему клиенту

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

## Размещение конфигураций и ресурсов

Сохраните все MOF-файлы конфигурации и ресурсы DSC, к которым должны обращаться клиентские узлы, в общей папке SMB.

Все MOF-файлы конфигурации должны иметь имена вида _ConfigurationID_.mof, где _ConfigurationID_ — значение свойства **ConfigurationID** LCM целевого узла. Дополнительные сведения о настройке опрашивающих клиентов см. в разделе [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md).

>**Примечание**. При использовании опрашивающего SMB-сервера необходимо использовать идентификаторы конфигурации. Имена конфигураций не поддерживаются SMB.

Все нужные клиенту ресурсы необходимо поместить в папку SMB-ресурса в виде архивов `.zip`.  

## Создание контрольной суммы MOF
MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. Чтобы создать контрольную сумму, вызовите командлет [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx). Командлет принимает параметр **Path**, указывающий папку, в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.

Файл контрольной суммы должен находиться в том же каталоге, что и MOF-файл конфигурации (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` по умолчанию), и иметь то же имя, что и у добавленного расширения `.checksum`.

>**Примечание**. Если вы измените MOF-файл конфигурации каким-либо образом, потребуется повторно создать файл контрольной суммы.

## Благодарности

Выражаю особую благодарность:

- Майку Ф. Роббинсу, чьи записи об использовании SMB для DSC помогли в составлении этой статьи. Ссылка на его блог — [Майк Ф. Роббинс](http://mikefrobbins.com/).
- Сергею Николайчуку, который создал модуль **cNtfsAccessControl**. Исходный код этого модуля доступен по ссылке https://github.com/SNikalaichyk/cNtfsAccessControl.

## См. также:
- [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
- [Применение конфигураций](enactingConfigurations.md)
- [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md)

 



<!--HONumber=Jun16_HO4-->


