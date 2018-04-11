---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Другие полезные объекты для сценариев
ms.assetid: 4d781196-720b-4ccc-90d2-c570e5e719f5
ms.openlocfilehash: 0e87e9919199e011ab5abec5b07dccc8494ad64a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="other-useful-scripting-objects"></a><span data-ttu-id="6eb5c-103">Другие полезные объекты для сценариев</span><span class="sxs-lookup"><span data-stu-id="6eb5c-103">Other Useful Scripting Objects</span></span>

<span data-ttu-id="6eb5c-104">Следующие объекты предоставляют дополнительные возможности создания сценариев в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-104">The following objects provide additional scripting functionality in Windows PowerShell ISE.</span></span> <span data-ttu-id="6eb5c-105">Они не являются частью иерархии **$psISE**.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-105">They are not part of the **$psISE** hierarchy.</span></span>

## <a name="useful-scripting-objects"></a><span data-ttu-id="6eb5c-106">Полезные объекты для сценариев</span><span class="sxs-lookup"><span data-stu-id="6eb5c-106">Useful Scripting objects</span></span>

### <a name="psunsupportedconsoleapplications"></a><span data-ttu-id="6eb5c-107">$psUnsupportedConsoleApplications</span><span class="sxs-lookup"><span data-stu-id="6eb5c-107">$psUnsupportedConsoleApplications</span></span>

<span data-ttu-id="6eb5c-108">Существуют некоторые ограничения, применяемые к взаимодействию интегрированной среды сценариев Windows PowerShell с консольными приложениями.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-108">There are some limitations on how Windows PowerShell ISE interacts with console applications.</span></span> <span data-ttu-id="6eb5c-109">Команда или сценарий автоматизации, требующие участия пользователя, могут не работать так, как при запуске из консоли Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-109">A command or an automation script that requires user intervention might not work the way it works from the Windows PowerShell console.</span></span> <span data-ttu-id="6eb5c-110">Может потребоваться заблокировать запуск этих команд или сценариев в области команд интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-110">You might want to block these commands or scripts from running in the Windows PowerShell ISE Command pane.</span></span> <span data-ttu-id="6eb5c-111">Объект **$PsUnsupportedConsoleApplications** хранит список таких команд.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-111">The **$psUnsupportedConsoleApplications** object keeps a list of such commands.</span></span> <span data-ttu-id="6eb5c-112">При попытке выполнить команды, указанные в этом списке, вы получите сообщение о том, что они не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-112">If you try to run the commands in this list, you get a message that they are not supported.</span></span> <span data-ttu-id="6eb5c-113">Следующий сценарий добавляет запись в этот список.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-113">The following script adds an entry to the list.</span></span>

```powershell
# List the unsupported commands
$psUnsupportedConsoleApplications

# Add a command to this list
$psUnsupportedConsoleApplications.Add('Mycommand')

# Show the augmented list of commands
$psUnsupportedConsoleApplications
```

### <a name="pslocalhelp"></a><span data-ttu-id="6eb5c-114">$psLocalHelp</span><span class="sxs-lookup"><span data-stu-id="6eb5c-114">$psLocalHelp</span></span>

<span data-ttu-id="6eb5c-115">Это объект словаря, который поддерживает сопоставление с учетом контекста разделов справки и связанных ссылок в локальном скомпилированном файле справки HTML.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-115">This is a dictionary object that maintains a context-sensitive mapping between Help topics and their associated links in the local compiled HTML Help file.</span></span> <span data-ttu-id="6eb5c-116">Он используется для поиска локальной справки для определенного раздела.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-116">It is used to locate the local Help for a particular topic.</span></span> <span data-ttu-id="6eb5c-117">Разделы в этом списке можно добавлять и удалять.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-117">You can add or delete topics from this list.</span></span> <span data-ttu-id="6eb5c-118">В следующем примере кода показаны некоторые примеры пар "ключ —значение", которые содержатся в объекте **$psLocalHelp**.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-118">The following code example shows some example key-value pairs that are contained in **$psLocalHelp**.</span></span>

```powershell
# See the local help map
$psLocalHelp | Format-List
```

