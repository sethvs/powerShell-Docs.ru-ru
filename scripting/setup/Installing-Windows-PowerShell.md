---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Установка Windows PowerShell"
ms.assetid: 6fbb0409-5a54-48ec-95e6-7f8b7d8c4969
ms.openlocfilehash: 2b4cdec52dfc98649a81ab2265a204fcdb0bd8d7
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="installing-windows-powershell"></a><span data-ttu-id="04a07-103">Установка Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="04a07-103">Installing Windows PowerShell</span></span>
<span data-ttu-id="04a07-104">В состав Windows® 8 и Windows Server® 2012 входит Windows PowerShell 3.0 и все необходимые компоненты этой оболочки.</span><span class="sxs-lookup"><span data-stu-id="04a07-104">Windows® 8 and Windows Server® 2012 include Windows PowerShell 3.0 and all of its prerequisites.</span></span> <span data-ttu-id="04a07-105">Система также включает модуль Windows PowerShell 2.0 для обеспечения обратной совместимости с основными программами, которые не могут использовать Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-105">The system also includes the Windows PowerShell 2.0 engine for backward compatibility with host programs that cannot use Windows PowerShell 3.0.</span></span>

<span data-ttu-id="04a07-106">В этой статье описана установка Windows PowerShell 3.0 в предыдущих версиях систем, а также установка и включение необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="04a07-106">This topic explains how to install Windows PowerShell 3.0 on earlier systems and install and enable the required features.</span></span>

<span data-ttu-id="04a07-107">Эта статья содержит следующие разделы.</span><span class="sxs-lookup"><span data-stu-id="04a07-107">This topic includes the following sections:</span></span>

-   [<span data-ttu-id="04a07-108">Установка Windows PowerShell в Windows 8 и Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="04a07-108">Installing Windows PowerShell on Windows 8 and Windows Server 2012</span></span>](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows8andWindowsServer2012)

-   [<span data-ttu-id="04a07-109">Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="04a07-109">Installing Windows PowerShell on Windows 7 and Windows Server 2008 R2</span></span>](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows7andWindowsServer2008R2)

-   [<span data-ttu-id="04a07-110">Установка Windows PowerShell в Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="04a07-110">Installing Windows PowerShell on Windows Server 2008</span></span>](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindowsServer2008LH)

-   [<span data-ttu-id="04a07-111">Установка Windows PowerShell в основных серверных компонентах</span><span class="sxs-lookup"><span data-stu-id="04a07-111">Installing Windows PowerShell on Server Core</span></span>](Installing-Windows-PowerShell.md#BKMK_InstallingOnServerCore)

-   [<span data-ttu-id="04a07-112">Развертывание Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="04a07-112">Deploying Windows PowerShell Web Access</span></span>](https://technet.microsoft.com/en-us/library/639d0eff-98a3-4124-b52c-26921ebd98b0)

-   [<span data-ttu-id="04a07-113">Установка подсистемы Windows PowerShell 2.0</span><span class="sxs-lookup"><span data-stu-id="04a07-113">Installing the Windows PowerShell 2.0 Engine</span></span>](Installing-the-Windows-PowerShell-2.0-Engine.md)

## <span data-ttu-id="04a07-114"><a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>Установка Windows PowerShell в Windows 8 и Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="04a07-114"><a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>Installing Windows PowerShell on Windows 8 and Windows Server 2012</span></span>
<span data-ttu-id="04a07-115">Windows PowerShell 3.0 предоставляется установленной, настроенной и готовой к использованию.</span><span class="sxs-lookup"><span data-stu-id="04a07-115">Windows PowerShell 3.0 arrives installed, configured, and ready to use.</span></span> <span data-ttu-id="04a07-116">Интегрированная среда сценариев Windows PowerShell (ISE) установлена и включена.</span><span class="sxs-lookup"><span data-stu-id="04a07-116">Windows PowerShell Integrated Scripting Environment (ISE) is installed and enabled.</span></span> <span data-ttu-id="04a07-117">Дополнительные сведения о запуске Windows PowerShell см. в статьях [Starting Windows PowerShell on Windows 8](https://technet.microsoft.com/en-us/library/d7be1668-8617-4890-ad90-dd9765fbd2c3) (Запуск Windows PowerShell в Windows 8) и [Starting Windows PowerShell on Windows Server 2012](https://technet.microsoft.com/library/hh831491.aspx#BKMK_powershell) (Запуск Windows PowerShell в Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="04a07-117">For information about starting Windows PowerShell, see [Starting Windows PowerShell on Windows 8](https://technet.microsoft.com/en-us/library/d7be1668-8617-4890-ad90-dd9765fbd2c3) and [Starting Windows PowerShell on Windows Server 2012](https://technet.microsoft.com/library/hh831491.aspx#BKMK_powershell).</span></span>

## <span data-ttu-id="04a07-118"><a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="04a07-118"><a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>Installing Windows PowerShell on Windows 7 and Windows Server 2008 R2</span></span>
<span data-ttu-id="04a07-119">Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1).</span><span class="sxs-lookup"><span data-stu-id="04a07-119">These instructions explain how to install Windows PowerShell 3.0 on computers running Windows 7 with Service Pack 1 and Windows Server 2008 R2 with Service Pack 1.</span></span> <span data-ttu-id="04a07-120">Ниже приведены отдельные инструкции по установке для компьютеров под управлением Windows Server 2008 R2 с установкой основных серверных компонентов.</span><span class="sxs-lookup"><span data-stu-id="04a07-120">There are separate installation instructions below for computers running with the Server Core installation option of Windows Server 2008 R2.</span></span>

#### <a name="getting-ready-to-install"></a><span data-ttu-id="04a07-121">Подготовка к установке</span><span class="sxs-lookup"><span data-stu-id="04a07-121">Getting ready to install</span></span>

-   <span data-ttu-id="04a07-122">Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-122">Before installing Windows Management Framework 3.0, uninstall any previous versions of Windows Management Framework 3.0.</span></span>

#### <a name="to-install-windows-powershell-30"></a><span data-ttu-id="04a07-123">Установка Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="04a07-123">To install Windows PowerShell 3.0</span></span>

1.  <span data-ttu-id="04a07-124">Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).</span><span class="sxs-lookup"><span data-stu-id="04a07-124">Install the full installation of Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).</span></span>

    <span data-ttu-id="04a07-125">Можно также установить Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).</span><span class="sxs-lookup"><span data-stu-id="04a07-125">Or, install Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).</span></span>

