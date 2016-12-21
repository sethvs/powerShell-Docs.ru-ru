---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "Объект ISEAddOnToolCollection"
ms.technology: powershell
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: 35327fafed0f6c6b1303f3bc99e9be8a9db4f61a
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="the-iseaddontoolcollection-object"></a>Объект ISEAddOnToolCollection
  Объект **ISEAddOnToolCollection** — это коллекция объектов **ISEAddOnTool**. Примером является объект **$psISE.CurrentPowerShellTab.VerticalAddOnTools**.

## <a name="methods"></a>Методы

### <a name="add-name-controltype-isvisible-"></a>Add\( Name, ControlType, \[IsVisible\] \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Добавляет новую надстройку в коллекцию. Метод возвращает добавленную надстройку. Перед выполнением этой команды необходимо установить надстройку на локальном компьютере и загрузить сборку.

 **Name** — строка. Задает отображаемое имя надстройки, добавляемой в интегрированную среду скриптов Windows PowerShell.

 **ControlType** — тип. Определяет добавляемый элемент управления.

 **\[IsVisible\]** — необязательный логический параметр. Если задано значение **$true**, надстройка сразу же отображается в связанной области инструментов.

```PowerShell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Remove\( Item \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Удаляет указанную надстройку из коллекции.

 **Item** — Microsoft.PowerShell.Host.ISE.ISEAddOnTool. Указывает объект, удаляемый из интегрированной среды скриптов Windows PowerShell.

```PowerShell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Выбирает вкладку PowerShell, указанную параметром **psTab**.

 **psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Выбираемая вкладка PowerShell.

```PowerShell
      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="remove-pstab-"></a>Remove\( psTab \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Удаляет вкладку PowerShell, указанную параметром **psTab**.

 **psTab** — Microsoft.PowerShell.Host.ISE.PowerShellTab. Удаляемая вкладка PowerShell.

```PowerShell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>См. также
- [Объект PowerShellTab](The-PowerShellTab-Object.md) 
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)

  
