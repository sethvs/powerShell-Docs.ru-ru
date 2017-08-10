---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Использование переменных для хранения объектов"
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 067948d7c234fb70c7cf9966c9ae3e8df1f99757
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="using-variables-to-store-objects"></a><span data-ttu-id="90cc5-103">Использование переменных для хранения объектов</span><span class="sxs-lookup"><span data-stu-id="90cc5-103">Using Variables to Store Objects</span></span>
<span data-ttu-id="90cc5-104">Windows PowerShell работает с объектами.</span><span class="sxs-lookup"><span data-stu-id="90cc5-104">Windows PowerShell works with objects.</span></span> <span data-ttu-id="90cc5-105">Можно создавать переменные, главным образом — именованные объекты, чтобы сохранять выходные данные для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="90cc5-105">Windows PowerShell lets you create variables - essentially named objects - to preserve output to use later.</span></span> <span data-ttu-id="90cc5-106">Если вы привыкли работать с переменными в других оболочках, помните, что переменные Windows PowerShell являются объектами, а не текстом.</span><span class="sxs-lookup"><span data-stu-id="90cc5-106">If you are used to working with variables in other shells, remember that Windows PowerShell variables are objects, not text.</span></span>

<span data-ttu-id="90cc5-107">Имена переменных всегда начинаются с символа $ и могут включать любые буквенно-цифровые символы или знаки подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="90cc5-107">Variables are always specified with the initial character $, and can include any alphanumeric characters or the underscore in their names.</span></span>

### <a name="creating-a-variable"></a><span data-ttu-id="90cc5-108">Создание переменной</span><span class="sxs-lookup"><span data-stu-id="90cc5-108">Creating a Variable</span></span>
<span data-ttu-id="90cc5-109">Чтобы создать переменную, можно ввести для нее допустимое имя:</span><span class="sxs-lookup"><span data-stu-id="90cc5-109">You can create a variable by typing a valid variable name:</span></span>

```
PS> $loc
PS>
```

<span data-ttu-id="90cc5-110">Это не возвращает никаких результатов, так как **$loc** не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="90cc5-110">This returns no result because **$loc** does not have a value.</span></span> <span data-ttu-id="90cc5-111">Создать переменную и присвоить ей значение можно в одном шаге.</span><span class="sxs-lookup"><span data-stu-id="90cc5-111">You can create a variable and assign it a value in the same step.</span></span> <span data-ttu-id="90cc5-112">Windows PowerShell создает переменную, только если она не существует; в противном случае указанное значение назначается существующей переменной.</span><span class="sxs-lookup"><span data-stu-id="90cc5-112">Windows PowerShell only creates the variable if it does not exist; otherwise, it assigns the specified value to the existing variable.</span></span> <span data-ttu-id="90cc5-113">Для сохранения текущего расположения в переменной **$loc** введите:</span><span class="sxs-lookup"><span data-stu-id="90cc5-113">To store your current location in the variable **$loc**, type:</span></span>

```
$loc = Get-Location
```

<span data-ttu-id="90cc5-114">При вводе этой команды выходные данные не отображаются, поскольку они отправляются в $loc.</span><span class="sxs-lookup"><span data-stu-id="90cc5-114">There is no output displayed when you type this command because the output is sent to $loc.</span></span> <span data-ttu-id="90cc5-115">В Windows PowerShell отображаемые выходные данные являются побочным эффектом той особенности, что данные, не ориентированные каким либо образом, всегда выводятся на экран.</span><span class="sxs-lookup"><span data-stu-id="90cc5-115">In Windows PowerShell, displayed output is a side effect of the fact that data which is not otherwise directed always gets sent to the screen.</span></span> <span data-ttu-id="90cc5-116">При вводе $loc отображается ваше текущее расположение:</span><span class="sxs-lookup"><span data-stu-id="90cc5-116">Typing $loc will show your current location:</span></span>

```
PS> $loc

Path
----
C:\temp
```

