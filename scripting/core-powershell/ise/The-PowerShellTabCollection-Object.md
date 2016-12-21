---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "Объект PowerShellTabCollection"
ms.technology: powershell
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: 38bac3445fd94022f03c0f336bd17f9033dfedc2
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="the-powershelltabcollection-object"></a>Объект PowerShellTabCollection
  Объект коллекции **PowerShellTabCollection** — это коллекция объектов **PowerShellTab**. Каждый объект **PowerShellTab** функционирует как отдельная среда выполнения. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.PowerShellTabs. Примером является объект **$psISE.PowerShellTabs**.

## <a name="methods"></a>Методы

### <a name="add"></a>Add \(\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Добавляет новую вкладку PowerShell в коллекцию. Метод возвращает вновь добавленную вкладку.

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет вкладку, которая указана параметром **psTab**.

 **psTab**
 — удаляемая вкладка PowerShell.

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выбирает вкладку PowerShell, которая задается параметром **psTab**, чтобы сделать ее активной вкладкой PowerShell.

 **psTab**
 — выбираемая вкладка PowerShell.

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a>См. также
- [Объект PowerShellTab](The-PowerShellTab-Object.md) 
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Иерархия объектной модели интегрированной среды скриптов](../ise/The-ISE-Object-Model-Hierarchy.md)

  
