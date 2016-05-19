---
title: Объект PowerShellTabCollection
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
---
# Объект PowerShellTabCollection
  Объект коллекции **PowerShellTabCollection** — это коллекция объектов **PowerShellTab**. Каждый объект **PowerShellTab** функционирует как отдельная среда выполнения. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.PowerShellTabs. Примером является объект **$psISE.PowerShellTabs**.

## Методы

### Add()
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Добавляет новую вкладку PowerShell в коллекцию. Метод возвращает вновь добавленную вкладку.

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### Remove(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет вкладку, которая указана параметром **psTab**.

 **psTab**
 Удаляемая вкладка PowerShell.

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### SetSelectedPowerShellTab(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Выбирает вкладку PowerShell, которая задается параметром **psTab**, чтобы сделать ее активной вкладкой PowerShell.

 **psTab**
 Выбираемая вкладка PowerShell.

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

## См. также
 [Объект PowerShellTab](The-PowerShellTab-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](../ise/The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


