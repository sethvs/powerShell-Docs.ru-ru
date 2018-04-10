---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Работа с программами установки программного обеспечения
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: bb97ad37c4295351c0fc2e3c6e1209c8dd673f06
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="working-with-software-installations"></a><span data-ttu-id="cd9f0-103">Работа с программами установки программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="cd9f0-103">Working with Software Installations</span></span>

<span data-ttu-id="cd9f0-104">Доступ к приложениям, использующим установщик Windows, можно получить в классе **Win32_Product** WMI, но не все современные приложения используют установщик Windows.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-104">Applications that are designed to use Windows Installer can be accessed through WMI's **Win32_Product** class, but not all applications in use today use the Windows Installer.</span></span> <span data-ttu-id="cd9f0-105">Так как установщик Windows предоставляет самый широкий ряд стандартных методов работы с устанавливаемыми приложениями, обратим внимание в первую очередь на эти приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-105">Because the Windows Installer provides the widest range of standard techniques for working with installable applications, we will focus primarily on those applications.</span></span> <span data-ttu-id="cd9f0-106">Установщик Windows обычно не управляет приложениями, использующими другие процедуры установки.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-106">Applications that use alternate setup routines will generally not be managed by the Windows Installer.</span></span> <span data-ttu-id="cd9f0-107">Конкретные техники работы с этими приложениями будут зависеть от программного обеспечения установщика и решений, принятых разработчиком приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-107">Specific techniques for working with those applications will depend on the installer software and decisions made by the application developer.</span></span>

> [!NOTE]
> <span data-ttu-id="cd9f0-108">Приложения, которые устанавливаются путем копирования файлов приложения на компьютер, обычно не могут управляться методами, описанными здесь.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-108">Applications that are installed by copying the application files to the computer usually cannot be managed by using techniques discussed here.</span></span> <span data-ttu-id="cd9f0-109">Вы можете управлять этими приложениями, как файлами и папками, с помощью способов, приведенных в разделе "Работа с файлами и папками".</span><span class="sxs-lookup"><span data-stu-id="cd9f0-109">You can manage these applications as files and folders by using the techniques discussed in the "Working With Files and Folders" section.</span></span>

### <a name="listing-windows-installer-applications"></a><span data-ttu-id="cd9f0-110">Создание списков приложений установщика Windows</span><span class="sxs-lookup"><span data-stu-id="cd9f0-110">Listing Windows Installer Applications</span></span>

<span data-ttu-id="cd9f0-111">Чтобы создать список приложений, установленных с помощью установщика Windows в локальной или удаленной системе, используйте следующий простой запрос WMI:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-111">To list the applications installed with the Windows Installer on a local or remote system, use the following simple WMI query:</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .

IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

<span data-ttu-id="cd9f0-112">Чтобы отобразить все свойства объекта Win32_Product, используйте параметр Properties командлетов форматирования, например Format-List, со значением \* (все).</span><span class="sxs-lookup"><span data-stu-id="cd9f0-112">To display all of the properties of the Win32_Product object to the display, use the Properties parameter of the formatting cmdlets, such as the Format-List cmdlet, with a value of \* (all).</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *

Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

<span data-ttu-id="cd9f0-113">Можно также использовать параметр **Get-WmiObject Filter**, чтобы выбрать только Microsoft .NET Framework 2.0.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-113">Or, you could use the **Get-WmiObject Filter** parameter to select only Microsoft .NET Framework 2.0.</span></span> <span data-ttu-id="cd9f0-114">Так как фильтр, использованный в этой команде, является фильтром WMI, он использует синтаксис языка запросов WMI (WQL), а не синтаксис Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-114">Because the filter used in this command is a WMI filter, it uses WMI Query Language (WQL) syntax, not Windows PowerShell syntax.</span></span> <span data-ttu-id="cd9f0-115">Вместо этого:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-115">Instead,:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

