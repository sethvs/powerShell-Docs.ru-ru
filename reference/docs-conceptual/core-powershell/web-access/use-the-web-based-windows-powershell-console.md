---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Использование веб-консоли Windows PowerShell"
ms.openlocfilehash: 48ed1646c00f909c4e950f197f51a30205060ef0
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
#  <a name="use-the-web-based-windows-powershell-console"></a><span data-ttu-id="d9826-103">Использование веб-консоли Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9826-103">Use the Web-based Windows PowerShell Console</span></span>

<span data-ttu-id="d9826-104">Обновлено: 24 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="d9826-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="d9826-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d9826-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="d9826-106">Windows PowerShell® Web Access предоставляет пользователям Windows PowerShell® возможность войти на защищенный по технологии SSL веб-сайт, чтобы использовать сеансы, командлеты и сценарии Windows PowerShell для администрирования удаленного компьютера.</span><span class="sxs-lookup"><span data-stu-id="d9826-106">Windows PowerShell® Web Access lets Windows PowerShell® users sign in to a Secure Sockets Layer (SSL)-secured website to use Windows PowerShell sessions, cmdlets, and scripts to manage a remote computer.</span></span> <span data-ttu-id="d9826-107">Поскольку консоль Windows PowerShell выполняется в веб-браузере, ее можно открыть с различных клиентских устройств, включая мобильные телефоны, планшетные компьютеры, общедоступные компьютеры, ноутбуки, общие или арендованные компьютеры.</span><span class="sxs-lookup"><span data-stu-id="d9826-107">Because the Windows PowerShell console runs in a web browser, it can be opened from a variety of client devices, including cell phones, tablet computers, public computing kiosks, laptop computers, or shared or borrowed computers.</span></span> <span data-ttu-id="d9826-108">Веб-консоль Windows PowerShell ориентирована на работу с удаленным компьютером, который пользователь указывает в процессе выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="d9826-108">The web-based Windows PowerShell console is targeted at a remote computer that is specified by users as part of the sign-in process.</span></span> <span data-ttu-id="d9826-109">В этом разделе рассказывается о том, как выполнить вход и приступить к использованию веб-консоли Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d9826-109">This topic describes how to sign in to and start using the Windows PowerShell Web Access web-based console.</span></span>

<span data-ttu-id="d9826-110">Данный раздел не касается способов использования Windows PowerShell или выполнения командлетов или сценариев.</span><span class="sxs-lookup"><span data-stu-id="d9826-110">This topic does not describe how to use Windows PowerShell or run cmdlets or scripts.</span></span> <span data-ttu-id="d9826-111">Сведения о том, как использовать Windows PowerShell и сценарии, см. в разделе "Дополнительная информация" в конце данного раздела.</span><span class="sxs-lookup"><span data-stu-id="d9826-111">For information about how to use Windows PowerShell, and scripting resources, see the See Also section at the end of this topic.</span></span>

<span data-ttu-id="d9826-112">Содержание раздела:</span><span class="sxs-lookup"><span data-stu-id="d9826-112">In this topic:</span></span>

