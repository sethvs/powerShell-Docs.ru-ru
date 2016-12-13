---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_публикация_модуля"
ms.technology: powershell
ms.openlocfilehash: a21351837d0cc63e56254911a1a436175a2734cd
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="publish-module"></a>Publish-Module

Публикует указанный модуль с локального компьютера в коллекцию в Интернете.

## <a name="description"></a>Описание

Командлет **Publish-Module** публикует модуль в коллекцию на основе NuGet в Интернете с помощью ключа API, который хранится как часть профиля пользователя в коллекции. Модуль для публикации можно указывать с помощью имени модуля или пути к папке, содержащей модуль.

Если модуль указывается по имени, командлет **Publish-Module** публикует первый модуль, найденный с помощью `Get-Module -ListAvailable <Name>`. Если указывается минимальная версия модуля для публикации, **Publish-Module** публикует первый модуль с версией, которая не ниже указанной минимальной версии.

Для публикации модуля требуются метаданные, которые отображаются на странице коллекции для этого модуля. Обязательные метаданные включают имя модуля, версию, описание и автора. Хотя большинство метаданных берется из манифеста модуля, некоторые метаданные должны указываться в параметрах командлета **Publish-Module**, таких как, например, *ReleaseNote, IconUri, ProjectUri* и *LicenseUri*, так как эти параметры соответствуют полям в коллекции на основе NuGet.

В параметре RequiredVersion можно указать точную версию модуля для публикации.
Параметр Path также поддерживает базовый путь к модулю с папкой версии.
Параметр Force командлета Publish-Module обеспечивает начальную загрузку NuGet.exe без запроса подтверждения.

## <a name="cmdlet-syntax"></a>Синтаксис командлета
```powershell
Get-Command -Name Publish-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Publish-Module](http://go.microsoft.com/fwlink/?LinkID=398575)

## <a name="example-commands"></a>Примеры команд

```powershell
ContosoServer module with different versions to be published.
PS C:\\windows\\system32> Get-Module -Name ContosoServer -ListAvailable
Directory: C:\\Program Files\\WindowsPowerShell\\Modules
ModuleType Version Name ExportedCommands
---------- ------- ---- ----------------
Manifest 2.8 ContosoServer Get-ContosoServer
Manifest 2.0 ContosoServer Get-ContosoServer
Manifest 1.5 ContosoServer Get-ContosoServer
Manifest 1.0 ContosoServer Get-ContosoServer
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.0 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Name ContosoServer -RequiredVersion 1.5 -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
PS C:\\windows\\system32> Publish-Module -Path "C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0" -Repository LocalRepo -NuGetApiKey Local-Repo-NuGet-ApiKey
PS C:\\windows\\system32> Find-Module -Name ContosoServer -Repository LocalRepo
Version Name Repository Description
_------ ---- ---------- -----------
1.0 ContosoServer LocalRepo ContosoServer module
1.5 ContosoServer LocalRepo ContosoServer module
2.0 ContosoServer LocalRepo ContosoServer module
```

## <a name="publishing-a-module-with-dependencies"></a>Публикация модуля с зависимостями

### <a name="create-a-module-with-dependencies-and-version-range-specified-in-requiredmodules-property-of-its-module-manifest"></a>Создайте модуль с зависимостями и диапазоном версий, указанным в свойстве RequiredModules манифеста этого модуля.

**Примечание**.
  - \* поддерживается только в MaximumVersion и также должен быть в конце строки версии. 
  - \* заменяется на 999999999 в объекте версии.

```powershell
PS C:\windows\system32> $requiredModules = @( @{ModuleName = 'RequiredModule1'; ModuleVersion = '0.1'; MaximumVersion = '1.9'; }, @{ModuleName = 'RequiredModule2'; MaximumVersion = '1.*'; })

PS C:\windows\system32> cd C:\MyModules\ModuleWithDependencies