<span data-ttu-id="cd9f0-116">Обратите внимание, что в запросах WQL часто используются символы (например, пробелы или знаки равенства), которые имеют особое значение в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-116">Note that WQL queries frequently use characters, such as spaces or equal signs, that have a special meaning in Windows PowerShell.</span></span> <span data-ttu-id="cd9f0-117">По этой причине целесообразно всегда заключать значение параметра фильтра в кавычки.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-117">For this reason, it is prudent to always enclose the value of the Filter parameter in quotation marks.</span></span> <span data-ttu-id="cd9f0-118">Кроме того, можно использовать escape-символ Windows PowerShell — обратный апостроф (\`), хотя это может ухудшить удобочитаемость.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-118">You can also use the Windows PowerShell escape character, a backtick (\`), although it may not improve readability.</span></span> <span data-ttu-id="cd9f0-119">Следующая команда эквивалентна предыдущей и возвращает те же результаты, но использует обратный апостроф в качестве escape-символа для специальных знаков вместо того, чтобы заключать в кавычки всю строку фильтра.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-119">The following command is equivalent to the previous command and returns the same results, but uses the backtick to escape special characters, instead of quoting the entire filter string.</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

<span data-ttu-id="cd9f0-120">Чтобы создать список только интересующих вас свойств, используйте параметр Property командлетов форматирования.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-120">To list only the properties that interest you, use the Property parameter of the formatting cmdlets to list the desired properties.</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

<span data-ttu-id="cd9f0-121">Наконец, чтобы найти имена только установленных приложений, упростите выходные данные с помощью оператора **Format-Wide**:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-121">Finally, to find only the names of installed applications, a simple **Format-Wide** statement simplifies the output:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

<span data-ttu-id="cd9f0-122">Несмотря на то что теперь нам известно несколько способов поиска приложений, использовавших установщик Windows, другие приложения не были рассмотрены.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-122">Although we now have several ways to look at applications that used the Windows Installer for installation, we have not considered other applications.</span></span> <span data-ttu-id="cd9f0-123">Так как большинство стандартных приложений регистрируют программу удаления в Windows, с ними можно работать локально, в реестре Windows.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-123">Because most standard applications register their uninstaller with Windows, we can work with those locally by finding them in the Windows registry.</span></span>

### <a name="listing-all-uninstallable-applications"></a><span data-ttu-id="cd9f0-124">Создание списка всех удаленных приложений</span><span class="sxs-lookup"><span data-stu-id="cd9f0-124">Listing All Uninstallable Applications</span></span>

<span data-ttu-id="cd9f0-125">Несмотря на то что не существует гарантированного способа найти все приложения в системе, можно найти все программы со списками, отображенными в диалоговом окне "Добавление или удаление программ".</span><span class="sxs-lookup"><span data-stu-id="cd9f0-125">Although there is no guaranteed way to find every application on a system, it is possible to find all programs with listings displayed in the Add or Remove Programs dialog box.</span></span> <span data-ttu-id="cd9f0-126">В окне "Добавление или удаление программ" выполняется поиск этих приложений в следующем разделе реестра:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-126">Add or Remove Programs finds these applications in the following registry key:</span></span>

<span data-ttu-id="cd9f0-127">**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-127">**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.</span></span>

<span data-ttu-id="cd9f0-128">В этом разделе также можно найти приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-128">We can also examine this key to find applications.</span></span> <span data-ttu-id="cd9f0-129">Чтобы упростить просмотр раздела "Удаление", можно сопоставить диск Windows PowerShell с данным расположением реестра:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-129">To make it easier to view the Uninstall key, we can map a Windows PowerShell drive to this registry location:</span></span>

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> <span data-ttu-id="cd9f0-130">Диск **HKLM:** сопоставляется с корнем **HKEY_LOCAL_MACHINE**, поэтому этот диск используется в пути к разделу Uninstall.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-130">The **HKLM:** drive is mapped to the root of **HKEY_LOCAL_MACHINE**, so we used that drive in the path to the Uninstall key.</span></span> <span data-ttu-id="cd9f0-131">Вместо **HKLM:** можно было указать путь к реестру с помощью **HKLM** или **HKEY_LOCAL_MACHINE**.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-131">Instead of **HKLM:** we could have specified the registry path by using either **HKLM** or **HKEY_LOCAL_MACHINE**.</span></span> <span data-ttu-id="cd9f0-132">Преимущество использования диска существующего реестра состоит в том, что теперь можно использовать клавишу TAB для заполнения названий разделов, а не вводить их.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-132">The advantage of using an existing registry drive is that we can use tab-completion to fill in the keys names, so we do not need to type them.</span></span>

<span data-ttu-id="cd9f0-133">Теперь диск с именем "Удаление" можно использовать для быстрого и удобного поиска установок приложений.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-133">We now have a drive named "Uninstall" that can be used to quickly and conveniently look for application installations.</span></span> <span data-ttu-id="cd9f0-134">Количество установленных приложений можно найти, подсчитав количество разделов реестра в разделе "Uninstall" для диска Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-134">We can find the number of installed applications by counting the number of registry keys in the Uninstall: Windows PowerShell drive:</span></span>

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

<span data-ttu-id="cd9f0-135">С помощью разных методов, начиная с **Get-ChildItem**, можно дальше выполнять поиск в списке приложений.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-135">We can search this list of applications further by using a variety of techniques, beginning with **Get-ChildItem**.</span></span> <span data-ttu-id="cd9f0-136">Чтобы получить список приложений и сохранить их в переменную **$UninstallableApplications**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-136">To get a list of applications and save them in the **$UninstallableApplications** variable, use the following command:</span></span>

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> <span data-ttu-id="cd9f0-137">В данном случае длинное имя переменной используется для ясности.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-137">We are using a lengthy variable name here for clarity.</span></span> <span data-ttu-id="cd9f0-138">При фактическом использовании нет причин использовать длинные имена.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-138">In actual use, there is no reason to use long names.</span></span> <span data-ttu-id="cd9f0-139">Хотя имена переменных и можно завершать нажатием клавиши TAB, для скорости можно использовать имена из одного или двух символов.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-139">Although you can use tab-completion for variable names, you can also use 1-2 character names for speed.</span></span> <span data-ttu-id="cd9f0-140">Длинные описательные имена полезны при разработке кода для повторного использования.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-140">Longer, descriptive names are most useful when you are developing code for reuse.</span></span>

<span data-ttu-id="cd9f0-141">Чтобы отобразить значения записей реестра в подразделах реестра раздела "Удаление", используйте метод GetValue.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-141">To display the values of the registry entries in the registry keys under Uninstall, use the GetValue method of the registry keys.</span></span> <span data-ttu-id="cd9f0-142">Значение метода является записью реестра.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-142">The value of the method is the name of the registry entry.</span></span>

<span data-ttu-id="cd9f0-143">Например, чтобы найти отображаемые имена приложений в разделе "Удаление", используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-143">For example, to find the display names of applications in the Uninstall key, use the following command:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

<span data-ttu-id="cd9f0-144">Нет никакой гарантии, что эти значения уникальны.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-144">There is no guarantee that these values are unique.</span></span> <span data-ttu-id="cd9f0-145">В следующем примере два установленных элемента отображаются как Windows Media Encoder 9 Series:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-145">In the following example, two installed items appear as "Windows Media Encoder 9 Series":</span></span>

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### <a name="installing-applications"></a><span data-ttu-id="cd9f0-146">Установка приложений</span><span class="sxs-lookup"><span data-stu-id="cd9f0-146">Installing Applications</span></span>

<span data-ttu-id="cd9f0-147">Вы можете использовать класс **Win32_Product** для удаленной или локальной установки пакетов установщика Windows.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-147">You can use the **Win32_Product** class to install Windows Installer packages, remotely or locally.</span></span>

> [!NOTE]
> <span data-ttu-id="cd9f0-148">Чтобы установить приложение в Windows Vista, Windows Server 2008 и более поздних версиях Windows, необходимо запустить Windows PowerShell с параметром "Запустить от имени администратора".</span><span class="sxs-lookup"><span data-stu-id="cd9f0-148">On Windows Vista, Windows Server 2008, and later versions of Windows, to install an application, you must start Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="cd9f0-149">При удаленной установке используйте сетевой UNC-путь, чтобы указать путь к пакету MSI, так как подсистема WMI не распознает пути Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-149">When installing remotely, use a Universal Naming Convention (UNC) network path to specify the path to the .msi package, because the WMI subsystem does not understand Windows PowerShell paths.</span></span> <span data-ttu-id="cd9f0-150">Например, чтобы установить пакет NewPackage.msi, расположенный в общей сетевой папке \\\\AppServ\\dsp на удаленном компьютере PC01, введите следующую команду в командной строке Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-150">For example, to install the NewPackage.msi package located in the network share \\\\AppServ\\dsp on the remote computer PC01, type the following command at the Windows PowerShell prompt:</span></span>

```powershell
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq 'Win32_Product'}).Install(\\AppSrv\dsp\NewPackage.msi)
```

<span data-ttu-id="cd9f0-151">Приложения, которые не используют метод установщика Windows, могут включать специальные методы для автоматического развертывания конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-151">Applications that do not use Windows Installer technology may have application-specific methods available for automated deployment.</span></span> <span data-ttu-id="cd9f0-152">Чтобы определить, существует ли метод автоматического развертывания, проверьте документацию приложения или обратитесь в службу поддержки поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-152">To determine whether there is a method for deployment automation, check the documentation for the application or consult the application vendor's support system.</span></span> <span data-ttu-id="cd9f0-153">В некоторых случаях даже в том случае, если поставщик приложения не разрабатывал способы автоматической установки в приложении, производитель программного обеспечения установщика мог включить некоторые методы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-153">In some cases, even if the application vendor did not specifically design the application for installation automation, the installer software manufacturer may have some techniques for automation.</span></span>

### <a name="removing-applications"></a><span data-ttu-id="cd9f0-154">Удаление приложений</span><span class="sxs-lookup"><span data-stu-id="cd9f0-154">Removing Applications</span></span>

<span data-ttu-id="cd9f0-155">Удаление пакета установщика Windows с помощью Windows PowerShell работает примерно так же, как и установка пакета.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-155">Removing a Windows Installer package by using Windows PowerShell works in approximately the same way as installing a package.</span></span> <span data-ttu-id="cd9f0-156">Далее представлен пример, в котором пакет для удаления выбирается на основе имени. В некоторых случаях его может быть проще отфильтровать с помощью **IdentifyingNumber**:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-156">Here is an example that selects the package to uninstall based on its name; in some cases it may be easier to filter with the **IdentifyingNumber**:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

<span data-ttu-id="cd9f0-157">Удаление других приложений не так просто, даже если оно выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-157">Removing other applications is not quite so simple, even when done locally.</span></span> <span data-ttu-id="cd9f0-158">Строки удаления командной строки для этих приложений можно найти путем извлечения свойства **UninstallString**.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-158">We can find the command line uninstallation strings for these applications by extracting the **UninstallString** property.</span></span> <span data-ttu-id="cd9f0-159">Этот способ работает для приложений установщика Windows и более старых программ, отображающихся в разделе "Удаление":</span><span class="sxs-lookup"><span data-stu-id="cd9f0-159">This method works for Windows Installer applications and for older programs appearing under the Uninstall key:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="cd9f0-160">Выходные данные при необходимости можно отфильтровать по отображаемому имени:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-160">You can filter the output by the display name, if you like:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="cd9f0-161">Однако эти строки невозможно напрямую использовать из командной строки Windows PowerShell без внесения некоторых изменений.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-161">However, these strings may not be directly usable from the Windows PowerShell prompt without some modification.</span></span>

### <a name="upgrading-windows-installer-applications"></a><span data-ttu-id="cd9f0-162">Обновление приложений установщика Windows</span><span class="sxs-lookup"><span data-stu-id="cd9f0-162">Upgrading Windows Installer Applications</span></span>

<span data-ttu-id="cd9f0-163">Чтобы обновить приложение, необходимо знать название приложения и путь к пакету обновлений приложения.</span><span class="sxs-lookup"><span data-stu-id="cd9f0-163">To upgrade an application, you need to know the name of the application and the path to the application upgrade package.</span></span> <span data-ttu-id="cd9f0-164">Получив эти сведения, можно обновить приложение с помощью одной команды Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="cd9f0-164">With that information, you can upgrade an application with a single Windows PowerShell command:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```