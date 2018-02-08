---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
contributor: keithb
title: "Установка и настройка WMF 5.1"
ms.openlocfilehash: f58676de6f7a5c51ba586a8c607097af8e60d0c9
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="install-and-configure-wmf-51"></a><span data-ttu-id="34073-103">Установка и настройка WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="34073-103">Install and Configure WMF 5.1</span></span> #


## <a name="download-and-install-the-wmf-51-package"></a><span data-ttu-id="34073-104">Скачать и установить пакет WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="34073-104">Download and install the WMF 5.1 package</span></span>

<span data-ttu-id="34073-105">Скачайте пакет WMF 5.1 для той операционной системы и архитектуры, в которой будет производиться установка.</span><span class="sxs-lookup"><span data-stu-id="34073-105">Download the WMF 5.1 package for the operating system and architecture you wish to install it on:</span></span>

| <span data-ttu-id="34073-106">Операционная система</span><span class="sxs-lookup"><span data-stu-id="34073-106">Operating System</span></span>       | <span data-ttu-id="34073-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="34073-107">Prerequisites</span></span>           | <span data-ttu-id="34073-108">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="34073-108">Package Links</span></span>                          |
|------------------------|-------------------------|----------------------------------------|
| <span data-ttu-id="34073-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="34073-109">Windows Server 2012 R2</span></span> |                         | <span data-ttu-id="34073-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="34073-110">[Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span> |
| <span data-ttu-id="34073-111">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="34073-111">Windows Server 2012</span></span>    |                         | <span data-ttu-id="34073-112">[W2K12-KB3191565-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="34073-112">[W2K12-KB3191565-x64.msu][]</span></span>            |
| <span data-ttu-id="34073-113">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="34073-113">Windows Server 2008 R2</span></span> | <span data-ttu-id="34073-114">[.NET Framework 4.5.2][]</span><span class="sxs-lookup"><span data-stu-id="34073-114">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="34073-115">[Win7AndW2K8R2-KB3191566-x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="34073-115">[Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span>    |
| <span data-ttu-id="34073-116">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="34073-116">Windows 8.1</span></span>            |                         | <span data-ttu-id="34073-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span><span class="sxs-lookup"><span data-stu-id="34073-117">**x64:** [Win8.1AndW2K12R2-KB3191564-x64.msu][]</span></span></br><span data-ttu-id="34073-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span><span class="sxs-lookup"><span data-stu-id="34073-118">**x86:** [Win8.1-KB3191564-x86.msu][]</span></span> |
| <span data-ttu-id="34073-119">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="34073-119">Windows 7 SP1</span></span>          | <span data-ttu-id="34073-120">[.NET Framework 4.5.2][]</span><span class="sxs-lookup"><span data-stu-id="34073-120">[.NET Framework 4.5.2][]</span></span>| <span data-ttu-id="34073-121">**x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="34073-121">**x64:** [Win7AndW2K8R2-KB3191566-x64.ZIP][]</span></span></br><span data-ttu-id="34073-122">**x86:** [Win7-KB3191566-x86.ZIP][]</span><span class="sxs-lookup"><span data-stu-id="34073-122">**x86:** [Win7-KB3191566-x86.ZIP][]</span></span> |

[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42642
[W2K12-KB3191565-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839513
[Win7-KB3191566-x86.ZIP]: https://go.microsoft.com/fwlink/?linkid=839522
[Win7AndW2K8R2-KB3191566-x64.ZIP]: https://go.microsoft.com/fwlink/?linkid=839523
[Win8.1-KB3191564-x86.msu]: https://go.microsoft.com/fwlink/?linkid=839521
[Win8.1AndW2K12R2-KB3191564-x64.msu]: https://go.microsoft.com/fwlink/?linkid=839516

## <a name="install-wmf-51-for-windows-server-2008-r2-and-windows-7"></a><span data-ttu-id="34073-129">Установить WMF 5.1 для Windows Server 2008 R2 и Windows 7</span><span class="sxs-lookup"><span data-stu-id="34073-129">Install WMF 5.1 for Windows Server 2008 R2 and Windows 7</span></span>

> <span data-ttu-id="34073-130">**Примечание**. Инструкции по установке для Windows Server 2008 R2 и Windows 7 изменились и отличаются от инструкций для других пакетов.</span><span class="sxs-lookup"><span data-stu-id="34073-130">**Note:** Installation instructions for Windows Server 2008 R2 and Windows 7 have changed, and differ from the instructions for the other packages.</span></span> <span data-ttu-id="34073-131">Инструкции по установке для Windows Server 2012 R2, Windows Server 2012 и Windows 8.1 см. ниже.</span><span class="sxs-lookup"><span data-stu-id="34073-131">Installation instructions for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1 are below.</span></span>

<span data-ttu-id="34073-132">**Установка WMF 5.1 на Windows Server 2008 R2 и Windows 7**</span><span class="sxs-lookup"><span data-stu-id="34073-132">**Installing WMF 5.1 on Windows Server 2008 R2 and Windows 7**</span></span>

1. <span data-ttu-id="34073-133">Перейдите в папку, куда был скачан ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="34073-133">Navigate to the folder into which you downloaded the ZIP file.</span></span>

2. <span data-ttu-id="34073-134">Щелкните его правой кнопкой мыши и выберите команду "Извлечь все...".</span><span class="sxs-lookup"><span data-stu-id="34073-134">Right-click on the ZIP file, and select "Extract All...".</span></span> <span data-ttu-id="34073-135">ZIP-файл содержит два файла: MSU и файл скрипта Install-WMF5.1.PS1.</span><span class="sxs-lookup"><span data-stu-id="34073-135">The Zip contains 2 files: an MSU and the Install-WMF5.1.PS1 script file.</span></span>
<span data-ttu-id="34073-136">После распаковки ZIP-файла вы можете скопировать его содержимое на любой компьютер под управлением Windows 7 или Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="34073-136">Once you have unpacked the ZIP file, you can copy the contents to any machine running Windows 7 or Windows Server 2008 R2.</span></span>

3. <span data-ttu-id="34073-137">После извлечения содержимого ZIP-файла откройте PowerShell от имени администратора, а затем перейдите к папке с содержимым ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="34073-137">After extracting the ZIP file contents, open PowerShell as administrator, then navigate to the folder containing the contents of the ZIP file.</span></span>

4. <span data-ttu-id="34073-138">Запустите скрипт Install-Wmf5.1.ps1 в этой папке и следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="34073-138">Run the Install-Wmf5.1.ps1 script in that folder, and follow the instructions.</span></span> <span data-ttu-id="34073-139">Этот скрипт проверит предварительные требования на локальном компьютере: если они выполнены, он установит WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="34073-139">This script will check the prerequisites on the local machine, and install WMF 5.1 if the prerequisites have been met.</span></span> <span data-ttu-id="34073-140">Предварительные требования перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="34073-140">The prerequisites are listed below.</span></span>

<span data-ttu-id="34073-141">Install-WMF5.1.ps1 принимает следующие параметры для упрощения автоматизации установки в Windows Server 2008 R2 и Windows 7:</span><span class="sxs-lookup"><span data-stu-id="34073-141">Install-WMF5.1.ps1 takes the following parameters to ease automating the installation on Windows Server 2008 R2 and Windows 7:</span></span>

- <span data-ttu-id="34073-142">AcceptEula: если этот параметр включен, условия EULA принимаются автоматически и не будут отображены.</span><span class="sxs-lookup"><span data-stu-id="34073-142">AcceptEula: When this parameter is included, the EULA is automatically accepted and will not be displayed.</span></span>
- <span data-ttu-id="34073-143">AllowRestart: этот параметр можно использовать, только если указан параметр AcceptEula.</span><span class="sxs-lookup"><span data-stu-id="34073-143">AllowRestart: This parameter can only be used if AcceptEula is specified.</span></span> <span data-ttu-id="34073-144">Если этот параметр включен и после установки WMF 5.1 требуется перезагрузка, она будет выполнена без запроса сразу после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="34073-144">If this parameter is included, and a restart is required after installing WMF 5.1, the restart will happen without prompting immediately after the installation is completed.</span></span>

<span data-ttu-id="34073-145">**Предварительные требования WMF 5.1 для Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1)**</span><span class="sxs-lookup"><span data-stu-id="34073-145">**WMF 5.1 Prerequisites for Windows Server 2008 R2 SP1 and Windows 7 SP1**</span></span>

<span data-ttu-id="34073-146">Для установки WMF 5.1 на компьютере с ОС Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="34073-146">Installation of WMF 5.1 on either Windows Server 2008 R2 SP1 or Windows 7 SP1, requires the following:</span></span>
- <span data-ttu-id="34073-147">Должен быть установлен последний пакет обновления.</span><span class="sxs-lookup"><span data-stu-id="34073-147">Latest service pack must be installed.</span></span>
- <span data-ttu-id="34073-148">Платформа WMF 3.0 **не должна** быть установлена.</span><span class="sxs-lookup"><span data-stu-id="34073-148">WMF 3.0 **must not** be installed.</span></span> <span data-ttu-id="34073-149">Установка WMF 5.1 поверх WMF 3.0 приведет к потере PSModulePath, что может вызвать сбой других приложений.</span><span class="sxs-lookup"><span data-stu-id="34073-149">Installing WMF 5.1 over WMF 3.0 will result in the loss of the PSModulePath, which can cause other applications to fail.</span></span> <span data-ttu-id="34073-150">Перед установкой WMF 5.1 нужно удалить WMF 3.0 или сохранить PSModulePath и восстановить его вручную после установки WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="34073-150">Before installing WMF 5.1, you must either un-install WMF 3.0, or save the PSModulePath and then restore it manually after WMF 5.1 installation is complete.</span></span>
- <span data-ttu-id="34073-151">WMF 5.1 требуется по крайней мере [.NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span><span class="sxs-lookup"><span data-stu-id="34073-151">WMF 5.1 requires at least [.NET Framework 4.5.2](https://www.microsoft.com/en-ca/download/details.aspx?id=42642).</span></span>
<span data-ttu-id="34073-152">Вы можете установить Microsoft .NET Framework 4.5.2, выполнив следующие инструкции по месту скачивания.</span><span class="sxs-lookup"><span data-stu-id="34073-152">You can install Microsoft .NET Framework 4.5.2 by following the instructions at the download location.</span></span>

<span data-ttu-id="34073-153">**Зависимость WinRM**</span><span class="sxs-lookup"><span data-stu-id="34073-153">**WinRM Dependency**</span></span>

<span data-ttu-id="34073-154">Служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM.</span><span class="sxs-lookup"><span data-stu-id="34073-154">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span>
<span data-ttu-id="34073-155">По умолчанию WinRM не включен в Windows Server 2008 R2 и Windows 7.</span><span class="sxs-lookup"><span data-stu-id="34073-155">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span>
<span data-ttu-id="34073-156">Чтобы включить WinRM, выполните команду `Set-WSManQuickConfig` в сеансе Windows PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="34073-156">Run `Set-WSManQuickConfig`, in a Windows PowerShell elevated session, to enable WinRM.</span></span>


## <a name="install-wmf-51-for-windows-server-2012-r2-windows-server-2012-and-windows-81"></a><span data-ttu-id="34073-157">Установка WMF 5.1 для Windows Server 2012 R2, Windows Server 2012 и Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="34073-157">Install WMF 5.1 for Windows Server 2012 R2, Windows Server 2012, and Windows 8.1</span></span>
<span data-ttu-id="34073-158">**Установка из проводника**</span><span class="sxs-lookup"><span data-stu-id="34073-158">**Install from Windows Explorer (or File Explorer in Windows Server 2012 R2 or Windows 8.1)**</span></span>

1. <span data-ttu-id="34073-159">Перейдите в папку, куда был скачан MSU-файл.</span><span class="sxs-lookup"><span data-stu-id="34073-159">Navigate to the folder into which you downloaded the MSU file.</span></span>
2. <span data-ttu-id="34073-160">Дважды щелкните этот файл для его запуска.</span><span class="sxs-lookup"><span data-stu-id="34073-160">Double-click the MSU to run it.</span></span>

<span data-ttu-id="34073-161">**Установка из командной строки**</span><span class="sxs-lookup"><span data-stu-id="34073-161">**Installing from the Command Prompt**</span></span>

1. <span data-ttu-id="34073-162">После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора").</span><span class="sxs-lookup"><span data-stu-id="34073-162">After downloading the correct package for your computer's architecture, open a Command Prompt window with elevated user rights (Run as Administrator).</span></span> <span data-ttu-id="34073-163">При выборе варианта "Установка основных серверных компонентов" для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="34073-163">On the Server Core installation options of Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1, Command Prompt opens with elevated user rights by default.</span></span>
2. <span data-ttu-id="34073-164">Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="34073-164">Change directories to the folder into which you have downloaded or copied the WMF 5.1 installation package.</span></span>
3. <span data-ttu-id="34073-165">Выполните одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="34073-165">Run one of the following commands:</span></span>
   - <span data-ttu-id="34073-166">На компьютерах с ОС Windows Server 2012 R2 или Windows 8.1 (64-разрядная версия) выполните команду `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="34073-166">On computers that are running Windows Server 2012 R2 or Windows 8.1 x64, run `Win8.1AndW2K12R2-KB3191564-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="34073-167">На компьютерах с ОС Windows Server 2012 выполните команду `W2K12-KB3191565-x64.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="34073-167">On computers that are running Windows Server 2012, run `W2K12-KB3191565-x64.msu /quiet`.</span></span>
   - <span data-ttu-id="34073-168">На компьютерах с ОС Windows 8.1 (32-разрядная версия) выполните команду `Win8.1-KB3191564-x86.msu /quiet`.</span><span class="sxs-lookup"><span data-stu-id="34073-168">On computers that are running Windows 8.1 x86, run `Win8.1-KB3191564-x86.msu /quiet`.</span></span>

> [!NOTE]
> <span data-ttu-id="34073-169">При установке WMF 5.1 требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="34073-169">Installing WMF 5.1 requires a reboot.</span></span> <span data-ttu-id="34073-170">Параметр `/quiet` инициирует перезагрузку системы без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="34073-170">Using the `/quiet` option will reboot the system without warning.</span></span>
> <span data-ttu-id="34073-171">Чтобы избежать перезагрузки, используйте параметр `/norestart`.</span><span class="sxs-lookup"><span data-stu-id="34073-171">Use the `/norestart` option to avoid rebooting.</span></span> <span data-ttu-id="34073-172">Однако установка WMF 5.1 не будет выполнена, пока вы не перезагрузите систему.</span><span class="sxs-lookup"><span data-stu-id="34073-172">However, WMF 5.1 will not be installed until you have rebooted.</span></span>