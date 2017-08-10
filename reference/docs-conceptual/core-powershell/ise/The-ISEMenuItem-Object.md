---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEMenuItem"
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 33de866d706ec2b0894c5bfe49e07fee142b95c0
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="1f4b8-103">Объект ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="1f4b8-103">The ISEMenuItem Object</span></span>
  <span data-ttu-id="1f4b8-104">Объект **ISEMenuItem** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItem.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="1f4b8-105">Все объекты в меню **Надстройки** являются экземплярами класса **Microsoft.PowerShell.Host.ISE.ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="1f4b8-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="1f4b8-106">Properties</span></span>

###  <span data-ttu-id="1f4b8-107"><a name="DisplayName"></a> DisplayName</span><span class="sxs-lookup"><span data-stu-id="1f4b8-107"><a name="DisplayName"></a> DisplayName</span></span>
  <span data-ttu-id="1f4b8-108">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1f4b8-109">Свойство только для чтения, которое получает отображаемое имя пункта меню.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-109">The read-only property that gets the display name of the menu item.</span></span>

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

###  <span data-ttu-id="1f4b8-110"><a name="Action"></a> Действие</span><span class="sxs-lookup"><span data-stu-id="1f4b8-110"><a name="Action"></a> Action</span></span>
  <span data-ttu-id="1f4b8-111">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1f4b8-112">Свойство только для чтения, которое получает блок сценария.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="1f4b8-113">Оно вызывает действие при щелчке по элементу меню.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-113">It invokes the action when you click the menu item.</span></span>

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

###  <span data-ttu-id="1f4b8-114"><a name="Shortcut"></a> Сочетания клавиш</span><span class="sxs-lookup"><span data-stu-id="1f4b8-114"><a name="Shortcut"></a> Shortcut</span></span>
  <span data-ttu-id="1f4b8-115">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1f4b8-116">Свойство только для чтения, которое получает сочетания клавиш Windows для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

###  <span data-ttu-id="1f4b8-117"><a name="Submenus"></a> Подменю</span><span class="sxs-lookup"><span data-stu-id="1f4b8-117"><a name="Submenus"></a> Submenus</span></span>
  <span data-ttu-id="1f4b8-118">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="1f4b8-119">Свойство только для чтения, которое получает [список подменю](The-ISEMenuItemCollection-Object.md) для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="1f4b8-120">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="1f4b8-120">Scripting example</span></span>
 <span data-ttu-id="1f4b8-121">Чтобы лучше понять, как пользоваться меню надстроек и его свойствами с поддержкой сценариев, прочтите следующий пример сценария.</span><span class="sxs-lookup"><span data-stu-id="1f4b8-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```

# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu - a parent and a child submenu item. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")

```

## <a name="see-also"></a><span data-ttu-id="1f4b8-122">См. также</span><span class="sxs-lookup"><span data-stu-id="1f4b8-122">See Also</span></span>
- [<span data-ttu-id="1f4b8-123">Объект ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="1f4b8-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md) 
- [<span data-ttu-id="1f4b8-124">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f4b8-124">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="1f4b8-125">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f4b8-125">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="1f4b8-126">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="1f4b8-126">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
