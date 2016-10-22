---
title: "Справочник по объектной модели интегрированной среды сценариев Windows PowerShell"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
translationtype: Human Translation
ms.sourcegitcommit: 16608d8b97ec816d77ec7b8ac2438a4d64b55fba
ms.openlocfilehash: c60a7adb5cce55392d5dc09c7ca357bfc4c73e15

---

# Справочник по объектной модели интегрированной среды сценариев Windows PowerShell
  
## Справочник по объектной модели
 Этот раздел содержит справку по базовым классам, определяющим различные объекты в интегрированной среде скриптов (ISE) Windows PowerShell®. Упорядочение объектов в соответствии с их иерархией рассматривается в статье [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md).

 [Объект ISEAddOnTool](The-ISEAddOnTool-Object.md)
 Примеры: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.

 [Объект ISEAddOnTool](The-ISEAddOnTool-Object.md)
  [Объект ISEEditor](The-ISEEditor-Object.md)
 Примеры: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.

 [Объект ISEFile](The-ISEFile-Object.md)
 Примеры: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].

 [Объект ISEFileCollection](The-ISEFileCollection-Object.md)
 Примеры: $psISE.PowerShellTabs.Files.

 [Объект ISEMenuItem](The-ISEMenuItem-Object.md)
 Примеры: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].

 [Объект ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md)
 Пример: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.

 [Объект ISEOptions](The-ISEOptions-Object.md)
 Примеры: $psISE.Options, $psISE.Options.DefaultOptions.

 [Объект ObjectModelRoot](The-ObjectModelRoot-Object.md)
 Пример: корневой объект $psISE.

 [Объект PowerShellTab](The-PowerShellTab-Object.md)
 Примеры: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].

 [Объект PowerShellTabCollection](The-PowerShellTabCollection-Object.md)
 Пример: $psISE.PowerShellTabs.

## См. также
- [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  



<!--HONumber=Oct16_HO2-->


