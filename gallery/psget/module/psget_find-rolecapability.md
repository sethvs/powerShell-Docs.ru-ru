---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: Find-RoleCapability
ms.openlocfilehash: 77c5b492d9681fa05315401fba410c508af1d13b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="find-rolecapability" class="xliff"></a>
# Find-RoleCapability

Находит возможности ролей в модулях.

<a id="description" class="xliff"></a>
## Описание
Командлет Find-RoleCapability находит возможности ролей PowerShell в модулях. Find-RoleCapability ищет модули в зарегистрированных репозиториях. Для каждой возможности роли, найденной командлетом, он возвращает объект PSGetRoleCapabilityInfo. Вы можете передать объект PSGetRoleCapabilityInfo в командлет Install-Module для установки модуля, содержащего эту возможность роли.
Возможности ролей PowerShell определяют, какие команды, приложения и т. п. будут доступны пользователю в конечной точке Just Enough Administration (JEA). Возможности ролей определяются файлами с расширением PSRC.

- Командлет Find-RoleCapability позволяет выполнять фильтрацию с помощью параметров версии: MinimumVersion, RequiredVersion, AllVersions.
  - Эти параметры являются взаимоисключающими.
  - Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.
  - Если параметр RequiredVersion не указан, командлет Find-RoleCapability возвращает последнюю версию модуля не ниже указанной минимальной версии или последнюю версию модуля, если минимальная версия не указана.
  - Если параметр RequiredVersion указан, Find-RoleCapability возвращает только версию модуля, которая точно совпадает с указанной версией.
- Командлет Find-RoleCapability позволяет фильтровать метаданные модуля с помощью параметра -Tag.
- Find-RoleCapability позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.
- Find-RoleCapability может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.

<a id="cmdlet-syntax" class="xliff"></a>
## Синтаксис командлета
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

<a id="cmdlet-online-help-reference" class="xliff"></a>
## Ссылка на раздел справки по командлету в Интернете

[Find-RoleCapability](http://go.microsoft.com/fwlink/?LinkId=718029)

<a id="example-commands" class="xliff"></a>
## Примеры команд
```powershell

# Find a specific role capability
Find-RoleCapability -Name Maintenance

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Maintenance                         1.5.0      RoleCapModule                       PrivatePSGallery

# Find multiple role capabilities
Find-RoleCapability -Name MyJeaRole, Maintenance

# Find all available role capabilities from all registered repositories
Find-RoleCapability

# Find available role capabilities from few registered repositories
Find-RoleCapability -Repository PSGallery,PrivatePSGallery

# Find all role capabilities in a specified repository
Find-RoleCapability -Repository PSGallery

# Find a role capability defined in a specific module
Find-RoleCapability -Name Maintenance -ModuleName RoleCapModule

# Find role capabilities from all versions of a module
Find-RoleCapability -ModuleName RoleCapModule -AllVersions

# Find role capabilities with module name and MinimumVersion.
Find-RoleCapability -ModuleName RoleCapModule -MinimumVersion 1.1

# Find role capabilities with module name and exact version
Find-RoleCapability -ModuleName RoleCapModule -RequiredVersion 1.4.0

# Find role capabilities defined modules with -Filter based search. -Filter searches in description and module names
Find-RoleCapability -Filter Cookbook
Find-RoleCapability -Filter RBAC

# Find all role capabilities with tags Azure or DSC in module metadata
Find-RoleCapability -Tag Azure, DSC

```

