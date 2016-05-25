---
title: Объект ISEMenuItem
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
---
# Объект ISEMenuItem
  Объект **ISEMenuItem** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItem. Все объекты в меню **Надстройки** являются экземплярами класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.

## Свойства

###  <a name="DisplayName"></a> DisplayName
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает отображаемое имя элемента меню.

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

###  <a name="Action"></a> Действие
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает блок сценария. Оно вызывает действие при щелчке по элементу меню.

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

###  <a name="Shortcut"></a> Установленное напрямую доверие
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает сочетания клавиш Windows для элемента меню.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

###  <a name="Submenus"></a> Подменю
  Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий. 

 Свойство только для чтения, которое получает [список подменю](The-ISEMenuItemCollection-Object.md) для элемента меню.

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## Пример сценария
 Чтобы лучше понять, как пользоваться меню надстроек и его свойствами с поддержкой сценариев, прочтите следующий пример сценария.

```

# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu – a parent and a child submenu item. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")

```

## См. также
 [Объект ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


