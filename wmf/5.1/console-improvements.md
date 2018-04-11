---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: Усовершенствования консоли в WMF 5.1
ms.openlocfilehash: 2abc02010c6c1d9f7fc617e9831b2d1243e0a3ee
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="console-improvements-in-wmf-51"></a><span data-ttu-id="116df-103">Усовершенствования консоли в WMF 5.1#</span><span class="sxs-lookup"><span data-stu-id="116df-103">Console Improvements in WMF 5.1#</span></span>

## <a name="powershell-console-improvements"></a><span data-ttu-id="116df-104">Усовершенствования консоли PowerShell</span><span class="sxs-lookup"><span data-stu-id="116df-104">PowerShell console improvements</span></span>

<span data-ttu-id="116df-105">Для улучшения работы с консолью в Powershell.exe в WMF 5.1 были внесены перечисленные ниже изменения.</span><span class="sxs-lookup"><span data-stu-id="116df-105">The following changes have been made to powershell.exe in WMF 5.1 to improve the console experience:</span></span>

###<a name="vt100-support"></a><span data-ttu-id="116df-106">Поддержка VT100</span><span class="sxs-lookup"><span data-stu-id="116df-106">VT100 support</span></span>

<span data-ttu-id="116df-107">В Windows 10 реализована поддержка [escape-последовательностей VT100](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="116df-107">Windows 10 added support for [VT100 escape sequences](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span></span>
<span data-ttu-id="116df-108">При расчете ширины таблиц PowerShell игнорирует некоторые escape-последовательности форматирования VT100.</span><span class="sxs-lookup"><span data-stu-id="116df-108">PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.</span></span>

<span data-ttu-id="116df-109">В PowerShell также появился новый интерфейс API, который можно использовать при форматировании кода для определения наличия поддержки VT100.</span><span class="sxs-lookup"><span data-stu-id="116df-109">PowerShell also added a new API that can be used in formatting code to determine if VT100 is supported.</span></span>
<span data-ttu-id="116df-110">Например:</span><span class="sxs-lookup"><span data-stu-id="116df-110">For example:</span></span>

```
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```
<span data-ttu-id="116df-111">Вот полный [пример](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7), который можно использовать для выделения совпадений в результатах выполнения командлета Select-String.</span><span class="sxs-lookup"><span data-stu-id="116df-111">Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from Select-String.</span></span>
<span data-ttu-id="116df-112">Сохраните пример в файле с именем `MatchInfo.format.ps1xml`. Чтобы использовать его, в своем профиле или другом месте выполните команду `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="116df-112">Save the example in a file named `MatchInfo.format.ps1xml`, then to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span></span>

<span data-ttu-id="116df-113">Имейте в виду, что escape-последовательности VT100 поддерживаются начиная с юбилейного обновления Windows 10. В более ранних системах они не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="116df-113">Note that VT100 escape sequences are only supported starting with the Windows 10 Anniversary update; they are not supported on earlier systems.</span></span>

### <a name="vi-mode-support-in-psreadline"></a><span data-ttu-id="116df-114">Поддержка режима vi в PSReadline</span><span class="sxs-lookup"><span data-stu-id="116df-114">Vi mode support in PSReadline</span></span>

<span data-ttu-id="116df-115">В [PSReadline](https://github.com/lzybkr/PSReadLine) добавлена поддержка режима vi.</span><span class="sxs-lookup"><span data-stu-id="116df-115">[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode.</span></span> <span data-ttu-id="116df-116">Чтобы включить режим vi, выполните команду `Set-PSReadlineOption -EditMode Vi`.</span><span class="sxs-lookup"><span data-stu-id="116df-116">To use vi mode, run `Set-PSReadlineOption -EditMode Vi`.</span></span>

### <a name="redirected-stdin-with-interactive-input"></a><span data-ttu-id="116df-117">Перенаправленный поток stdin с интерактивным вводом</span><span class="sxs-lookup"><span data-stu-id="116df-117">Redirected stdin with interactive input</span></span>

<span data-ttu-id="116df-118">В предыдущих версиях среду PowerShell требовалось запускать с помощью команды `powershell -File -`, если поток stdin перенаправлялся и необходимо было вводить команды в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="116df-118">In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and you wanted to enter commands interactively.</span></span>

<span data-ttu-id="116df-119">В WMF 5.1 этот сложный для обнаружения вариант больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="116df-119">With WMF 5.1, this hard to discover option is no longer necessary.</span></span>
<span data-ttu-id="116df-120">PowerShell можно запустить без параметров, например `powershell`.</span><span class="sxs-lookup"><span data-stu-id="116df-120">You can start PowerShell without any options, e.g. `powershell`.</span></span>

<span data-ttu-id="116df-121">Обратите внимание на то, что PSReadline в настоящее время не поддерживает перенаправленный поток stdin, а встроенные возможности редактирования в командной строке с перенаправленным потоком stdin крайне ограничены, например не работают клавиши со стрелками.</span><span class="sxs-lookup"><span data-stu-id="116df-121">Note that PSReadline does not currently support redirected stdin, and the built-in command-line editing experience with redirected stdin is extremely limited, for example, arrow keys don't work.</span></span>
<span data-ttu-id="116df-122">В будущих версиях PSReadline эта проблема должна быть решена.</span><span class="sxs-lookup"><span data-stu-id="116df-122">A future release of PSReadline should address this issue.</span></span>