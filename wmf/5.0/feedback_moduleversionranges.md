---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: b64464eb2b4dd87ebe716e159fb916ac328b3b37
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="1161c-102">Поддержка модулей для объявления диапазонов версий (1.* и т. д.)</span><span class="sxs-lookup"><span data-stu-id="1161c-102">Modules support for declaring version ranges (1.*, etc)</span></span>
<span data-ttu-id="1161c-103">В сочетании с **-MinimumVersion** **-MaximumVersion** дает пользователю возможность получения и импорта модуля в пределах определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="1161c-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="1161c-104">Параметр также поддерживает **.***.</span><span class="sxs-lookup"><span data-stu-id="1161c-104">The parameter also support **.***.</span></span> <span data-ttu-id="1161c-105">В следующем примере показано, как это работает:</span><span class="sxs-lookup"><span data-stu-id="1161c-105">The following example shows how it works:</span></span>

```PowerShell
Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:

PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```

