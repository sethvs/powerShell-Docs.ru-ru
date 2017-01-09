---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "Приложение 1. Псевдонимы совместимости"
ms.technology: powershell
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 126c124bd9bd4aa7c724fc0ef0b075a649d66f44
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="appendix-1---compatibility-aliases"></a>Приложение 1. Псевдонимы совместимости
Windows PowerShell имеет несколько псевдонимов перехода, позволяющих пользователям UNIX и Cmd применять знакомые команды в Windows PowerShell. Наиболее распространенные псевдонимы приведены в таблице ниже, также там указана команда Windows PowerShell для псевдонима и стандартный псевдоним Windows PowerShell, если он существует.

Найти команду Windows PowerShell, на которую указывает псевдоним из Windows PowerShell, можно с помощью командлета Get-Alias. Например, введите **get-alias cls**.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|Команда CMD|Команда UNIX|Команда PS|Псевдоним PS|
|---------------|----------------|--------------|------------|
|**dir**|**ls**|**Get-ChildItem**|**gci**|
|**cls**|**clear**|**Clear-Host** (функция)|**cls**|
|**del, erase, rmdir**|**rm**|**Remove-Item**|**ri**|
|**copy**|**cp**|**Copy-Item**|**ci**|
|**move**|**mv**|**Move-Item**|**mi**|
|**rename**|**mv**|**Rename-Item**|**rni**|
|**type**|**cat**|**Get-Content**|**gc**|
|**cd**|**cd**|**Set-Location**|**sl**|
|**md**|**mkdir**|**New-Item**|**ni**|
|**pushd**|**pushd**|**Push-Location**|**pushd**|
|**popd**|**popd**|**Pop-Location**|**popd**|

