---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Прямое управление элементами
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: 688f9194bd16793331325999c69e88df3e94c976
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="69412-103">Прямое управление элементами</span><span class="sxs-lookup"><span data-stu-id="69412-103">Manipulating Items Directly</span></span>

<span data-ttu-id="69412-104">Элементы, которые отображаются на дисках Windows PowerShell, например файлы и папки на дисках файловой системы и разделы реестра на дисках реестра Windows PowerShell, называются в Windows PowerShell *элементами*.</span><span class="sxs-lookup"><span data-stu-id="69412-104">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="69412-105">Командлеты для работы с ними содержат существительное **Item** в именах.</span><span class="sxs-lookup"><span data-stu-id="69412-105">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="69412-106">В выходных данных команды **Get-Command -Noun Item** показано, что есть девять элементов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69412-106">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

### <a name="creating-new-items-new-item"></a><span data-ttu-id="69412-107">Создание новых элементов (New-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-107">Creating New Items (New-Item)</span></span>

<span data-ttu-id="69412-108">Чтобы создать элемент в файловой системе, используйте командлет **New-Item**.</span><span class="sxs-lookup"><span data-stu-id="69412-108">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="69412-109">Включите параметр **Path** с путем к элементу и параметр **ItemType** сo значением file или directory.</span><span class="sxs-lookup"><span data-stu-id="69412-109">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="69412-110">Например, чтобы создать каталог с именем "New.Directory" в каталоге C:\\Temp, введите:</span><span class="sxs-lookup"><span data-stu-id="69412-110">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="69412-111">Чтобы создать файл, измените значение параметра **ItemType** на file.</span><span class="sxs-lookup"><span data-stu-id="69412-111">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="69412-112">Например, чтобы создать файл с именем file1.txt в каталоге New.Directory, введите:</span><span class="sxs-lookup"><span data-stu-id="69412-112">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="69412-113">Тот же метод можно использовать для создания нового раздела реестра.</span><span class="sxs-lookup"><span data-stu-id="69412-113">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="69412-114">На самом деле, раздел реестра создать проще, так как единственный тип элементов в реестре Windows — это раздел.</span><span class="sxs-lookup"><span data-stu-id="69412-114">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="69412-115">(Записи реестра — это *свойства* элементов.) Например, чтобы создать ключ с именем _Test в подразделе CurrentVersion, введите:</span><span class="sxs-lookup"><span data-stu-id="69412-115">(Registry entries are item *properties*.) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="69412-116">При вводе пути реестра не забудьте добавить двоеточие (**:**) в имена дисков Windows PowerShell — HKLM: и HKCU:.</span><span class="sxs-lookup"><span data-stu-id="69412-116">When typing a registry path, be sure to include the colon (**:**) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="69412-117">Без двоеточия Windows PowerShell не распознает имена дисков в пути.</span><span class="sxs-lookup"><span data-stu-id="69412-117">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

### <a name="why-registry-values-are-not-items"></a><span data-ttu-id="69412-118">Причины, по которым значения реестра не являются элементами</span><span class="sxs-lookup"><span data-stu-id="69412-118">Why Registry Values are not Items</span></span>

<span data-ttu-id="69412-119">При использовании командлета **Get-ChildItem** для поиска элементов в разделе реестра вы не увидите фактических записей реестра или их значений.</span><span class="sxs-lookup"><span data-stu-id="69412-119">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="69412-120">Например, раздел реестра **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** обычно содержит записи реестра, представляющие приложения, которые выполняются при запуске системы.</span><span class="sxs-lookup"><span data-stu-id="69412-120">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="69412-121">Однако при использовании **Get-ChildItem** для поиска дочерних элементов в разделе отобразится только подраздел или раздел **OptionalComponents**:</span><span class="sxs-lookup"><span data-stu-id="69412-121">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="69412-122">Хотя удобнее использовать записи реестра как элементы, невозможно указать путь к записи реестра способом, гарантирующим его уникальность.</span><span class="sxs-lookup"><span data-stu-id="69412-122">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="69412-123">Нотация пути не различает подраздел реестра с именем **Run** и запись реестра **(Default)** в подразделе **Run**.</span><span class="sxs-lookup"><span data-stu-id="69412-123">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="69412-124">Кроме того, так как имена записей реестра могут содержать обратную косую черту (**\\**), если записи реестра были элементами, то нотацию пути невозможно использовать для различения записи реестра с именем **Windows\\CurrentVersion\\Run** от подраздела, расположенного по этому пути.</span><span class="sxs-lookup"><span data-stu-id="69412-124">Furthermore, because registry entry names can contain the backslash character (**\\**), if regsitry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

### <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="69412-125">Переименование существующих элементов (Rename-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-125">Renaming Existing Items (Rename-Item)</span></span>

