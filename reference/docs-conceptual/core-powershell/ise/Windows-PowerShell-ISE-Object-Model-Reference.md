---
ms.date: 2017-06-05T00:00:00.000Z
keywords: "powershell,командлет"
title: "Справочник по объектной модели интегрированной среды сценариев Windows PowerShell"
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
ms.openlocfilehash: e5d4ae03158d9b5b0efd98db1272bc13872181ac
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="windows-powershell-ise-object-model-reference"></a>Справочник по объектной модели интегрированной среды сценариев Windows PowerShell
  
## <a name="object-model-reference"></a>Справочник по объектной модели
 Этот раздел содержит справку по базовым классам, определяющим различные объекты в интегрированной среде скриптов (ISE) Windows PowerShell®. Упорядочение объектов в соответствии с их иерархией рассматривается в статье [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md).

 [Объект ISEAddOnTool](The-ISEAddOnTool-Object.md) Примеры: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.

 [Объект ISEAddOnTool](The-ISEAddOnTool-Object.md) [Объект ISEEditor](The-ISEEditor-Object.md) Примеры: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.

 [Объект ISEFile](The-ISEFile-Object.md) Примеры: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].

 [Объект ISEFileCollection](The-ISEFileCollection-Object.md) Примеры: $psISE.PowerShellTabs.Files.

 [Объект ISEMenuItem](The-ISEMenuItem-Object.md) Примеры: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].

 [Объект ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md) Пример: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.

 [Объект ISEOptions](The-ISEOptions-Object.md) Примеры: $psISE.Options, $psISE.Options.DefaultOptions.

 [Объект ObjectModelRoot](The-ObjectModelRoot-Object.md) Пример: корневой объект $psISE.

 [Объект PowerShellTab](The-PowerShellTab-Object.md) Примеры: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].

 [Объект PowerShellTabCollection](The-PowerShellTabCollection-Object.md) Пример: $psISE.PowerShellTabs.

## <a name="see-also"></a>См. также
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  
