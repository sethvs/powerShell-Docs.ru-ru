---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Управление дисками Windows PowerShell
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: cfc5418e9d2efb1a786817e1b941d75e22291742
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="managing-windows-powershell-drives"></a><span data-ttu-id="f1f03-103">Управление дисками Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1f03-103">Managing Windows PowerShell Drives</span></span>

<span data-ttu-id="f1f03-104">*Диск Windows PowerShell* — это расположение хранилища данных, доступ к которому можно получить так же, как к диску файловой системы в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-104">A *Windows PowerShell drive* is a data store location that you can access like a file system drive in Windows PowerShell.</span></span> <span data-ttu-id="f1f03-105">Поставщики Windows PowerShell создают несколько дисков, например диски файловой системы (включая C: и D:), диски реестра (HKCU: и HKLM:) и диск сертификата (Cert:), а вы можете создать собственные диски Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-105">The Windows PowerShell providers create some drives for you, such as the file system drives (including C: and D:), the registry drives (HKCU: and HKLM:), and the certificate drive (Cert:), and you can create your own Windows PowerShell drives.</span></span> <span data-ttu-id="f1f03-106">Эти диски очень полезны, но они доступны только в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-106">These drives are very useful, but they are available only within Windows PowerShell.</span></span> <span data-ttu-id="f1f03-107">К ним невозможно получить доступ с помощью других средств Windows, например проводника или Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="f1f03-107">You cannot access them by using other Windows tools, such as File Explorer or Cmd.exe.</span></span>

<span data-ttu-id="f1f03-108">Windows PowerShell использует существительное **PSDrive** для команд, которые работают на дисках Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-108">Windows PowerShell uses the noun, **PSDrive**, for commands that work with Windows PowerShell drives.</span></span> <span data-ttu-id="f1f03-109">Для получения списка дисков Windows PowerShell в сеансе Windows PowerShell используйте командлет **Get-PSDrive**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-109">For a list of the Windows PowerShell drives in your Windows PowerShell session, use the **Get-PSDrive** cmdlet.</span></span>

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

<span data-ttu-id="f1f03-110">Хотя отображение дисков в списке зависит от дисков в вашей системе, список будет выглядеть аналогично выходным данным команды **Get-PSDrive**, показанной выше.</span><span class="sxs-lookup"><span data-stu-id="f1f03-110">Although the drives in the display vary with the drives on your system, the listing will look similar to the output of the **Get-PSDrive** command shown above.</span></span>

<span data-ttu-id="f1f03-111">Диски файловой системы являются подмножеством дисков Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-111">File system drives are a subset of the Windows PowerShell drives.</span></span> <span data-ttu-id="f1f03-112">Их можно идентифицировать по записи FileSystem в столбце "Поставщик".</span><span class="sxs-lookup"><span data-stu-id="f1f03-112">You can identify the file system drives by the FileSystem entry in the Provider column.</span></span> <span data-ttu-id="f1f03-113">(Диски файловой системы в Windows PowerShell поддерживаются поставщиком FileSystem Windows PowerShell.)</span><span class="sxs-lookup"><span data-stu-id="f1f03-113">(The file system drives in Windows PowerShell are supported by the Windows PowerShell FileSystem provider.)</span></span>

<span data-ttu-id="f1f03-114">Чтобы просмотреть синтаксис командлета **Get-PSDrive**, введите команду **Get-Command** с параметром **Syntax**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-114">To see the syntax of the **Get-PSDrive** cmdlet, type a **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

<span data-ttu-id="f1f03-115">Параметр **PSProvider** позволит отобразить только диски Windows PowerShell, поддерживаемые конкретным поставщиком.</span><span class="sxs-lookup"><span data-stu-id="f1f03-115">The **PSProvider** parameter lets you display only the Windows PowerShell drives that are supported by a particular provider.</span></span> <span data-ttu-id="f1f03-116">Например, чтобы отобразить только те диски Windows PowerShell, которые поддерживаются поставщиком FileSystem Windows PowerShell, введите команду **Get-PSDrive** с параметром **PSProvider** и значением **FileSystem**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-116">For example, to display only the Windows PowerShell drives that are supported by the Windows PowerShell FileSystem provider, type a **Get-PSDrive** command with the **PSProvider** parameter and the **FileSystem** value:</span></span>

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