<span data-ttu-id="69412-126">Чтобы изменить имя файла или папки, используйте командлет **Rename-Item**.</span><span class="sxs-lookup"><span data-stu-id="69412-126">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="69412-127">Следующая команда изменяет имя файла **file1.txt** на **fileOne.txt**.</span><span class="sxs-lookup"><span data-stu-id="69412-127">The following command changes the name of the **file1.txt** file to **fileOne.txt**.</span></span>

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="69412-128">Командлет **Rename-Item** может изменить имя файла или папки, но не может переместить элемент.</span><span class="sxs-lookup"><span data-stu-id="69412-128">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="69412-129">Произойдет сбой следующей команды, так как она попытается переместить файл из каталога New.Directory во временный каталог.</span><span class="sxs-lookup"><span data-stu-id="69412-129">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a><span data-ttu-id="69412-130">Перемещение элементов (Move-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-130">Moving Items (Move-Item)</span></span>

<span data-ttu-id="69412-131">Чтобы переместить файл или папку, используйте командлет **Move-Item**.</span><span class="sxs-lookup"><span data-stu-id="69412-131">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="69412-132">Например, следующая команда перемещает каталог New.Directory из каталога C:\\temp в корень диска C:.</span><span class="sxs-lookup"><span data-stu-id="69412-132">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="69412-133">Чтобы убедиться, что элемент перемещен, включите параметр **PassThru** командлета **Move-Item**.</span><span class="sxs-lookup"><span data-stu-id="69412-133">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="69412-134">Без **Passthru** командлет **Move-Item** не отображает результаты.</span><span class="sxs-lookup"><span data-stu-id="69412-134">Without **Passthru**, the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a><span data-ttu-id="69412-135">Копирование элементов (Copy-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-135">Copying Items (Copy-Item)</span></span>

<span data-ttu-id="69412-136">Если вы знакомы с операциями копирования в других оболочках, поведение командлета **Copy-Item** в Windows PowerShell может показаться нестандартным.</span><span class="sxs-lookup"><span data-stu-id="69412-136">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="69412-137">При копировании элемента из одного расположения в другое командлет Copy-Item не копирует его содержимое по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="69412-137">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="69412-138">Например, при копировании каталога **New.Directory** с диска C: в каталог C:\\temp команда выполняется, но файлы в каталоге New.Directory не копируются.</span><span class="sxs-lookup"><span data-stu-id="69412-138">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="69412-139">Если отобразить содержимое **C:\\temp\\New.Directory**, там не будет файлов:</span><span class="sxs-lookup"><span data-stu-id="69412-139">If you display the contents of **C:\\temp\\New.Directory**, you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="69412-140">Почему командлет **Copy-Item** не копирует содержимое в новое расположение?</span><span class="sxs-lookup"><span data-stu-id="69412-140">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="69412-141">Командлет **Copy-Item** предполагалось использовать как универсальный. Он не предназначен для простого копирования файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="69412-141">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="69412-142">Кроме того, даже при копировании файлов и папок может потребоваться копировать только контейнер без элементов внутри него.</span><span class="sxs-lookup"><span data-stu-id="69412-142">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="69412-143">Чтобы скопировать все содержимое папки, включите параметр **Recurse** командлета **Copy-Item** в команду.</span><span class="sxs-lookup"><span data-stu-id="69412-143">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="69412-144">Если вы уже скопировали каталог без содержимого, добавьте параметр **Force**, который позволит перезаписать пустую папку.</span><span class="sxs-lookup"><span data-stu-id="69412-144">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

### <a name="deleting-items-remove-item"></a><span data-ttu-id="69412-145">Удаление элементов (Remove-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-145">Deleting Items (Remove-Item)</span></span>

<span data-ttu-id="69412-146">Чтобы удалить файлы и папки, используйте командлет **Remove-Item**.</span><span class="sxs-lookup"><span data-stu-id="69412-146">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="69412-147">Командлеты Windows PowerShell, например **Remove-Item**, которые могут вносить значительные и необратимые изменения, часто будут запрашивать подтверждение при вводе команд.</span><span class="sxs-lookup"><span data-stu-id="69412-147">Windows PowerShell cmdlets, such as **Remove-Item**, that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="69412-148">Например, при попытке удалить папку **New.Directory** вам предлагается подтвердить команду, так как папка содержит файлы:</span><span class="sxs-lookup"><span data-stu-id="69412-148">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="69412-149">Так как ответ **Да** является ответом по умолчанию, чтобы удалить папку вместе файлами, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="69412-149">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="69412-150">Чтобы удалить папку без подтверждения, используйте параметр **-Recurse**.</span><span class="sxs-lookup"><span data-stu-id="69412-150">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a><span data-ttu-id="69412-151">Выполнение элементов (Invoke-Item)</span><span class="sxs-lookup"><span data-stu-id="69412-151">Executing Items (Invoke-Item)</span></span>

<span data-ttu-id="69412-152">Windows PowerShell использует командлет **Invoke-Item** для выполнения действия по умолчанию для файла или папки.</span><span class="sxs-lookup"><span data-stu-id="69412-152">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="69412-153">Это действие по умолчанию определяется обработчиком приложений по умолчанию в реестре; эффект будет таким же, что и при двойном щелчке элемента в проводнике.</span><span class="sxs-lookup"><span data-stu-id="69412-153">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="69412-154">Предположим, вы запускаете следующую команду:</span><span class="sxs-lookup"><span data-stu-id="69412-154">For example, suppose you run the following command:</span></span>

```powershell
Invoke-Item C:\WINDOWS
```

<span data-ttu-id="69412-155">Появится окно проводника, расположенного в C:\\Windows, как если бы вы дважды щелкнули папку C:\\Windows.</span><span class="sxs-lookup"><span data-stu-id="69412-155">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="69412-156">При вызове файла **Boot.ini** в системе, предшествующей Windows Vista:</span><span class="sxs-lookup"><span data-stu-id="69412-156">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```powershell
Invoke-Item C:\boot.ini
```

<span data-ttu-id="69412-157">Если тип INI-файла связан с Блокнотом, файл boot.ini будет открыт в Блокноте.</span><span class="sxs-lookup"><span data-stu-id="69412-157">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>