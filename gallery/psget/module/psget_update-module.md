---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_обновление_модуля"
ms.technology: powershell
ms.openlocfilehash: 3f843bcf667bdb40f45613911647acf464cbbf29
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="update-module"></a>Update-Module

Скачивает последние версии указанных модулей из веб-коллекции и устанавливает их на локальном компьютере.

## <a name="description"></a>Описание

Командлет Update-Module устанавливает более новую версию модуля Windows PowerShell, который был установлен из веб-коллекции командлетом Install-Module на локальный компьютер.

По умолчанию устанавливается самая последняя версия указанного модуля, доступная в веб-коллекции, если не указана конкретная версия. Можно обновить существующий установленный модуль, указав имя модуля. Командлет Update-Module ищет в $env:PSModulePath обновляемый модуль.

При запуске Update-Module без параметра Name будут обновлены все модули, которые можно обновить на локальном компьютере.

### <a name="notes"></a>Заметки

- Этот командлет работает в Windows PowerShell 3.0 и последующих версиях в Windows 7, Windows Server 2008 R2 и более поздних версиях Windows.
- Если модуль, указанный в параметре Name, не был установлен командлетом Install-Module, возникнет ошибка. Командлет Update-Module можно выполнять только для модулей, установленных из веб-коллекции при помощи Install-Module.
- Если командлет Update-Module пытается обновить двоичные файлы, которые используются, то он возвращает ошибку, указывающую на проблемные процессы и информирующую пользователя о необходимости повторного своего запуска после остановки таких процессов.
- В PowerShell 5.0 и более поздних версиях при обновлении командлетом Update-Module модуля он добавляет последнюю (или указанную) версию модуля. Так старая и более новая версии размещаются параллельно в одном и том же каталоге. Теперь было бы полезно показать пример выходных данных этих команд.


## <a name="cmdlet-syntax"></a>Синтаксис командлета
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Update-Module](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a>Примеры команд

```powershell
PS C:\\windows\\system32> Update-Module -Name ContosoServer -RequiredVersion 1.5
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
PS C:\\windows\\system32> Update-Module -Name ContosoServer
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.8.1
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.8.1
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
```


###  <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a>Обновите модуль TestDepWithNestedRequiredModules1 с зависимостями.
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
```