### <a name="sample-output"></a><span data-ttu-id="6eb5c-119">Пример вывода</span><span class="sxs-lookup"><span data-stu-id="6eb5c-119">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="6eb5c-120">Ключ: Add-Computer</span><span class="sxs-lookup"><span data-stu-id="6eb5c-120">Key : Add-Computer</span></span>|<span data-ttu-id="6eb5c-121">Значение: WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span><span class="sxs-lookup"><span data-stu-id="6eb5c-121">Value : WindowsPowerShellHelp.chm::/html/093f660c-b8d5-43cf-aa0c-54e5e54e76f9.htm</span></span>|
|<span data-ttu-id="6eb5c-122">Ключ: Add-Content</span><span class="sxs-lookup"><span data-stu-id="6eb5c-122">Key : Add-Content</span></span>|<span data-ttu-id="6eb5c-123">Значение: WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span><span class="sxs-lookup"><span data-stu-id="6eb5c-123">Value : WindowsPowerShellHelp.chm::/html/0c836a1b-f389-4e9a-9325-0f415686d194.htm</span></span>|

<span data-ttu-id="6eb5c-124">Следующий сценарий добавляет запись в этот список.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-124">The following script adds an entry to the list.</span></span>

```powershell
$psLocalHelp.Add("get-myNoun", "c:\MyFolder\MyHelpChm.chm::/html/0198854a-1298-57ae-aa0c-87b5e5a84712.htm")
```

### <a name="psonlinehelp"></a><span data-ttu-id="6eb5c-125">$psOnlineHelp</span><span class="sxs-lookup"><span data-stu-id="6eb5c-125">$psOnlineHelp</span></span>

<span data-ttu-id="6eb5c-126">Это объект словаря, который поддерживает сопоставление с учетом контекста заголовков разделов справки и связанных внешних URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-126">This is a dictionary object that maintains a context-sensitive mapping between topic titles of Help topics and their associated external URLs.</span></span> <span data-ttu-id="6eb5c-127">Он используется для поиска справки для определенного раздела в Интернете.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-127">It is used to locate the Help for a particular topic on the web.</span></span> <span data-ttu-id="6eb5c-128">Разделы в этом списке можно добавлять и удалять.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-128">You can add or delete topics from this list.</span></span>

```powershell
$psOnlineHelp | Format-List
```

### <a name="sample-output"></a><span data-ttu-id="6eb5c-129">Пример вывода</span><span class="sxs-lookup"><span data-stu-id="6eb5c-129">Sample Output</span></span>

|||
|-|-|
|<span data-ttu-id="6eb5c-130">Ключ: Add-Computer</span><span class="sxs-lookup"><span data-stu-id="6eb5c-130">Key : Add-Computer</span></span>|<span data-ttu-id="6eb5c-131">Значение: http://go.microsoft.com/fwlink/p/?LinkID=135194</span><span class="sxs-lookup"><span data-stu-id="6eb5c-131">Value : http://go.microsoft.com/fwlink/p/?LinkID=135194</span></span>|
|<span data-ttu-id="6eb5c-132">Ключ: Add-Content</span><span class="sxs-lookup"><span data-stu-id="6eb5c-132">Key : Add-Content</span></span>|<span data-ttu-id="6eb5c-133">Значение: http://go.microsoft.com/fwlink/p/?LinkID=113278</span><span class="sxs-lookup"><span data-stu-id="6eb5c-133">Value : http://go.microsoft.com/fwlink/p/?LinkID=113278</span></span>|

 <span data-ttu-id="6eb5c-134">Следующий сценарий добавляет запись в этот список.</span><span class="sxs-lookup"><span data-stu-id="6eb5c-134">The following script adds an entry to the list.</span></span>

```powershell
$psOnlineHelp.Add("get-myNoun", "http://www.mydomain.com/MyNoun.html")
```

## <a name="see-also"></a><span data-ttu-id="6eb5c-135">См. также</span><span class="sxs-lookup"><span data-stu-id="6eb5c-135">See Also</span></span>

- [<span data-ttu-id="6eb5c-136">Назначение объектной модели скриптов интегрированной среды скриптов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6eb5c-136">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)