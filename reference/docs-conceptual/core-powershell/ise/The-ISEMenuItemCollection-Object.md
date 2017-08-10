---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISEMenuItemCollection"
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7ce9132021d4d5e755503e0adb355beb388a625a
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="b1a44-103">Объект ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="b1a44-103">The ISEMenuItemCollection Object</span></span>
  <span data-ttu-id="b1a44-104">Объект **ISEMenuItemCollection**  — это коллекция объектов **ISEMenuItem**.</span><span class="sxs-lookup"><span data-stu-id="b1a44-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="b1a44-105">Он является экземпляром класса Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection.</span><span class="sxs-lookup"><span data-stu-id="b1a44-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="b1a44-106">Примером является объект **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus**, используемый для настройки меню **Надстройка** (Add-On) в интегрированной среде скриптов Windows PowerShell® (ISE).</span><span class="sxs-lookup"><span data-stu-id="b1a44-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="b1a44-107">Метод</span><span class="sxs-lookup"><span data-stu-id="b1a44-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="b1a44-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span><span class="sxs-lookup"><span data-stu-id="b1a44-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>
  <span data-ttu-id="b1a44-109">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="b1a44-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="b1a44-110">Добавляет пункт меню в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="b1a44-110">Adds a menu item to the collection.</span></span>

 <span data-ttu-id="b1a44-111">**DisplayName**
 — отображаемое имя добавляемого меню.</span><span class="sxs-lookup"><span data-stu-id="b1a44-111">**DisplayName**
 The display name of the menu to be added.</span></span>

 <span data-ttu-id="b1a44-112">**Action**
 — объект **System.Management.Automation.ScriptBlock**, указывающий действие, связанное с этим пунктом меню.</span><span class="sxs-lookup"><span data-stu-id="b1a44-112">**Action**
 The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

 <span data-ttu-id="b1a44-113">**Shortcut**
 — сочетание клавиш для действия.</span><span class="sxs-lookup"><span data-stu-id="b1a44-113">**Shortcut**
 The keyboard shortcut for the action.</span></span>

 <span data-ttu-id="b1a44-114">**Returns**
 — объект ISEMenuItem, который был только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="b1a44-114">**Returns**
 The ISEMenuItem object that was just added.</span></span>

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### <a name="clear"></a><span data-ttu-id="b1a44-115">Clear\(\)</span><span class="sxs-lookup"><span data-stu-id="b1a44-115">Clear\(\)</span></span>
  <span data-ttu-id="b1a44-116">Поддерживается в интегрированной среде сценариев Windows PowerShell 2.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="b1a44-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="b1a44-117">Удаляет все подменю из пункта меню.</span><span class="sxs-lookup"><span data-stu-id="b1a44-117">Removes all submenus from the menu item.</span></span>

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## <a name="see-also"></a><span data-ttu-id="b1a44-118">См. также</span><span class="sxs-lookup"><span data-stu-id="b1a44-118">See Also</span></span>
- [<span data-ttu-id="b1a44-119">Объект ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="b1a44-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md) 
- [<span data-ttu-id="b1a44-120">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1a44-120">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="b1a44-121">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1a44-121">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="b1a44-122">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="b1a44-122">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
