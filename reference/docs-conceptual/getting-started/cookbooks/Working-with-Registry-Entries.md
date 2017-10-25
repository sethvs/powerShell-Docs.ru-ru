---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Работа с записями реестра"
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: 039203a1a6549d4ba33424a278e4803a5e143d4d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="4b93b-103">Работа с записями реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-103">Working with Registry Entries</span></span>
<span data-ttu-id="4b93b-104">Так как записи реестра являются свойствами разделов и их невозможно открыть напрямую, при работе с ними необходимо использовать немного другой подход.</span><span class="sxs-lookup"><span data-stu-id="4b93b-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

### <a name="listing-registry-entries"></a><span data-ttu-id="4b93b-105">Создание списков записей реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-105">Listing Registry Entries</span></span>
<span data-ttu-id="4b93b-106">Существует несколько способов просмотра реестра.</span><span class="sxs-lookup"><span data-stu-id="4b93b-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="4b93b-107">Самый простой — получить имена свойств, связанные с разделом.</span><span class="sxs-lookup"><span data-stu-id="4b93b-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="4b93b-108">Например, чтобы увидеть имена записей в разделе реестра **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, используйте **Get-Item**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-108">For example, to see the names of the entries in the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, use **Get-Item**.</span></span> <span data-ttu-id="4b93b-109">Разделы реестра содержат свойство с универсальным именем Property, которое является списком записей реестра в разделе.</span><span class="sxs-lookup"><span data-stu-id="4b93b-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span> <span data-ttu-id="4b93b-110">Следующая команда выбирает свойство Property и расширяет элементы так, чтобы они отображались в списке:</span><span class="sxs-lookup"><span data-stu-id="4b93b-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="4b93b-111">Чтобы просмотреть записи реестра в более удобочитаемой форме, используйте **Get-ItemProperty**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-111">To view the registry entries in a more readable form, use **Get-ItemProperty**:</span></span>

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

<span data-ttu-id="4b93b-112">Все свойства Windows PowerShell раздела имеют префиксы PS, например **PSPath**, **PSParentPath**, **PSChildName** и **PSProvider**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="4b93b-113">Для ссылки на текущее расположение можно использовать нотацию "**.**".</span><span class="sxs-lookup"><span data-stu-id="4b93b-113">You can use the "**.**" notation for referring to the current location.</span></span> <span data-ttu-id="4b93b-114">**Set-Location** можно использовать, чтобы изначально изменить значение на контейнер реестра **CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-114">You can use **Set-Location** to change to the **CurrentVersion** registry container first:</span></span>

```
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="4b93b-115">Кроме того, можно использовать встроенный диск HKLM PSDrive с **Set-Location**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-115">Alternatively, you can use the built-in HKLM PSDrive with **Set-Location**:</span></span>

```
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="4b93b-116">Затем можно использовать нотацию "**.**" для текущего расположения, чтобы перечислить свойства без указания полного пути:</span><span class="sxs-lookup"><span data-stu-id="4b93b-116">You can then use the "**.**" notation for the current location to list the properties without specifying a full path:</span></span>

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="4b93b-117">Расширение пути работает так же, как и в файловой системе, поэтому в этом расположении можно получить перечисление **ItemProperty** для **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** с помощью **Get-ItemProperty -Path ..\\Help**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** by using **Get-ItemProperty -Path ..\\Help**.</span></span>

### <a name="getting-a-single-registry-entry"></a><span data-ttu-id="4b93b-118">Получение одной записи реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-118">Getting a Single Registry Entry</span></span>
<span data-ttu-id="4b93b-119">Если необходимо получить конкретную запись в разделе реестра, можно использовать один из нескольких возможных подходов.</span><span class="sxs-lookup"><span data-stu-id="4b93b-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="4b93b-120">В этом примере выполняется поиск значения **DevicePath** в **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-120">This example finds the value of **DevicePath** in **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span>

<span data-ttu-id="4b93b-121">Используйте вместе с **Get-ItemProperty** параметр **Path**, чтобы указать имя раздела, и параметр **Name**, чтобы указать имя записи **DevicePath**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-121">Using **Get-ItemProperty**, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

