---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Объект ISEMenuItem
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 556f88117c07100b1734c8ffd8956dce6efe6fb1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="the-isemenuitem-object"></a>Объект ISEMenuItem

Объект **ISEMenuItem** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItem. Все объекты в меню **Надстройки** являются экземплярами класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.

## <a name="properties"></a>Свойства

### <a name="displayname"></a>DisplayName

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает отображаемое имя пункта меню.

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a>Действие

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает блок сценария. Оно вызывает действие при щелчке по элементу меню.

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a>Установленное напрямую доверие

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает сочетания клавиш Windows для пункта меню.

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a>Подменю

Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.

Свойство только для чтения, которое получает [список подменю](The-ISEMenuItemCollection-Object.md) для пункта меню.

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a>Пример сценария

Чтобы лучше понять, как пользоваться меню надстроек и его свойствами с поддержкой сценариев, прочтите следующий пример сценария.

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a>См. также

- [Объект ISEMenuItemCollection](The-ISEMenuItemCollection-Object.md)
- [Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)