---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_отмена_регистрации_репозитория_ps"
ms.technology: powershell
ms.openlocfilehash: c90710db47dbfdc58e1ca7f84c6d6fd8f04b5109
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="unregister-psrepository"></a>Unregister-PSRepository

Отмена регистрации репозитория.

## <a name="description"></a>Описание

Командлет Unregister-PSRepository отменяет регистрацию репозитория для текущего пользователя.
- Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.
- Пользователи могут повторно зарегистрировать PSGallery, просто выполнив команду `Register-PSRepository -Default`.
- Так как PSGallery — это репозиторий для публикации по умолчанию в командлетах Publish-Module и Publish-Script, возникнет ошибка, если коллекция PSGallery недоступна в списке зарегистрированных репозиториев.

## <a name="cmdlet-syntax"></a>Синтаксис командлета

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Unregister-PSRepository](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a>Примеры команд

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a>Отмена регистрации и повторная регистрация репозитория PSGallery допустима для корпоративного и автономного сценариев.
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```

