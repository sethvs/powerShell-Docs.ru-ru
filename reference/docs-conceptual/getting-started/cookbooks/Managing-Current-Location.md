---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Управление текущим расположением"
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 20b3828d12587e675ed51863e5d96c37839b62d6
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="managing-current-location"></a><span data-ttu-id="077a0-103">Управление текущим расположением</span><span class="sxs-lookup"><span data-stu-id="077a0-103">Managing Current Location</span></span>
<span data-ttu-id="077a0-104">При навигации по системам папок в проводнике у вас обычно есть определенное рабочее расположение, т. е. текущая открытая папка.</span><span class="sxs-lookup"><span data-stu-id="077a0-104">When navigating folder systems in File Explorer, you usually have a specific working location - namely, the current open folder.</span></span> <span data-ttu-id="077a0-105">Элементами в текущей папке можно легко управлять, щелкая их.</span><span class="sxs-lookup"><span data-stu-id="077a0-105">Items in the current folder can be manipulated easily by clicking them.</span></span> <span data-ttu-id="077a0-106">Когда в интерфейсе командной строки (например, Cmd.exe) открыта папка, в которой находится определенный файл, вы можете получить к нему доступ, указав короткое имя, а не вводить весь путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="077a0-106">For command-line interfaces such as Cmd.exe, when you are in the same folder as a particular file, you can access it by specifying a relatively short name, rather than needing to specify the entire path to the file.</span></span> <span data-ttu-id="077a0-107">Текущий каталог называется рабочим.</span><span class="sxs-lookup"><span data-stu-id="077a0-107">The current directory is called the working directory.</span></span>

<span data-ttu-id="077a0-108">Windows PowerShell использует существительное **Location** для ссылки на рабочий каталог и реализует семейство командлетов для просмотра расположения и управления им.</span><span class="sxs-lookup"><span data-stu-id="077a0-108">Windows PowerShell uses the noun **Location** to refer to the working directory, and implements a family of cmdlets to examine and manipulate your location.</span></span>

### <a name="getting-your-current-location-get-location"></a><span data-ttu-id="077a0-109">Получение текущего расположения (Get-Location)</span><span class="sxs-lookup"><span data-stu-id="077a0-109">Getting Your Current Location (Get-Location)</span></span>
<span data-ttu-id="077a0-110">Чтобы определить путь к текущему каталогу, введите команду **Get-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-110">To determine the path of your current directory location, enter the **Get-Location** command:</span></span>

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="077a0-111">Командлет Get-Location аналогичен команде **pwd** в оболочке BASH.</span><span class="sxs-lookup"><span data-stu-id="077a0-111">The Get-Location cmdlet is similar to the **pwd** command in the BASH shell.</span></span> <span data-ttu-id="077a0-112">Командлет Set-Location аналогичен команде **cd** в Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="077a0-112">The Set-Location cmdlet is similar to the **cd** command in Cmd.exe.</span></span>

### <a name="setting-your-current-location-set-location"></a><span data-ttu-id="077a0-113">Настройка текущего расположения (Set-Location)</span><span class="sxs-lookup"><span data-stu-id="077a0-113">Setting Your Current Location (Set-Location)</span></span>
<span data-ttu-id="077a0-114">Команда **Get-Location** используется с командой **Set-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-114">The **Get-Location** command is used with the **Set-Location** command.</span></span> <span data-ttu-id="077a0-115">Команда **Set-Location** позволяет вам указать расположение текущего каталога.</span><span class="sxs-lookup"><span data-stu-id="077a0-115">The **Set-Location** command allows you to specify your current directory location.</span></span>

```
PS> Set-Location -Path C:\Windows
```

<span data-ttu-id="077a0-116">Обратите внимание, что после ввода команды вы не получите прямого отклика о действии команды.</span><span class="sxs-lookup"><span data-stu-id="077a0-116">After you enter the command, you will notice that you do not receive any direct feedback about the effect of the command.</span></span> <span data-ttu-id="077a0-117">Большинство команд Windows PowerShell, выполняющих действия, практически не создают выходных данных, так как выходные данные не всегда полезны.</span><span class="sxs-lookup"><span data-stu-id="077a0-117">Most Windows PowerShell commands that perform an action produce little or no output because the output is not always useful.</span></span> <span data-ttu-id="077a0-118">Чтобы проверить успешность внесения изменения в каталог при вводе команды **Set-Location**, укажите параметр **-PassThru** при вводе команды **Set-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-118">To verify that a successful directory change has occurred when you enter the **Set-Location** command, include the **-PassThru** parameter when you enter the **Set-Location** command:</span></span>

```
PS> Set-Location -Path C:\Windows -PassThru
Path
----
C:\WINDOWS
```

