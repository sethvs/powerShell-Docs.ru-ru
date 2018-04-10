---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Find-RoleCapability
ms.openlocfilehash: 89aacd604d54f6a5e9752790be65cc3bcc77c8e1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="find-rolecapability"></a>Find-RoleCapability

Находит возможности ролей в модулях.

## <a name="description"></a>Описание
Командлет Find-RoleCapability находит возможности ролей PowerShell в модулях. Find-RoleCapability ищет модули в зарегистрированных репозиториях.
Для каждой возможности роли, найденной командлетом, он возвращает объект PSGetRoleCapabilityInfo. Вы можете передать объект PSGetRoleCapabilityInfo в командлет Install-Module для установки модуля, содержащего эту возможность роли.
Возможности ролей PowerShell определяют, какие команды, приложения и т. п. будут доступны пользователю в конечной точке Just Enough Administration (JEA). Возможности ролей определяются файлами с расширением PSRC.

- Командлет Find-RoleCapability позволяет выполнять фильтрацию с помощью параметров версии: MinimumVersion, RequiredVersion, AllVersions.
  - Эти параметры являются взаимоисключающими.
  - Эти параметры версии допускаются только с единственным именем модуля без каких-либо подстановочных знаков.
  - Если параметр RequiredVersion не указан, командлет Find-RoleCapability возвращает последнюю версию модуля не ниже указанной минимальной версии или последнюю версию модуля, если минимальная версия не указана.
  - Если параметр RequiredVersion указан, Find-RoleCapability возвращает только версию модуля, которая точно совпадает с указанной версией.
- Командлет Find-RoleCapability позволяет фильтровать метаданные модуля с помощью параметра -Tag.
- Find-RoleCapability позволяет фильтровать язык поиска для определенного репозитория с помощью параметра -Filter.
- Find-RoleCapability может фильтровать модули из всех или некоторых из зарегистрированных репозиториев.

## <a name="cmdlet-syntax"></a>Синтаксис командлета
```powershell
Get-Command -Name Find-RoleCapability -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Find-RoleCapability](http://go.microsoft.com/fwlink/?LinkId=718029)

## <a name="example-commands"></a>Примеры команд
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