<span data-ttu-id="90cc5-117">**Get-Member** можно использовать для отображения сведений о содержимом переменных.</span><span class="sxs-lookup"><span data-stu-id="90cc5-117">You can use **Get-Member** to display information about the contents of variables.</span></span> <span data-ttu-id="90cc5-118">Передача $loc в Get-Member покажет, что это объект **PathInfo**, так же как и выходные данные Get-Location:</span><span class="sxs-lookup"><span data-stu-id="90cc5-118">Piping $loc to Get-Member will show you that it is a **PathInfo** object, just like the output from Get-Location:</span></span>

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a><span data-ttu-id="90cc5-119">Работа с переменными</span><span class="sxs-lookup"><span data-stu-id="90cc5-119">Manipulating Variables</span></span>
<span data-ttu-id="90cc5-120">Windows PowerShell предоставляет несколько команд для работы с переменными.</span><span class="sxs-lookup"><span data-stu-id="90cc5-120">Windows PowerShell provides several commands to manipulate variables.</span></span> <span data-ttu-id="90cc5-121">Полный список в удобочитаемой форме можно получить, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="90cc5-121">You can see a complete listing in a readable form by typing:</span></span>

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

<span data-ttu-id="90cc5-122">Кроме переменных, создаваемых в текущем сеансе Windows PowerShell, существует несколько системных переменных.</span><span class="sxs-lookup"><span data-stu-id="90cc5-122">In addition to the variables you create in your current Windows PowerShell session, there are several system-defined variables.</span></span> <span data-ttu-id="90cc5-123">Можно использовать командлет **Remove-Variable**, чтобы очистить все переменные, которые не управляются с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90cc5-123">You can use the **Remove-Variable** cmdlet to clear out all of the variables which are not controlled by Windows PowerShell.</span></span> <span data-ttu-id="90cc5-124">Введите следующую команду для очистки всех переменных:</span><span class="sxs-lookup"><span data-stu-id="90cc5-124">Type the following command to clear all variables:</span></span>

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

<span data-ttu-id="90cc5-125">В результате выводится приведенный ниже запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="90cc5-125">This will produce the confirmation prompt you see below.</span></span>

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

<span data-ttu-id="90cc5-126">Если вы запустите командлет **Get-Variable**, то увидите остальные переменные Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90cc5-126">If you then run the **Get-Variable** cmdlet, you will see the remaining Windows PowerShell variables.</span></span> <span data-ttu-id="90cc5-127">Поскольку существует и переменный диск Windows PowerShell, можно также отобразить все переменные Windows PowerShell, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="90cc5-127">Since there is also a variable Windows PowerShell drive, you can also display all Windows PowerShell variables by typing:</span></span>

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a><span data-ttu-id="90cc5-128">Использование переменных Cmd.exe</span><span class="sxs-lookup"><span data-stu-id="90cc5-128">Using Cmd.exe Variables</span></span>
<span data-ttu-id="90cc5-129">Хотя система Windows PowerShell — это не Cmd.exe, она выполняется в среде командной оболочки и может использовать переменные, доступные в любой среде в Windows.</span><span class="sxs-lookup"><span data-stu-id="90cc5-129">Although Windows PowerShell is not Cmd.exe, it runs in a command shell environment and can use the same variables available in any environment in Windows.</span></span> <span data-ttu-id="90cc5-130">Эти переменные предоставляются посредством диска с именем **env:**.</span><span class="sxs-lookup"><span data-stu-id="90cc5-130">These variables are exposed through a drive named **env**:.</span></span> <span data-ttu-id="90cc5-131">Эти переменные можно просмотреть, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="90cc5-131">You can view these variables by typing:</span></span>

```
Get-ChildItem env:
```

<span data-ttu-id="90cc5-132">Хотя стандартные командлеты переменных не предназначены для работы с переменными **env:**, их все равно можно использовать, указав префикс **env:**.</span><span class="sxs-lookup"><span data-stu-id="90cc5-132">Although the standard variable cmdlets are not designed to work with **env:** variables, you can still use them by specifying the **env:** prefix.</span></span> <span data-ttu-id="90cc5-133">Например, для просмотра корневого каталога операционной системы можно использовать переменную **%SystemRoot%** командной оболочки из Windows PowerShell, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="90cc5-133">For example, to see the operating system root directory, you can use the command-shell **%SystemRoot%** variable from within Windows PowerShell by typing:</span></span>

```
PS> $env:SystemRoot
C:\WINDOWS
```

<span data-ttu-id="90cc5-134">В Windows PowerShell также можно создавать и изменять переменные среды.</span><span class="sxs-lookup"><span data-stu-id="90cc5-134">You can also create and modify environment variables from within Windows PowerShell.</span></span> <span data-ttu-id="90cc5-135">Переменные среды из Windows PowerShell соответствует обычным правилам для переменных среды в рамках всей системы Windows.</span><span class="sxs-lookup"><span data-stu-id="90cc5-135">Environment variables accessed from Windows PowerShell conform to the normal rules for environment variables elsewhere in Windows.</span></span>

