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
# <a name="the-isemenuitem-object"></a><span data-ttu-id="7bc4a-103">Объект ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="7bc4a-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="7bc4a-104">Объект **ISEMenuItem** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItem.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="7bc4a-105">Все объекты в меню **Надстройки** являются экземплярами класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="7bc4a-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="7bc4a-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="7bc4a-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7bc4a-107">DisplayName</span></span>

<span data-ttu-id="7bc4a-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7bc4a-109">Свойство только для чтения, которое получает отображаемое имя пункта меню.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="7bc4a-110">Действие</span><span class="sxs-lookup"><span data-stu-id="7bc4a-110">Action</span></span>

<span data-ttu-id="7bc4a-111">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7bc4a-112">Свойство только для чтения, которое получает блок сценария.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="7bc4a-113">Оно вызывает действие при щелчке по элементу меню.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="7bc4a-114">Установленное напрямую доверие</span><span class="sxs-lookup"><span data-stu-id="7bc4a-114">Shortcut</span></span>

<span data-ttu-id="7bc4a-115">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7bc4a-116">Свойство только для чтения, которое получает сочетания клавиш Windows для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="7bc4a-117">Подменю</span><span class="sxs-lookup"><span data-stu-id="7bc4a-117">Submenus</span></span>

<span data-ttu-id="7bc4a-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7bc4a-119">Свойство только для чтения, которое получает [список подменю](The-ISEMenuItemCollection-Object.md) для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="7bc4a-120">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="7bc4a-120">Scripting example</span></span>

<span data-ttu-id="7bc4a-121">Чтобы лучше понять, как пользоваться меню надстроек и его свойствами с поддержкой сценариев, прочтите следующий пример сценария.</span><span class="sxs-lookup"><span data-stu-id="7bc4a-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7bc4a-122">См. также</span><span class="sxs-lookup"><span data-stu-id="7bc4a-122">See Also</span></span>

- [<span data-ttu-id="7bc4a-123">Объект ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="7bc4a-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="7bc4a-124">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bc4a-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7bc4a-125">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="7bc4a-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)