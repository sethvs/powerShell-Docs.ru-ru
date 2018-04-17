---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 89e908969641afd9ad9541dcfedcc8eb6315d07c
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="82daa-102">Поддержка модулей для объявления диапазонов версий (1.\* и т. д.)</span><span class="sxs-lookup"><span data-stu-id="82daa-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="82daa-103">В сочетании с **-MinimumVersion** **-MaximumVersion** дает пользователю возможность получения и импорта модуля в пределах определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="82daa-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="82daa-104">Параметр также поддерживает **.** \*.</span><span class="sxs-lookup"><span data-stu-id="82daa-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="82daa-105">В следующем примере показано, как это работает:</span><span class="sxs-lookup"><span data-stu-id="82daa-105">The following example shows how it works:</span></span>

<span data-ttu-id="82daa-106">Теперь можно объединить **- MinimumVersion** и **- MaximumVersion** для импорта модуля в пределах определенного диапазона:</span><span class="sxs-lookup"><span data-stu-id="82daa-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

```powershell
PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```
