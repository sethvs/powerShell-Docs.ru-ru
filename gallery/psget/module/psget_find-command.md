---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Find-Command
ms.openlocfilehash: 26ddf4824816db245131a0fc95b7d2a88bef8f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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