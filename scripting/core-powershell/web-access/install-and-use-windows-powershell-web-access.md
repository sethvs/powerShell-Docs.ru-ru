---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Установка и использование Windows PowerShell Web Access"
ms.openlocfilehash: a860f7c22829da46f0458ea729fa0afd1fe4fb6f
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
#  <a name="install-and-use-windows-powershell-web-access"></a><span data-ttu-id="db0de-103">Установка и использование Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="db0de-103">Install and Use Windows PowerShell Web Access</span></span>

<span data-ttu-id="db0de-104">Обновлено: 5 ноября 2013 г.</span><span class="sxs-lookup"><span data-stu-id="db0de-104">Updated: November 5, 2013</span></span>

<span data-ttu-id="db0de-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="db0de-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="db0de-106">Компонент Windows PowerShell® Web Access, впервые представленный в Windows Server® 2012, действует как шлюз Windows PowerShell, предоставляя веб-консоль Windows PowerShell для удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="db0de-106">Windows PowerShell® Web Access, first introduced in Windows Server® 2012, acts as a Windows PowerShell gateway, providing a web-based Windows PowerShell console that is targeted at a remote computer.</span></span> <span data-ttu-id="db0de-107">Она позволяет ИТ-специалистам выполнять команды и сценарии Windows PowerShell с консоли Windows PowerShell в веб-браузере без установки Windows PowerShell, программ для удаленного управления или подключаемых модулей браузера, необходимых на устройстве клиента.</span><span class="sxs-lookup"><span data-stu-id="db0de-107">It enables IT Pros to run Windows PowerShell commands and scripts from a Windows PowerShell console in a web browser, with no Windows PowerShell, remote management software, or browser plug-in installation necessary on the client device.</span></span> <span data-ttu-id="db0de-108">Для работы веб-консоли Windows PowerShell требуется только правильно настроенный шлюз Windows PowerShell и браузер на устройстве клиента, который поддерживает JavaScript® и принимает cookie-файлы.</span><span class="sxs-lookup"><span data-stu-id="db0de-108">All that is required to run the web-based Windows PowerShell console is a properly-configured Windows PowerShell Web Access gateway, and a client device browser that supports JavaScript® and accepts cookies.</span></span>

<span data-ttu-id="db0de-109">Примерами клиентских устройств могут служить ноутбуки, персональные компьютеры, не являющиеся служебными, арендованные компьютеры, планшетные компьютеры, веб-киоски, компьютеры без операционной системы на базе Windows и браузеры сотовых телефонов.</span><span class="sxs-lookup"><span data-stu-id="db0de-109">Examples of client devices include laptops, non-work personal computers, borrowed computers, tablet computers, web kiosks, computers that are not running a Windows-based operating system, and cell phone browsers.</span></span> <span data-ttu-id="db0de-110">ИТ-специалисты могут выполнять важные задачи управления на удаленных серверах на базе ОС Windows с устройств, имеющих доступ к Интернету и веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="db0de-110">IT Pros can perform critical management tasks on remote Windows-based servers from devices that have access to an Internet connection and a web browser.</span></span>

<span data-ttu-id="db0de-111">После успешной установки и настройки шлюза пользователи получают доступ к консоли Windows PowerShell с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="db0de-111">After successful gateway setup and configuration, users can access a Windows PowerShell console by using a web browser.</span></span> <span data-ttu-id="db0de-112">Пользователи, открывающие защищенный веб-сайт Windows PowerShell, могут запускать веб-консоль Windows PowerShell после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="db0de-112">When users open the secured Windows PowerShell Web Access website, they can run a web-based Windows PowerShell console after successful authentication.</span></span>

<span data-ttu-id="db0de-113">Для установки и настройки Windows PowerShell Web Access требуются три шага.</span><span class="sxs-lookup"><span data-stu-id="db0de-113">Windows PowerShell Web Access setup and configuration is a three-step process:</span></span>

1.  <span data-ttu-id="db0de-114">Установка Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="db0de-114">Installing Windows PowerShell Web Access</span></span>

2.  <span data-ttu-id="db0de-115">Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="db0de-115">Configuring the gateway</span></span>

3.  <span data-ttu-id="db0de-116">Настройка правил авторизации, которые разрешают пользователям осуществлять доступ к веб-консоли Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="db0de-116">Configuring authorization rules that allow users access to the web-based Windows PowerShell console</span></span>

<span data-ttu-id="db0de-117">Перед установкой и настройкой Windows PowerShell Web Access рекомендуется внимательно ознакомиться с этим руководством, поскольку здесь содержатся инструкции по установке, удалению и обеспечению безопасности Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-117">Before you install and configure Windows PowerShell Web Access, we recommend that you read this entire guide, which includes instructions about how to install, secure, and uninstall Windows PowerShell Web Access.</span></span> <span data-ttu-id="db0de-118">В разделе [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx) описан вход пользователей в веб-консоль, представлены ограничения и различия между веб-консолью Windows PowerShell и консолью **powershell.exe**.</span><span class="sxs-lookup"><span data-stu-id="db0de-118">The [Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx) topic describes how users sign in to the web-based console, and covers limitations and differences between the web-based Windows PowerShell console and the **powershell.exe** console.</span></span> <span data-ttu-id="db0de-119">Конечным пользователям веб-консоли необходимо ознакомиться со статьей [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx), но нет необходимости читать остальное руководство.</span><span class="sxs-lookup"><span data-stu-id="db0de-119">End users of the web-based console should read [Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx), but do not need to read the rest of this guide.</span></span>

<span data-ttu-id="db0de-120">В этой статье не приводятся подробные рекомендации по работе с веб-сервером (IIS). Описаны только шаги, необходимые для настройки шлюза Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-120">This topic does not provide in-depth Web Server (IIS) operations guidance; only those steps required to configure the Windows PowerShell Web Access gateway are described in this topic.</span></span> <span data-ttu-id="db0de-121">Дополнительные сведения о настройке и обеспечении безопасности веб-сайтов в IIS см. в документации по IIS (в разделе "См. также").</span><span class="sxs-lookup"><span data-stu-id="db0de-121">For more information about configuring and securing websites in IIS, see the IIS documentation resources in the See Also section.</span></span>

<span data-ttu-id="db0de-122">Следующая схема демонстрирует работу Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-122">The following diagram shows how Windows PowerShell Web Access works.</span></span>

<span><img src="https://i-technet.sec.s-msft.com/dynimg/IC564303.jpeg" title="Windows PowerShell Web Access diagram" alt="Windows PowerShell Web Access diagram" id="ee15fa8f-ce13-49e5-933d-514f6d60a2b1" /></span>

<span data-ttu-id="db0de-123">Содержание раздела:</span><span class="sxs-lookup"><span data-stu-id="db0de-123">In this topic:</span></span>

