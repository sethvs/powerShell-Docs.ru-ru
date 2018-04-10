---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Get-PSRepository
ms.openlocfilehash: 97279a8ed0087c835fb924991484959cd7237016
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="get-psrepository"></a>Get-PSRepository

Возвращает информацию о зарегистрированных репозиториях, которая есть на компьютере.

## <a name="description"></a>Описание

Командлет Get-PSRepository возвращает репозитории модуля PowerShell, зарегистрированные для текущего пользователя на компьютере.

Для каждого зарегистрированного репозитория Get-PSRepository возвращает объект PSRepository, который при необходимости может быть передан в командлет Unregister-PSRepository для отмены регистрации зарегистрированного репозитория.

## <a name="cmdlet-syntax"></a>Синтаксис командлета
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Get-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a>Примеры команд

```powershell

# Properties of Get-PSRepository returned object
Get-PSRepository PSGallery | Format-List * -Force

Name                      : PSGallery
SourceLocation            : https://www.powershellgallery.com/api/v2/
Trusted                   : False
Registered                : True
InstallationPolicy        : Untrusted
PackageManagementProvider : NuGet
PublishLocation           : https://www.powershellgallery.com/api/v2/package/
ScriptSourceLocation      : https://www.powershellgallery.com/api/v2/items/psscript/
ScriptPublishLocation     : https://www.powershellgallery.com/api/v2/package/
ProviderOptions           : {}

# Get all registered repositories
Get-PSRepository

# Get a specific registered repository
Get-PSRepository PSGallery

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/

# Get registered repository with wildcards
Get-PSRepository *Gallery*

```