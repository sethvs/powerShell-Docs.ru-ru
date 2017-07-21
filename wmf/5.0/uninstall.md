---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 3392db954c22030bb64ae5093619d23952e1fcdb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="92827-102">Инструкции по удалению</span><span class="sxs-lookup"><span data-stu-id="92827-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="92827-103">Использование командной строки</span><span class="sxs-lookup"><span data-stu-id="92827-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="92827-104">Откройте окно **Командная строка**.</span><span class="sxs-lookup"><span data-stu-id="92827-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="92827-105">Запустите [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) (Автономное средство запуска Центра обновления Windows), как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="92827-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="92827-106">В Windows Server 2012 R2 и Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="92827-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="92827-107">В Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="92827-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="92827-108">В Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):</span><span class="sxs-lookup"><span data-stu-id="92827-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="92827-109">Использование панели управления</span><span class="sxs-lookup"><span data-stu-id="92827-109">Using Control Panel</span></span>
1.  <span data-ttu-id="92827-110">Откройте **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="92827-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="92827-111">Откройте **Программы** и выберите **Удаление программы**.</span><span class="sxs-lookup"><span data-stu-id="92827-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="92827-112">Щелкните **Просмотр установленных обновлений**.</span><span class="sxs-lookup"><span data-stu-id="92827-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="92827-113">Выберите **Windows Management Framework 5.0** в списке установленных обновлений.</span><span class="sxs-lookup"><span data-stu-id="92827-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="92827-114">Это соответствует *KB3134758*, *KB3134759* или *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="92827-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="92827-115">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="92827-115">Click **Uninstall.**</span></span>