2.  <span data-ttu-id="04a07-126">Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="04a07-126">Install Windows Management Framework 3.0 from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span>

<span data-ttu-id="04a07-127">Сведения о запуске Windows PowerShell 3.0 см. в статье [Запуск Windows PowerShell в более ранних версиях Windows](Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md).</span><span class="sxs-lookup"><span data-stu-id="04a07-127">For information about starting Windows PowerShell 3.0, see [Starting Windows PowerShell on Earlier Versions of Windows](Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md).</span></span>

## <span data-ttu-id="04a07-128"><a name="BKMK_InstallingOnServerCore"></a>Установка Windows PowerShell в основных серверных компонентах</span><span class="sxs-lookup"><span data-stu-id="04a07-128"><a name="BKMK_InstallingOnServerCore"></a>Installing Windows PowerShell on Server Core</span></span>
<span data-ttu-id="04a07-129">Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) с установкой основных серверных компонентов.</span><span class="sxs-lookup"><span data-stu-id="04a07-129">These instructions explain how to install Windows PowerShell 3.0 on computers running the Server Core installation option of Windows Server 2008 R2 with Service Pack 1.</span></span>

<span data-ttu-id="04a07-130">Первые шаги в процедуре используют команды системы обслуживания образов развертывания и управления ими (DISM) для установки Microsoft .NET Framework 2.0 для основных серверных компонентов и Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-130">The first steps in the procedure use Deployment Image Servicing and Management (DISM) commands to install Microsoft .NET Framework 2.0 for Server Core and Windows PowerShell 2.0.</span></span> <span data-ttu-id="04a07-131">Эти программы являются необходимыми компонентами для Windows Management Framework 3.0, который устанавливается на последующем шаге.</span><span class="sxs-lookup"><span data-stu-id="04a07-131">These programs are prerequisites for Windows Management Framework 3.0, which is installed in a subsequent step.</span></span>

#### <a name="getting-ready-to-install"></a><span data-ttu-id="04a07-132">Подготовка к установке</span><span class="sxs-lookup"><span data-stu-id="04a07-132">Getting ready to install</span></span>

-   <span data-ttu-id="04a07-133">Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-133">Before installing Windows Management Framework 3.0, uninstall any previous versions of Windows Management Framework 3.0.</span></span>

#### <a name="to-install-windows-powershell-30"></a><span data-ttu-id="04a07-134">Установка Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="04a07-134">To install Windows PowerShell 3.0</span></span>

1.  <span data-ttu-id="04a07-135">Запуск Cmd.exe</span><span class="sxs-lookup"><span data-stu-id="04a07-135">Start Cmd.exe</span></span>

2.  <span data-ttu-id="04a07-136">Выполните указанные ниже команды DISM.</span><span class="sxs-lookup"><span data-stu-id="04a07-136">Run the following DISM commands.</span></span> <span data-ttu-id="04a07-137">Эти команды устанавливают .NET Framework 2.0 и Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-137">These commands install .NET Framework 2.0 and Windows PowerShell 2.0.</span></span>

    ```
    dism /online /enable-feature:NetFx2-ServerCore
    dism /online /enable-feature:MicrosoftWindowsPowerShell
    dism /online /enable-feature:NetFx2-ServerCore-WOW64
    ```

