---
title: Объект ISEMenuItemCollection
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
---
# Объект ISEMenuItemCollection
  Объект **ISEMenuItemCollection**  — это коллекция объектов **ISEMenuItem**. Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection. Примером является объект **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus**, используемый для настройки меню **Надстройки** в интегрированной среде сценариев Windows PowerShell® (ISE).

## Метод

### Add(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Добавляет пункт меню в коллекцию.

 **DisplayName**
 Отображаемое имя добавляемого меню.

 **Действие**
 Объект **System.Management.Automation.ScriptBlock**, указывающий действие, связанное с этим пунктом меню.

 **Установленное напрямую доверие**
 Сочетание клавиш для действия.

 **Возвращает**
 объект ISEMenuItem, который был только что добавлен.

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### Clear()
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Удаляет все подменю из пункта меню.

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## См. также
 [Объект ISEMenuItem](The-ISEMenuItem-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