<span data-ttu-id="077a0-119">Параметр **-PassThru** можно использовать с некоторыми командами Set в Windows PowerShell для возврата сведений о результате, когда отсутствуют выходные данные по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="077a0-119">The **-PassThru** parameter can be used with many Set commands in Windows PowerShell to return information about the result in cases in which there is no default output.</span></span>

<span data-ttu-id="077a0-120">Вы можете указать пути относительно текущего расположения так же, как и в большинстве командных оболочек UNIX и Windows.</span><span class="sxs-lookup"><span data-stu-id="077a0-120">You can specify paths relative to your current location in the same way as you would in most UNIX and Windows command shells.</span></span> <span data-ttu-id="077a0-121">В стандартной нотации для относительных путей точка (**.**) представляет текущую папку, а две точки (**..**) — родительский каталог текущего расположения.</span><span class="sxs-lookup"><span data-stu-id="077a0-121">In standard notation for relative paths, a period (**.**)represents your current folder, and a doubled period (**..**) represents the parent directory of your current location.</span></span>

<span data-ttu-id="077a0-122">Например, если вы находитесь в папке **C:\\Windows**, точка (**.**) представляет **C:\\Windows**, а две точки (**..**) представляют **C:**.</span><span class="sxs-lookup"><span data-stu-id="077a0-122">For example, if you are in the **C:\\Windows** folder, a period (**.**)represents **C:\\Windows** and double periods (**..**) represent **C:**.</span></span> <span data-ttu-id="077a0-123">Текущее расположение можно изменить на корень диска C: путем ввода следующей команды:</span><span class="sxs-lookup"><span data-stu-id="077a0-123">You can change from your current location to the root of the C: drive by typing:</span></span>

<pre>PS> Set-Location -Path .. -PassThru
Path
----
C:\</pre>

<span data-ttu-id="077a0-124">Тот же метод работает для дисков Windows PowerShell, которые не являются дисками файловой системы, например **HKLM:**.</span><span class="sxs-lookup"><span data-stu-id="077a0-124">The same technique works on Windows PowerShell drives that are not file system drives, such as **HKLM:**.</span></span> <span data-ttu-id="077a0-125">В реестре в качестве расположения можно задать раздел HKLM\\Software путем ввода следующего кода:</span><span class="sxs-lookup"><span data-stu-id="077a0-125">You can set your location to the HKLM\\Software key in the registry by typing:</span></span>

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

<span data-ttu-id="077a0-126">После этого можно изменить расположение каталога на родительский каталог, который является корнем диска Windows PowerShell HKLM: с помощью относительного пути:</span><span class="sxs-lookup"><span data-stu-id="077a0-126">You can then change the directory location to the parent directory, which is the root of the Windows PowerShell HKLM: drive, by using a relative path:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

<span data-ttu-id="077a0-127">Вы можете ввести Set-Location или использовать любой из встроенных псевдонимов Windows PowerShell для Set-Location (cd, chdir, sl).</span><span class="sxs-lookup"><span data-stu-id="077a0-127">You can type Set-Location or use any of the built-in Windows PowerShell aliases for Set-Location (cd, chdir, sl).</span></span> <span data-ttu-id="077a0-128">Например:</span><span class="sxs-lookup"><span data-stu-id="077a0-128">For example:</span></span>

```
cd -Path C:\Windows
```

```
chdir -Path .. -PassThru
```