<span data-ttu-id="4b93b-122">Эта команда возвращает стандартные свойства Windows PowerShell, а также свойство **DevicePath**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="4b93b-123">Хотя **Get-ItemProperty** содержит параметры **Filter**, **Include** и **Exclude**, их невозможно использовать для фильтрации по имени свойства.</span><span class="sxs-lookup"><span data-stu-id="4b93b-123">Although **Get-ItemProperty** has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="4b93b-124">Эти параметры относятся в разделам реестра (путям элементов), а не к записям реестра (свойствам элементов).</span><span class="sxs-lookup"><span data-stu-id="4b93b-124">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="4b93b-125">Другой вариант — использовать средство командной строки Reg.exe.</span><span class="sxs-lookup"><span data-stu-id="4b93b-125">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="4b93b-126">Для получения справки по reg.exe введите **reg.exe /?**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-126">For help with reg.exe, type **reg.exe /?**</span></span> <span data-ttu-id="4b93b-127">в командной строке.</span><span class="sxs-lookup"><span data-stu-id="4b93b-127">at a command prompt.</span></span> <span data-ttu-id="4b93b-128">Чтобы найти запись DevicePath, используйте reg.exe, как показано в следующей команде:</span><span class="sxs-lookup"><span data-stu-id="4b93b-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="4b93b-129">Также можно использовать объект **WshShell COM**, чтобы найти некоторые записи реестра, хотя этот метод не работает с большими двоичными данными или именами записей реестра, включающими такие символы, как "\\".</span><span class="sxs-lookup"><span data-stu-id="4b93b-129">You can also use the **WshShell COM** object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="4b93b-130">Добавьте имя свойства с разделителем "\\" в путь элемента:</span><span class="sxs-lookup"><span data-stu-id="4b93b-130">Append the property name to the item path with a \\ separator:</span></span>

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a><span data-ttu-id="4b93b-131">Создание новых записей реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-131">Creating New Registry Entries</span></span>
<span data-ttu-id="4b93b-132">Чтобы добавить новую запись реестра с именем PowerShellPath в раздел **CurrentVersion**, используйте **New-ItemProperty** с путем к разделу, именем записи и значением записи.</span><span class="sxs-lookup"><span data-stu-id="4b93b-132">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use **New-ItemProperty** with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="4b93b-133">В этом примере использовано значение переменной Windows PowerShell **$PSHome**, в которой хранится путь к каталогу установки для Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b93b-133">For this example, we will take the value of the Windows PowerShell variable **$PSHome**, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="4b93b-134">Вы можете добавить новую запись в раздел с помощью следующей команды, и команда также вернет сведения о новой записи:</span><span class="sxs-lookup"><span data-stu-id="4b93b-134">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

<span data-ttu-id="4b93b-135">Значение **PropertyType** должно быть именем элемента перечисления **Microsoft.Win32.RegistryValueKind** из следующей таблицы:</span><span class="sxs-lookup"><span data-stu-id="4b93b-135">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="4b93b-136">Значение PropertyType</span><span class="sxs-lookup"><span data-stu-id="4b93b-136">PropertyType Value</span></span>|<span data-ttu-id="4b93b-137">Значение</span><span class="sxs-lookup"><span data-stu-id="4b93b-137">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="4b93b-138">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="4b93b-138">Binary</span></span>|<span data-ttu-id="4b93b-139">Двоичные данные</span><span class="sxs-lookup"><span data-stu-id="4b93b-139">Binary data</span></span>|
|<span data-ttu-id="4b93b-140">DWord</span><span class="sxs-lookup"><span data-stu-id="4b93b-140">DWord</span></span>|<span data-ttu-id="4b93b-141">Число, которое является допустимым UInt32</span><span class="sxs-lookup"><span data-stu-id="4b93b-141">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="4b93b-142">ExpandString</span><span class="sxs-lookup"><span data-stu-id="4b93b-142">ExpandString</span></span>|<span data-ttu-id="4b93b-143">Строка, которая может содержать динамически раскрывающиеся переменные среды</span><span class="sxs-lookup"><span data-stu-id="4b93b-143">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="4b93b-144">MultiString</span><span class="sxs-lookup"><span data-stu-id="4b93b-144">MultiString</span></span>|<span data-ttu-id="4b93b-145">Многострочная строка</span><span class="sxs-lookup"><span data-stu-id="4b93b-145">A multiline string</span></span>|
|<span data-ttu-id="4b93b-146">Строка</span><span class="sxs-lookup"><span data-stu-id="4b93b-146">String</span></span>|<span data-ttu-id="4b93b-147">Любое строковое значение</span><span class="sxs-lookup"><span data-stu-id="4b93b-147">Any string value</span></span>|
|<span data-ttu-id="4b93b-148">QWord</span><span class="sxs-lookup"><span data-stu-id="4b93b-148">QWord</span></span>|<span data-ttu-id="4b93b-149">8 байтов двоичных данных</span><span class="sxs-lookup"><span data-stu-id="4b93b-149">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="4b93b-150">Запись реестра можно добавить в несколько расположений, указав массив значений для параметра **Path**:</span><span class="sxs-lookup"><span data-stu-id="4b93b-150">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

<span data-ttu-id="4b93b-151">Кроме того, можно перезаписать имеющееся значение записи реестра, добавив параметр **Force** в любую команду **New-ItemProperty**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-151">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any **New-ItemProperty** command.</span></span>

### <a name="renaming-registry-entries"></a><span data-ttu-id="4b93b-152">Переименование записей реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-152">Renaming Registry Entries</span></span>
<span data-ttu-id="4b93b-153">Чтобы переименовать запись **PowerShellPath** на PSHome, используйте **Rename-ItemProperty**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-153">To rename the **PowerShellPath** entry to "PSHome," use **Rename-ItemProperty**:</span></span>

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="4b93b-154">Чтобы отобразить переименованное значение, добавьте параметр **PassThru** в команду.</span><span class="sxs-lookup"><span data-stu-id="4b93b-154">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a><span data-ttu-id="4b93b-155">Удаление записей реестра</span><span class="sxs-lookup"><span data-stu-id="4b93b-155">Deleting Registry Entries</span></span>
<span data-ttu-id="4b93b-156">Чтобы удалить записи реестра PSHome и PowerShellPath, используйте **Remove-ItemProperty**.</span><span class="sxs-lookup"><span data-stu-id="4b93b-156">To delete both the PSHome and PowerShellPath registry entries, use **Remove-ItemProperty**:</span></span>

```
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```

