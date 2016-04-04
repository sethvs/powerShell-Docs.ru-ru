# Настройка опрашивающего SMB-сервера DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Опрашивающий SMB-сервер DSC представляет собой файловый SMB-ресурс, который делает конфигурации DSC или ресурсы DSC
доступными для целевых узлов, когда эти узлы запрашивают их.

Для использования опрашивающего SMB-сервера DSC необходимо выполнить следующее:
- Настроить файловый SMB-ресурс на сервере, с PowerShell 4.0 или более поздней версии.
- Настроить клиент с PowerShell 4.0 или более поздней версии для получения данных с этого файлового SMB-ресурса.

## Использование ресурса xSmbShare для создания файлового SMB-ресурса

Существует несколько способов настройки файлового SMB-ресурса. Давайте рассмотрим, как это можно сделать с помощью DSC.

### Установка ресурса xSmbShare

Для установки модуля xSmbShare используйте командлет Install-Module.
>Примечание. Install-Module включен в модуль PowerShellGet, который входит в состав PowerShell 5.0. Модуль PowerShellGet для PowerShell 3.0 и 4.0 можно скачать
>в разделе Предварительная версия модулей PackageManagement PowerShell. XSmbShare содержит ресурс DSC xSmbShare, с помощью которого можно
создать файловый SMB-ресурс.

### Создание файлового ресурса и каталога

В следующей конфигурации ресурс File используется для создания каталога для ресурса, а ресурс xSmbShare — для настройки SMB-ресурса:

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

Конфигурация создает каталог `C:\DscSmbShare`, если его еще не существует, и затем использует этот каталог в качестве файлового SMB-ресурса. Разрешение FullAccess необходимо предоставить всем
учетным записям, которым нужно записывать или удалять данные из файлового ресурса, а разрешение ReadAccess — всем узлам клиента, которые получат конфигурации или ресурсы DSC из общего ресурса 
(это вызвано тем, что DSC по умолчанию выполняется с системной учетной записью, чтобы у самого компьютера был доступ к общему ресурсу).


### Предоставление файловой системе доступа к опрашивающему клиенту

Предоставление разрешения ReadAccess клиенту узла позволяет этому узлу обращаться к SMB-ресурсу, но не к файлам или папкам в этом ресурсе. Следует явно предоставить узлам клиента доступ к папке и вложенным папкам
SMB-ресурса. Сделать это можно с помощью DSC, используя ресурс cNtfsPermissionEntry, который содержится в модуле CNtfsAccessControl.
  Следующая конфигурация добавляет блок cNtfsPermissionEntry, который предоставляет разрешение ReadAndExecute опрашивающему клиенту:

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

Все MOF-файлы конфигурации должны иметь имена вида ConfigurationID.mof, где ConfigurationID — значение свойства ConfigurationID LCM целевого узла. Дополнительные сведения
о настройке опрашивающих клиентов см. в разделе Настройка опрашивающего клиента с помощью идентификатора конфигурации.

>Примечание. При использовании опрашивающего SMB-сервера необходимо использовать идентификаторы конфигурации. Имена конфигураций не поддерживаются SMB.

Все нужные клиенту ресурсы необходимо поместить в папку SMB-ресурса в виде архивов `.zip`.  

## Создание контрольной суммы MOF
MOF-файл конфигурации необходимо сопоставить с файлом контрольной суммы, чтобы LCM на целевом узле мог проверить конфигурацию. 
Для вычисления контрольной суммы вызовите командлет New-DSCCheckSum. Командлет принимает параметр Path, указывающий папку, 
в которой располагается MOF-файл конфигурации. Командлет создает файл контрольной суммы `ConfigurationMOFName.mof.checksum`, где `ConfigurationMOFName` — имя MOF-файла конфигурации. 
Если в указанной папке есть несколько MOF-файлов конфигурации, контрольная сумма создается для каждой конфигурации в папке.

Файл контрольной суммы должен находиться в том же каталоге, что и MOF-файл конфигурации (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` по умолчанию), и иметь то же имя, что и у добавленного расширения `.checksum`.

>Примечание. При изменении MOF-файла конфигурации необходимо повторно создать файл контрольной суммы.

## Благодарности

Выражаю особую благодарность:

- Майку Ф. Роббинсу, чьи записи об использовании SMB для DSC помогли в составлении этой статьи. Ссылка на его блог — Майк Ф. Роббинс.
- Сергею Николайчуку, который создал модуль cNtfsAccessControl. Исходный код этого модуля доступен по ссылке https://github.com/SNikalaichyk/cNtfsAccessControl.

## См. также:
- [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
- [Применение конфигураций](enactingConfigurations.md)
- [Настройка опрашивающего клиента с помощью идентификатора конфигурации](pullClientConfigID.md)

 

<!--HONumber=Mar16_HO2-->