<span data-ttu-id="f1f03-117">Чтобы просмотреть диски Windows PowerShell, представляющие кусты реестра, используйте параметр **PSProvider** для отображения только тех дисков Windows PowerShell, которые поддерживаются поставщиком реестра Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1f03-117">To view the Windows PowerShell drives that represent registry hives, use the **PSProvider** parameter to display only the Windows PowerShell drives that are supported by the Windows PowerShell Registry provider:</span></span>

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

<span data-ttu-id="f1f03-118">С дисками Windows PowerShell также можно использовать стандартные командлеты расположения:</span><span class="sxs-lookup"><span data-stu-id="f1f03-118">You can also use the standard Location cmdlets with the Windows PowerShell drives:</span></span>

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a><span data-ttu-id="f1f03-119">Добавление новых дисков Windows PowerShell (New-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="f1f03-119">Adding New Windows PowerShell Drives (New-PSDrive)</span></span>

<span data-ttu-id="f1f03-120">Добавить собственные диски Windows PowerShell можно с помощью команды **New-PSDrive**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-120">You can add your own Windows PowerShell drives by using the **New-PSDrive** command.</span></span> <span data-ttu-id="f1f03-121">Чтобы получить синтаксис для команды **New-PSDrive**, введите команду **Get-Command** с параметром **Syntax**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-121">To get the syntax for the **New-PSDrive** command, enter the **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

<span data-ttu-id="f1f03-122">Чтобы создать новый диск Windows PowerShell, необходимо указать три параметра:</span><span class="sxs-lookup"><span data-stu-id="f1f03-122">To create a new Windows PowerShell drive, you must supply three parameters:</span></span>

- <span data-ttu-id="f1f03-123">имя диска (можно использовать любое допустимое имя Windows PowerShell);</span><span class="sxs-lookup"><span data-stu-id="f1f03-123">A name for the drive (you can use any valid Windows PowerShell name)</span></span>

- <span data-ttu-id="f1f03-124">PSProvider (используйте FileSystem для расположений файловой системы и Registry для расположений реестра);</span><span class="sxs-lookup"><span data-stu-id="f1f03-124">The PSProvider (use "FileSystem" for file system locations and "Registry" for registry locations)</span></span>

- <span data-ttu-id="f1f03-125">корень, т. е. путь к корню нового диска.</span><span class="sxs-lookup"><span data-stu-id="f1f03-125">The root, that is, the path to the root of the new drive</span></span>

<span data-ttu-id="f1f03-126">Например, можно создать диск с именем "Office", который сопоставляется с папкой, содержащей приложения Microsoft Office на компьютере, такой как **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-126">For example, you can create a drive named "Office" that is mapped to the folder that contains the Microsoft Office applications on your computer, such as **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span></span> <span data-ttu-id="f1f03-127">Чтобы создать диск, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f1f03-127">To create the drive, type the following command:</span></span>

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> <span data-ttu-id="f1f03-128">Обычно пути не зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="f1f03-128">In general, paths are not case-sensitive.</span></span>

<span data-ttu-id="f1f03-129">Ссылка на новый диск Windows PowerShell, как и на все диски Windows PowerShell, указывается по его имени, за которым следует двоеточие (**:**).</span><span class="sxs-lookup"><span data-stu-id="f1f03-129">You refer to the new Windows PowerShell drive as you do all Windows PowerShell drives -- by its name followed by a colon (**:**).</span></span>

<span data-ttu-id="f1f03-130">Диск Windows PowerShell может упростить множество задач.</span><span class="sxs-lookup"><span data-stu-id="f1f03-130">A Windows PowerShell drive can make many tasks much simpler.</span></span> <span data-ttu-id="f1f03-131">Например, некоторые наиболее важные разделы в реестре Windows содержат слишком длинные пути, что делает их громоздкими и сложными для запоминания.</span><span class="sxs-lookup"><span data-stu-id="f1f03-131">For example, some of the most important keys in the Windows registry have extremely long paths, making them cumbersome to access and difficult to remember.</span></span> <span data-ttu-id="f1f03-132">Критически важные сведения о конфигурации находятся в разделе **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-132">Critical configuration information resides under **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span> <span data-ttu-id="f1f03-133">Чтобы просмотреть и изменить элементы в разделе реестра CurrentVersion, можно создать диск Windows PowerShell, корень которого находится в этом разделе, введя:</span><span class="sxs-lookup"><span data-stu-id="f1f03-133">To view and change items in the CurrentVersion registry key, you can create a Windows PowerShell drive that is rooted in that key by typing:</span></span>

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

<span data-ttu-id="f1f03-134">После этого можно изменить расположение на диск **cvkey:** (как и для любого другого диска):</span><span class="sxs-lookup"><span data-stu-id="f1f03-134">You can then change location to the **cvkey:** drive as you would any other drive:``</span></span>

`PS> cd cvkey:`

<span data-ttu-id="f1f03-135">или:</span><span class="sxs-lookup"><span data-stu-id="f1f03-135">or:</span></span>

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

<span data-ttu-id="f1f03-136">Командлет New-PsDrive добавляет новый диск только в текущий сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-136">The New-PsDrive cmdlet adds the new drive only to the current Windows PowerShell session.</span></span> <span data-ttu-id="f1f03-137">Если закрыть окно Windows PowerShell, новый диск будет потерян.</span><span class="sxs-lookup"><span data-stu-id="f1f03-137">If you close the Windows PowerShell window, the new drive is lost.</span></span> <span data-ttu-id="f1f03-138">Чтобы сохранить диск Windows PowerShell, используйте командлет Export-Console для экспорта текущего сеанса Windows PowerShell, а затем используйте параметр **PSConsoleFile** PowerShell.exe для импорта.</span><span class="sxs-lookup"><span data-stu-id="f1f03-138">To save a Windows PowerShell drive, use the Export-Console cmdlet to export the current Windows PowerShell session, and then use the PowerShell.exe **PSConsoleFile** parameter to import it.</span></span> <span data-ttu-id="f1f03-139">Также можно добавить новый диск в профиль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-139">Or, add the new drive to your Windows PowerShell profile.</span></span>

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a><span data-ttu-id="f1f03-140">Удаление дисков Windows PowerShell (Remove-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="f1f03-140">Deleting Windows PowerShell Drives (Remove-PSDrive)</span></span>

<span data-ttu-id="f1f03-141">Диски из Windows PowerShell можно удалить, используя командлет **Remove-PSDrive**.</span><span class="sxs-lookup"><span data-stu-id="f1f03-141">You can delete drives from Windows PowerShell by using the **Remove-PSDrive** cmdlet.</span></span> <span data-ttu-id="f1f03-142">Командлет **Remove-PSDrive** прост в использовании. Чтобы удалить определенный диск Windows PowerShell, необходимо только указать имя диска Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1f03-142">The **Remove-PSDrive** cmdlet is easy to use; to delete a specific Windows PowerShell drive, you just supply the Windows PowerShell drive name.</span></span>

<span data-ttu-id="f1f03-143">Например, если вы добавили диск Windows PowerShell **Office:**, как показано в статье **New-PSDrive**, можно удалить его, введя:</span><span class="sxs-lookup"><span data-stu-id="f1f03-143">For example, if you added the **Office:** Windows PowerShell drive, as shown in the **New-PSDrive** topic, you can delete it by typing:</span></span>

```powershell
Remove-PSDrive -Name Office
```

<span data-ttu-id="f1f03-144">Чтобы удалить диск Windows PowerShell **cvkey:**, также показанный в статье **New-PSDrive**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f1f03-144">To delete the **cvkey:** Windows PowerShell drive, also shown in the **New-PSDrive** topic, use the following command:</span></span>

```powershell
Remove-PSDrive -Name cvkey
```

<span data-ttu-id="f1f03-145">Удалить диск Windows PowerShell легко, но его невозможно удалить, если он открыт.</span><span class="sxs-lookup"><span data-stu-id="f1f03-145">It's easy to delete a Windows PowerShell drive, but you can't delete it while you are in the drive.</span></span> <span data-ttu-id="f1f03-146">Например:</span><span class="sxs-lookup"><span data-stu-id="f1f03-146">For example:</span></span>

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a><span data-ttu-id="f1f03-147">Добавление и удаление дисков за пределами Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1f03-147">Adding and Removing Drives Outside Windows PowerShell</span></span>

<span data-ttu-id="f1f03-148">Windows PowerShell обнаруживает диски файловой системы, которые добавляются или удаляются в Windows, включая сопоставленные сетевые диски, подключенные USB-накопители и удаленные диски, с помощью команды **net use** или методов **WScript.Network MapNetworkDrive** и **RemoveNetworkDrive** сценария сервера сценариев Windows (WSH).</span><span class="sxs-lookup"><span data-stu-id="f1f03-148">Windows PowerShell detects file system drives that are added or removed in Windows, including network drives that are mapped, USB drives that are attached, and drives that are deleted by using either the **net use** command or the **WScript.NetworkMapNetworkDrive** and **RemoveNetworkDrive** methods from a Windows Script Host (WSH) script.</span></span>