-   [<span data-ttu-id="d9826-113">Поддерживаемые браузеры и клиентские устройства</span><span class="sxs-lookup"><span data-stu-id="d9826-113">Supported browsers and client devices</span></span>](#BKMK_browser)

-   [<span data-ttu-id="d9826-114">Вход в Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="d9826-114">Signing in to Windows PowerShell Web Access</span></span>](#BKMK_sign)

-   [<span data-ttu-id="d9826-115">Выход и превышение времени ожидания</span><span class="sxs-lookup"><span data-stu-id="d9826-115">Signing out and timing out</span></span>](#BKMK_timeout)

-   [<span data-ttu-id="d9826-116">Отличительные особенности веб-консоли Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9826-116">Differences in the web-based Windows PowerShell console</span></span>](#BKMK_web)

<a href="" id="BKMK_browser"></a>
------------------------------------------------------------------------

<span data-ttu-id="d9826-117">Windows PowerShell Web Access поддерживает перечисленные ниже веб-браузеры.</span><span class="sxs-lookup"><span data-stu-id="d9826-117">Windows PowerShell Web Access supports the following Internet browsers.</span></span> <span data-ttu-id="d9826-118">Хотя браузеры для мобильных устройств официально не поддерживаются, многие из них могут выполнять веб-консоль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9826-118">Although mobile browsers are not officially supported, many may be able to run the web-based Windows PowerShell console.</span></span> <span data-ttu-id="d9826-119">Ожидается, что другие браузеры, которые принимают куки-файлы, выполняют JavaScript и выполняют веб-сайты HTTPS, также будут работать, но официально они не протестированы.</span><span class="sxs-lookup"><span data-stu-id="d9826-119">Other browsers that accept cookies, run JavaScript, and run HTTPS websites are expected to work, but are not officially tested.</span></span>

###

<span data-ttu-id="d9826-120"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Поддерживаемые браузеры для настольных компьютеров</span></a></span><span class="sxs-lookup"><span data-stu-id="d9826-120"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Supported desktop computer browsers</span></a></span></span>

------------------------------------------------------------------------

-   <span data-ttu-id="d9826-121">Windows® Internet Explorer® для Microsoft Windows® 8.0, 9.0, 10.0 и 11.0</span><span class="sxs-lookup"><span data-stu-id="d9826-121">Windows® Internet Explorer® for Microsoft Windows® 8.0, 9.0, 10.0, and 11.0</span></span>

-   <span data-ttu-id="d9826-122">Mozilla Firefox® 10.0.2</span><span class="sxs-lookup"><span data-stu-id="d9826-122">Mozilla Firefox® 10.0.2</span></span>

-   <span data-ttu-id="d9826-123">Google Chrome™ 17.0.963.56m для Windows</span><span class="sxs-lookup"><span data-stu-id="d9826-123">Google Chrome™ 17.0.963.56m for Windows</span></span>

-   <span data-ttu-id="d9826-124">Apple Safari® 5.1.2 для Windows</span><span class="sxs-lookup"><span data-stu-id="d9826-124">Apple Safari® 5.1.2 for Windows</span></span>

-   <span data-ttu-id="d9826-125">Apple Safari 5.1.2 для Mac OS®</span><span class="sxs-lookup"><span data-stu-id="d9826-125">Apple Safari 5.1.2 for Mac OS®</span></span>

###

<span data-ttu-id="d9826-126"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Минимально протестированные мобильные устройства или браузеры</span></a></span><span class="sxs-lookup"><span data-stu-id="d9826-126"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Minimally-tested mobile devices or browsers</span></a></span></span>

------------------------------------------------------------------------

-   <span data-ttu-id="d9826-127">Windows Phone 7 и 7.5</span><span class="sxs-lookup"><span data-stu-id="d9826-127">Windows Phone 7 and 7.5</span></span>

-   <span data-ttu-id="d9826-128">Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)</span><span class="sxs-lookup"><span data-stu-id="d9826-128">Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)</span></span>

-   <span data-ttu-id="d9826-129">Apple Safari для операционной системы 5.0.1 для iPhone</span><span class="sxs-lookup"><span data-stu-id="d9826-129">Apple Safari for iPhone operating system 5.0.1</span></span>

-   <span data-ttu-id="d9826-130">Apple Safari для операционной системы 5.0.1 для iPad 2</span><span class="sxs-lookup"><span data-stu-id="d9826-130">Apple Safari for iPad 2 operating system 5.0.1</span></span>

###

<span data-ttu-id="d9826-131"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования к браузерам</span></a></span><span class="sxs-lookup"><span data-stu-id="d9826-131"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Browser requirements</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-132">Чтобы использовать веб-консоль Windows PowerShell Web Access, браузеры должны иметь следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="d9826-132">To use the Windows PowerShell Web Access web-based console, browsers must do the following.</span></span>

-   <span data-ttu-id="d9826-133">Разрешать файлы cookie с веб-сайта шлюза Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d9826-133">Allow cookies from the Windows PowerShell Web Access gateway website.</span></span>

-   <span data-ttu-id="d9826-134">Открывать и читать HTTPS-страницы.</span><span class="sxs-lookup"><span data-stu-id="d9826-134">Be able to open and read HTTPS pages.</span></span>

-   <span data-ttu-id="d9826-135">Открывать и выполнять веб-сайты, использующие JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d9826-135">Open and run websites that use JavaScript.</span></span>

<a href="" id="BKMK_sign"></a>

<span data-ttu-id="d9826-136"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Вход в Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="d9826-136"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Signing in to Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-137">Администратор Windows PowerShell Web Access должен предоставить вам URL-адрес веб-сайта шлюза Windows PowerShell Web Access для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d9826-137">Your Windows PowerShell Web Access administrator should provide you with a URL that is the address of your organization’s Windows PowerShell Web Access gateway website.</span></span> <span data-ttu-id="d9826-138">По умолчанию используется следующий адрес веб-сайта: https://&lt;имя_сервера&gt;/pswa.</span><span class="sxs-lookup"><span data-stu-id="d9826-138">By default, this website address is https://&lt;server_name&gt;/pswa.</span></span> <span data-ttu-id="d9826-139">Прежде чем выполнить вход в Windows PowerShell Web Access, убедитесь, что у вас есть имя или IP-адрес удаленного компьютера, который предполагается администрировать.</span><span class="sxs-lookup"><span data-stu-id="d9826-139">Before you sign in to Windows PowerShell Web Access, be sure that you have the name or IP address of the remote computer that you want to manage.</span></span> <span data-ttu-id="d9826-140">Вы должны быть полномочным пользователем удаленного компьютера, а компьютер должен быть настроен для удаленного администрирования.</span><span class="sxs-lookup"><span data-stu-id="d9826-140">You must be an authorized user on the remote computer, and it must be configured to allow remote management.</span></span> <span data-ttu-id="d9826-141">Дополнительные сведения о настройке компьютера для удаленного администрирования см. в разделе [Включение и использование удаленных команд в Windows PowerShell](https://technet.microsoft.com/magazine/ff700227.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9826-141">For more information about configuring your computer to allow remote management, see [Enable and Use Remote Commands in Windows PowerShell](https://technet.microsoft.com/magazine/ff700227.aspx).</span></span> <span data-ttu-id="d9826-142">Настроить компьютер для удаленного администрирования проще всего, выполнив на нем командлет **Enable-PSRemoting -force** в сеансе Windows PowerShell с повышенными привилегиями пользователя (**Запуск от имени администратора**).</span><span class="sxs-lookup"><span data-stu-id="d9826-142">The simplest method of configuring your computer to allow remote management is to run the **Enable-PSRemoting -force** cmdlet on the computer, in a Windows PowerShell session that has been opened with elevated user rights (**Run as Administrator**).</span></span>

### <a name="to-sign-in-to-windows-powershell-web-access"></a><span data-ttu-id="d9826-143">Вход в систему Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="d9826-143">To sign in to Windows PowerShell Web Access</span></span>

1.  <span data-ttu-id="d9826-144">Откройте веб-сайт Windows PowerShell Web Access в браузере или на вкладке.</span><span class="sxs-lookup"><span data-stu-id="d9826-144">Open the Windows PowerShell Web Access website in an Internet browser window or tab.</span></span>

2.  <span data-ttu-id="d9826-145">На странице входа Windows PowerShell Web Access укажите имя пользователя сети, пароль и имя компьютера, который вы хотите администрировать (вы должны быть полномочным пользователем этого компьютера).</span><span class="sxs-lookup"><span data-stu-id="d9826-145">On the Windows PowerShell Web Access sign-in page, provide your network user name, password, and the name of the computer that you want to manage (and on which you are an authorized user).</span></span> <span data-ttu-id="d9826-146">Если администратор Windows PowerShell Web Access проинструктировал о необходимости использовать вместо имени компьютера URI-адрес пользовательского сайта или прокси-сервера, выберите **URI подключения** в поле **Тип подключения**, а затем укажите URI.</span><span class="sxs-lookup"><span data-stu-id="d9826-146">If the Windows PowerShell Web Access administrator has instructed you to use a URI to a custom site or proxy server instead of a computer name, select **Connection URI** in the **Connection type** field, and then provide the URI.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="d9826-147"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></span><span class="sxs-lookup"><span data-stu-id="d9826-147"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p><span data-ttu-id="d9826-148">Если целевой компьютер входит в рабочую группу, используйте следующий синтаксис, чтобы указать имя пользователя и войти в систему компьютера: &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em>имя_пользователя</em>&gt;.</span><span class="sxs-lookup"><span data-stu-id="d9826-148">If the destination computer is in a workgroup, use the following syntax to provide your user name and sign in to the computer:&lt;<em>workgroup_name</em>&gt;\&lt;<em>user_name</em>&gt;.</span></span></p></li>
    <li><p><span data-ttu-id="d9826-149">Если целевой компьютер является сервером шлюза, то в поле <strong>Имя компьютера</strong> можно указать <strong>localhost</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9826-149">If the destination computer is the gateway server, you can specify <strong>localhost</strong> in the <strong>Computer name</strong> field.</span></span></p></li>
    <li><p><span data-ttu-id="d9826-150">Если целевой компьютер является сервером шлюза и входит в рабочую группу, можно указать <strong>localhost</strong> в поле <strong>Имя компьютера</strong>, но в этом случае нельзя использовать localhost\&lt;<em>имя_пользователя</em>&gt; в поле <strong>Имя пользователя</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9826-150">If the destination computer is the gateway server, and the gateway server is in a workgroup, you can use <strong>localhost</strong> in the <strong>Computer name</strong> field, but do not use localhost\&lt;<em>user_name</em>&gt; in the <strong>User name</strong> field.</span></span> <span data-ttu-id="d9826-151">Вы должны указать &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em>имя_пользователя</em>&gt;.</span><span class="sxs-lookup"><span data-stu-id="d9826-151">You must use &lt;<em>workgroup name</em>&gt;\&lt;<em>user_name</em>&gt;.</span></span></p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

3.  <span data-ttu-id="d9826-152">Раздел **Дополнительные параметры подключения** касается требований к проверке подлинности удаленного компьютера, который предполагается администрировать.</span><span class="sxs-lookup"><span data-stu-id="d9826-152">The **Optional Connection Settings** section relates to the authorization requirements of the remote computer that you want to manage.</span></span> <span data-ttu-id="d9826-153">Дополнительные сведения о параметрах, эквивалентных дополнительным параметрам подключения, см. в разделе [Справка по командлету Enter-PSSession](https://technet.microsoft.com/library/dd315384.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9826-153">For more information about the parameters that are equivalent to optional connection settings, see the [Enter-PSSession cmdlet Help](https://technet.microsoft.com/library/dd315384.aspx).</span></span>

    <span data-ttu-id="d9826-154">Как правило, учетные данные, которые передаются через шлюз Windows PowerShell Web Access, — это те же данные, которые принимаются удаленным компьютером, который предполагается администрировать.</span><span class="sxs-lookup"><span data-stu-id="d9826-154">Typically, the credentials you use to pass through the Windows PowerShell Web Access gateway are the same that are recognized by the remote computer that you want to manage.</span></span> <span data-ttu-id="d9826-155">Тем не менее, если для администрирования удаленного компьютера, указанного на шаге 2, необходимо использовать другие учетные данные, разверните раздел **Дополнительные параметры подключения** и укажите альтернативные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="d9826-155">However, if you want to use different credentials to manage the remote computer that you specified in step 2, expand the **Optional Connection Settings** section, and provide the alternate credentials.</span></span> <span data-ttu-id="d9826-156">В противном случае переходите к шагу 6.</span><span class="sxs-lookup"><span data-stu-id="d9826-156">Otherwise, skip to step 6.</span></span>

4.  <span data-ttu-id="d9826-157">Если администратор Windows PowerShell Web Access создал пользовательскую конфигурацию сеанса для пользователей Windows PowerShell Web Access, укажите имя данной пользовательской конфигурации в поле **Имя конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="d9826-157">If the Windows PowerShell Web Access administrator has created a custom session configuration for Windows PowerShell Web Access users, type the name of the session configuration name in the **Configuration name** field.</span></span> <span data-ttu-id="d9826-158">Дополнительные сведения о конфигурации сеанса см. в разделе [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx) на веб-сайте Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d9826-158">For more information about session configurations, see [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx) on the Microsoft website.</span></span>

5.  <span data-ttu-id="d9826-159">Не изменяйте значение **Тип проверки подлинности** (**По умолчанию**), если администратор Windows PowerShell Web Access не выдал вам иные инструкции.</span><span class="sxs-lookup"><span data-stu-id="d9826-159">Keep the **Authentication type** set to **Default** unless you have been instructed to do otherwise by the Windows PowerShell Web Access administrator.</span></span>

6.  <span data-ttu-id="d9826-160">Нажмите кнопку **Войти**.</span><span class="sxs-lookup"><span data-stu-id="d9826-160">Click **Sign in**.</span></span>

<a href="" id="BKMK_timeout"></a>

<span data-ttu-id="d9826-161"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Выход и превышение времени ожидания</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="d9826-161"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Signing out and timing out</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-162">Любое из следующих действий приводит к завершению сеанса Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9826-162">Any of the following signs you out of a web-based Windows PowerShell session.</span></span>

-   <span data-ttu-id="d9826-163">Нажатие кнопки **Выйти** в правом нижнем углу консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-163">Clicking **Sign out** in the lower right corner of the console.</span></span> <span data-ttu-id="d9826-164">(только для Windows Server 2012)</span><span class="sxs-lookup"><span data-stu-id="d9826-164">(Windows Server 2012 only)</span></span>

-   <span data-ttu-id="d9826-165">Нажатие кнопки **Сохранить** или **Выход** в правом нижнем углу консоли (только в Windows Server 2012 R2).</span><span class="sxs-lookup"><span data-stu-id="d9826-165">Clicking **Save** or **Exit** in the lower right corner of the console (Windows Server 2012 R2 only).</span></span> <span data-ttu-id="d9826-166">При нажатии кнопки **Сохранить** ваш сеанс Windows PowerShell Web Access сохраняется и закрывается; позднее вы можете заново подключиться к этому сеансу.</span><span class="sxs-lookup"><span data-stu-id="d9826-166">Clicking **Save** saves and closes your Windows PowerShell Web Access session; you can reconnect to the session later.</span></span> <span data-ttu-id="d9826-167">При повторном входе в Windows PowerShell Web Access отображается список сохраненных сеансов; вы можете выбрать сохраненный сеанс и повторно подключиться к нему или начать новый сеанс.</span><span class="sxs-lookup"><span data-stu-id="d9826-167">When you sign in to Windows PowerShell Web Access again, Windows PowerShell Web Access displays a list of your saved sessions; you can either select and reconnect to a saved session, or start a new session.</span></span> <span data-ttu-id="d9826-168">Максимальное количество сеансов, как сохраненных, так и активных, которое разрешено открывать пользователю, настраивается администратором шлюза.</span><span class="sxs-lookup"><span data-stu-id="d9826-168">The maximum number of open sessions that users are allowed, both saved and active, is configured by the gateway administrator.</span></span>

    <span data-ttu-id="d9826-169">При нажатии кнопки **Выход** вы выходите из сеанса Windows PowerShell Web Access без его сохранения.</span><span class="sxs-lookup"><span data-stu-id="d9826-169">Clicking **Exit** signs you out of the Windows PowerShell Web Access session without saving it.</span></span>

-   <span data-ttu-id="d9826-170">Попытка войти в систему для администрирования другого удаленного компьютера в том же сеансе браузера или в новой вкладке того же сеанса.</span><span class="sxs-lookup"><span data-stu-id="d9826-170">Attempting to sign in to manage a different remote computer in the same browser session, or in a new tab of the same browser session.</span></span> <span data-ttu-id="d9826-171">(Это не применимо, если сервер шлюза работает под управлением Windows Server 2012 R2; Windows PowerShell Web Access, работающий в Windows Server 2012 R2, разрешает несколько сеансов пользователя в новых вкладках в одном и том же сеансе браузера.) Дополнительные сведения о том, как использовать более одного активного сеанса на одном компьютере см. в пункте "Одновременное подключение к нескольким конечным компьютерам" подраздела [Ограничения веб-консоли](#BKMK_limits) данного раздела.</span><span class="sxs-lookup"><span data-stu-id="d9826-171">(This does not apply if the gateway server is running Windows Server 2012 R2; Windows PowerShell Web Access running on Windows Server 2012 R2 does allow multiple user sessions in new tabs in the same browser session.) For more information about how to use more than one active session on the same computer, see “Connecting to multiple target computers simultaneously” in the [Limitations of the web-based console](#BKMK_limits) section of this topic.</span></span>

-   <span data-ttu-id="d9826-172">20 минут бездействия в сеансе.</span><span class="sxs-lookup"><span data-stu-id="d9826-172">20 minutes of inactivity in the session.</span></span> <span data-ttu-id="d9826-173">Администратор шлюза может изменить время ожидания при бездействии; дополнительные сведения см. в разделе [Управление сеансами](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx#BKMK_sesmgmt).</span><span class="sxs-lookup"><span data-stu-id="d9826-173">The gateway administrator can customize the inactivity time-out period; for more information, see [Session management](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx#BKMK_sesmgmt).</span></span>

    -   <span data-ttu-id="d9826-174">Если вы отключились от сеанса в веб-консоли в результате сетевых ошибок или другого незапланированного завершения работы или сбоя, а не потому, что сами закрыли свой сеанс, этот сеанс Windows PowerShell Web Access продолжает работать, оставаясь подключенными к целевому компьютеру, пока не истечет время ожидания на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d9826-174">If you are disconnected from a session in the web-based console because of a network error or other unplanned shutdown or failure, and not because you have closed the session yourself, the Windows PowerShell Web Access session continues to run, connected to the target computer, until the time-out period on the client side lapses.</span></span> <span data-ttu-id="d9826-175">По умолчанию это время ожидания составляет 20 минут и настраивается администратором шлюза.</span><span class="sxs-lookup"><span data-stu-id="d9826-175">By default, this time-out period is 20 minutes, and is configured by the gateway administrator.</span></span> <span data-ttu-id="d9826-176">Сеанс отключается после истечения либо 20 минут, установленных по умолчанию, либо времени ожидания, заданного администратором шлюза, в зависимости от того, какой период короче.</span><span class="sxs-lookup"><span data-stu-id="d9826-176">The session is disconnected after either the default 20 minutes, or after the time-out period specified by the gateway administrator, whichever is shorter.</span></span>

        <span data-ttu-id="d9826-177">Если сервер шлюза работает под управлением Windows Server 2012 R2, Windows PowerShell Web Access предоставляет пользователям возможность повторного подключения к сохраненным сеансам позднее, но пользователи не смогут увидеть сохраненные сеансы и повторно к ним подключиться, пока не истечет время ожидания, заданное администратором шлюза.</span><span class="sxs-lookup"><span data-stu-id="d9826-177">If the gateway server is running Windows Server 2012 R2, Windows PowerShell Web Access lets users reconnect to saved sessions at a later time, but you cannot see or reconnect to saved sessions until after the time-out period specified by the gateway administrator has lapsed.</span></span>

-   <span data-ttu-id="d9826-178">Закрытие окна или вкладки браузера.</span><span class="sxs-lookup"><span data-stu-id="d9826-178">Closing the browser window or tab.</span></span>

-   <span data-ttu-id="d9826-179">Выключение клиентского устройства, на котором открыт браузер или отключение его от сети.</span><span class="sxs-lookup"><span data-stu-id="d9826-179">Turning off the client device on which the browser is running, or disconnecting it from the network.</span></span>

-   <span data-ttu-id="d9826-180">Выполнение команды **Exit** в веб-консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-180">Running the **Exit** command in the web console.</span></span> <span data-ttu-id="d9826-181">Эта команда не действует, если в конфигурации сеанса, которая используется для подключения, настроена поддержка режима [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) или пространство выполнения ограничено.</span><span class="sxs-lookup"><span data-stu-id="d9826-181">This command does not work if the session configuration to which you are connected to is configured to support [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) mode, or is in a restricted runspace.</span></span>

<span data-ttu-id="d9826-182">Если необходимо снова выполнить вход, откройте веб-страницу Windows PowerShell Web Access и войдите, выполняя шаги, описанные в подразделе [Вход в систему Windows PowerShell Web Access](#BKMK_signin) данного раздела.</span><span class="sxs-lookup"><span data-stu-id="d9826-182">If you want to sign in again, open the Windows PowerShell Web Access web page again, and sign in by following the steps in [To sign in to Windows PowerShell Web Access](#BKMK_signin) in this topic.</span></span>

<a href="" id="BKMK_web"></a>

<span data-ttu-id="d9826-183"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Отличительные особенности веб-консоли Windows PowerShell</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="d9826-183"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Differences in the web-based Windows PowerShell console</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-184">После входа в Windows PowerShell Web в браузер или на вкладке открывается веб-консоль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9826-184">After signing in to Windows PowerShell Web Access, a web-based Windows PowerShell console opens in your browser window or tab.</span></span> <span data-ttu-id="d9826-185">Поскольку консоль подключается к удаленному компьютеру, который вы указали в процессе входа, можно использовать только те командлеты или сценарии Windows PowerShell, которые доступны на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="d9826-185">Because the console is connected to the remote computer that you specified during the sign-in process, only those Windows PowerShell cmdlets or scripts that are available on the remote computer can be used in the console.</span></span> <span data-ttu-id="d9826-186">В этом разделе описываются другие ограничения консолей Windows PowerShell Web Access, а также различия между консолями Windows PowerShell Web Access и установленной консолью **PowerShell.exe**.</span><span class="sxs-lookup"><span data-stu-id="d9826-186">This section describes other limitations of Windows PowerShell Web Access consoles, and differences between Windows PowerShell Web Access consoles and the installed **PowerShell.exe** console.</span></span>

###

<span data-ttu-id="d9826-187"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Принципиальные функциональные отличия от PowerShell.exe</span></a></span><span class="sxs-lookup"><span data-stu-id="d9826-187"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Functional disparity with PowerShell.exe</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-188">Большая часть базового функционала Windows PowerShell доступна в веб-консоли Windows PowerShell Web Access, но некоторые функции все же отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="d9826-188">The majority of Windows PowerShell host functionality is available in the Windows PowerShell Web Access web-based console, but there are some features that are not available.</span></span>

-   <span data-ttu-id="d9826-189"><span class="label">Многоуровневое отображение хода выполнения.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-189"><span class="label">Nested progress displays.</span></span></span>  <span data-ttu-id="d9826-190">Windows PowerShell Web Access отображает элемент управления пользовательского интерфейса "Ход выполнения" для командлетов, которые сообщают о ходе выполнения, но выводится только информация верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d9826-190">Windows PowerShell Web Access displays a progress GUI for cmdlets that report progress, but only top-level progress information is displayed.</span></span>

-   <span data-ttu-id="d9826-191"><span class="label">Изменение цветов ввода.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-191"><span class="label">Input color modification.</span></span></span>  <span data-ttu-id="d9826-192">Цвета ввода (фоновый и основной) нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="d9826-192">The input color (both foreground and background) cannot be changed.</span></span> <span data-ttu-id="d9826-193">Стиль вывода, предупреждения, подробности и сообщения об ошибках можно изменить путем выполнения сценария.</span><span class="sxs-lookup"><span data-stu-id="d9826-193">The style of output, warning, verbose, and error messages can all be changed by running a script.</span></span>

-   <span data-ttu-id="d9826-194"><span class="label">PSHostRawUserInterface.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-194"><span class="label">PSHostRawUserInterface.</span></span></span>  <span data-ttu-id="d9826-195">Windows PowerShell Web Access реализуется через удаленное управление Windows PowerShell и использует удаленное пространство выполнения.</span><span class="sxs-lookup"><span data-stu-id="d9826-195">Windows PowerShell Web Access is implemented over Windows PowerShell remote management, and uses a remote runspace.</span></span> <span data-ttu-id="d9826-196">Windows PowerShell Web Access в своем интерфейсе не реализует ряд методов, например любые команды, осуществляющие запись в консоль Windows.</span><span class="sxs-lookup"><span data-stu-id="d9826-196">Windows PowerShell Web Access does not implement some methods in this interface; for example, any command that writes to the Windows console.</span></span> <span data-ttu-id="d9826-197">Такие команды как **PowerTab** в Windows PowerShell Web Access не работают.</span><span class="sxs-lookup"><span data-stu-id="d9826-197">Commands such as **PowerTab** do not work in Windows PowerShell Web Access.</span></span>

-   <span data-ttu-id="d9826-198"><span class="label">Функциональные клавиши.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-198"><span class="label">Function keys.</span></span></span>  <span data-ttu-id="d9826-199">Windows PowerShell Web Access не поддерживает некоторые сочетания клавиш, во многих случаях потому, что эти клавиши зарезервированы для команд браузера.</span><span class="sxs-lookup"><span data-stu-id="d9826-199">Windows PowerShell Web Access does not support some function keys, in many cases because the commands are reserved by the browser.</span></span>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><span data-ttu-id="d9826-200">Неподдерживаемые сочетания клавиш</span><span class="sxs-lookup"><span data-stu-id="d9826-200">Unsupported Function Key</span></span></p></th>
<th><p><span data-ttu-id="d9826-201">Действие</span><span class="sxs-lookup"><span data-stu-id="d9826-201">Action</span></span></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span data-ttu-id="d9826-202">CTRL+C</span><span class="sxs-lookup"><span data-stu-id="d9826-202">Ctrl+C</span></span></p></td>
<td><p><span data-ttu-id="d9826-203">В Windows PowerShell Web Access для копирования содержимого с помощью браузера используется сочетание клавиш <strong>Ctrl+C</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9826-203">In Windows PowerShell Web Access, <strong>Ctrl+C</strong> is used by the browser to copy content.</span></span> <span data-ttu-id="d9826-204">Для отмены команд в консоли имеется кнопка <strong>Отмена</strong>; кроме этой кнопки пользователи могут использовать клавиши <strong>CTRL+Q</strong>.</span><span class="sxs-lookup"><span data-stu-id="d9826-204">The console offers a <strong>Cancel</strong> button, and users can also use <strong>Ctrl+Q</strong> to cancel commands.</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-205">ALT-ПРОБЕЛ, e, l</span><span class="sxs-lookup"><span data-stu-id="d9826-205">Alt-space, e, l</span></span></p></td>
<td><p><span data-ttu-id="d9826-206">Прокрутка буфера экрана</span><span class="sxs-lookup"><span data-stu-id="d9826-206">Scroll through the screen buffer</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-207">ALT+ПРОБЕЛ, e, f</span><span class="sxs-lookup"><span data-stu-id="d9826-207">Alt+Space, e, f</span></span></p></td>
<td><p><span data-ttu-id="d9826-208">Поиск текста в буфере экрана</span><span class="sxs-lookup"><span data-stu-id="d9826-208">Search for text in the screen buffer</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-209">ALT+ПРОБЕЛ, e, k</span><span class="sxs-lookup"><span data-stu-id="d9826-209">Alt+Space, e, k</span></span></p></td>
<td><p><span data-ttu-id="d9826-210">Выбор текста для копирования из буфера экрана</span><span class="sxs-lookup"><span data-stu-id="d9826-210">Select text to be copied from the screen buffer</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-211">ALT+ПРОБЕЛ, e, p</span><span class="sxs-lookup"><span data-stu-id="d9826-211">Alt+Space, e, p</span></span></p></td>
<td><p><span data-ttu-id="d9826-212">Вставка содержимого буфера обмена в консоль Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9826-212">Paste clipboard contents into the Windows PowerShell console</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-213">ALT+ПРОБЕЛ, c</span><span class="sxs-lookup"><span data-stu-id="d9826-213">Alt+Space, c</span></span></p></td>
<td><p><span data-ttu-id="d9826-214">Закрытие консоли Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9826-214">Close the Windows PowerShell console</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-215">CTRL+BREAK.</span><span class="sxs-lookup"><span data-stu-id="d9826-215">Ctrl+Break</span></span></p></td>
<td><p><span data-ttu-id="d9826-216">Принудительное закрытие окна Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9826-216">Force the Windows PowerShell window to close</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-217">CTRL+HOME</span><span class="sxs-lookup"><span data-stu-id="d9826-217">Ctrl+Home</span></span></p></td>
<td><p><span data-ttu-id="d9826-218">Удаление символов с начала текущей командной строки до курсора</span><span class="sxs-lookup"><span data-stu-id="d9826-218">Deletes from the beginning of the current command line</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-219">CTRL+END</span><span class="sxs-lookup"><span data-stu-id="d9826-219">Ctrl+End</span></span></p></td>
<td><p><span data-ttu-id="d9826-220">Удаление символов от курсора до конца командной строки</span><span class="sxs-lookup"><span data-stu-id="d9826-220">Deletes to end of the command line</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-221">F1</span><span class="sxs-lookup"><span data-stu-id="d9826-221">F1</span></span></p></td>
<td><p><span data-ttu-id="d9826-222">Перемещение курсора в командной строке на один символ вправо</span><span class="sxs-lookup"><span data-stu-id="d9826-222">Move cursor one character to the right on your command line</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-223">F2</span><span class="sxs-lookup"><span data-stu-id="d9826-223">F2</span></span></p></td>
<td><p><span data-ttu-id="d9826-224">Создание новой команды посредством копирования последней команды до текущего символа</span><span class="sxs-lookup"><span data-stu-id="d9826-224">Creates a new command by copying your last command up to the character that you type</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-225">F3</span><span class="sxs-lookup"><span data-stu-id="d9826-225">F3</span></span></p></td>
<td><p><span data-ttu-id="d9826-226">Завершение командной строки посредством вставки содержимого последней командной строки</span><span class="sxs-lookup"><span data-stu-id="d9826-226">Complete the command line with content from your last command line</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-227">F4</span><span class="sxs-lookup"><span data-stu-id="d9826-227">F4</span></span></p></td>
<td><p><span data-ttu-id="d9826-228">Удаление символов в позиции курсора</span><span class="sxs-lookup"><span data-stu-id="d9826-228">Deletes characters from cursor position</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-229">F5</span><span class="sxs-lookup"><span data-stu-id="d9826-229">F5</span></span></p></td>
<td><p><span data-ttu-id="d9826-230">Просмотр введенных ранее команд.</span><span class="sxs-lookup"><span data-stu-id="d9826-230">Scan backward through your command history.</span></span> <span data-ttu-id="d9826-231">Для доступа к введенным ранее командам в Windows PowerShell Web Access нажмите кнопку прокрутки <strong>Журнал</strong> в веб-консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-231">To access commands in the command history in Windows PowerShell Web Access, click the <strong>History</strong> scroll buttons in the web-based console.</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-232">F7</span><span class="sxs-lookup"><span data-stu-id="d9826-232">F7</span></span></p></td>
<td><p><span data-ttu-id="d9826-233">Интерактивный выбор команд из журнала команд</span><span class="sxs-lookup"><span data-stu-id="d9826-233">Interactively select a command from your command history</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-234">F8</span><span class="sxs-lookup"><span data-stu-id="d9826-234">F8</span></span></p></td>
<td><p><span data-ttu-id="d9826-235">Просмотр журнала с выводом команд, содержащих текущий текст</span><span class="sxs-lookup"><span data-stu-id="d9826-235">Scan history displaying commands that match current text</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-236">F9</span><span class="sxs-lookup"><span data-stu-id="d9826-236">F9</span></span></p></td>
<td><p><span data-ttu-id="d9826-237">Запуск команды с определенным номером в журнале</span><span class="sxs-lookup"><span data-stu-id="d9826-237">Run a specific numbered command from history</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-238">PAGE UP</span><span class="sxs-lookup"><span data-stu-id="d9826-238">Page Up</span></span></p></td>
<td><p><span data-ttu-id="d9826-239">Запуск первой команды в журнале</span><span class="sxs-lookup"><span data-stu-id="d9826-239">Run the first command in the history</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="d9826-240">PAGE DOWN</span><span class="sxs-lookup"><span data-stu-id="d9826-240">Page Down</span></span></p></td>
<td><p><span data-ttu-id="d9826-241">Запуск последней команды в журнале</span><span class="sxs-lookup"><span data-stu-id="d9826-241">Run the last command in the history</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="d9826-242">ALT+F7</span><span class="sxs-lookup"><span data-stu-id="d9826-242">Alt+F7</span></span></p></td>
<td><p><span data-ttu-id="d9826-243">Очистка списка журнала команд</span><span class="sxs-lookup"><span data-stu-id="d9826-243">Clear the command history list</span></span></p></td>
</tr>
</tbody>
</table><span data-ttu-id="d9826-244">

<a href="" id="BKMK_limits"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Ограничения веб-консоли</span></a></span><span class="sxs-lookup"><span data-stu-id="d9826-244">

<a href="" id="BKMK_limits"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Limitations of the web-based console</span></a></span></span>

------------------------------------------------------------------------

-   <span data-ttu-id="d9826-245"><span class="label">Двойной прыжок.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-245"><span class="label">Double-hop.</span></span></span>   <span data-ttu-id="d9826-246">Вы можете столкнуться с ограничением двойного прыжка (или подключения ко второму компьютеру из первого подключения) при попытке создания нового сеанса с помощью Windows PowerShell Web Access или работы в нем.</span><span class="sxs-lookup"><span data-stu-id="d9826-246">You can encounter the double-hop (or connecting to a second computer from the first connection) limitation if you try to create or work on a new session by using Windows PowerShell Web Access.</span></span> <span data-ttu-id="d9826-247">Windows PowerShell Web Access использует удаленное пространство выполнения, и на данный момент **PowerShell.exe** не поддерживает установление удаленного подключения ко второму компьютеру из удаленного пространства выполнения.</span><span class="sxs-lookup"><span data-stu-id="d9826-247">Windows PowerShell Web Access uses a remote runspace, and currently, **PowerShell.exe** does not support establishing a remote connection to a second computer from a remote runspace.</span></span> <span data-ttu-id="d9826-248">При попытке подключиться ко второму удаленному компьютеру из существующего подключения, например с помощью командлета **Enter-PSSession**, возможно возникновение различных ошибок типа "Не удается получить сетевые ресурсы".</span><span class="sxs-lookup"><span data-stu-id="d9826-248">If you attempt to connect to a second remote computer from an existing connection by using the **Enter-PSSession** cmdlet, for example, you can get various errors, such as “Cannot get network resources.”</span></span>

    <span data-ttu-id="d9826-249">Чтобы избежать ошибок двойного подключения, администратор должен настроить в сетевой среде организации проверку подлинности CredSSP.</span><span class="sxs-lookup"><span data-stu-id="d9826-249">To avoid double-hop errors, your administrator should configure CredSSP authentication in your organization’s network environment.</span></span> <span data-ttu-id="d9826-250">Дополнительные сведения о настройке проверки подлинности CredSSP см. в разделе [CredSSP для двойного удаленного подключения](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) веб-сайта Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d9826-250">For more information about configuring CredSSP authentication, see [CredSSP for second-hop remoting](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) on the Microsoft website.</span></span> <span data-ttu-id="d9826-251">Кроме того, можно также явно указать учетные данные для администрирования второго удаленного компьютера; неявное указание учетных данных для двойного подключения вряд ли позволит выполнить второе подключение.</span><span class="sxs-lookup"><span data-stu-id="d9826-251">You can also provide explicit credentials when you want to manage a second remote computer; implicit credentials are unlikely to allow the second hop.</span></span>

-   <span data-ttu-id="d9826-252">В Windows PowerShell Web Access используются и действуют те же ограничения, как и в удаленном сеансе Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9826-252">Windows PowerShell Web Access uses and has the same limitations as a remote Windows PowerShell session.</span></span> <span data-ttu-id="d9826-253">Команды, которые напрямую вызывают API консоли Windows, например команды для консольных редакторов или программы текстовых меню, не действуют, поскольку эти команды не могут выполнять чтение или запись в стандартный ввод, вывод и каналы ошибок.</span><span class="sxs-lookup"><span data-stu-id="d9826-253">Commands that directly call Windows console APIs, such as those for console-based editors or text-based menu programs, do not work because the commands do not read or write to standard input, output, and error pipes.</span></span> <span data-ttu-id="d9826-254">Следовательно, команды, запускающие исполняемые файлы, например **notepad.exe**, или отображающие графический интерфейс пользователя, например <span class="code">OpenGridView</span> или <span class="code">ogv</span>, также не работают.</span><span class="sxs-lookup"><span data-stu-id="d9826-254">Therefore, commands that launch an executable file, such as **notepad.exe**, or display a GUI, such as <span class="code">OpenGridView</span> or <span class="code">ogv</span>, do not work.</span></span> <span data-ttu-id="d9826-255">Это поведение влияет на взаимодействие с пользователем; создается впечатление, что Windows PowerShell Web Access не реагирует на команды.</span><span class="sxs-lookup"><span data-stu-id="d9826-255">Your experience is affected by this behavior; to you, it appears that Windows PowerShell Web Access is not responding to your command.</span></span>

-   <span data-ttu-id="d9826-256">Заполнение нажатием клавиши TAB не действует в сеансах, сконфигурированных для работы в ограниченном пространстве выполнения или в режиме **NoLanguage**.</span><span class="sxs-lookup"><span data-stu-id="d9826-256">Tab completion does not work in a session configuration with a restricted runspace or one that is in **NoLanguage** mode.</span></span> <span data-ttu-id="d9826-257">Хотя администраторы могут настроить поддержку заполнения клавишей TAB для сеанса, этого не рекомендуется делать из соображений безопасности, потому что случайный пользователь сможет получить несанкционированный доступ к следующим сведениям.</span><span class="sxs-lookup"><span data-stu-id="d9826-257">Although administrators can configure a session to support tab completion, it is discouraged for security reasons, because it can expose the following information to unauthorized users.</span></span>

    -   <span data-ttu-id="d9826-258">Внутренние пути файловой системы</span><span class="sxs-lookup"><span data-stu-id="d9826-258">Internal file system paths</span></span>

    -   <span data-ttu-id="d9826-259">Общие папки на внутренних компьютерах</span><span class="sxs-lookup"><span data-stu-id="d9826-259">Shared folders on internal computers</span></span>

    -   <span data-ttu-id="d9826-260">Переменные в пространстве выполнения</span><span class="sxs-lookup"><span data-stu-id="d9826-260">Variables in the runspace</span></span>

    -   <span data-ttu-id="d9826-261">Загруженные типы пространств имен или пространства имен .NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9826-261">Loaded types or.NET Framework namespaces</span></span>

    -   <span data-ttu-id="d9826-262">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="d9826-262">Environment variables</span></span>

-   <span data-ttu-id="d9826-263">Пользователи, выполнившие вход в конфигурацию сеанса **NoLanguage** или в ограниченное пространство выполнения в Windows PowerShell Web Access, не могут запустить команду **Exit** для завершения сеанса.</span><span class="sxs-lookup"><span data-stu-id="d9826-263">Users who are signed in to a **NoLanguage** session configuration or a restricted runspace in Windows PowerShell Web Access cannot run the **Exit** command to end the session.</span></span> <span data-ttu-id="d9826-264">Для выхода такие пользователи должны нажать кнопку **Выйти** на странице консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-264">To sign out, users should click **Sign Out** on the console page.</span></span>

-   <span data-ttu-id="d9826-265"><span class="label">Одновременное подключение к нескольким целевым компьютерам.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-265"><span class="label">Connecting to multiple target computers simultaneously.</span></span></span>   <span data-ttu-id="d9826-266">Если сервер шлюза работает под управлением Windows Server 2012, Windows PowerShell Web Access разрешает только одно подключение к удаленному компьютеру в одном сеансе браузера; пользователям не разрешается выполнить один вход и подключиться к нескольким удаленным компьютерам, используя отдельные вкладки браузера.</span><span class="sxs-lookup"><span data-stu-id="d9826-266">If the gateway server is running Windows Server 2012, Windows PowerShell Web Access allows only one remote computer connection per browser session; it does not allow users to sign in once, and connect to multiple remote computers by using separate browser tabs.</span></span> <span data-ttu-id="d9826-267">Если вы откроете новую вкладку или новое окно браузера, Windows PowerShell Web Access предложит вам завершить текущий сеанс и начать новый, чтобы обеспечить возможность подключения к новому (или тому же) удаленному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="d9826-267">When you open a new tab or new browser window, Windows PowerShell Web Access prompts you to disconnect your current session and start a new session, so that you can connect to the new (or the same) remote computer.</span></span> <span data-ttu-id="d9826-268">Если все же желательно запустить два или более отдельных сеансов для разных удаленных компьютеров, в Internet Explorer есть средство, с помощью которого можно начать новый сеанс.</span><span class="sxs-lookup"><span data-stu-id="d9826-268">If two or more separate sessions to different remote computers are desired, however, a feature in Internet Explorer lets you create a new session.</span></span> <span data-ttu-id="d9826-269">Чтобы начать новый сеанс браузера в Internet Explorer, нажмите клавишу **ALT**, откройте меню **Файл**, а затем выберите **Новый сеанс**.</span><span class="sxs-lookup"><span data-stu-id="d9826-269">To start a new browser session in Internet Explorer, press **ALT**, open the **File** menu, and then select **New Session**.</span></span> <span data-ttu-id="d9826-270">Затем откройте веб-сайт Windows PowerShell Web Access в этом новом сеансе и выполните вход, чтобы получить доступ к другому удаленному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="d9826-270">Then, open the Windows PowerShell Web Access website in the new session, and sign in to access another remote computer.</span></span>

    <span data-ttu-id="d9826-271">Если шлюз Windows PowerShell Web Access работает под управлением Windows Server 2012 R2, пользователи могут открывать несколько подключений к удаленным компьютерам на разных вкладках браузера.</span><span class="sxs-lookup"><span data-stu-id="d9826-271">When the Windows PowerShell Web Access gateway is running on Windows Server 2012 R2, users can open multiple connections to remote computers in different browser tabs.</span></span> <span data-ttu-id="d9826-272">Если вы хотите открыть несколько подключений к удаленному компьютеру с помощью веб-консоли Windows PowerShell, узнайте у вашего администратора шлюза Windows PowerShell Web Access, поддерживается ли эта функциональность сервером шлюза.</span><span class="sxs-lookup"><span data-stu-id="d9826-272">If you want to open more than one connection to a remote computer by using the web-based Windows PowerShell console, check with your Windows PowerShell Web Access gateway administrator to see if this feature is supported by the gateway server.</span></span>

-   <span data-ttu-id="d9826-273"><span class="label">Постоянные сеансы Windows PowerShell (повторное подключение).</span></span><span class="sxs-lookup"><span data-stu-id="d9826-273"><span class="label">Persistent Windows PowerShell sessions (Reconnection).</span></span></span>   <span data-ttu-id="d9826-274">После истечения времени ожидания шлюза Windows PowerShell Web Access удаленное подключение между шлюзом и целевым компьютером закрывается.</span><span class="sxs-lookup"><span data-stu-id="d9826-274">After you time out of the Windows PowerShell Web Access gateway, the remote connection between the gateway and the target computer is closed.</span></span> <span data-ttu-id="d9826-275">При этом прекращается выполнение всех командлетов или сценариев.</span><span class="sxs-lookup"><span data-stu-id="d9826-275">This stops any cmdlets or scripts that are currently in process.</span></span> <span data-ttu-id="d9826-276">При выполнении продолжительных задач рекомендуется использовать инфраструктуру **-Job** Windows PowerShell, чтобы можно было запустить задания, отключиться от компьютера, а затем снова подключиться без прекращения выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="d9826-276">You are encouraged to use the Windows PowerShell **-Job** infrastructure when you are performing long-running tasks, so that you can start jobs, disconnect from the computer, reconnect later, and have jobs persist.</span></span> <span data-ttu-id="d9826-277">Другое преимущество использования командлетов **-Job** состоит в том, что их можно запустить с помощью Windows PowerShell Web Access, выйти из системы и подключиться снова, запустив Windows PowerShell Web Access или другой узел (например, интегрированную среду сценариев (ISE) Windows PowerShell®).</span><span class="sxs-lookup"><span data-stu-id="d9826-277">Another benefit of using **-Job** cmdlets is that you can start them by using Windows PowerShell Web Access, sign out, and then reconnect later, either by running Windows PowerShell Web Access or another host (such as Windows PowerShell® Integrated Scripting Environment (ISE)).</span></span>

-   <span data-ttu-id="d9826-278"><span class="label">Изменение размеров окна консоли.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-278"><span class="label">Console resizing.</span></span></span>   <span data-ttu-id="d9826-279">Размеры окна консоли **PowerShell.exe** можно изменить следующими тремя способами.</span><span class="sxs-lookup"><span data-stu-id="d9826-279">The **PowerShell.exe** console window can be resized in the following three ways.</span></span>

    -   <span data-ttu-id="d9826-280">Отрегулировать размер окна консоли при помощи мыши.</span><span class="sxs-lookup"><span data-stu-id="d9826-280">Drag and adjust the console window size with a mouse</span></span>

    -   <span data-ttu-id="d9826-281">Изменить свойства "высота" и "ширина" при помощи пользовательского интерфейса для изменения свойств консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-281">Change the height and width properties by using a GUI for console properties</span></span>

    -   <span data-ttu-id="d9826-282">Изменить высоту и ширину окна консоли при помощи командлета.</span><span class="sxs-lookup"><span data-stu-id="d9826-282">Changing the height and width of console windows with a cmdlet</span></span>

        <span data-ttu-id="d9826-283">Далее показано, как настроить окно консоли для Windows PowerShell Web Access при помощи командлетов.</span><span class="sxs-lookup"><span data-stu-id="d9826-283">The console window for Windows PowerShell Web Access can be configured by using the cmdlets as follows.</span></span> <span data-ttu-id="d9826-284">В следующем примере пользователь изменяет ширину окна консоли Windows PowerShell Web Access до **20**.</span><span class="sxs-lookup"><span data-stu-id="d9826-284">In the following example, a user changes the width of Windows PowerShell Web Access console to **20**.</span></span>

        [<span data-ttu-id="d9826-285">Copy</span><span class="sxs-lookup"><span data-stu-id="d9826-285">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_778d5e55-9195-4bd7-b313-d1fbca7876e4'); "Копировать в буфер обмена".)

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        <span data-ttu-id="d9826-286">Таким же способом изменяется высота окна консоли.</span><span class="sxs-lookup"><span data-stu-id="d9826-286">You can change the height of the console in a similar manner.</span></span>

        <span data-ttu-id="d9826-287">Дополнительные примеры по настройке внешнего вида консоли доступны в [блоге группы Windows PowerShell](http://blogs.msdn.com/b/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d9826-287">Additional examples for customizing the console view are available in the [Windows PowerShell Team Blog](http://blogs.msdn.com/b/powershell/).</span></span>

<span data-ttu-id="d9826-288"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="d9826-288"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">See Also</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="d9826-289">[Справочник по командлетам Windows PowerShell](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
[Windows PowerShell в Microsoft TechNet](https://technet.microsoft.com/library/bb978526.aspx)
[Репозиторий центра сценариев TechNet](http://gallery.technet.microsoft.com/scriptcenter)
[Центр сценариев — эй, сценарист!](https://technet.microsoft.com/scriptcenter)
[Блог группы Windows PowerShell](http://blogs.msdn.com/b/powershell/)</span><span class="sxs-lookup"><span data-stu-id="d9826-289">[Windows PowerShell Cmdlet Reference](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
[Windows PowerShell on Microsoft TechNet](https://technet.microsoft.com/library/bb978526.aspx)
[TechNet Script Center Repository](http://gallery.technet.microsoft.com/scriptcenter)
[Script Center - Hey, Scripting Guy!](https://technet.microsoft.com/scriptcenter)
[Windows PowerShell Team Blog](http://blogs.msdn.com/b/powershell/)</span></span>

<span data-ttu-id="d9826-290"><span>Демонстрация:</span> унаследованная защита</span><span class="sxs-lookup"><span data-stu-id="d9826-290"><span>Show:</span> Inherited Protected</span></span>

<span data-ttu-id="d9826-291"><span class="stdr-votetitle">Эта страница была полезной?</span></span><span class="sxs-lookup"><span data-stu-id="d9826-291"><span class="stdr-votetitle">Was this page helpful?</span></span></span>
<span data-ttu-id="d9826-292">Да Нет</span><span class="sxs-lookup"><span data-stu-id="d9826-292">Yes No</span></span>

<span data-ttu-id="d9826-293">Дополнительные отзывы?</span><span class="sxs-lookup"><span data-stu-id="d9826-293">Additional feedback?</span></span>

<span data-ttu-id="d9826-294">Осталось <span class="stdr-count"><span class="stdr-charcnt">1500</span> символов</span> Отправить Пропустить</span><span class="sxs-lookup"><span data-stu-id="d9826-294"><span class="stdr-count"><span class="stdr-charcnt">1500</span> characters remaining</span> Submit Skip this</span></span>

<span data-ttu-id="d9826-295"><span class="stdr-thankyou">Спасибо!</span></span><span class="sxs-lookup"><span data-stu-id="d9826-295"><span class="stdr-thankyou">Thank you!</span></span></span> <span data-ttu-id="d9826-296"><span class="stdr-appreciate">Мы ценим ваши отзывы.</span></span><span class="sxs-lookup"><span data-stu-id="d9826-296"><span class="stdr-appreciate">We appreciate your feedback.</span></span></span>

[<span data-ttu-id="d9826-297">Управление профилем</span><span class="sxs-lookup"><span data-stu-id="d9826-297">Manage Your Profile</span></span>](https://social.technet.microsoft.com/profile)

|

<span data-ttu-id="d9826-298"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a> Отзыв о сайте</span><span class="sxs-lookup"><span data-stu-id="d9826-298"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Site Feedback</a> Site Feedback</span></span>

<span data-ttu-id="d9826-299"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span><span class="sxs-lookup"><span data-stu-id="d9826-299"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span></span>

<span data-ttu-id="d9826-300">Расскажите о своих впечатлениях...</span><span class="sxs-lookup"><span data-stu-id="d9826-300">Tell us about your experience...</span></span>

<span data-ttu-id="d9826-301">Быстро ли загрузилась страница?</span><span class="sxs-lookup"><span data-stu-id="d9826-301">Did the page load quickly?</span></span>

<span data-ttu-id="d9826-302"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="d9826-302"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="d9826-303">Вам нравится дизайн страницы?</span><span class="sxs-lookup"><span data-stu-id="d9826-303">Do you like the page design?</span></span>

<span data-ttu-id="d9826-304"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="d9826-304"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="d9826-305">Расскажите подробнее</span><span class="sxs-lookup"><span data-stu-id="d9826-305">Tell us more</span></span>

-   [<span data-ttu-id="d9826-306">Информационный бюллетень Flash</span><span class="sxs-lookup"><span data-stu-id="d9826-306">Flash Newsletter</span></span>](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [<span data-ttu-id="d9826-307">Контакты</span><span class="sxs-lookup"><span data-stu-id="d9826-307">Contact Us</span></span>](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [<span data-ttu-id="d9826-308">Заявление о конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="d9826-308">Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)
-   |
-   [<span data-ttu-id="d9826-309">Условия использования</span><span class="sxs-lookup"><span data-stu-id="d9826-309">Terms of Use</span></span>](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [<span data-ttu-id="d9826-310">Товарные знаки</span><span class="sxs-lookup"><span data-stu-id="d9826-310">Trademarks</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

<span data-ttu-id="d9826-311">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="d9826-311">© 2016 Microsoft</span></span>

<span data-ttu-id="d9826-312">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="d9826-312">© 2016 Microsoft</span></span>

<span data-ttu-id="d9826-313">Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющимися владельцами такого кода, а не корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d9826-313">Third party scripts and code linked to or referenced from this website are licensed to you by the parties that own such code, not by Microsoft.</span></span> <span data-ttu-id="d9826-314">См. условия использования ASP.NET Ajax CDN — http://www.asp.net/ajaxlibrary/CDN.ashx.</span><span class="sxs-lookup"><span data-stu-id="d9826-314">See ASP.NET Ajax CDN Terms of Use - http://www.asp.net/ajaxlibrary/CDN.ashx.</span></span>
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />

