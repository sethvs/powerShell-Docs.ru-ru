---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Приложение 1. Псевдонимы совместимости
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 113bbee1af185f98777df5767022d54accb69447
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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