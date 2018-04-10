---
ms.date: 10/17/2017
contributor: keithb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Save-Script
ms.openlocfilehash: 67697fc0e70fb31cad9ad5ae7ce01debef160b81
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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

### <a name="example-3-save-a-prerelease-version-of-a-script-from-a-repository"></a>Пример 3. Сохранение предварительной версии сценария из репозитория
Эта команда сохраняет последнюю версию скрипта Fabrikam-ClientScript из репозитория GalleryINT в локальную папку C:\ScriptSharingDemo.

```powershell
Save-Script -Name Fabrikam-ClientScript -Path C:\ScriptSharingDemo -AllowPrerelease
```