```
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a><span data-ttu-id="077a0-129">Сохранение и отзыв последних расположений (Push-Location и Pop-Location)</span><span class="sxs-lookup"><span data-stu-id="077a0-129">Saving and Recalling Recent Locations (Push-Location and Pop-Location)</span></span>
<span data-ttu-id="077a0-130">При изменении расположения полезно отслеживать свое предыдущее расположение и иметь возможность вернуться к нему.</span><span class="sxs-lookup"><span data-stu-id="077a0-130">When changing locations, it is helpful to keep track of where you have been and to be able to return to your previous location.</span></span> <span data-ttu-id="077a0-131">Командлет **Push-Location** в Windows PowerShell создает упорядоченный журнал ("стек") путей к каталогам, которые вы открывали, чтобы можно было вернуться по нему на шаг назад, используя дополнительный командлет **Pop-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-131">The **Push-Location** cmdlet in Windows PowerShell creates a ordered history (a "stack") of directory paths where you have been, and you can step back through the history of directory paths by using the complementary **Pop-Location** cmdlet.</span></span>

<span data-ttu-id="077a0-132">Например, Windows PowerShell обычно запускается в корневом каталоге пользователя.</span><span class="sxs-lookup"><span data-stu-id="077a0-132">For example, Windows PowerShell typically starts in the user's home directory.</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="077a0-133">Слово *стек* имеет специальное значение во многих параметрах программирования, включая .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="077a0-133">The word *stack* has a special meaning in many programming settings, including .NET Framework.</span></span> <span data-ttu-id="077a0-134">Например, в физическом стеке элементов последний элемент, помещенный в стек, является первым элементом, который можно извлечь из него.</span><span class="sxs-lookup"><span data-stu-id="077a0-134">Like a physical stack of items, the last item you put onto the stack is the first item that you can pull off the stack.</span></span> <span data-ttu-id="077a0-135">Добавление элемента в стек в разговорной речи называется "проталкиванием" элемента в стек.</span><span class="sxs-lookup"><span data-stu-id="077a0-135">Adding an item to a stack is colloquially known as "pushing" the item onto the stack.</span></span> <span data-ttu-id="077a0-136">Извлечение элемента из стека в разговорной речи называется "выводом" элемента из стека.</span><span class="sxs-lookup"><span data-stu-id="077a0-136">Pulling an item off the stack is colloquially known as "popping" the item off the stack.</span></span>

<span data-ttu-id="077a0-137">Чтобы передать текущее расположение в стек, а затем переместить его в папку локальных параметров, введите:</span><span class="sxs-lookup"><span data-stu-id="077a0-137">To push the current location onto the stack, and then move to the Local Settings folder, type:</span></span>

```
PS> Push-Location -Path "Local Settings"
```

<span data-ttu-id="077a0-138">После этого можно передать расположение локальных параметров в стек и переместить его в папку Temp, введя:</span><span class="sxs-lookup"><span data-stu-id="077a0-138">You can then push the Local Settings location onto the stack and and move to the Temp folder by typing:</span></span>

```
PS> Push-Location -Path Temp
```

<span data-ttu-id="077a0-139">Чтобы убедиться, что каталоги изменены, введите команду **Get-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-139">You can verify that you changed directories by entering the **Get-Location** command:</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

<span data-ttu-id="077a0-140">После этого можно перейти в последний открытый каталог, введя команду **Pop-Location**, и проверить изменение, введя команду **Get-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-140">You can then pop back into the most recently visited directory by entering the **Pop-Location** command, and verify the change by entering the **Get-Location** command:</span></span>

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

<span data-ttu-id="077a0-141">Как и в случае с командлетом **Set-Location**, можно включить параметр **-PassThru** при вводе командлета **Pop-Location**, чтобы открыть указанный каталог.</span><span class="sxs-lookup"><span data-stu-id="077a0-141">Just as with the **Set-Location** cmdlet, you can include the **-PassThru** parameter when you enter the **Pop-Location** cmdlet to display the directory that you entered:</span></span>

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

<span data-ttu-id="077a0-142">Кроме того, можно использовать командлеты расположения с сетевыми путями.</span><span class="sxs-lookup"><span data-stu-id="077a0-142">You can also use the Location cmdlets with network paths.</span></span> <span data-ttu-id="077a0-143">Если у вас есть сервер FS01 с общей папкой Public, можно изменить расположение, введя</span><span class="sxs-lookup"><span data-stu-id="077a0-143">If you have a server named FS01 with an share named Public, you can change your location by typing</span></span>

```
Set-Location \\FS01\Public
```

<span data-ttu-id="077a0-144">или</span><span class="sxs-lookup"><span data-stu-id="077a0-144">or</span></span>

```
Push-Location \\FS01\Public
```

<span data-ttu-id="077a0-145">Чтобы изменить расположение на любой доступный диск, можно использовать команды **Push-Location** и **Set-Location**.</span><span class="sxs-lookup"><span data-stu-id="077a0-145">You can use the **Push-Location** and **Set-Location** commands to change the location to any available drive.</span></span> <span data-ttu-id="077a0-146">Например, если у вас есть локальный дисковод компакт-дисков с буквой диска D, содержащий компакт-диск с данными, вы можете изменить расположение на него, введя команду **Set-Location D:**.</span><span class="sxs-lookup"><span data-stu-id="077a0-146">For example, if you have a local CD-ROM drive with drive letter D that contains a data CD, you can change the location to the CD drive by entering the **Set-Location D:** command.</span></span>

<span data-ttu-id="077a0-147">Если дисковод пуст, вы получите следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="077a0-147">If the drive is empty, you will get the following error message:</span></span>

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

<span data-ttu-id="077a0-148">В интерфейсе командной строки проводник неудобно использовать для просмотра свободных физических дисков.</span><span class="sxs-lookup"><span data-stu-id="077a0-148">When you are using a command-line interface, it is not convenient to use File Explorer to examine the available physical drives.</span></span> <span data-ttu-id="077a0-149">Также в проводнике будут показаны не все диски PowerShell.</span><span class="sxs-lookup"><span data-stu-id="077a0-149">Also, File Explorer would not show you the all of the Windows PowerShell drives.</span></span> <span data-ttu-id="077a0-150">Windows PowerShell предоставляет набор команд для управления дисками Windows PowerShell, о которых речь пойдет далее.</span><span class="sxs-lookup"><span data-stu-id="077a0-150">Windows PowerShell provides a set of commands for manipulating Windows PowerShell drives, and we will talk about these next.</span></span>

