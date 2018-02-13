---
ms.date: 2017-08-09
keywords: "powershell, cmdlet, командлет, download, скачать, install, установить, setup, установка, windows 10, windows 8.1, windows 8.0, windows 7"
title: "Установка Windows PowerShell"
ms.openlocfilehash: ec8f09087a5c5f2e7ea6237faa01ea3f447ad1f3
ms.sourcegitcommit: 755d7bc0740573d73613cedcf79981ca3dc81c5e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/09/2018
---
# <a name="installing-windows-powershell"></a><span data-ttu-id="19bb2-103">Установка Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="19bb2-103">Installing Windows PowerShell</span></span>

<span data-ttu-id="19bb2-104">PowerShell установлен по умолчанию в каждой ОС Windows, начиная с Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="19bb2-104">PowerShell comes installed by default in every Windows, starting with Windows 7 SP1 and Windows Server 2008 R2 SP1.</span></span>

<span data-ttu-id="19bb2-105">Пользователям Linux, macOS и Windows, которые хотят установить **PowerShell 6** (бета-версия) на компьютерах, нужно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="19bb2-105">Linux, macOS, and Windows users that would like to install **PowerShell 6** (beta), in their machines, need to:</span></span>

1. <span data-ttu-id="19bb2-106">Получить PowerShell для конкретной ОС и версии с [GitHub](https://github.com/powershell/powershell#get-powershell).</span><span class="sxs-lookup"><span data-stu-id="19bb2-106">Get PowerShell for the specific OS and version, from [GitHub](https://github.com/powershell/powershell#get-powershell)</span></span>
1. <span data-ttu-id="19bb2-107">Следовать инструкциям по установке.</span><span class="sxs-lookup"><span data-stu-id="19bb2-107">Follow the installation instructions</span></span>
  - [<span data-ttu-id="19bb2-108">Linux</span><span class="sxs-lookup"><span data-stu-id="19bb2-108">Linux</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md)
  - [<span data-ttu-id="19bb2-109">macOS</span><span class="sxs-lookup"><span data-stu-id="19bb2-109">macOS</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/macos.md)
  - [<span data-ttu-id="19bb2-110">Windows</span><span class="sxs-lookup"><span data-stu-id="19bb2-110">Windows</span></span>](https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi)

<span data-ttu-id="19bb2-111">PowerShell 6 также доступен для Docker; см. инструкции по [установке Docker](https://github.com/PowerShell/PowerShell/tree/master/docker).</span><span class="sxs-lookup"><span data-stu-id="19bb2-111">PowerShell 6 is also available for Docker; see [Docker installation](https://github.com/PowerShell/PowerShell/tree/master/docker) instructions.</span></span>

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a><span data-ttu-id="19bb2-112">Поиск PowerShell в Windows 10, 8.1, 8.0 и 7</span><span class="sxs-lookup"><span data-stu-id="19bb2-112">Finding PowerShell in Windows 10, 8.1, 8.0, and 7</span></span>

<span data-ttu-id="19bb2-113">Иногда найти консоль PowerShell или ISE (интегрированную среду сценариев) в Windows может быть сложно, так как ее расположение в разных версиях Windows отличается.</span><span class="sxs-lookup"><span data-stu-id="19bb2-113">Sometimes locating PowerShell console or ISE (Integrated Scripting Environment) in Windows can be difficult, as it's location moves from one version of Windows to the next.</span></span>

<span data-ttu-id="19bb2-114">Следующие таблицы помогут найти PowerShell в вашей версии Windows.</span><span class="sxs-lookup"><span data-stu-id="19bb2-114">The following tables should help you find PowerShell in your Windows version.</span></span>
<span data-ttu-id="19bb2-115">Все указанные версии являются оригинальными, сразу после выпуска и без обновлений.</span><span class="sxs-lookup"><span data-stu-id="19bb2-115">All versions listed here are the original version, as released, with no updates.</span></span>

### <a name="for-console"></a><span data-ttu-id="19bb2-116">Консоль</span><span class="sxs-lookup"><span data-stu-id="19bb2-116">For Console</span></span>

<span data-ttu-id="19bb2-117">Версия</span><span class="sxs-lookup"><span data-stu-id="19bb2-117">Version</span></span> | <span data-ttu-id="19bb2-118">Расположение</span><span class="sxs-lookup"><span data-stu-id="19bb2-118">Location</span></span>
-- | --
<span data-ttu-id="19bb2-119">Windows 10</span><span class="sxs-lookup"><span data-stu-id="19bb2-119">Windows 10</span></span> | <span data-ttu-id="19bb2-120">Щелкните значок Windows в левом нижнем углу и начните вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-120">Click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="19bb2-121">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-121">Windows 8.1, 8.0</span></span> | <span data-ttu-id="19bb2-122">На начальном экране начните вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-122">On the start screen, start typing PowerShell.</span></span><br/><span data-ttu-id="19bb2-123">Если вы находитесь на рабочем столе, щелкните значок Windows в левом нижнем углу и начните вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-123">If on desktop, click left lower corner Windows icon, start typing PowerShell</span></span>
<span data-ttu-id="19bb2-124">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="19bb2-124">Windows 7 SP1</span></span> | <span data-ttu-id="19bb2-125">Щелкните значок Windows в левом нижнем углу и в поле поиска начните вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-125">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

### <a name="for-ise"></a><span data-ttu-id="19bb2-126">ISE</span><span class="sxs-lookup"><span data-stu-id="19bb2-126">For ISE</span></span>

<span data-ttu-id="19bb2-127">Версия</span><span class="sxs-lookup"><span data-stu-id="19bb2-127">Version</span></span> | <span data-ttu-id="19bb2-128">Расположение</span><span class="sxs-lookup"><span data-stu-id="19bb2-128">Location</span></span>
-- | --
<span data-ttu-id="19bb2-129">Windows 10</span><span class="sxs-lookup"><span data-stu-id="19bb2-129">Windows 10</span></span> | <span data-ttu-id="19bb2-130">Щелкните значок Windows в левом нижнем углу и начните вводить ISE.</span><span class="sxs-lookup"><span data-stu-id="19bb2-130">Click left lower corner Windows icon, start typing ISE</span></span>
<span data-ttu-id="19bb2-131">Windows 8.1, 8.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-131">Windows 8.1, 8.0</span></span> | <span data-ttu-id="19bb2-132">На начальном экране введите **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-132">On the start screen, type **PowerShell ISE**.</span></span><br/><span data-ttu-id="19bb2-133">Если вы находитесь на рабочем столе, щелкните значок Windows в левом нижнем углу и введите **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-133">If on desktop, click left lower corner Windows icon, type **PowerShell ISE**</span></span>
<span data-ttu-id="19bb2-134">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="19bb2-134">Windows 7 SP1</span></span> | <span data-ttu-id="19bb2-135">Щелкните значок Windows в левом нижнем углу и в поле поиска начните вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-135">Click left lower corner Windows icon, on the search box start typing PowerShell</span></span>

## <a name="finding-powershell-in-windows-server-versions"></a><span data-ttu-id="19bb2-136">Поиск PowerShell в версиях Windows Server</span><span class="sxs-lookup"><span data-stu-id="19bb2-136">Finding PowerShell in Windows Server versions</span></span>

<span data-ttu-id="19bb2-137">Начиная с Windows Server 2008 R2, операционную систему Windows можно установить без графического пользовательского интерфейса (GUI).</span><span class="sxs-lookup"><span data-stu-id="19bb2-137">Starting with Windows Server 2008 R2, Windows operating system can be installed without the graphical user interface (GUI).</span></span>
<span data-ttu-id="19bb2-138">Выпуски Windows Server без GUI называются выпусками **Core**, а выпуски с GUI — **Desktop**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-138">Editions of Windows Server without GUI are named **Core** editions, and editions with the GUI are named **Desktop**.</span></span>

### <a name="windows-server-core-editions"></a><span data-ttu-id="19bb2-139">Выпуски Windows Server Core</span><span class="sxs-lookup"><span data-stu-id="19bb2-139">Windows Server Core editions</span></span>

<span data-ttu-id="19bb2-140">Во всех выпусках Core при входе на сервер открывается окно командной строки Windows.</span><span class="sxs-lookup"><span data-stu-id="19bb2-140">In all Core editions, when you log to the server you get a Windows command prompt window.</span></span>

<span data-ttu-id="19bb2-141">Введите `powershell` и нажмите клавишу **ВВОД**, чтобы запустить PowerShell в сеансе командной строки.</span><span class="sxs-lookup"><span data-stu-id="19bb2-141">Type `powershell` and press **ENTER** to start PowerShell inside the command prompt session.</span></span> <span data-ttu-id="19bb2-142">Введите `exit`, чтобы завершить сеанс PowerShell и вернуться к командной строке.</span><span class="sxs-lookup"><span data-stu-id="19bb2-142">Type `exit` to terminate the PowerShell session and return to command prompt.</span></span>

### <a name="windows-server-desktop-editions"></a><span data-ttu-id="19bb2-143">Выпуски Windows Server Desktop</span><span class="sxs-lookup"><span data-stu-id="19bb2-143">Windows Server Desktop editions</span></span>

<span data-ttu-id="19bb2-144">Во всех выпусках Desktop нужно щелкнуть значок Windows в левом нижнем углу и начать вводить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-144">In all desktop editions, click the left lower corner Windows icon, start typing PowerShell.</span></span>
<span data-ttu-id="19bb2-145">Появятся параметры консоли и ISE.</span><span class="sxs-lookup"><span data-stu-id="19bb2-145">You get both console and ISE options.</span></span>

<span data-ttu-id="19bb2-146">Единственное исключение из этого правила — ISE в Windows Server 2008 R2 с пакетом обновления 1 (SP1). В этом случае щелкните значок Windows в левом нижнем углу и введите PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="19bb2-146">The only exception to the above rule is the ISE in Windows Server 2008 R2 SP1; in this case, click the left lower corner Windows icon, type PowerShell ISE.</span></span>

## <a name="how-to-check-the-version-of-powershell"></a><span data-ttu-id="19bb2-147">Проверка версии PowerShell</span><span class="sxs-lookup"><span data-stu-id="19bb2-147">How to check the version of PowerShell</span></span>

<span data-ttu-id="19bb2-148">Чтобы узнать, какая версия PowerShell установлена, запустите консоль PowerShell (или ISE), введите `$PSVersionTable` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-148">To find which version of PowerShell you have installed, start a PowerShell console (or the ISE) and type `$PSVersionTable` and press **ENTER**.</span></span>

## <a name="upgrading-existing-windows-powershell"></a><span data-ttu-id="19bb2-149">Обновление существующей версии Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="19bb2-149">Upgrading existing Windows PowerShell</span></span>

<span data-ttu-id="19bb2-150">В пакет установки для PowerShell входит установщик WMF.</span><span class="sxs-lookup"><span data-stu-id="19bb2-150">The installation package for PowerShell comes inside a WMF installer.</span></span>
<span data-ttu-id="19bb2-151">Версия установщика WMF совпадает с версией PowerShell. Для Windows PowerShell нет отдельного установщика.</span><span class="sxs-lookup"><span data-stu-id="19bb2-151">The version of the WMF installer matches the version of PowerShell; there's no stand alone installer for Windows PowerShell.</span></span>

<span data-ttu-id="19bb2-152">Если вам нужно обновить существующую версию PowerShell, в Windows используйте следующую таблицу, чтобы найти установщик для нужной версии PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19bb2-152">If you need to update your existing version of PowerShell, in Windows, use the following table to locate the installer for the version of PowerShell you want to update to.</span></span>

<span data-ttu-id="19bb2-153">Windows</span><span class="sxs-lookup"><span data-stu-id="19bb2-153">Windows</span></span> | <span data-ttu-id="19bb2-154">PS 3.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-154">PS 3.0</span></span> | <span data-ttu-id="19bb2-155">PS 4.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-155">PS 4.0</span></span> | <span data-ttu-id="19bb2-156">PS 5.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-156">PS 5.0</span></span> | <span data-ttu-id="19bb2-157">PS 5.1</span><span class="sxs-lookup"><span data-stu-id="19bb2-157">PS 5.1</span></span> |
--|--|--|--|--|
<span data-ttu-id="19bb2-158">Windows 10 (см. примечание 1)</span><span class="sxs-lookup"><span data-stu-id="19bb2-158">Windows 10 (see Note1)</span></span><br/><span data-ttu-id="19bb2-159">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="19bb2-159">Windows Server 2016</span></span> | - | - | - | <span data-ttu-id="19bb2-160">установлено</span><span class="sxs-lookup"><span data-stu-id="19bb2-160">installed</span></span>
<span data-ttu-id="19bb2-161">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="19bb2-161">Windows 8.1</span></span><br/><span data-ttu-id="19bb2-162">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="19bb2-162">Windows Server 2012 R2</span></span> | - | <span data-ttu-id="19bb2-163">установлено</span><span class="sxs-lookup"><span data-stu-id="19bb2-163">installed</span></span> | [<span data-ttu-id="19bb2-164">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-164">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="19bb2-165">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="19bb2-165">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="19bb2-166">Windows 8</span><span class="sxs-lookup"><span data-stu-id="19bb2-166">Windows 8</span></span><br/><span data-ttu-id="19bb2-167">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="19bb2-167">Windows Server 2012</span></span> | <span data-ttu-id="19bb2-168">установлено</span><span class="sxs-lookup"><span data-stu-id="19bb2-168">installed</span></span> | [<span data-ttu-id="19bb2-169">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-169">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="19bb2-170">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-170">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="19bb2-171">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="19bb2-171">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
<span data-ttu-id="19bb2-172">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="19bb2-172">Windows 7 SP1</span></span><br/><span data-ttu-id="19bb2-173">Windows Server 2008 R2 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="19bb2-173">Windows Server 2008 R2 SP1</span></span> | [<span data-ttu-id="19bb2-174">WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-174">WMF 3.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [<span data-ttu-id="19bb2-175">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-175">WMF 4.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [<span data-ttu-id="19bb2-176">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="19bb2-176">WMF 5.0</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [<span data-ttu-id="19bb2-177">WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="19bb2-177">WMF 5.1</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> <span data-ttu-id="19bb2-178">**Примечание 1**.</span><span class="sxs-lookup"><span data-stu-id="19bb2-178">**Note 1**:</span></span>
  >>
  >> <span data-ttu-id="19bb2-179">Если в начальном выпуске Windows 10 включены автоматические обновления, PowerShell обновляется с версии 5.0 до 5.1.</span><span class="sxs-lookup"><span data-stu-id="19bb2-179">On the initial release of Windows 10, with automatic updates enabled, PowerShell gets updated from version 5.0 to 5.1.</span></span>
  >>
  >> <span data-ttu-id="19bb2-180">Если оригинальная версия Windows 10 не обновлена в Центре обновления Windows, версия PowerShell будет 5.0.</span><span class="sxs-lookup"><span data-stu-id="19bb2-180">If the original version of Windows 10 is not updated through Windows Updates, the version of PowerShell is 5.0.</span></span>

## <a name="need-azure-powershell"></a><span data-ttu-id="19bb2-181">Необходимость Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="19bb2-181">Need Azure PowerShell</span></span>

<span data-ttu-id="19bb2-182">Если вы ищете **Azure PowerShell**, можно начать с раздела [Общие сведения об Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span><span class="sxs-lookup"><span data-stu-id="19bb2-182">If you're looking for **Azure PowerShell**, you could start with [Overview of Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure).</span></span>

<span data-ttu-id="19bb2-183">Либо вам нужен раздел [Установка и настройка Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="19bb2-183">Otherwise, what you might need is [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)</span></span>

## <a name="see-also"></a><span data-ttu-id="19bb2-184">См. также</span><span class="sxs-lookup"><span data-stu-id="19bb2-184">See Also</span></span>

- [<span data-ttu-id="19bb2-185">Требования Windows PowerShell к системе</span><span class="sxs-lookup"><span data-stu-id="19bb2-185">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)
- [<span data-ttu-id="19bb2-186">Запуск Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="19bb2-186">Starting Windows PowerShell</span></span>](Starting-Windows-PowerShell.md)
