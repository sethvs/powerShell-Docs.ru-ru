---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Объект ISESnippetCollection"
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: b19c5b5c88f7c8bd0d0c466c7861fa9288bdc7a2
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="859cf-103">Объект ISESnippetCollection</span><span class="sxs-lookup"><span data-stu-id="859cf-103">The ISESnippetCollection Object</span></span>
  <span data-ttu-id="859cf-104">Объект **ISESnippetCollection** — это коллекция объектов **ISESnippet**.</span><span class="sxs-lookup"><span data-stu-id="859cf-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="859cf-105">Коллекция файлов, с которой связан объект **PowerShellTab**, является членом этого класса.</span><span class="sxs-lookup"><span data-stu-id="859cf-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="859cf-106">Примером является коллекция **$psISE.CurrentPowerShellTab.Files**.</span><span class="sxs-lookup"><span data-stu-id="859cf-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="859cf-107">Методы</span><span class="sxs-lookup"><span data-stu-id="859cf-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="859cf-108">Load\( FilePathName \)</span><span class="sxs-lookup"><span data-stu-id="859cf-108">Load\( FilePathName \)</span></span>
  <span data-ttu-id="859cf-109">Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях.</span><span class="sxs-lookup"><span data-stu-id="859cf-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="859cf-110">Загружает SNIPPETS.PS1XML-файл, содержащий определяемые пользователем фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="859cf-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="859cf-111">Для создания фрагментов кода проще всего использовать командлет New-IseSnippet, который автоматически сохраняет фрагменты в папке профиля, чтобы загружать их при каждом запуске интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="859cf-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

 <span data-ttu-id="859cf-112">**FilePathName** — строка. Путь к файлу с расширением SNIPPETS.PS1XML и его имя. В нем содержатся определения фрагментов.</span><span class="sxs-lookup"><span data-stu-id="859cf-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a><span data-ttu-id="859cf-113">См. также</span><span class="sxs-lookup"><span data-stu-id="859cf-113">See Also</span></span>
- [<span data-ttu-id="859cf-114">Объект ISESnippet</span><span class="sxs-lookup"><span data-stu-id="859cf-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md) 
- [<span data-ttu-id="859cf-115">Объектная модель скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="859cf-115">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="859cf-116">Справочник по объектной модели интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="859cf-116">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="859cf-117">Иерархия объектной модели интегрированной среды скриптов</span><span class="sxs-lookup"><span data-stu-id="859cf-117">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
