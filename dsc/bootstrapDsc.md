---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Настройка виртуальных машин при начальной загрузке с помощью DSC"
ms.openlocfilehash: ff06aafa6db49d93a9b42e38ac7c3e9a11657bd5
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
><span data-ttu-id="4ae6b-103">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4ae6b-103">Applies To: Windows PowerShell 5.0</span></span>

><span data-ttu-id="4ae6b-104">**Примечание.** Раздел реестра **DSCAutomationHostEnabled**, описанный в этом разделе, недоступен в PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-104">**Note:** The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
<span data-ttu-id="4ae6b-105">Сведения о настройке новых виртуальных машин при начальной загрузке в PowerShell 4.0 см. в разделе [Требуется автоматически настроить машины с помощью DSC при начальной загрузке?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-105">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="4ae6b-106">Настройка виртуальных машин при начальной загрузке с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="4ae6b-106">Configure a virtual machines at initial boot-up by using DSC</span></span>

## <a name="requirements"></a><span data-ttu-id="4ae6b-107">Требования</span><span class="sxs-lookup"><span data-stu-id="4ae6b-107">Requirements</span></span>

<span data-ttu-id="4ae6b-108">Для выполнения этих примеров требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="4ae6b-109">Загрузочный VHD.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-109">A bootable VHD to work with.</span></span> <span data-ttu-id="4ae6b-110">ISO-файл с пробной версией Windows Server 2016 можно скачать в центре [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-110">You can download an ISO with an evaluation copy of Windows Server 2016 at [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016).</span></span> <span data-ttu-id="4ae6b-111">Инструкции по созданию VHD из ISO-образа см. в разделе [Создание загрузочных виртуальных жестких дисков](https://technet.microsoft.com/library/gg318049.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](https://technet.microsoft.com/library/gg318049.aspx).</span></span>
- <span data-ttu-id="4ae6b-112">Компьютер с включенным Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="4ae6b-113">Дополнительные сведения см. в статье [Обзор Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-113">For information, see [Hyper-V overview](https://technet.microsoft.com/library/hh831531.aspx).</span></span>

<span data-ttu-id="4ae6b-114">С помощью DSC можно автоматизировать установку и настройку программного обеспечения для компьютера при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
<span data-ttu-id="4ae6b-115">Для этого необходимо добавить документ MOF конфигурации или метаконфигурацию на загрузочный носитель (например, VHD), чтобы они выполнялись при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
<span data-ttu-id="4ae6b-116">Такое поведение контролируется [разделом реестра DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) в разделе **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span></span>
<span data-ttu-id="4ae6b-117">По умолчанию значение этого раздела — 2, что позволяет DSC запускаться во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

<span data-ttu-id="4ae6b-118">Если запускать DSC во время загрузки не следует, задайте для [раздела реестра DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) значение 0.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="4ae6b-119">Добавление документа MOF конфигурации в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="4ae6b-120">Добавление метаконфигурации DSC в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="4ae6b-121">Отключение DSC при загрузке</span><span class="sxs-lookup"><span data-stu-id="4ae6b-121">Disable DSC at boot time</span></span>

><span data-ttu-id="4ae6b-122">**Примечание.** На компьютер можно одновременно добавить `Pending.mof` и `MetaConfig.mof`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-122">**Note:** You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
<span data-ttu-id="4ae6b-123">Если присутствуют оба файла, более высокий приоритет имеют параметры, указанные в `MetaConfig.mof`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="4ae6b-124">Добавление документа MOF конфигурации в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="4ae6b-125">Для применения конфигурации при начальной загрузке добавьте скомпилированный документ MOF конфигурации в VHD в качестве его файла `Pending.mof`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="4ae6b-126">Если раздел реестра **DSCAutomationHostEnabled** имеет значение 2 (значение по умолчанию), DSC применяет конфигурацию, определенную в `Pending.mof`, при первой загрузке компьютера.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="4ae6b-127">В этом примере используется следующая конфигурация, которая устанавливает службы IIS на новом компьютере.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="4ae6b-128">Добавление документа MOF конфигурации в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="4ae6b-129">Подключите VHD, в который нужно добавить конфигурацию, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-130">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-130">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. <span data-ttu-id="4ae6b-131">На компьютере с PowerShell 5.0 или более поздней версией сохраните указанную выше конфигурацию (**SampleIISInstall**) как файл сценария PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="4ae6b-132">В консоли PowerShell перейдите в папку, где был сохранен PS1-файл.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="4ae6b-133">Выполните следующие команды PowerShell для компиляции документа MOF (дополнительные сведения о компиляции конфигураций DSC см. в разделе [Конфигурации DSC](configurations.md)).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. <span data-ttu-id="4ae6b-134">Будет создан файл `localhost.mof` в новой папке с именем `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
<span data-ttu-id="4ae6b-135">Переименуйте и переместите этот файл в нужное место на VHD как `Pending.mof` при помощи командлета [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-136">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-136">For example:</span></span>

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
    ```
6. <span data-ttu-id="4ae6b-137">Отключите VHD, вызвав командлет [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-137">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-138">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-138">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. <span data-ttu-id="4ae6b-139">Создайте виртуальную машину с помощью VHD, на который установлен документ MOF DSC.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span> <span data-ttu-id="4ae6b-140">После первоначальной загрузки и установки операционной системы будут установлены службы IIS.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-140">After intial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="4ae6b-141">Это можно проверить, вызвав командлет [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-141">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="4ae6b-142">Добавление метаконфигурации DSC в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="4ae6b-143">Также можно настроить на компьютере извлечение конфигурации при начальной загрузке, добавив метаконфигурацию (см. раздел [Настройка локального диспетчера конфигурации [LCM]](metaConfig.md)) в VHD в качестве его файла `MetaConfig.mof`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-143">You can also configure a computer to pull a configuration at intial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="4ae6b-144">Если раздел реестра **DSCAutomationHostEnabled** имеет значение 2 (значение по умолчанию), DSC применяет к локальному диспетчеру конфигурации метаконфигурацию, определенную в `MetaConfig.mof` при первой загрузке компьютера.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="4ae6b-145">Если в метаконфигурации указано, что локальный диспетчер конфигурации должен извлекать конфигурации с опрашивающего сервера, компьютер попытается извлечь конфигурации с этого сервера при начальной загрузке.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at inital boot-up.</span></span>
<span data-ttu-id="4ae6b-146">Сведения о настройке опрашивающего сервера DSC см. в разделе [Настройка опрашивающего веб-сервера DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span>

<span data-ttu-id="4ae6b-147">В этом примере используется конфигурация, описанная в предыдущем разделе (**SampleIISInstall**), и следующая метаконфигурация.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="4ae6b-148">Добавление документа MOF метаконфигурации в VHD</span><span class="sxs-lookup"><span data-stu-id="4ae6b-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="4ae6b-149">Подключите VHD, в который нужно добавить метаконфигурацию, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-150">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-150">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="4ae6b-151">[Настройте опрашивающий веб-сервер DSC](pullServer.md) и сохраните конфигурацию **SampleIISInistall** в соответствующую папку.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-151">[Set up a DSC web pull server](pullServer.md), and save the **SampleIISInistall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="4ae6b-152">На компьютере с PowerShell 5.0 или более поздней версией сохраните указанную выше метаконфигурацию (**PullClientBootstrap**) как файл сценария PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="4ae6b-153">В консоли PowerShell перейдите в папку, где был сохранен PS1-файл.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="4ae6b-154">Выполните следующие команды PowerShell для компиляции документа MOF метаконфигурации (дополнительные сведения о компиляции конфигураций DSC см. в разделе [Конфигурации DSC](configurations.md)).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. <span data-ttu-id="4ae6b-155">Будет создан файл `localhost.meta.mof` в новой папке с именем `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
<span data-ttu-id="4ae6b-156">Переименуйте и переместите этот файл в нужное место на VHD как `MetaConfig.mof` при помощи командлета [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span>

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. <span data-ttu-id="4ae6b-157">Отключите VHD, вызвав командлет [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-157">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-158">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-158">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. <span data-ttu-id="4ae6b-159">Создайте виртуальную машину с помощью VHD, на который установлен документ MOF DSC.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>
<span data-ttu-id="4ae6b-160">После первоначальной загрузки и установки операционной системы DSC извлечет конфигурацию из опрашивающего сервера и будут установлены службы IIS.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-160">After intial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="4ae6b-161">Это можно проверить, вызвав командлет [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-161">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="4ae6b-162">Отключение DSC при загрузке</span><span class="sxs-lookup"><span data-stu-id="4ae6b-162">Disable DSC at boot time</span></span>

<span data-ttu-id="4ae6b-163">По умолчанию раздел **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** имеет значение 2, что позволяет запускать конфигурацию DSC, если компьютер находится в состоянии ожидания или в текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-163">By default, the value of the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="4ae6b-164">Если запускать конфигурацию при начальной загрузке не следует, необходимо задать для этого раздела значение 0.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="4ae6b-165">Подключите VHD, вызвав командлет [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ae6b-165">Mount the VHD by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="4ae6b-166">Например:</span><span class="sxs-lookup"><span data-stu-id="4ae6b-166">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="4ae6b-167">Загрузите подраздел реестра **HKLM\Software** с VHD, вызвав `reg load`.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-167">Load the registry **HKLM\Software** subkey from the VHD by calling `reg load`.</span></span>

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. <span data-ttu-id="4ae6b-168">Перейдите в раздел **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*** с помощью поставщика реестра PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-168">Navigate to the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*** by using the PowerShell Registry provider.</span></span>

    ```powershell
    Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
    ```

4. <span data-ttu-id="4ae6b-169">Измените значение `DSCAutomationHostEnabled` на 0.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

    ```powershell
    Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
    ```

5. <span data-ttu-id="4ae6b-170">Выгрузите реестр, выполнив следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4ae6b-170">Unload the registry by running the following commands:</span></span>

    ```powershell
    [gc]::Collect()
    reg unload HKLM\Vhd
    ```

## <a name="see-also"></a><span data-ttu-id="4ae6b-171">См. также</span><span class="sxs-lookup"><span data-stu-id="4ae6b-171">See Also</span></span>

- [<span data-ttu-id="4ae6b-172">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="4ae6b-172">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="4ae6b-173">Раздел реестра DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="4ae6b-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)
- [<span data-ttu-id="4ae6b-174">Настройка локального диспетчера конфигураций (LCM)</span><span class="sxs-lookup"><span data-stu-id="4ae6b-174">Configuring the Local Configuration Manager (LCM)</span></span>](metaConfig.md)
- [<span data-ttu-id="4ae6b-175">Настройка опрашивающего веб-сервера DSC</span><span class="sxs-lookup"><span data-stu-id="4ae6b-175">Setting up a DSC web pull server</span></span>](pullServer.md)