-   [<span data-ttu-id="db0de-124">Требования для запуска Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="db0de-124">Requirements for running Windows PowerShell Web Access</span></span>](#BKMK_reqs)

-   [<span data-ttu-id="db0de-125">Поддержка браузеров и клиентских устройств</span><span class="sxs-lookup"><span data-stu-id="db0de-125">Browser and client device support</span></span>](#BKMK_browser)

-   [<span data-ttu-id="db0de-126">Рекомендуемая схема (быстрого) развертывания</span><span class="sxs-lookup"><span data-stu-id="db0de-126">Recommended (quick) deployment</span></span>](#BKMK_recm)

-   [<span data-ttu-id="db0de-127">Пользовательское развертывание</span><span class="sxs-lookup"><span data-stu-id="db0de-127">Custom deployment</span></span>](#BKMK_custom)

-   [<span data-ttu-id="db0de-128">Настройка подлинного сертификата</span><span class="sxs-lookup"><span data-stu-id="db0de-128">Configure a genuine certificate</span></span>](#BKMK_configcert)

<a href="" id="BKMK_reqs"></a>

<span data-ttu-id="db0de-129"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования для запуска Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_0" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-129"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Requirements for running Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_0" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-130">Для работы Windows PowerShell Web Access необходимо, чтобы веб-сервер (IIS), .NET Framework 4.5 и Windows PowerShell 3.0 или Windows PowerShell 4.0 выполнялись на сервере, на котором предполагается запустить шлюз.</span><span class="sxs-lookup"><span data-stu-id="db0de-130">Windows PowerShell Web Access requires Web Server (IIS), .NET Framework 4.5, and Windows PowerShell 3.0 or Windows PowerShell 4.0 to be running on the server on which you want to run the gateway.</span></span> <span data-ttu-id="db0de-131">Можно установить Windows PowerShell Web Access на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью мастера добавления ролей и компонентов в диспетчере серверов или командлетов развертывания Windows PowerShell для диспетчера серверов.</span><span class="sxs-lookup"><span data-stu-id="db0de-131">You can install Windows PowerShell Web Access on a server that is running Windows Server 2012 R2 or Windows Server 2012 by using either the Add Roles and Features Wizard in Server Manager, or Windows PowerShell deployment cmdlets for Server Manager.</span></span> <span data-ttu-id="db0de-132">При установке Windows PowerShell Web Access с помощью диспетчера серверов или командлетов развертывания необходимые роли и компоненты добавляются автоматически в процессе установки.</span><span class="sxs-lookup"><span data-stu-id="db0de-132">When you install Windows PowerShell Web Access by using Server Manager or its deployment cmdlets, required roles and features are automatically added as part of the installation process.</span></span>

<span data-ttu-id="db0de-133">Windows PowerShell Web Access позволяет удаленным пользователям получать доступ к компьютерам в вашей организации, используя Windows PowerShell в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="db0de-133">Windows PowerShell Web Access allows remote users to access computers in your organization by using Windows PowerShell in a web browser.</span></span> <span data-ttu-id="db0de-134">Хотя Windows PowerShell Web Access является удобным и мощным инструментом управления, доступ через Интернет связан с рисками для безопасности и должен настраиваться с максимально возможной безопасностью.</span><span class="sxs-lookup"><span data-stu-id="db0de-134">Although Windows PowerShell Web Access is a convenient and powerful management tool, the web-based access poses security risks, and should be configured as securely as possible.</span></span> <span data-ttu-id="db0de-135">Мы рекомендуем администраторам, настраивающим шлюз Windows PowerShell Web Access, использовать как уровни безопасности, доступные в правилах авторизации на основе командлетов, включаемых в Windows PowerShell Web Access, так и уровни безопасности, доступные в веб-сервере (IIS) и приложениях сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="db0de-135">We recommend that administrators who configure the Windows PowerShell Web Access gateway use available security layers, both the cmdlet-based authorization rules included with Windows PowerShell Web Access, and security layers that are available in Web Server (IIS) and third-party applications.</span></span> <span data-ttu-id="db0de-136">В данную документацию включены как небезопасные примеры, которые рекомендуются только для тестовых сред, так и примеры, рекомендуемые для безопасного развертывания.</span><span class="sxs-lookup"><span data-stu-id="db0de-136">This documentation includes both unsecure examples that are only recommended for test environments, as well as examples that are recommended for secure deployments.</span></span>

<a href="" id="BKMK_browser"></a>

<span data-ttu-id="db0de-137"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Поддержка браузеров и клиентских устройств</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-137"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Browser and client device support</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-138">Windows PowerShell Web Access поддерживает перечисленные ниже веб-браузеры.</span><span class="sxs-lookup"><span data-stu-id="db0de-138">Windows PowerShell Web Access supports the following Internet browsers.</span></span> <span data-ttu-id="db0de-139">Хотя браузеры для мобильных устройств официально не поддерживаются, многие из них могут выполнять веб-консоль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db0de-139">Although mobile browsers are not officially supported, many may be able to run the web-based Windows PowerShell console.</span></span> <span data-ttu-id="db0de-140">Ожидается, что другие браузеры, которые принимают куки-файлы, выполняют JavaScript и выполняют веб-сайты HTTPS, также будут работать, но официально они не протестированы.</span><span class="sxs-lookup"><span data-stu-id="db0de-140">Other browsers that accept cookies, run JavaScript, and run HTTPS websites are expected to work, but are not officially tested.</span></span>

###

<span data-ttu-id="db0de-141"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Поддерживаемые браузеры для настольных компьютеров</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-141"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Supported desktop computer browsers</span></a></span></span>

------------------------------------------------------------------------

-   <span data-ttu-id="db0de-142">Windows® Internet Explorer® для Microsoft Windows® 8.0, 9.0, 10.0 и 11.0</span><span class="sxs-lookup"><span data-stu-id="db0de-142">Windows® Internet Explorer® for Microsoft Windows® 8.0, 9.0, 10.0, and 11.0</span></span>

-   <span data-ttu-id="db0de-143">Mozilla Firefox® 10.0.2</span><span class="sxs-lookup"><span data-stu-id="db0de-143">Mozilla Firefox® 10.0.2</span></span>

-   <span data-ttu-id="db0de-144">Google Chrome™ 17.0.963.56m для Windows</span><span class="sxs-lookup"><span data-stu-id="db0de-144">Google Chrome™ 17.0.963.56m for Windows</span></span>

-   <span data-ttu-id="db0de-145">Apple Safari® 5.1.2 для Windows</span><span class="sxs-lookup"><span data-stu-id="db0de-145">Apple Safari® 5.1.2 for Windows</span></span>

-   <span data-ttu-id="db0de-146">Apple Safari 5.1.2 для Mac OS®</span><span class="sxs-lookup"><span data-stu-id="db0de-146">Apple Safari 5.1.2 for Mac OS®</span></span>

###

<span data-ttu-id="db0de-147"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Минимально протестированные мобильные устройства или браузеры</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-147"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Minimally-tested mobile devices or browsers</span></a></span></span>

------------------------------------------------------------------------

-   <span data-ttu-id="db0de-148">Windows Phone 7 и 7.5</span><span class="sxs-lookup"><span data-stu-id="db0de-148">Windows Phone 7 and 7.5</span></span>

-   <span data-ttu-id="db0de-149">Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)</span><span class="sxs-lookup"><span data-stu-id="db0de-149">Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)</span></span>

-   <span data-ttu-id="db0de-150">Apple Safari для операционной системы 5.0.1 для iPhone</span><span class="sxs-lookup"><span data-stu-id="db0de-150">Apple Safari for iPhone operating system 5.0.1</span></span>

-   <span data-ttu-id="db0de-151">Apple Safari для операционной системы 5.0.1 для iPad 2</span><span class="sxs-lookup"><span data-stu-id="db0de-151">Apple Safari for iPad 2 operating system 5.0.1</span></span>

###

<span data-ttu-id="db0de-152"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования к браузерам</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-152"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Browser requirements</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-153">Чтобы использовать веб-консоль Windows PowerShell Web Access, браузеры должны иметь следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="db0de-153">To use the Windows PowerShell Web Access web-based console, browsers must do the following.</span></span>

-   <span data-ttu-id="db0de-154">Разрешать файлы cookie с веб-сайта шлюза Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-154">Allow cookies from the Windows PowerShell Web Access gateway website.</span></span>

-   <span data-ttu-id="db0de-155">Открывать и читать HTTPS-страницы.</span><span class="sxs-lookup"><span data-stu-id="db0de-155">Be able to open and read HTTPS pages.</span></span>

-   <span data-ttu-id="db0de-156">Открывать и выполнять веб-сайты, использующие JavaScript.</span><span class="sxs-lookup"><span data-stu-id="db0de-156">Open and run websites that use JavaScript.</span></span>

<a href="" id="BKMK_recm"></a>

<span data-ttu-id="db0de-157"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Рекомендуемая схема (быстрого) развертывания</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-157"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Recommended (quick) deployment</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-158">Шлюз Windows PowerShell Web Access можно установить на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью командлетов развертывания Windows PowerShell или мастера добавления ролей и компонентов в диспетчере серверов.</span><span class="sxs-lookup"><span data-stu-id="db0de-158">You can install the Windows PowerShell Web Access gateway on a server that is running Windows Server 2012 R2 or Windows Server 2012 by using either Windows PowerShell cmdlets, or by using the Add Roles and Features Wizard that is opened from within Server Manager.</span></span> <span data-ttu-id="db0de-159">Для быстрой установки и настройки воспользуйтесь командлетами Windows PowerShell, как описано в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="db0de-159">For quick installation and configuration, use Windows PowerShell cmdlets, as described in this section.</span></span>

-   [<span data-ttu-id="db0de-160">Шаг 1. Установка Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="db0de-160">Step 1: Install Windows PowerShell Web Access</span></span>](#BKMK_step1)

-   [<span data-ttu-id="db0de-161">Шаг 2. Настройка шлюза</span><span class="sxs-lookup"><span data-stu-id="db0de-161">Step 2: Configure the gateway</span></span>](#BKMK_step2)

-   [<span data-ttu-id="db0de-162">Шаг 3. Настройка ограничивающего правила авторизации</span><span class="sxs-lookup"><span data-stu-id="db0de-162">Step 3: Configure a restrictive authorization rule</span></span>](#BKMK_step3)

<a href="" id="BKMK_step1"></a>
###

<span data-ttu-id="db0de-163"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Установка Windows PowerShell Web Access</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-163"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 1: Install Windows PowerShell Web Access</span></a></span></span>

------------------------------------------------------------------------

#### <a name="to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a><span data-ttu-id="db0de-164">Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="db0de-164">To install Windows PowerShell Web Access by using Windows PowerShell cmdlets</span></span>

1.  <span data-ttu-id="db0de-165">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="db0de-165">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span>

    -   <span data-ttu-id="db0de-166">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-166">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="db0de-167">На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-167">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-168"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-168"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-169">В Windows PowerShell 3.0 и 4.0 не нужно импортировать модуль командлета диспетчера серверов в сеанс Windows PowerShell перед запуском командлетов, которые являются частью этого модуля.</span><span class="sxs-lookup"><span data-stu-id="db0de-169">In Windows PowerShell 3.0 and 4.0, there is no need to import the Server Manager cmdlet module into the Windows PowerShell session before running cmdlets that are part of the module.</span></span> <span data-ttu-id="db0de-170">Модуль автоматически импортируется при первом выполнении командлета, входящего в модуль.</span><span class="sxs-lookup"><span data-stu-id="db0de-170">A module is automatically imported the first time you run a cmdlet that is part of the module.</span></span> <span data-ttu-id="db0de-171">Кроме того, командлеты Windows PowerShell не учитывают регистр.</span><span class="sxs-lookup"><span data-stu-id="db0de-171">Also, Windows PowerShell cmdlets are not case-sensitive.</span></span></p></td>
    </tr>
    </tbody>
    </table>

2.  <span data-ttu-id="db0de-172">Введите следующую команду и нажмите клавишу **ВВОД**, где *computer_name* представляет имя удаленного компьютера, на который требуется установить Windows PowerShell Web Access, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="db0de-172">Type the following, and then press **Enter**, where *computer_name* represents a remote computer on which you want to install Windows PowerShell Web Access, if applicable.</span></span> <span data-ttu-id="db0de-173">Параметр <span class="code">Restart</span> автоматически перезапускает целевой сервер при необходимости.</span><span class="sxs-lookup"><span data-stu-id="db0de-173">The <span class="code">Restart</span> parameter automatically restarts destination servers if required.</span></span>

    [<span data-ttu-id="db0de-174">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-174">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_374a9c21-4f6e-471e-b957-bb190a594533'); "Копировать в буфер обмена".)

        Install-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-175"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-175"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-176">Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell не добавляет средства управления веб-сервера (IIS) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="db0de-176">Installing Windows PowerShell Web Access by using Windows PowerShell cmdlets does not add Web Server (IIS) management tools by default.</span></span> <span data-ttu-id="db0de-177">Если требуется установить средства управления на тот же сервер, на котором выполняется шлюз Windows PowerShell Web Access, добавьте в команду установки параметр <span class="code">IncludeManagementTools</span> (как указано в этом шаге).</span><span class="sxs-lookup"><span data-stu-id="db0de-177">If you want to install the management tools on the same server as the Windows PowerShell Web Access gateway, add the <span class="code">IncludeManagementTools</span> parameter to the installation command (as provided in this step).</span></span> <span data-ttu-id="db0de-178">Если управление веб-сайтом Windows PowerShell Web Access осуществляется с удаленного компьютера, установите оснастку "Диспетчер служб IIS", установив <a href="http://go.microsoft.com/fwlink/?LinkID=304145">Средства удаленного администрирования сервера для Windows 8.1</a> или <a href="http://go.microsoft.com/fwlink/p/?LinkID=238560">Средства удаленного администрирования сервера для Windows 8</a> на компьютере, с которого будет осуществляться управление шлюзом.</span><span class="sxs-lookup"><span data-stu-id="db0de-178">If you are managing the Windows PowerShell Web Access website from a remote computer, install the IIS Manager snap-in by installing <a href="http://go.microsoft.com/fwlink/?LinkID=304145">Remote Server Administration Tools for Windows 8.1</a> or <a href="http://go.microsoft.com/fwlink/p/?LinkID=238560">Remote Server Administration Tools for Windows 8</a> on the computer from which you want to manage the gateway.</span></span></p></td>
    </tr>
    </tbody>
    </table>

    <span data-ttu-id="db0de-179">Чтобы установить роли и компоненты на автономном виртуальном жестком диске (VHD), необходимо добавить оба параметра — <span class="code">ComputerName</span> и <span class="code">VHD</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-179">To install roles and features on an offline VHD, you must add both the <span class="code">ComputerName</span> parameter and the <span class="code">VHD</span> parameter.</span></span> <span data-ttu-id="db0de-180">Параметр <span class="code">ComputerName</span> содержит имя сервера, на котором следует подключить виртуальный жесткий диск, а параметр <span class="code">VHD</span> — путь к VHD-файлу на указанном сервере.</span><span class="sxs-lookup"><span data-stu-id="db0de-180">The <span class="code">ComputerName</span> parameter contains the name of the server on which to mount the VHD, and the <span class="code">VHD</span> parameter contains the path to the VHD file on the specified server.</span></span>

    [<span data-ttu-id="db0de-181">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-181">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_d841d509-347e-49d0-bf54-8d1f306bece6'); "Копировать в буфер обмена".)

        Install-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart

3.  <span data-ttu-id="db0de-182">Когда установка завершена, убедитесь, что Windows PowerShell Web Access установлен на целевых серверах, запустив командлет **Get-WindowsFeature** на целевом сервере в консоли Windows PowerShell, которая была открыта с повышенными правами пользователя.</span><span class="sxs-lookup"><span data-stu-id="db0de-182">When installation is complete, verify that Windows PowerShell Web Access was installed on destination servers by running the **Get-WindowsFeature** cmdlet on a destination server, in a Windows PowerShell console that has been opened with elevated user rights.</span></span> <span data-ttu-id="db0de-183">Можно также проверить установку Windows PowerShell Web Access в консоли диспетчера серверов, выбрав целевой сервер на странице **Все серверы**, а затем просмотрев плитку **Роли и компоненты** для выбранного сервера.</span><span class="sxs-lookup"><span data-stu-id="db0de-183">You can also verify that Windows PowerShell Web Access was installed in the Server Manager console, by selecting a destination server on the **All Servers** page, and then viewing the **Roles and Features** tile for the selected server.</span></span> <span data-ttu-id="db0de-184">Можно также просмотреть файл сведений для Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-184">You can also view the readme file for Windows PowerShell Web Access.</span></span>

4.  <span data-ttu-id="db0de-185">После завершения установки Windows PowerShell Web Access выводится приглашение прочитать файл сведений, содержащий основные инструкции по установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="db0de-185">After Windows PowerShell Web Access is installed, you are prompted to review the readme file, which contains basic, required setup instructions for the gateway.</span></span> <span data-ttu-id="db0de-186">Эти инструкции по установке приводятся также в следующем разделе [Шаг 2. Настройка шлюза](#BKMK_step2).</span><span class="sxs-lookup"><span data-stu-id="db0de-186">These setup instructions are also in the following section, [Step 2: Configure the gateway](#BKMK_step2).</span></span> <span data-ttu-id="db0de-187">Путь к файлу сведений: <span class="computerOutputInline">C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-187">The path to the readme file is <span class="computerOutputInline">C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>.</span></span>

<a href="" id="BKMK_step2"></a>
###

<span data-ttu-id="db0de-188"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Настройка шлюза</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-188"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 2: Configure the gateway</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-189">Командлет **Install-PswaWebApplication** позволяет быстро выполнить настройку Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-189">The **Install-PswaWebApplication** cmdlet is a quick way to get Windows PowerShell Web Access configured.</span></span> <span data-ttu-id="db0de-190">Хотя можно добавить параметр <span class="code">UseTestCertificate</span> в командлет <span class="code">Install-PswaWebApplication</span>, чтобы установить самозаверяющий SSL-сертификат для целей тестирования, это небезопасно. Для безопасной производственной среды всегда используйте действительный SSL-сертификат, подписанный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="db0de-190">Although you can add the <span class="code">UseTestCertificate</span> parameter to the <span class="code">Install-PswaWebApplication</span> cmdlet to install a self-signed SSL certificate for test purposes, this is not secure; for a secure production environment, always use a valid SSL certificate that has been signed by a certification authority (CA).</span></span> <span data-ttu-id="db0de-191">Администраторы могут заменить тестовый сертификат на подписанный сертификат по своему выбору с помощью консоли "Диспетчер служб IIS".</span><span class="sxs-lookup"><span data-stu-id="db0de-191">Administrators can replace the test certificate with a signed certificate of their choice by using the IIS Manager console.</span></span>

<span data-ttu-id="db0de-192">Вы можете завершить настройку веб-приложения Windows PowerShell Web Access с помощью командлета <span class="code">Install-PswaWebApplication</span> или выполнив процедуру настройки через пользовательский интерфейс диспетчера служб IIS.</span><span class="sxs-lookup"><span data-stu-id="db0de-192">You can complete Windows PowerShell Web Access web application configuration either by running the <span class="code">Install-PswaWebApplication</span> cmdlet or by performing GUI-based configuration steps in IIS Manager.</span></span> <span data-ttu-id="db0de-193">По умолчанию командлет устанавливает веб-приложение **pswa** (и пул приложений для него, **pswa_pool**) в контейнер **Веб-сайт по умолчанию**, как показано в диспетчере служб IIS. Если требуется, вы можете изменить в командлете контейнер сайта по умолчанию для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="db0de-193">By default, the cmdlet installs the web application, **pswa** (and an application pool for it, **pswa_pool**), in the **Default Web Site** container, as shown in IIS Manager; if desired, you can instruct the cmdlet to change the default site container of the web application.</span></span> <span data-ttu-id="db0de-194">Диспетчер служб IIS предлагает параметры настройки, доступные для веб-приложений, например, изменение номера порта или SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="db0de-194">IIS Manager offers configuration options that are available for web applications, such as changing the port number or the Secure Sockets Layer (SSL) certificate.</span></span>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th><span data-ttu-id="db0de-195"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Примечание о безопасности </span></span><span class="sxs-lookup"><span data-stu-id="db0de-195"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Security Note </span></span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span data-ttu-id="db0de-196">Мы настоятельно рекомендуем администраторам настраивать шлюз на использование действительного сертификата, подписанного центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="db0de-196">We strongly recommend that administrators configure the gateway to use a valid certificate that has been signed by a CA.</span></span></p></td>
</tr>
</tbody>
</table>

-   [<span data-ttu-id="db0de-197">Настройка шлюза Windows PowerShell Web Access с тестовым сертификатом с помощью командлета Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="db0de-197">To configure the Windows PowerShell Web Access gateway with a test certificate by using Install-PswaWebApplication</span></span>](#BKMK_testcert)

-   [<span data-ttu-id="db0de-198">Настройка шлюза Windows PowerShell Web Access с подлинным сертификатом с использованием командлета Install-PswaWebApplication и диспетчера IIS</span><span class="sxs-lookup"><span data-stu-id="db0de-198">To configure the Windows PowerShell Web Access gateway with a genuine certificate by using Install-PswaWebApplication and IIS Manager</span></span>](#BKMK_gencert)

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-test-certificate-by-using-install-pswawebapplication"></a><span data-ttu-id="db0de-199">Настройка шлюза Windows PowerShell Web Access с тестовым сертификатом с помощью Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="db0de-199">To configure the Windows PowerShell Web Access gateway with a test certificate by using Install-PswaWebApplication</span></span>

1.  <span data-ttu-id="db0de-200">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db0de-200">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="db0de-201">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.</span><span class="sxs-lookup"><span data-stu-id="db0de-201">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="db0de-202">На **начальном** экране Windows щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="db0de-202">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2.  <span data-ttu-id="db0de-203">Введите следующую команду и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="db0de-203">Type the following, and then press **Enter**.</span></span>

    <span data-ttu-id="db0de-204">**Install-PswaWebApplication -UseTestCertificate**</span><span class="sxs-lookup"><span data-stu-id="db0de-204">**Install-PswaWebApplication -UseTestCertificate**</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-205"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Примечание о безопасности </span></span><span class="sxs-lookup"><span data-stu-id="db0de-205"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Security Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-206">Параметр <span class="code">UseTestCertificate</span> следует использовать только в частной тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="db0de-206">The <span class="code">UseTestCertificate</span> parameter should only be used in a private test environment.</span></span> <span data-ttu-id="db0de-207">Для безопасной производственной среды мы рекомендуем использовать действительный сертификат, подписанный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="db0de-207">For a secure production environment, we recommend using a valid certificate that has been signed by a CA.</span></span></p></td>
    </tr>
    </tbody>
    </table>

    <span data-ttu-id="db0de-208">При выполнении командлета веб-приложение Windows PowerShell Web Access устанавливается в контейнер IIS "Веб-сайт по умолчанию".</span><span class="sxs-lookup"><span data-stu-id="db0de-208">Running the cmdlet installs the Windows PowerShell Web Access web application within the IIS Default Web Site container.</span></span> <span data-ttu-id="db0de-209">Этот командлет создает инфраструктуру, необходимую для выполнения Windows PowerShell Web Access на веб-сайте по умолчанию https://&lt;имя_сервера&gt;/pswa.</span><span class="sxs-lookup"><span data-stu-id="db0de-209">The cmdlet creates the infrastructure required to run Windows PowerShell Web Access on the default website, https://&lt;server_name&gt;/pswa.</span></span> <span data-ttu-id="db0de-210">Чтобы установить веб-приложение на другой веб-сайт, введите имя веб-сайта, добавив параметр <span class="code">WebSiteName</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-210">To install the web application in a different website, provide the website name by adding the <span class="code">WebSiteName</span> parameter.</span></span> <span data-ttu-id="db0de-211">Чтобы изменить имя веб-приложения (по умолчанию <span class="code">pswa</span>), добавьте параметр <span class="code">WebApplicationName</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-211">To change the name of the web application (the default is <span class="code">pswa</span>), add the <span class="code">WebApplicationName</span> parameter.</span></span>

    <span data-ttu-id="db0de-212">Следующие параметры настраиваются при выполнении командлета.</span><span class="sxs-lookup"><span data-stu-id="db0de-212">The following settings are configured by running the cmdlet.</span></span> <span data-ttu-id="db0de-213">Если требуется, вы можете изменить их вручную в консоли "Диспетчер служб IIS".</span><span class="sxs-lookup"><span data-stu-id="db0de-213">You can change these manually in the IIS Manager console, if desired.</span></span>

    -   <span data-ttu-id="db0de-214">Path: /pswa</span><span class="sxs-lookup"><span data-stu-id="db0de-214">Path: /pswa</span></span>

    -   <span data-ttu-id="db0de-215">ApplicationPool: pswa_pool</span><span class="sxs-lookup"><span data-stu-id="db0de-215">ApplicationPool: pswa_pool</span></span>

    -   <span data-ttu-id="db0de-216">EnabledProtocols: http</span><span class="sxs-lookup"><span data-stu-id="db0de-216">EnabledProtocols: http</span></span>

    -   <span data-ttu-id="db0de-217">PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot</span><span class="sxs-lookup"><span data-stu-id="db0de-217">PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot</span></span>

    <span data-ttu-id="db0de-218"><span class="label">Пример:</span> <span class="code">Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate</span></span><span class="sxs-lookup"><span data-stu-id="db0de-218"><span class="label">Example:</span> <span class="code">Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate</span></span></span>

    <span data-ttu-id="db0de-219">В этом примере адрес результирующего сайта для Windows PowerShell Web Access таков: https://&lt;*имя_сервера*&gt;/myWebApp.</span><span class="sxs-lookup"><span data-stu-id="db0de-219">In this example, the resulting website for Windows PowerShell Web Access is https://&lt; *server_name*&gt;/myWebApp.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-220"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-220"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-221">Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-221">You cannot sign in until users have been granted access to the website by adding authorization rules.</span></span> <span data-ttu-id="db0de-222">Дополнительные сведения см. в разделе <a href="#BKMK_step3">Шаг 3. Настройка ограничивающего правила авторизации</a> и <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access</a>.</span><span class="sxs-lookup"><span data-stu-id="db0de-222">For more information, see <a href="#BKMK_step3">Step 3: Configure a restrictive authorization rule</a> and <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Authorization Rules and Security Features of Windows PowerShell Web Access</a>.</span></span></p></td>
    </tr>
    </tbody>
    </table>

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-genuine-certificate-by-using-install-pswawebapplication-and-iis-manager"></a><span data-ttu-id="db0de-223">Настройка шлюза Windows PowerShell Web Access с подлинным сертификатом с использованием командлета Install-PswaWebApplication и диспетчера IIS</span><span class="sxs-lookup"><span data-stu-id="db0de-223">To configure the Windows PowerShell Web Access gateway with a genuine certificate by using Install-PswaWebApplication and IIS Manager</span></span>

1.  <span data-ttu-id="db0de-224">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db0de-224">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="db0de-225">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.</span><span class="sxs-lookup"><span data-stu-id="db0de-225">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="db0de-226">На **начальном** экране Windows щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="db0de-226">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2.  <span data-ttu-id="db0de-227">Введите следующую команду и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="db0de-227">Type the following, and then press **Enter**.</span></span>

    <span data-ttu-id="db0de-228">**Install-PswaWebApplication**</span><span class="sxs-lookup"><span data-stu-id="db0de-228">**Install-PswaWebApplication**</span></span>

    <span data-ttu-id="db0de-229">Следующие параметры шлюза настраиваются при выполнении командлета.</span><span class="sxs-lookup"><span data-stu-id="db0de-229">The following gateway settings are configured by running the cmdlet.</span></span> <span data-ttu-id="db0de-230">Если требуется, вы можете изменить их вручную в консоли "Диспетчер служб IIS".</span><span class="sxs-lookup"><span data-stu-id="db0de-230">You can change these manually in the IIS Manager console, if desired.</span></span> <span data-ttu-id="db0de-231">Можно также указать значения для параметров <span class="code">WebsiteName</span> и <span class="code">WebApplicationName</span> командлета <span class="code">Install-PswaWebApplication</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-231">You can also specify values for the <span class="code">WebsiteName</span> and <span class="code">WebApplicationName</span> parameters of the <span class="code">Install-PswaWebApplication</span> cmdlet.</span></span>

    -   <span data-ttu-id="db0de-232">Path: /pswa</span><span class="sxs-lookup"><span data-stu-id="db0de-232">Path: /pswa</span></span>

    -   <span data-ttu-id="db0de-233">ApplicationPool: pswa_pool</span><span class="sxs-lookup"><span data-stu-id="db0de-233">ApplicationPool: pswa_pool</span></span>

    -   <span data-ttu-id="db0de-234">EnabledProtocols: http</span><span class="sxs-lookup"><span data-stu-id="db0de-234">EnabledProtocols: http</span></span>

    -   <span data-ttu-id="db0de-235">PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot</span><span class="sxs-lookup"><span data-stu-id="db0de-235">PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot</span></span>

3.  <span data-ttu-id="db0de-236">Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="db0de-236">Open the IIS Manager console by doing one of the following.</span></span>

    -   <span data-ttu-id="db0de-237">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="db0de-237">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="db0de-238">В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="db0de-238">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="db0de-239">На **начальном** экране в Windows выберите **Диспетчер серверов**.</span><span class="sxs-lookup"><span data-stu-id="db0de-239">On the Windows **Start** screen, click **Server Manager**.</span></span>

4.  <span data-ttu-id="db0de-240">В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-240">In the IIS Manager tree pane, expand the node for the server on which Windows PowerShell Web Access is installed until the **Sites** folder is visible.</span></span> <span data-ttu-id="db0de-241">Разверните папку **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-241">Expand the **Sites** folder.</span></span>

5.  <span data-ttu-id="db0de-242">Выберите веб-сайт, на котором было установлено веб-приложение Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-242">Select the website in which you have installed the Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="db0de-243">В области **Действия** щелкните элемент **Привязки**.</span><span class="sxs-lookup"><span data-stu-id="db0de-243">In the **Actions** pane, click **Bindings**.</span></span>

6.  <span data-ttu-id="db0de-244">В диалоговом окне **Привязки сайта** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="db0de-244">In the **Site Binding** dialog box, click **Add**.</span></span>

7.  <span data-ttu-id="db0de-245">В диалоговом окне **Добавление привязки сайта** выберите в поле **Тип** значение **https**.</span><span class="sxs-lookup"><span data-stu-id="db0de-245">In the **Add Site Binding** dialog box, in the **Type** field, select **https**.</span></span>

8.  <span data-ttu-id="db0de-246">В поле **Сертификат SSL** выберите ваш подписанный сертификат в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="db0de-246">In the **SSL certificate** field, select your signed certificate from the drop-down menu.</span></span> <span data-ttu-id="db0de-247">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-247">Click **OK**.</span></span> <span data-ttu-id="db0de-248">Дополнительные сведения о получении сертификата см. в разделе [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) в данной статье.</span><span class="sxs-lookup"><span data-stu-id="db0de-248">See [To configure an SSL certificate in IIS Manager](#BKMK_cert) in this topic for more information about how to obtain a certificate.</span></span>

    <span data-ttu-id="db0de-249">Теперь веб-приложение Windows PowerShell Web Access настроено для использования вашего подписанного сертификата.</span><span class="sxs-lookup"><span data-stu-id="db0de-249">The Windows PowerShell Web Access web application is now configured to use your signed SSL certificate.</span></span> <span data-ttu-id="db0de-250">Чтобы получить доступ к Windows PowerShell Web Access, откройте https://&lt;имя_сервера&gt;/pswa в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="db0de-250">You can access Windows PowerShell Web Access by opening https://&lt;server_name&gt;/pswa in a browser window.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-251"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-251"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-252">Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-252">You cannot sign in until users have been granted access to the website by adding authorization rules.</span></span> <span data-ttu-id="db0de-253">Дополнительные сведения см. в разделе <a href="#BKMK_step3">Шаг 3. Настройка ограничивающего правила авторизации</a> и <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access</a>.</span><span class="sxs-lookup"><span data-stu-id="db0de-253">For more information, see <a href="#BKMK_step3">Step 3: Configure a restrictive authorization rule</a> and <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Authorization Rules and Security Features of Windows PowerShell Web Access</a>.</span></span></p></td>
    </tr>
    </tbody>
    </table><span data-ttu-id="db0de-254">

<a href="" id="BKMK_step3"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 3. Настройка ограничивающего правила авторизации</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-254">

<a href="" id="BKMK_step3"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 3: Configure a restrictive authorization rule</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-255">После установки Windows PowerShell Web Access и настройки шлюза пользователи могут открывать страницу входа в браузере, но они не могут выполнить вход, пока администратор Windows PowerShell Web Access не предоставит им доступ в явном виде.</span><span class="sxs-lookup"><span data-stu-id="db0de-255">After Windows PowerShell Web Access is installed and the gateway is configured, users can open the sign-in page in a browser, but they cannot sign in until the Windows PowerShell Web Access administrator grants users access explicitly.</span></span> <span data-ttu-id="db0de-256">Управление доступом в Windows PowerShell Web Access осуществляется с помощью набора командлетов Windows PowerShell, описанных в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="db0de-256">Windows PowerShell Web Access access control is managed by using the set of Windows PowerShell cmdlets described in the following table.</span></span> <span data-ttu-id="db0de-257">Нет соответствующего графического пользовательского интерфейса для добавления правил авторизации или управления ими.</span><span class="sxs-lookup"><span data-stu-id="db0de-257">There is no comparable GUI for adding or managing authorization rules.</span></span> <span data-ttu-id="db0de-258">Подробные сведения о командлетах Windows PowerShell Web Access см. в справочных разделах по командлетам в статье [Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-258">For more detailed information about Windows PowerShell Web Access cmdlets, see the cmdlet reference topics, [Windows PowerShell Web Access Cmdlets](https://technet.microsoft.com/library/hh918342.aspx).</span></span>

<span data-ttu-id="db0de-259">Дополнительные сведения о безопасности и правилах авторизации Windows PowerShell Web Access см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-259">For more detail about Windows PowerShell Web Access authorization rules and security, see [Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx).</span></span>

#### <a name="to-add-a-restrictive-authorization-rule"></a><span data-ttu-id="db0de-260">Добавление ограничивающего правила авторизации</span><span class="sxs-lookup"><span data-stu-id="db0de-260">To add a restrictive authorization rule</span></span>

1.  <span data-ttu-id="db0de-261">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="db0de-261">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span>

    -   <span data-ttu-id="db0de-262">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-262">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="db0de-263">На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-263">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

2.  <span data-ttu-id="db0de-264"><span class="label">Необязательный шаг для ограничения доступа пользователей с помощью конфигураций сеансов: </span> убедитесь, что конфигурации сеансов, которые вы хотите использовать в своих правилах, уже существуют.</span><span class="sxs-lookup"><span data-stu-id="db0de-264"><span class="label">Optional step for restricting user access by using session configurations:</span> Verify that session configurations that you want to use in your rules already exist.</span></span> <span data-ttu-id="db0de-265">В противном случае выполните инструкции по созданию конфигураций сеансов, приведенные в статье [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="db0de-265">If they have not yet been created, use instructions for creating session configurations in [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) on MSDN.</span></span>

3.  <span data-ttu-id="db0de-266">Введите следующую команду и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="db0de-266">Type the following, and then press **Enter**.</span></span>

    [<span data-ttu-id="db0de-267">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-267">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_f9e7959b-75d0-4d63-8f8e-02334a8dd09d'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    <span data-ttu-id="db0de-268">Это правило авторизации разрешает конкретному пользователю доступ к одному сетевому компьютеру, к которому обычно требуется доступ, с доступом к конкретной конфигурации сеанса, область которого соответствует потребностям пользовательских скриптов и командлетов.</span><span class="sxs-lookup"><span data-stu-id="db0de-268">This authorization rule allows a specific user access to one computer on the network to which they typically have access, with access to a specific session configuration that is scoped to the user’s typical scripting and cmdlet needs.</span></span> <span data-ttu-id="db0de-269">В следующем примере пользователю с именем <span class="code">JSmith</span> в домене <span class="code">Contoso</span> предоставляется доступ для управления компьютером <span class="code">Contoso\_214</span> и использования конфигурации сеанса с именем <span class="code">NewAdminsOnly</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-269">In the following example, a user named <span class="code">JSmith</span> in the <span class="code">Contoso</span> domain is granted access to manage the computer <span class="code">Contoso_214</span>, and use a session configuration named <span class="code">NewAdminsOnly</span>.</span></span>

    [<span data-ttu-id="db0de-270">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-270">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ebd5bc5e-ec5d-4955-a86a-63843e480e37'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  <span data-ttu-id="db0de-271">Убедитесь, что правило создано, выполнив командлет **Get-PswaAuthorizationRule** или **Test-PswaAuthorizationRule -UserName &lt;домен\\пользователь | компьютер\\пользователь&gt; -ComputerName** &lt;имя_компьютера&gt;.</span><span class="sxs-lookup"><span data-stu-id="db0de-271">Verify that the rule has been created by running either the **Get-PswaAuthorizationRule** cmdlet, or **Test-PswaAuthorizationRule -UserName &lt;domain\\user | computer\\user&gt; -ComputerName** &lt;computer_name&gt;.</span></span> <span data-ttu-id="db0de-272">Например, **Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214**.</span><span class="sxs-lookup"><span data-stu-id="db0de-272">For example, **Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214**.</span></span>

<span data-ttu-id="db0de-273">После настройки правила авторизации авторизованные пользователи могут выполнить вход в веб-консоль и приступить к использованию Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-273">After you have configured an authorization rule, you are ready for authorized users to sign in to the web-based console and begin using Windows PowerShell Web Access.</span></span>

<a href="" id="BKMK_custom"></a>

<span data-ttu-id="db0de-274"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Пользовательское развертывание</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-274"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Custom deployment</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-275">Шлюз Windows PowerShell Web Access можно установить на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью мастера добавления ролей и компонентов в диспетчере серверов.</span><span class="sxs-lookup"><span data-stu-id="db0de-275">You can install the Windows PowerShell Web Access gateway on a server that is running Windows Server 2012 R2 or Windows Server 2012 by using the Add Roles and Features Wizard in Server Manager.</span></span> <span data-ttu-id="db0de-276">После установки Windows PowerShell Web Access можно настроить конфигурацию шлюза в диспетчере IIS.</span><span class="sxs-lookup"><span data-stu-id="db0de-276">After Windows PowerShell Web Access is installed, you can customize the configuration of the gateway in IIS Manager.</span></span>

<a href="" id="BKMK_custom1"></a>
###

<span data-ttu-id="db0de-277"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Установка Windows PowerShell Web Access</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-277"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 1: Install Windows PowerShell Web Access</span></a></span></span>

------------------------------------------------------------------------

#### <a name="to-install-windows-powershell-web-access-by-using-the-add-roles-and-features-wizard"></a><span data-ttu-id="db0de-278">Установка Windows PowerShell Web Access с помощью мастера добавления ролей и компонентов</span><span class="sxs-lookup"><span data-stu-id="db0de-278">To install Windows PowerShell Web Access by using the Add Roles and Features Wizard</span></span>

1.  <span data-ttu-id="db0de-279">Если диспетчер серверов уже открыт, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="db0de-279">If Server Manager is already open, go on to the next step.</span></span> <span data-ttu-id="db0de-280">Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="db0de-280">If Server Manager is not already open, open it by doing one of the following.</span></span>

    -   <span data-ttu-id="db0de-281">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="db0de-281">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span>

    -   <span data-ttu-id="db0de-282">На **начальном** экране в Windows выберите **Диспетчер серверов**.</span><span class="sxs-lookup"><span data-stu-id="db0de-282">On the Windows **Start** screen, click **Server Manager**.</span></span>

2.  <span data-ttu-id="db0de-283">В меню **Управление** выберите команду **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-283">On the **Manage** menu, click **Add Roles and Features**.</span></span>

3.  <span data-ttu-id="db0de-284">На странице **Выбор типа установки** выберите **Установка ролей или компонентов**.</span><span class="sxs-lookup"><span data-stu-id="db0de-284">On the **Select installation type** page, select **Role-based or feature-based installation**.</span></span> <span data-ttu-id="db0de-285">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="db0de-285">Click **Next**.</span></span>

4.  <span data-ttu-id="db0de-286">На странице **Выбор целевого сервера** выберите сервер из пула серверов или автономный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="db0de-286">On the **Select destination server** page, select a server from the server pool, or select an offline VHD.</span></span> <span data-ttu-id="db0de-287">Чтобы выбрать автономный виртуальный жесткий диск в качестве конечного сервера, сначала выберите сервер, на котором будет подключен виртуальный жесткий диск, а затем выберите VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="db0de-287">To select an offline VHD as your destination server, first select the server on which to mount the VHD, and then select the VHD file.</span></span> <span data-ttu-id="db0de-288">Сведения о добавлении серверов в пул серверов см. в справке диспетчера серверов.</span><span class="sxs-lookup"><span data-stu-id="db0de-288">For information about how to add servers to your server pool, see the Server Manager Help.</span></span> <span data-ttu-id="db0de-289">Выбрав конечный сервер, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="db0de-289">After you have selected the destination server, click **Next**.</span></span>

5.  <span data-ttu-id="db0de-290">На странице **Выбор компонентов** мастера разверните узел **Windows PowerShell** и выберите **Windows PowerShell Web Access**.</span><span class="sxs-lookup"><span data-stu-id="db0de-290">On the **Select features** page of the wizard, expand **Windows PowerShell**, and then select **Windows PowerShell Web Access**.</span></span>

6.  <span data-ttu-id="db0de-291">Отметим, что выводится приглашение добавить необходимые компоненты, такие как .NET Framework 4.5 и службы ролей веб-сервера (IIS).</span><span class="sxs-lookup"><span data-stu-id="db0de-291">Note that you are prompted to add required features, such as .NET Framework 4.5, and role services of Web Server (IIS).</span></span> <span data-ttu-id="db0de-292">Добавьте необходимые компоненты и продолжайте работу.</span><span class="sxs-lookup"><span data-stu-id="db0de-292">Add required features and continue.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-293"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-293"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-294">При установке Windows PowerShell Web Access с помощью мастера добавления ролей и компонентов также устанавливается веб-сервер (IIS), включая оснастку диспетчера служб IIS.</span><span class="sxs-lookup"><span data-stu-id="db0de-294">Installing Windows PowerShell Web Access by using the Add Roles and Features Wizard also installs Web Server (IIS), including the IIS Manager snap-in.</span></span> <span data-ttu-id="db0de-295">Если используется мастер добавления ролей и компонентов, оснастка и другие средства управления IIS устанавливаются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="db0de-295">The snap-in and other IIS management tools are installed by default if you use Add Roles and Features Wizard.</span></span> <span data-ttu-id="db0de-296">При установке Windows PowerShell Web Access с помощью командлетов Windows PowerShell, как описано в следующей процедуре, средства управления не устанавливаются по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="db0de-296">If you install Windows PowerShell Web Access by using Windows PowerShell cmdlets as described in the following procedure, management tools are not added by default.</span></span></p></td>
    </tr>
    </tbody>
    </table>

7.  <span data-ttu-id="db0de-297">На странице **Подтверждение выбранных элементов для установки**, если файлы компонентов для Windows PowerShell Web Access не сохраняются на целевом сервере, выбранном на шаге 4, щелкните **Указать альтернативный исходный путь** и укажите путь к файлам компонентов.</span><span class="sxs-lookup"><span data-stu-id="db0de-297">On the **Confirm installation selections** page, if the feature files for Windows PowerShell Web Access are not stored on the destination server that you selected in step 4, click **Specify an alternate source path**, and provide the path to the feature files.</span></span> <span data-ttu-id="db0de-298">В противном случае нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="db0de-298">Otherwise, click **Install**.</span></span>

8.  <span data-ttu-id="db0de-299">После щелчка **Установить** на странице **Ход установки** отображаются ход выполнения установки, результаты и сообщения, такие как предупреждения, сообщения об ошибках и шаги по настройке после установки, необходимые для Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-299">After you click **Install**, the **Installation progress** page displays installation progress, results, and messages such as warnings, failures, or post-installation configuration steps that are required for Windows PowerShell Web Access.</span></span> <span data-ttu-id="db0de-300">После завершения установки Windows PowerShell Web Access выводится приглашение прочитать файл сведений, содержащий основные инструкции по установке шлюза.</span><span class="sxs-lookup"><span data-stu-id="db0de-300">After Windows PowerShell Web Access is installed, you are prompted to review the readme file, which contains basic, required setup instructions for the gateway.</span></span> <span data-ttu-id="db0de-301">Эти инструкции также являются частью этого раздела.</span><span class="sxs-lookup"><span data-stu-id="db0de-301">These instructions are also included in this topic.</span></span> <span data-ttu-id="db0de-302">Путь к файлу сведений: <span class="computerOutputInline">C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-302">The path to the readme file is <span class="computerOutputInline">C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt</span>.</span></span>

###

<span data-ttu-id="db0de-303"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Настройка шлюза</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-303"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 2: Configure the gateway</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-304">Этот раздел содержит инструкции по установке веб-приложения Windows PowerShell Web Access в подкаталог, а не в корневой каталог веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="db0de-304">Instructions in this section are for installing the Windows PowerShell Web Access web application in a subdirectory—and not in the root directory—of your website.</span></span> <span data-ttu-id="db0de-305">Данная процедура, выполняемая через пользовательский интерфейс, эквивалентна действиям, выполняемым с помощью командлета <span class="code">Install-PswaWebApplication</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-305">This procedure is the GUI-based equivalent of the actions performed by the <span class="code">Install-PswaWebApplication</span> cmdlet.</span></span> <span data-ttu-id="db0de-306">В раздел также включены инструкции по использованию диспетчера служб IIS для настройки шлюза Windows PowerShell Web Access в качестве корневого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="db0de-306">This section also includes instructions for how to use IIS Manager to configure the Windows PowerShell Web Access gateway as a root website.</span></span>

-   [<span data-ttu-id="db0de-307">Использование диспетчера IIS для настройки шлюза на существующем веб-сайте</span><span class="sxs-lookup"><span data-stu-id="db0de-307">To use IIS Manager to configure the gateway in an existing website</span></span>](#BKMK_configman)

-   [<span data-ttu-id="db0de-308">Использование диспетчера IIS для настройки шлюза в качестве корневого веб-сайта с тестовым сертификатом</span><span class="sxs-lookup"><span data-stu-id="db0de-308">To use IIS Manager to configure the gateway as a root website with a test certificate</span></span>](#BKMK_configroot)

-   

#### <a name="to-use-iis-manager-to-configure-the-gateway-in-an-existing-website"></a><span data-ttu-id="db0de-309">Использование диспетчера служб IIS для настройки шлюза в существующем веб-сайте</span><span class="sxs-lookup"><span data-stu-id="db0de-309">To use IIS Manager to configure the gateway in an existing website</span></span>

1.  <span data-ttu-id="db0de-310">Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="db0de-310">Open the IIS Manager console by doing one of the following.</span></span>

    -   <span data-ttu-id="db0de-311">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="db0de-311">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="db0de-312">В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="db0de-312">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="db0de-313">На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="db0de-313">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="db0de-314">Щелкните ярлык, когда он появится в списке результатов **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="db0de-314">Click the shortcut when it is displayed in the **Apps** results.</span></span>

2.  <span data-ttu-id="db0de-315">Создайте новый пул приложений для Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-315">Create a new application pool for Windows PowerShell Web Access.</span></span> <span data-ttu-id="db0de-316">Разверните узел сервера шлюза в области дерева диспетчера служб IIS, выберите **Пулы приложений** и щелкните **Добавить пул приложений** в области **Действия**.</span><span class="sxs-lookup"><span data-stu-id="db0de-316">Expand the node of the gateway server in the IIS Manager tree pane, select **Application Pools**, and click **Add Application Pool** in the **Actions** pane.</span></span>

3.  <span data-ttu-id="db0de-317">Добавьте новый пул приложений с именем **pswa_pool** или укажите другое имя.</span><span class="sxs-lookup"><span data-stu-id="db0de-317">Add a new application pool with the name **pswa_pool**, or provide another name.</span></span> <span data-ttu-id="db0de-318">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-318">Click **OK**.</span></span>

4.  <span data-ttu-id="db0de-319">В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-319">In the IIS Manager tree pane, expand the node for the server on which Windows PowerShell Web Access is installed until the **Sites** folder is visible.</span></span> <span data-ttu-id="db0de-320">Выберите папку **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-320">Select the **Sites** folder.</span></span>

5.  <span data-ttu-id="db0de-321">Щелкните правой кнопкой мыши веб-сайт (например, **Веб-сайт по умолчанию**), в который следует добавить веб-сайт Windows PowerShell Web Access, а затем выберите команду **Добавить приложение**.</span><span class="sxs-lookup"><span data-stu-id="db0de-321">Right-click the website (for example, **Default Web Site**) to which you would like to add the Windows PowerShell Web Access website, and then click **Add Application**.</span></span>

6.  <span data-ttu-id="db0de-322">В поле **Псевдоним** введите pswa или укажите другой псевдоним.</span><span class="sxs-lookup"><span data-stu-id="db0de-322">In the **Alias** field, type pswa, or provide another alias.</span></span> <span data-ttu-id="db0de-323">Псевдоним становится именем виртуального каталога.</span><span class="sxs-lookup"><span data-stu-id="db0de-323">The alias becomes the virtual directory name.</span></span> <span data-ttu-id="db0de-324">Так **pswa** в следующем URL-адресе представляет псевдоним, заданный на этом шаге: https://&lt;имя_сервера&gt;/pswa.</span><span class="sxs-lookup"><span data-stu-id="db0de-324">For example, **pswa** in the following URL represents the alias specified in this step: https://&lt;server_name&gt;/pswa.</span></span>

7.  <span data-ttu-id="db0de-325">В поле **Пул приложений** выберите пул приложений, созданный на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="db0de-325">In the **Application pool** field, select the application pool that you created in step 3.</span></span>

8.  <span data-ttu-id="db0de-326">В поле **Физический путь** найдите расположение приложения.</span><span class="sxs-lookup"><span data-stu-id="db0de-326">In the **Physical path** field, browse for the location of the application.</span></span> <span data-ttu-id="db0de-327">Можно использовать расположение по умолчанию %windir%/Web/PowerShellWebAccess/wwwroot.</span><span class="sxs-lookup"><span data-stu-id="db0de-327">You can use the default location, %windir%/Web/PowerShellWebAccess/wwwroot.</span></span> <span data-ttu-id="db0de-328">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-328">Click **OK**.</span></span>

9.  <span data-ttu-id="db0de-329">Следуйте инструкциями в процедуре [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) этого раздела.</span><span class="sxs-lookup"><span data-stu-id="db0de-329">Follow the steps in the procedure [To configure an SSL certificate in IIS Manager](#BKMK_cert) in this topic.</span></span>

10. <span data-ttu-id="db0de-330"><span class="label">Дополнительный шаг по обеспечению безопасности.</span> Когда веб-сайт выбран в области дерева, дважды щелкните **Параметры SSL** в области содержимого.</span><span class="sxs-lookup"><span data-stu-id="db0de-330"><span class="label">Optional security step:</span> With the website selected in the tree pane, double-click **SSL Settings** in the content pane.</span></span> <span data-ttu-id="db0de-331">Выберите **Требовать SSL**, а затем в области **Действия** щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="db0de-331">Select **Require SSL**, and then in the **Actions** pane, click **Apply**.</span></span> <span data-ttu-id="db0de-332">Дополнительно в области **Параметры SSL** можно потребовать, чтобы пользователи, подключающиеся к веб-сайту Windows PowerShell Web Access, имели клиентские сертификаты.</span><span class="sxs-lookup"><span data-stu-id="db0de-332">Optionally, in the **SSL Settings** pane, you can require that users connecting to the Windows PowerShell Web Access website have client certificates.</span></span> <span data-ttu-id="db0de-333">Клиентские сертификаты помогают проверить идентификацию пользователя клиентского устройства.</span><span class="sxs-lookup"><span data-stu-id="db0de-333">Client certificates help to verify the identity of a client device user.</span></span> <span data-ttu-id="db0de-334">Дополнительные сведения о том, как требование клиентских сертификатов может повысить безопасность Windows PowerShell Web Access, см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx) в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="db0de-334">For more information about how requiring client certificates can increase the security of Windows PowerShell Web Access, see [Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx) in this guide.</span></span>

11. <span data-ttu-id="db0de-335">Откройте сеанс браузера на клиентском устройстве.</span><span class="sxs-lookup"><span data-stu-id="db0de-335">Open a browser session on a client device.</span></span> <span data-ttu-id="db0de-336">Дополнительные сведения о поддерживаемых браузерах и устройствах см. в разделе [Поддержка браузеров и клиентских устройств](#BKMK_browser) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="db0de-336">For more information about supported browsers and devices, see [Browser and client device support](#BKMK_browser) in this topic.</span></span>

12. <span data-ttu-id="db0de-337">Откройте новый веб-сайт Windows PowerShell Web Access — https://&lt;*имя_сервера_шлюза*&gt;/pswa.</span><span class="sxs-lookup"><span data-stu-id="db0de-337">Open the new Windows PowerShell Web Access website, https://&lt; *gateway_server_name*&gt;/pswa.</span></span>

    <span data-ttu-id="db0de-338">В браузере должна появиться страница входа в консоль Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-338">The browser should display the Windows PowerShell Web Access console sign-in page.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-339"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-339"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-340">Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-340">You cannot sign in until users have been granted access to the website by adding authorization rules.</span></span></p></td>
    </tr>
    </tbody>
    </table>

13. <span data-ttu-id="db0de-341">В сеансе Windows PowerShell, который был открыт с повышенными правами (запуск от имени администратора), выполните следующий сценарий, в котором *application_pool_name* представляет имя пула приложений, созданного на шаге 3, чтобы предоставить пулу приложений права доступа к файлу авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-341">In a Windows PowerShell session that has been opened with elevated user rights (Run as Administrator), run the following script, in which *application_pool_name* represents the name of the application pool that you created in step 3, to give the application pool access rights to the authorization file.</span></span>

    [<span data-ttu-id="db0de-342">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-342">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_c1a80a93-8fcf-4beb-a025-5f81bfb8bdae'); "Копировать в буфер обмена".)

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    <span data-ttu-id="db0de-343">Чтобы просмотреть права доступа к файлу авторизации, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db0de-343">To view existing access rights on the authorization file, run the following command:</span></span>

    [<span data-ttu-id="db0de-344">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-344">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ac2179c2-9548-4a17-8663-267fdd105380'); "Копировать в буфер обмена".)

        c:\windows\system32\icacls.exe $authorizationFile

#### <a name="to-use-iis-manager-to-configure-the-gateway-as-a-root-website-with-a-test-certificate"></a><span data-ttu-id="db0de-345">Использование диспетчера служб IIS для настройки шлюза в качестве корневого веб-сайта с тестовым сертификатом</span><span class="sxs-lookup"><span data-stu-id="db0de-345">To use IIS Manager to configure the gateway as a root website with a test certificate</span></span>

1.  <span data-ttu-id="db0de-346">Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="db0de-346">Open the IIS Manager console by doing one of the following.</span></span>

    -   <span data-ttu-id="db0de-347">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="db0de-347">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="db0de-348">В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="db0de-348">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="db0de-349">На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="db0de-349">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="db0de-350">Щелкните ярлык, когда он появится в списке результатов **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="db0de-350">Click the shortcut when it is displayed in the **Apps** results.</span></span>

2.  <span data-ttu-id="db0de-351">В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-351">In the IIS Manager tree pane, expand the node for the server on which Windows PowerShell Web Access is installed until the **Sites** folder is visible.</span></span> <span data-ttu-id="db0de-352">Выберите папку **Сайты**.</span><span class="sxs-lookup"><span data-stu-id="db0de-352">Select the **Sites** folder.</span></span>

3.  <span data-ttu-id="db0de-353">В области **Действия** щелкните **Добавить веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="db0de-353">In the **Actions** pane, click **Add Website**.</span></span>

4.  <span data-ttu-id="db0de-354">Введите имя веб-сайта, например **Windows PowerShell Web Access**.</span><span class="sxs-lookup"><span data-stu-id="db0de-354">Type a name for the website, such as **Windows PowerShell Web Access**.</span></span>

5.  <span data-ttu-id="db0de-355">Автоматически создается пул приложений для нового веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="db0de-355">An application pool is automatically created for the new website.</span></span> <span data-ttu-id="db0de-356">Чтобы использовать другой пул приложений, щелкните **Выбрать**, чтобы выбрать пул приложений, связываемый с новым веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="db0de-356">To use a different application pool, click **Select** to select an application pool to associate with the new website.</span></span> <span data-ttu-id="db0de-357">Выберите другой пул приложений в диалоговом окне **Выбор пула приложений** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-357">Select the alternate application pool in the **Select Application Pool** dialog box, and then click **OK**.</span></span>

6.  <span data-ttu-id="db0de-358">В поле **Физический путь** перейдите к папке %*windir*%/Web/PowerShellWebAccess/wwwroot.</span><span class="sxs-lookup"><span data-stu-id="db0de-358">In the **Physical path** text box, navigate to %*windir*%/Web/PowerShellWebAccess/wwwroot.</span></span>

7.  <span data-ttu-id="db0de-359">В поле **Тип** в области **Привязка** выберите **https**.</span><span class="sxs-lookup"><span data-stu-id="db0de-359">In the **Type** field of the **Binding** area, select **https**.</span></span>

8.  <span data-ttu-id="db0de-360">Назначьте веб-сайту номер порта, который еще не используется другим сайтом или приложением.</span><span class="sxs-lookup"><span data-stu-id="db0de-360">Assign a port number to the website that is not already in use by another site or application.</span></span> <span data-ttu-id="db0de-361">Чтобы найти открытые порты, можно выполнить команду **netstat** в окне командной строки.</span><span class="sxs-lookup"><span data-stu-id="db0de-361">To locate open ports, you can run the **netstat** command in a Command Prompt window.</span></span> <span data-ttu-id="db0de-362">Номер порта по умолчанию: 443.</span><span class="sxs-lookup"><span data-stu-id="db0de-362">The default port number is 443.</span></span>

    <span data-ttu-id="db0de-363">Измените номер порта по умолчанию, если порт 443 уже используется другим веб-сайтом или имеются другие соображения безопасности для изменения номера порта.</span><span class="sxs-lookup"><span data-stu-id="db0de-363">Change the default port if another website is already using 443, or if you have other security reasons for changing the port number.</span></span> <span data-ttu-id="db0de-364">Если выбранный вами порт используется другим веб-сайтом, который выполняется на вашем сервере шлюза, при нажатии кнопки **ОК** выводится предупреждение в диалоговом окне **Добавление веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="db0de-364">If another website that is running on your gateway server is using your selected port, a warning is displayed when you click **OK** in the **Add Website** dialog box.</span></span> <span data-ttu-id="db0de-365">Для запуска Windows PowerShell Web Access необходимо использовать неиспользуемый порт.</span><span class="sxs-lookup"><span data-stu-id="db0de-365">You must use an unused port to run Windows PowerShell Web Access.</span></span>

9.  <span data-ttu-id="db0de-366">Дополнительно, если требуется для вашей организации, укажите понятное имя узла, например **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="db0de-366">Optionally, if needed for your organization, specify a host name that makes sense to your organization and users, such as **www.contoso.com**.</span></span> <span data-ttu-id="db0de-367">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-367">Click **OK**.</span></span>

10. <span data-ttu-id="db0de-368">Чтобы обезопасить производственную среду, мы настоятельно рекомендуем предоставить действительный сертификат, подписанный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="db0de-368">For a more secure production environment, we strongly recommend providing a valid certificate that has been signed by a CA.</span></span> <span data-ttu-id="db0de-369">Вы должны предоставить SSL-сертификат, поскольку пользователи могут подключаться к Windows PowerShell Web Access только по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="db0de-369">You must provide an SSL certificate, because users can only connect to Windows PowerShell Web Access through an HTTPS website.</span></span> <span data-ttu-id="db0de-370">Дополнительные сведения о получении сертификата см. в разделе [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) в данной статье.</span><span class="sxs-lookup"><span data-stu-id="db0de-370">See [To configure an SSL certificate in IIS Manager](#BKMK_cert) in this topic for more information about how to obtain a certificate.</span></span>

11. <span data-ttu-id="db0de-371">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="db0de-371">Click **OK** to close the **Add Website** dialog box.</span></span>

12. <span data-ttu-id="db0de-372">В сеансе Windows PowerShell, который был открыт с повышенными правами (запуск от имени администратора), выполните следующий сценарий, в котором *application_pool_name* представляет имя пула приложений, созданного на шаге 4, чтобы предоставить пулу приложений права доступа к файлу авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-372">In a Windows PowerShell session that has been opened with elevated user rights (Run as Administrator), run the following script, in which *application_pool_name* represents the name of the application pool that you created in step 4, to give the application pool access rights to the authorization file.</span></span>

    [<span data-ttu-id="db0de-373">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-373">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_35ae9944-ca44-4af7-9c96-616083b3e3db'); "Копировать в буфер обмена".)

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    <span data-ttu-id="db0de-374">Чтобы просмотреть права доступа к файлу авторизации, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="db0de-374">To view existing access rights on the authorization file, run the following command:</span></span>

    [<span data-ttu-id="db0de-375">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-375">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_0eb6d70a-2807-498b-b088-fa5233ed68d5'); "Копировать в буфер обмена".)

        c:\windows\system32\icacls.exe $authorizationFile

13. <span data-ttu-id="db0de-376">Когда новый веб-сайт выбран в области дерева диспетчера служб IIS, в области **Действия** щелкните **Запуск**, чтобы запустить веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="db0de-376">With the new website selected in the IIS Manager tree pane, click **Start** in the **Actions** pane to start the website.</span></span>

14. <span data-ttu-id="db0de-377">Откройте сеанс браузера на клиентском устройстве.</span><span class="sxs-lookup"><span data-stu-id="db0de-377">Open a browser session on a client device.</span></span> <span data-ttu-id="db0de-378">Дополнительные сведения о поддерживаемых браузерах и устройствах см. в разделе [Поддержка браузеров и клиентских устройств](#BKMK_browser) в данном документе.</span><span class="sxs-lookup"><span data-stu-id="db0de-378">For more information about supported browsers and devices, see [Browser and client device support](#BKMK_browser) in this document.</span></span>

15. <span data-ttu-id="db0de-379">Откройте новый веб-сайт Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-379">Open the new Windows PowerShell Web Access website.</span></span>

    <span data-ttu-id="db0de-380">Так как корневой веб-сайт указывает на папку Windows PowerShell Web Access, то если открыть в браузере адрес https://&lt;*имя_сервера_шлюза*&gt;, появится страница входа Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-380">Because the root website points to the Windows PowerShell Web Access folder, the browser should display the Windows PowerShell Web Access sign-in page when you open https://&lt; *gateway_server_name*&gt;.</span></span> <span data-ttu-id="db0de-381">Нет необходимости добавлять **/pswa** в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="db0de-381">You should not need to add **/pswa** to the URL.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="db0de-382"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="db0de-382"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="db0de-383">Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</span><span class="sxs-lookup"><span data-stu-id="db0de-383">You cannot sign in until users have been granted access to the website by adding authorization rules.</span></span></p></td>
    </tr>
    </tbody>
    </table>

###

<span data-ttu-id="db0de-384"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 3. Настройка ограничивающего правила авторизации</span></a></span><span class="sxs-lookup"><span data-stu-id="db0de-384"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 3: Configure a restrictive authorization rule</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-385">После установки Windows PowerShell Web Access и настройки шлюза пользователи могут открывать страницу входа в браузере, но они не могут выполнить вход, пока администратор Windows PowerShell Web Access не предоставит им доступ в явном виде.</span><span class="sxs-lookup"><span data-stu-id="db0de-385">After Windows PowerShell Web Access is installed and the gateway is configured, users can open the sign-in page in a browser, but they cannot sign in until the Windows PowerShell Web Access administrator grants users access explicitly.</span></span> <span data-ttu-id="db0de-386">Управление доступом в Windows PowerShell Web Access осуществляется с помощью набора командлетов Windows PowerShell, описанных в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="db0de-386">Windows PowerShell Web Access access control is managed by using the set of Windows PowerShell cmdlets described in the following table.</span></span> <span data-ttu-id="db0de-387">Нет соответствующего графического пользовательского интерфейса для добавления правил авторизации или управления ими.</span><span class="sxs-lookup"><span data-stu-id="db0de-387">There is no comparable GUI for adding or managing authorization rules.</span></span> <span data-ttu-id="db0de-388">Подробные сведения о командлетах Windows PowerShell Web Access см. в справочных разделах по командлетам в статье [Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-388">For more detailed information about Windows PowerShell Web Access cmdlets, see the cmdlet reference topics, [Windows PowerShell Web Access Cmdlets](https://technet.microsoft.com/library/hh918342.aspx).</span></span>

<span data-ttu-id="db0de-389">Дополнительные сведения о безопасности и правилах авторизации Windows PowerShell Web Access см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-389">For more detail about Windows PowerShell Web Access authorization rules and security, see [Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx).</span></span>

#### <a name="to-add-a-restrictive-authorization-rule"></a><span data-ttu-id="db0de-390">Добавление ограничивающего правила авторизации</span><span class="sxs-lookup"><span data-stu-id="db0de-390">To add a restrictive authorization rule</span></span>

1.  <span data-ttu-id="db0de-391">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="db0de-391">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span>

    -   <span data-ttu-id="db0de-392">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-392">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="db0de-393">На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="db0de-393">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

2.  <span data-ttu-id="db0de-394"><span class="label">Необязательный шаг для ограничения доступа пользователей с помощью конфигураций сеансов: </span> убедитесь, что конфигурации сеансов, которые вы хотите использовать в своих правилах, уже существуют.</span><span class="sxs-lookup"><span data-stu-id="db0de-394"><span class="label">Optional step for restricting user access by using session configurations:</span> Verify that session configurations that you want to use in your rules already exist.</span></span> <span data-ttu-id="db0de-395">В противном случае выполните инструкции по созданию конфигураций сеансов, приведенные в статье [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="db0de-395">If they have not yet been created, use instructions for creating session configurations in [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) on MSDN.</span></span>

3.  <span data-ttu-id="db0de-396">Введите следующую команду и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="db0de-396">Type the following, and then press **Enter**.</span></span>

    [<span data-ttu-id="db0de-397">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-397">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_4df22c91-f56f-4bb5-91e7-99f9b365ed5d'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    <span data-ttu-id="db0de-398">Это правило авторизации разрешает конкретному пользователю доступ к одному сетевому компьютеру, к которому обычно требуется доступ, с доступом к конкретной конфигурации сеанса, область которого соответствует потребностям пользовательских скриптов и командлетов.</span><span class="sxs-lookup"><span data-stu-id="db0de-398">This authorization rule allows a specific user access to one computer on the network to which they typically have access, with access to a specific session configuration that is scoped to the user’s typical scripting and cmdlet needs.</span></span> <span data-ttu-id="db0de-399">В следующем примере пользователю с именем <span class="code">JSmith</span> в домене <span class="code">Contoso</span> предоставляется доступ для управления компьютером <span class="code">Contoso\_214</span> и использования конфигурации сеанса с именем <span class="code">NewAdminsOnly</span>.</span><span class="sxs-lookup"><span data-stu-id="db0de-399">In the following example, a user named <span class="code">JSmith</span> in the <span class="code">Contoso</span> domain is granted access to manage the computer <span class="code">Contoso_214</span>, and use a session configuration named <span class="code">NewAdminsOnly</span>.</span></span>

    [<span data-ttu-id="db0de-400">Copy</span><span class="sxs-lookup"><span data-stu-id="db0de-400">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_efc3999a-2905-453f-86cd-014b41658ffc'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  <span data-ttu-id="db0de-401">Убедитесь, что правило создано, выполнив командлет **Get-PswaAuthorizationRule** или **Test-PswaAuthorizationRule -UserName &lt;домен\\пользователь | компьютер\\пользователь&gt; -ComputerName** &lt;имя_компьютера&gt;.</span><span class="sxs-lookup"><span data-stu-id="db0de-401">Verify that the rule has been created by running either the **Get-PswaAuthorizationRule** cmdlet, or **Test-PswaAuthorizationRule -UserName &lt;domain\\user | computer\\user&gt; -ComputerName** &lt;computer_name&gt;.</span></span> <span data-ttu-id="db0de-402">Например, **Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214**.</span><span class="sxs-lookup"><span data-stu-id="db0de-402">For example, **Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214**.</span></span>

<span data-ttu-id="db0de-403">После настройки правила авторизации авторизованные пользователи могут выполнить вход в веб-консоль и приступить к использованию Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-403">After you have configured an authorization rule, you are ready for authorized users to sign in to the web-based console and begin using Windows PowerShell Web Access.</span></span>

<a href="" id="BKMK_configcert"></a>

<span data-ttu-id="db0de-404"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Настройка подлинного сертификата</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-404"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Configure a genuine certificate</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-405">Для безопасной производственной среды следует всегда использовать действительный сертификат SSL, подписанный центром сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="db0de-405">For a secure production environment, always use a valid SSL certificate that has been signed by a certification authority (CA).</span></span> <span data-ttu-id="db0de-406">В этом разделе описано, как получить и установить действительный SSL-сертификат от центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="db0de-406">The procedure in this section describes how to obtain and apply a valid SSL certificate from a CA.</span></span>

### <a name="to-configure-an-ssl-certificate-in-iis-manager"></a><span data-ttu-id="db0de-407">Настройка SSL-сертификата в диспетчере служб IIS</span><span class="sxs-lookup"><span data-stu-id="db0de-407">To configure an SSL certificate in IIS Manager</span></span>

1.  <span data-ttu-id="db0de-408">В области дерева диспетчера служб IIS выберите сервер, на котором установлен компонент Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-408">In the IIS Manager tree pane, select the server on which Windows PowerShell Web Access is installed.</span></span>

2.  <span data-ttu-id="db0de-409">В области содержимого дважды щелкните **Сертификаты сервера**.</span><span class="sxs-lookup"><span data-stu-id="db0de-409">In the content pane, double click **Server Certificates**.</span></span>

3.  <span data-ttu-id="db0de-410">В области **Действия** выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="db0de-410">In the **Actions** pane, do one of the following.</span></span> <span data-ttu-id="db0de-411">Дополнительные сведения о настройке сертификатов сервера в IIS см. в статье [Настройка сертификатов сервера в службах IIS 7](https://technet.microsoft.com/library/cc732230.aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-411">For more information about configuring server certificates in IIS, see [Configuring Server Certificates in IIS 7](https://technet.microsoft.com/library/cc732230.aspx).</span></span>

    -   <span data-ttu-id="db0de-412">Щелкните **Импорт**, чтобы импортировать имеющийся действительный сертификат из расположения в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="db0de-412">Click **Import** to import an existing, valid certificate from a location on your network.</span></span>

    -   <span data-ttu-id="db0de-413">Щелкните **Создать запрос сертификата**, чтобы запросить сертификат из центра сертификации, например из VeriSign™, Thawte или GeoTrust®.</span><span class="sxs-lookup"><span data-stu-id="db0de-413">Click **Create Certificate Request** to request a certificate from a CA such as VeriSign™, Thawte, or GeoTrust®.</span></span> <span data-ttu-id="db0de-414">Общее имя сертификата должно совпадать с заголовком узла в запросе.</span><span class="sxs-lookup"><span data-stu-id="db0de-414">The certificate's common name must match the host header in the request.</span></span> <span data-ttu-id="db0de-415">Например, если браузер клиента запрашивает http://www.contoso.com/, общим именем также должно быть http://www.contoso.com/.</span><span class="sxs-lookup"><span data-stu-id="db0de-415">For example, if the client browser requests http://www.contoso.com/, then the common name must also be http://www.contoso.com/.</span></span> <span data-ttu-id="db0de-416">Это самый безопасный и рекомендуемый вариант предоставления сертификата для шлюза Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="db0de-416">This is the most secure and recommended option for providing the Windows PowerShell Web Access gateway with a certificate.</span></span>

    -   <span data-ttu-id="db0de-417">Щелкните **Создать самозаверяющий сертификат**, чтобы создать сертификат, который можно использовать немедленно, а при необходимости подписать в ЦС позже.</span><span class="sxs-lookup"><span data-stu-id="db0de-417">Click **Create a Self-Signed Certificate** to create a certificate that you can use immediately, and have signed later by a CA if desired.</span></span> <span data-ttu-id="db0de-418">Введите понятное имя самозаверяющего сертификата, например **Windows PowerShell Web Access**.</span><span class="sxs-lookup"><span data-stu-id="db0de-418">Specify a friendly name for the self-signed certificate, such as **Windows PowerShell Web Access**.</span></span> <span data-ttu-id="db0de-419">Этот вариант не считается безопасным и рекомендуется только для частной тестовой среды.</span><span class="sxs-lookup"><span data-stu-id="db0de-419">This option is not considered secure, and is recommended only for a private test environment.</span></span>

4.  <span data-ttu-id="db0de-420">После создания или получения сертификата выберите веб-сайт, к которому применяется сертификат (например, **Веб-сайт по умолчанию**) в области дерева диспетчера служб IIS, а затем щелкните **Привязки** в области **Действия**.</span><span class="sxs-lookup"><span data-stu-id="db0de-420">After creating or obtaining a certificate, select the website to which the certificate is applied (for example, **Default Web Site**) in the IIS Manager tree pane, and then click **Bindings** in the **Actions** pane.</span></span>

5.  <span data-ttu-id="db0de-421">В диалоговом окне **Добавление привязки сайта** добавьте привязку **https** для сайта, если такая привязка еще не отображается.</span><span class="sxs-lookup"><span data-stu-id="db0de-421">In the **Add Site Binding** dialog box, add an **https** binding for the site, if one is not already displayed.</span></span> <span data-ttu-id="db0de-422">Если вы не используете самозаверяющий сертификат, укажите имя узла из шага 3 данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="db0de-422">If you are not using a self-signed certificate, specify the host name from step 3 of this procedure.</span></span> <span data-ttu-id="db0de-423">Если вы используете самозаверяющий сертификат, этот шаг не требуется.</span><span class="sxs-lookup"><span data-stu-id="db0de-423">If you are using a self-signed certificate, this step is not required.</span></span>

6.  <span data-ttu-id="db0de-424">Выберите сертификат, полученный или созданный на шаге 3 данной процедуры, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="db0de-424">Select the certificate that you obtained or created in step 3 of this procedure, and then click **OK**.</span></span>

<a href="" id="BKMK_using"></a>

<span data-ttu-id="db0de-425"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Использование веб-консоли Windows PowerShell</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_5" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-425"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Using the web-based Windows PowerShell console</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_5" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-426">После установки Windows PowerShell Web Access и завершения настройки шлюза, описанной в этой статье, веб-консоль Windows PowerShell готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="db0de-426">After Windows PowerShell Web Access is installed and the gateway configuration is finished as described in this topic, the Windows PowerShell web-based console is ready to use.</span></span> <span data-ttu-id="db0de-427">Дополнительные сведения о начале работы с веб-консолью см. в статье [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="db0de-427">For more information about getting started in the web-based console, see [Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx).</span></span>

<span data-ttu-id="db0de-428"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_6" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="db0de-428"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">See Also</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_6" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="db0de-429">[Документация по Internet Information Services (IIS) 7.0](https://technet.microsoft.com/library/cc753433.aspx)
[Справка по IIS Manager 7.0](https://technet.microsoft.com/library/cc732664.aspx)
[Настройка безопасности веб-сервера (IIS 7)](https://technet.microsoft.com/library/cc731278.aspx)
[Ресурсы развертывания IPsec](https://technet.microsoft.com/network/bb531150)</span><span class="sxs-lookup"><span data-stu-id="db0de-429">[Internet Information Services (IIS) 7.0 Documentation](https://technet.microsoft.com/library/cc753433.aspx)
[IIS Manager 7.0 Help](https://technet.microsoft.com/library/cc732664.aspx)
[Configure Web Server Security (IIS 7)](https://technet.microsoft.com/library/cc731278.aspx)
[IPsec Deployment Resources](https://technet.microsoft.com/network/bb531150)</span></span>

<span data-ttu-id="db0de-430"><span>Демонстрация:</span> унаследованная защита</span><span class="sxs-lookup"><span data-stu-id="db0de-430"><span>Show:</span> Inherited Protected</span></span>

<span data-ttu-id="db0de-431"><span class="stdr-votetitle">Эта страница была полезной?</span></span><span class="sxs-lookup"><span data-stu-id="db0de-431"><span class="stdr-votetitle">Was this page helpful?</span></span></span>
<span data-ttu-id="db0de-432">Да Нет</span><span class="sxs-lookup"><span data-stu-id="db0de-432">Yes No</span></span>

<span data-ttu-id="db0de-433">Дополнительные отзывы?</span><span class="sxs-lookup"><span data-stu-id="db0de-433">Additional feedback?</span></span>

<span data-ttu-id="db0de-434">Осталось <span class="stdr-count"><span class="stdr-charcnt">1500</span> символов</span> Отправить Пропустить</span><span class="sxs-lookup"><span data-stu-id="db0de-434"><span class="stdr-count"><span class="stdr-charcnt">1500</span> characters remaining</span> Submit Skip this</span></span>

<span data-ttu-id="db0de-435"><span class="stdr-thankyou">Спасибо!</span></span><span class="sxs-lookup"><span data-stu-id="db0de-435"><span class="stdr-thankyou">Thank you!</span></span></span> <span data-ttu-id="db0de-436"><span class="stdr-appreciate">Мы ценим ваши отзывы.</span></span><span class="sxs-lookup"><span data-stu-id="db0de-436"><span class="stdr-appreciate">We appreciate your feedback.</span></span></span>

[<span data-ttu-id="db0de-437">Управление профилем</span><span class="sxs-lookup"><span data-stu-id="db0de-437">Manage Your Profile</span></span>](https://social.technet.microsoft.com/profile)

|

<span data-ttu-id="db0de-438"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a> Отзыв о сайте</span><span class="sxs-lookup"><span data-stu-id="db0de-438"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Site Feedback</a> Site Feedback</span></span>

<span data-ttu-id="db0de-439"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span><span class="sxs-lookup"><span data-stu-id="db0de-439"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span></span>

<span data-ttu-id="db0de-440">Расскажите о своих впечатлениях...</span><span class="sxs-lookup"><span data-stu-id="db0de-440">Tell us about your experience...</span></span>

<span data-ttu-id="db0de-441">Быстро ли загрузилась страница?</span><span class="sxs-lookup"><span data-stu-id="db0de-441">Did the page load quickly?</span></span>

<span data-ttu-id="db0de-442"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="db0de-442"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="db0de-443">Вам нравится дизайн страницы?</span><span class="sxs-lookup"><span data-stu-id="db0de-443">Do you like the page design?</span></span>

<span data-ttu-id="db0de-444"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="db0de-444"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="db0de-445">Расскажите подробнее</span><span class="sxs-lookup"><span data-stu-id="db0de-445">Tell us more</span></span>

-   [<span data-ttu-id="db0de-446">Информационный бюллетень Flash</span><span class="sxs-lookup"><span data-stu-id="db0de-446">Flash Newsletter</span></span>](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [<span data-ttu-id="db0de-447">Контакты</span><span class="sxs-lookup"><span data-stu-id="db0de-447">Contact Us</span></span>](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [<span data-ttu-id="db0de-448">Заявление о конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="db0de-448">Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)
-   |
-   [<span data-ttu-id="db0de-449">Условия использования</span><span class="sxs-lookup"><span data-stu-id="db0de-449">Terms of Use</span></span>](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [<span data-ttu-id="db0de-450">Товарные знаки</span><span class="sxs-lookup"><span data-stu-id="db0de-450">Trademarks</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

<span data-ttu-id="db0de-451">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="db0de-451">© 2016 Microsoft</span></span>

<span data-ttu-id="db0de-452">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="db0de-452">© 2016 Microsoft</span></span>

<span data-ttu-id="db0de-453">Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющимися владельцами такого кода, а не корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="db0de-453">Third party scripts and code linked to or referenced from this website are licensed to you by the parties that own such code, not by Microsoft.</span></span> <span data-ttu-id="db0de-454">См. условия использования ASP.NET Ajax CDN — http://www.asp.net/ajaxlibrary/CDN.ashx.</span><span class="sxs-lookup"><span data-stu-id="db0de-454">See ASP.NET Ajax CDN Terms of Use - http://www.asp.net/ajaxlibrary/CDN.ashx.</span></span>
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />

