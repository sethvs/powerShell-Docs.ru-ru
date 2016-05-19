---
title: Объект ISEAddOnToolCollection
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
---
# Объект ISEAddOnToolCollection
  Объект **ISEAddOnToolCollection** — это коллекция объектов **ISEAddOnTool**. Примером является объект **$psISE.CurrentPowerShellTab.VerticalAddOnTools**.

## Методы

### Add( Name, ControlType, [IsVisible] )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Добавляет новую надстройку в коллекцию. Метод возвращает добавленную надстройку. Перед выполнением этой команды необходимо установить надстройку на локальном компьютере и загрузить сборку.

 **Name** — строка.
 Задает отображаемое имя надстройки, добавляемой в интегрированную среду сценариев Windows PowerShell.

 **ControlType** — тип.
 Определяет добавляемый элемент управления.

 **[IsVisible]** — необязательный логический параметр.
 Если задано значение **$true**, надстройка сразу же отображается в связанной области инструментов.

```
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)

```

### Remove( Item )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Удаляет указанную надстройку из коллекции.

 **Item** — Microsoft.PowerShell.Host.ISE.ISEAddOnTool.
 Указывает объект, удаляемый из интегрированной среды сценариев Windows PowerShell.

```
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)

```

### SetSelectedPowerShellTab( psTab )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Выбирает вкладку PowerShell, указанную параметром **psTab**.

 **psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab.
 Выбираемая вкладка PowerShell.

```

      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"

```

### Remove( psTab )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Удаляет вкладку PowerShell, указанную параметром **psTab**.

 **psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab.
 Удаляемая вкладка PowerShell.

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## См. также
 [Объект PowerShellTab](The-PowerShellTab-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


