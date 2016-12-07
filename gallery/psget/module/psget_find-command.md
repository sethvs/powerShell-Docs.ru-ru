---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_нахождение_команды"
ms.technology: powershell
ms.openlocfilehash: 99091130ea89023495e5e3aacafb292f67f2db30
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="find-command"></a>Find-Command

Ищет команды PowerShell в модулях.

## <a name="description"></a>Описание
Командлет Find-Command ищет команды PowerShell, такие как командлеты, псевдонимы, функции и рабочие процессы. Find-Command ищет их в модулях из зарегистрированных репозиториев.
Для каждой команды, им обнаруженной, он возвращает объект PSGetCommandInfo. Вы можете передать объект PSGetCommandInfo в командлет Install-Module для установки модуля, содержащего конкретную команду.

- Командлет Find-Command позволяет выполнять фильтрацию при помощи параметров версии: MinimumVersion, RequiredVersion, AllVersions.
  - Эти параметры являются взаимоисключающими.
  - Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.
  - Если параметр RequiredVersion не указан, командлет Find-Command возвращает последнюю версию модуля, которая не ниже указанной минимальной версии, или последнюю версию модуля, если минимальная версия не указана.
  - Если параметр RequiredVersion указан, Find-Command возвращает только версию модуля, которая точно совпадает с указанной версией.
- Find-Command позволяет фильтровать метаданные модуля при помощи параметра -Tag.
- Find-Command позволяет фильтровать язык поиска для определенного репозитория при помощи параметра -Filter.
- Find-Command может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.

## <a name="cmdlet-syntax"></a>Синтаксис командлета
```powershell
Get-Command -Name Find-Command -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Find-Command](http://go.microsoft.com/fwlink/?LinkId=733636)

## <a name="example-commands"></a>Примеры команд
```powershell

# Find a specific command
Find-Command -Name Get-ScriptAnalyzerRule

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Get-ScriptAnalyzerRule              1.5.0      PSScriptAnalyzer                    PSGallery

# Find multiple commands
Find-Command -Name Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

# Find all available commands from all registered repositories
Find-Command

# Find available commands from few registered repositories
Find-Command -Repository PSGallery,PrivatePSGallery

# Find all commands in a specified repository
Find-Command -Repository PSGallery

# Find a command defined in a specific module
Find-Command -Name Get-ScriptAnalyzerRule -Module PSScriptAnalyzer

# Find commands from all versions of a module
Find-Command -ModuleName PSReadline -AllVersions

# Find commands with module name and MinimumVersion.
Find-Command -ModuleName PSReadline -MinimumVersion 1.1

# Find commands with module name and exact version
Find-Command -ModuleName AzureRM -RequiredVersion 1.4.0

# Find commands defined modules with -Filter based search. -Filter searches in description and module names
Find-Command -Filter Cookbook
Find-Command -Filter RBAC

# Find all commands with tags Azure or DSC in module metadata
Find-Command -Tag Azure, DSC

```

