---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_скрипт_сохранения"
ms.technology: powershell
ms.openlocfilehash: 58003350b991ca10b1d8bc65964bbfdd324334b5
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="save-script"></a>Save-Script

Командлет Save-Script позволяет просмотреть файл сценария, сохранив его в указанном расположении.

## <a name="description"></a>Описание

Командлет Save-Script сохраняет указанный скрипт.

## <a name="cmdlet-syntax"></a>Синтаксис командлета

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Ссылка на раздел справки по командлету в Интернете

[Save-Script](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a>Примеры команд

### <a name="example-1-save-a-script-from-a-repository"></a>Пример 1. Сохранение скрипта из репозитория
Эта команда сохраняет последнюю версию скрипта Fabrikam-ClientScript из репозитория GalleryINT в локальную папку C:\ScriptSharingDemo.

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a>Пример 2. Сохранение версии скрипта по конвейеру из командлета Find-Script

Первая команда находит версию 1.5 скрипта Fabrikam-ClientScript в репозитории GalleryINT и сохраняет ее в папку C:\ScriptSharingDemo.

Вторая команда проверяет метаданные сохраненного скрипта.

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```

