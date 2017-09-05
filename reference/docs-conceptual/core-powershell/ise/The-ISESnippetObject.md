---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISESnippet"
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: 6112f5252d2d1e868092da4a6cd04feb1875b597
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
# <a name="the-isesnippetobject"></a><span data-ttu-id="78531-103">Объект ISESnippet</span><span class="sxs-lookup"><span data-stu-id="78531-103">The ISESnippetObject</span></span>
  <span data-ttu-id="78531-104">Объект **ISESnippet** является экземпляром класса Microsoft.PowerShell.Host.ISE.ISESnippet.</span><span class="sxs-lookup"><span data-stu-id="78531-104">An **ISESnippet** object is an instance of the Microsoft.PowerShell.Host.ISE.ISESnippet class.</span></span> <span data-ttu-id="78531-105">Элементы коллекции **$psISE.CurrentPowerShellTab.Snippets** являются примерами объектов **ISESnippet**.</span><span class="sxs-lookup"><span data-stu-id="78531-105">The members of the **$psISE.CurrentPowerShellTab.Snippets** collection are all examples of **ISESnippet** objects.</span></span> <span data-ttu-id="78531-106">Самый простой способ создать фрагмент кода — использовать командлет [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0).</span><span class="sxs-lookup"><span data-stu-id="78531-106">The easiest way to create a snippet is to use the [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet.</span></span>

## <a name="properties"></a><span data-ttu-id="78531-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="78531-107">Properties</span></span>

### <a name="author"></a><span data-ttu-id="78531-108">Дизайнер</span><span class="sxs-lookup"><span data-stu-id="78531-108">Author</span></span>
  <span data-ttu-id="78531-109">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="78531-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="78531-110">Свойство только для чтения, которое получает имя автора фрагмента.</span><span class="sxs-lookup"><span data-stu-id="78531-110">The read-only property that gets the name of the author of the snippet.</span></span>

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a><span data-ttu-id="78531-111">CodeFragment</span><span class="sxs-lookup"><span data-stu-id="78531-111">CodeFragment</span></span>
  <span data-ttu-id="78531-112">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="78531-112">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="78531-113">Свойство только для чтения, которое получает фрагмент кода, вставляемый в редактор.</span><span class="sxs-lookup"><span data-stu-id="78531-113">The read-only property that gets the code fragment to be inserted into the editor.</span></span>

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a><span data-ttu-id="78531-114">Установленное напрямую доверие</span><span class="sxs-lookup"><span data-stu-id="78531-114">Shortcut</span></span>
  <span data-ttu-id="78531-115">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="78531-115">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="78531-116">Свойство только для чтения, которое получает сочетания клавиш Windows для пункта меню.</span><span class="sxs-lookup"><span data-stu-id="78531-116">The read-only property that gets the Windows keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a><span data-ttu-id="78531-117">См. также</span><span class="sxs-lookup"><span data-stu-id="78531-117">See Also</span></span>
- [<span data-ttu-id="78531-118">Объект ISESnippetCollection</span><span class="sxs-lookup"><span data-stu-id="78531-118">The ISESnippetCollection Object</span></span>](The-ISESnippetCollection-Object.md) 
- [<span data-ttu-id="78531-119">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="78531-119">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="78531-120">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="78531-120">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="78531-121">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="78531-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