PS C:\MyModules\ModuleWithDependencies> New-ModuleManifest -Path .\ModuleWithDependencies.psd1 -ModuleVersion 1.0 -RequiredModules $requiredModules -Description 'ModuleWithDependencies demo module'
```

### <a name="publish-modulewithdependencies-module-with-dependencies-to-the-repository"></a>Опубликуйте модуль ModuleWithDependencies с зависимостями в репозитории.

```powershell
PS C:\MyModules\ModuleWithDependencies> Publish-Module -Path C:\MyModules\ModuleWithDependencies -Repository LocalRepo
```

### <a name="find-modulewithdependencies-module-with-its-dependencies-by-specifying--includedependencies"></a>Найдите модуль ModuleWithDependencies вместе с зависимостями, указав -IncludeDependencies.

```powershell
PS C:\MyModules\ModuleWithDependencies> Find-Module -Name ModuleWithDependencies -Repository LocalRepo -IncludeDependencies

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="install-the-modulewithdependencies-module-with-dependencies"></a>Установите модуль ModuleWithDependencies с зависимостями.
Обратите внимание, что диапазоны версий учитываются во время установки зависимостей.

```powershell
PS C:\windows\system32> Get-InstalledModule
PS C:\windows\system32>
PS C:\windows\system32> Install-Module -Name ModuleWithDependencies -Repository LocalRepo
PS C:\windows\system32>
PS C:\windows\system32> Get-InstalledModule

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.0        ModuleWithDependencies              Module     localrepo            ModuleWithDependencies demo module
1.5        RequiredModule1                     Module     localrepo            RequiredModule1 module
1.5        RequiredModule2                     Module     localrepo            RequiredModule2 module
```

### <a name="contents-of-modulewithdependencies2-module-manifest-file"></a>Содержимое файла манифеста для модуля ModuleWithDependencies2

```powershell
@{
# Version number of this module.
ModuleVersion = '2.0'
# ID used to uniquely identify this module
GUID = '0eae34da-99dd-4608-8d28-c614fe7b0841'
# Author of this module
Author = 'manikb'
# Company or vendor of this module
CompanyName = 'Unknown'
# Copyright statement for this module
Copyright = '(c) 2015 manikb. All rights reserved.'
# Description of the functionality provided by this module
Description = 'ModuleWithDependencies2 module'
# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @('RequiredModule1',
@{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'RequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'RequiredModule4'; ModuleVersion = '1.1'; MaximumVersion = '2.0'; },
@{ModuleName = 'RequiredModule5'; MaximumVersion = '1.5'; })
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @('NestedRequiredModule1',
@{ModuleName = 'NestedRequiredModule2'; ModuleVersion = '2.0'; },
@{ModuleName = 'NestedRequiredModule3'; RequiredVersion = '2.5'; },
@{ModuleName = 'NestedRequiredModule4'; ModuleVersion = '0.7'; MaximumVersion = '2.4'; },
@{ModuleName = 'NestedRequiredModule5'; MaximumVersion = '1.6'; },'ModuleWithDependencies2.psm1')
# Functions to export from this module
FunctionsToExport = '\*'
# Cmdlets to export from this module
CmdletsToExport = '\*'
# Variables to export from this module
VariablesToExport = '\*'
# Aliases to export from this module
AliasesToExport = '\*'
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
      # Tags applied to this module. These help with module discovery in online galleries.
      Tags = 'Tag1', 'Tag2', 'Tag-ModuleWithDependencies2-2.0'
      # A URL to the license for this module.
      LicenseUri = 'http://modulewithdependencies2.com/license'
      # A URL to the main website for this project.
      ProjectUri = 'http://modulewithdependencies2.com/'
      # A URL to an icon representing this module.
      IconUri = 'http://modulewithdependencies2.com/icon'
      # ReleaseNotes of this module
      ReleaseNotes = 'ModuleWithDependencies2 release notes'
    } # End of PSData hashtable
} # End of PrivateData hashtable
}
```


### <a name="external-dependencies"></a>Внешние зависимости
Некоторые зависимости модуля могут управляться извне; в этом случае они должны добавляться в запись ExternalModuleDependencies раздела PSData манифеста модуля.

Если SnippetPx не доступен в репозитории, возникнет следующая ошибка.
```powershell
Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
```