3.  <span data-ttu-id="04a07-138">Установите полную версию Microsoft .NET Framework 4.0 для основных серверных компонентов из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450).</span><span class="sxs-lookup"><span data-stu-id="04a07-138">Install Microsoft .NET Framework 4.0 full installation for Server Core from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450).</span></span>

4.  <span data-ttu-id="04a07-139">Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="04a07-139">Install Windows Management Framework 3.0 from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span>

## <span data-ttu-id="04a07-140"><a name="BKMK_InstallingOnWindowsServer2008LH"></a>Установка Windows PowerShell в Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="04a07-140"><a name="BKMK_InstallingOnWindowsServer2008LH"></a>Installing Windows PowerShell on Windows Server 2008</span></span>
<span data-ttu-id="04a07-141">Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 с пакетом обновления 2 (SP2).</span><span class="sxs-lookup"><span data-stu-id="04a07-141">These instructions explain how to install Windows PowerShell 3.0 on computers running Windows Server 2008 with Service Pack 2.</span></span>

<span data-ttu-id="04a07-142">В системах Windows Server 2008 Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) является необходимым компонентом для Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-142">On Windows Server 2008 systems, Windows Management Framework (Windows PowerShell 2.0, KB 968930) is a prerequisite for Windows Management Framework 3.0.</span></span> <span data-ttu-id="04a07-143">Компонент расширенной защиты для проверки подлинности защищает компьютер от атак перенаправления проверки подлинности и позволяет использовать параметр **UseSSL** при создании удаленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="04a07-143">The "Extended Protection for Authentication" feature protects the computer from authentication forwarding attacks and allows you to use the **UseSSL** parameter when creating remote sessions.</span></span> <span data-ttu-id="04a07-144">Чтобы установить Windows PowerShell 3.0 и модуль Windows PowerShell 2.0, используйте следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="04a07-144">To install Windows PowerShell 3.0 and the Windows PowerShell 2.0 Engine, use the following procedure.</span></span>

#### <a name="getting-ready-to-install"></a><span data-ttu-id="04a07-145">Подготовка к установке</span><span class="sxs-lookup"><span data-stu-id="04a07-145">Getting ready to install</span></span>

-   <span data-ttu-id="04a07-146">Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="04a07-146">Before installing Windows Management Framework 3.0, uninstall any previous versions of Windows Management Framework 3.0.</span></span>

#### <a name="to-install-windows-powershell-30"></a><span data-ttu-id="04a07-147">Установка Windows PowerShell 3.0</span><span class="sxs-lookup"><span data-stu-id="04a07-147">To install Windows PowerShell 3.0</span></span>

1.  <span data-ttu-id="04a07-148">Установите Microsoft .NET Framework 3.5 с пакетом обновления 1 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910).</span><span class="sxs-lookup"><span data-stu-id="04a07-148">Install Microsoft .NET Framework 3.5 with Service Pack 1 from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910).</span></span>

2.  <span data-ttu-id="04a07-149">Установите Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035).</span><span class="sxs-lookup"><span data-stu-id="04a07-149">Install Windows Management Framework (Windows PowerShell 2.0, KB 968930) from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035).</span></span>

3.  <span data-ttu-id="04a07-150">Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).</span><span class="sxs-lookup"><span data-stu-id="04a07-150">Install the full installation of Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).</span></span>

    <span data-ttu-id="04a07-151">Можно также установить Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).</span><span class="sxs-lookup"><span data-stu-id="04a07-151">Or, install Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).</span></span>

4.  <span data-ttu-id="04a07-152">Установите компонент расширенной защиты для проверки подлинности (статья базы знаний 968389) по адресу [http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398).</span><span class="sxs-lookup"><span data-stu-id="04a07-152">Install "Extended Protection for Authentication" (KB 968389) from [http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398).</span></span>

5.  <span data-ttu-id="04a07-153">Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="04a07-153">Install Windows Management Framework 3.0 from the Microsoft Download Center at [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span>

## <a name="see-also"></a><span data-ttu-id="04a07-154">См. также</span><span class="sxs-lookup"><span data-stu-id="04a07-154">See Also</span></span>
- [<span data-ttu-id="04a07-155">Требования Windows PowerShell к системе</span><span class="sxs-lookup"><span data-stu-id="04a07-155">Windows PowerShell System Requirements</span></span>](Windows-PowerShell-System-Requirements.md)
- [<span data-ttu-id="04a07-156">Запуск Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="04a07-156">Starting Windows PowerShell</span></span>](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)

