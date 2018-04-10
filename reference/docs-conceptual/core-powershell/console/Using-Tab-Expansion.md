---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Расширение по клавише TAB
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-tab-expansion"></a><span data-ttu-id="235b4-103">Расширение по клавише TAB</span><span class="sxs-lookup"><span data-stu-id="235b4-103">Using Tab Expansion</span></span>

<span data-ttu-id="235b4-104">Оболочки командной строки часто позволяют автоматически завершать длинные имена файлов или команд, что ускоряет ввод и позволяет использовать подсказки.</span><span class="sxs-lookup"><span data-stu-id="235b4-104">Command-line shells often provide a way to complete the names of long files or commands automatically, speeding up command entry and providing .</span></span> <span data-ttu-id="235b4-105">Windows PowerShell позволяет завершать имена файлов и командлетов нажатием клавиши **TAB**.</span><span class="sxs-lookup"><span data-stu-id="235b4-105">Windows PowerShell allows you to fill in file names and cmdlet names by pressing the **Tab** key.</span></span>

> [!NOTE]
> <span data-ttu-id="235b4-106">Завершением по клавише TAB управляет внутренняя функция TabExpansion или TabExpansion2.</span><span class="sxs-lookup"><span data-stu-id="235b4-106">Tab expansion is controlled by the internal function TabExpansion or TabExpansion2.</span></span> <span data-ttu-id="235b4-107">Так как ее можно изменить или переопределить, приведенные инструкции распространяются на стандартную конфигурацию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="235b4-107">Since this function can be modified or overridden, this discussion is a guide to the behavior of the default PowerShell configuration.</span></span>

<span data-ttu-id="235b4-108">Для автоматического завершения имени файла или пути из доступных вариантов введите часть имени и нажмите клавишу **TAB**.</span><span class="sxs-lookup"><span data-stu-id="235b4-108">To fill in a filename or path from the available choices automatically, type part of the name and press the **Tab** key.</span></span> <span data-ttu-id="235b4-109">PowerShell автоматически расширяет имя до первого совпадения.</span><span class="sxs-lookup"><span data-stu-id="235b4-109">PowerShell will automatically expand the name to the first match that it finds.</span></span> <span data-ttu-id="235b4-110">Нажимая клавишу **TAB**, можно перебрать все варианты.</span><span class="sxs-lookup"><span data-stu-id="235b4-110">Pressing the **Tab** key repeatedly will cycle through all of the available choices.</span></span>

<span data-ttu-id="235b4-111">Расширение имен командлетов по клавише TAB происходит немного иначе.</span><span class="sxs-lookup"><span data-stu-id="235b4-111">The tab expansion of cmdlet names is slightly different.</span></span> <span data-ttu-id="235b4-112">Чтобы использовать расширение по клавише TAB для имени командлета, введите всю первую часть имени (глагол) и дефис после нее.</span><span class="sxs-lookup"><span data-stu-id="235b4-112">To use tab expansion on a cmdlet name, type the entire first part of the name (the verb) and the hyphen that follows it.</span></span> <span data-ttu-id="235b4-113">Можно указать дополнительную часть имени для поиска частичного совпадения.</span><span class="sxs-lookup"><span data-stu-id="235b4-113">You can fill in more of the name for a partial match.</span></span> <span data-ttu-id="235b4-114">Например, если ввести **get-co** и нажать клавишу **TAB**, PowerShell автоматически расширяет это выражение до командлета **Get-Command** (при этом регистр букв также приводится к стандартной форме).</span><span class="sxs-lookup"><span data-stu-id="235b4-114">For example, if you type **get-co** and then press the **Tab** key, PowerShell will automatically expand this to the **Get-Command** cmdlet (notice that it also changes the case of letters to their standard form).</span></span> <span data-ttu-id="235b4-115">Если еще раз нажать клавишу **TAB**, PowerShell заменяет это другим подходящим именем командлета — **Get-Content**.</span><span class="sxs-lookup"><span data-stu-id="235b4-115">If you press **Tab** key again, PowerShell replaces this with the only other matching cmdlet name, **Get-Content**.</span></span>

<span data-ttu-id="235b4-116">Расширение по клавише TAB можно использовать несколько раз в одной строке.</span><span class="sxs-lookup"><span data-stu-id="235b4-116">You can use tab expansion repeatedly on the same line.</span></span> <span data-ttu-id="235b4-117">Например, можно использовать эту функцию для имени командлета **Get-Content**, введя:</span><span class="sxs-lookup"><span data-stu-id="235b4-117">For example, you can use tab expansion on the name of the **Get-Content** cmdlet by entering:</span></span>

```
PS> Get-Con<Tab>
```

<span data-ttu-id="235b4-118">При нажатии клавиши **TAB** команда расширяет до следующей:</span><span class="sxs-lookup"><span data-stu-id="235b4-118">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content
```

<span data-ttu-id="235b4-119">После этого можно указать часть пути к файлу журнала активной установки и снова воспользоваться описанной функцией:</span><span class="sxs-lookup"><span data-stu-id="235b4-119">You can then partially specify the path to the Active Setup log file and use tab expansion again:</span></span>

```
PS> Get-Content c:\windows\acts<Tab>
```

<span data-ttu-id="235b4-120">При нажатии клавиши **TAB** команда расширяет до следующей:</span><span class="sxs-lookup"><span data-stu-id="235b4-120">When you press the **Tab** key, the command expands to:</span></span>

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> <span data-ttu-id="235b4-121">Единственным ограничением этого процесса является то, что символы табуляции принимаются за попытки завершения слова.</span><span class="sxs-lookup"><span data-stu-id="235b4-121">One limitation of the tab expansion process is that tabs are always interpreted as attempts to complete a word.</span></span> <span data-ttu-id="235b4-122">При копировании и вставке примеров команд в консоль PowerShell убедитесь, что пример не содержит символы табуляции. В противном случае результаты будут непредсказуемыми и почти наверняка будут отличаться от требуемых.</span><span class="sxs-lookup"><span data-stu-id="235b4-122">If you copy and paste command examples into a PowerShell console, make sure that the sample does not contain tabs; if it does, the results will be unpredictable and will almost certainly not be what you intended.</span></span>