---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Устранение неполадок с доступом в Windows PowerShell Web Access"
ms.openlocfilehash: c10e19b177110ff62d44f28b6a523380b55b79e0
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
#  <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a><span data-ttu-id="4d323-103">Устранение неполадок с доступом в Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="4d323-103">Troubleshooting Access Problems in Windows PowerShell Web Access</span></span>

<span data-ttu-id="4d323-104">Обновлено: 24 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="4d323-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="4d323-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4d323-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<a href="" id="BKMK_trouble"></a>

------------------------------------------------------------------------

<span data-ttu-id="4d323-106">В следующей таблице перечислены часто возникающие проблемы пользователей при попытках подключения к удаленному компьютеру с помощью Windows PowerShell Web Access и предложения по разрешению таких проблем.</span><span class="sxs-lookup"><span data-stu-id="4d323-106">The following table identifies some common problems that users might experience when they are attempting to connect to a remote computer by using Windows PowerShell Web Access, and includes suggestions for resolving the problems.</span></span>

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><span data-ttu-id="4d323-107">Проблема</span><span class="sxs-lookup"><span data-stu-id="4d323-107">Problem</span></span></p></th>
<th><p><span data-ttu-id="4d323-108">Возможная причина и решение</span><span class="sxs-lookup"><span data-stu-id="4d323-108">Possible cause and solution</span></span></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span data-ttu-id="4d323-109">Сбой при входе</span><span class="sxs-lookup"><span data-stu-id="4d323-109">Sign-in failure</span></span></p></td>
<td><p><span data-ttu-id="4d323-110">Сбой может возникать по любой из следующих причин.</span><span class="sxs-lookup"><span data-stu-id="4d323-110">Failure could occur because of any of the following.</span></span></p>
<ul>
<li><p><span data-ttu-id="4d323-111">Отсутствуют правило авторизации, которое позволяет пользователю получить доступ к компьютеру, или конкретная конфигурация сеанса на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d323-111">An authorization rule that allows the user access to the computer, or a specific session configuration on the remote computer, does not exist.</span></span> <span data-ttu-id="4d323-112">Безопасность Windows PowerShell Web Access является ограничивающей. Пользователям необходимо явным образом предоставлять доступ к удаленным компьютерам с помощью правил авторизации.</span><span class="sxs-lookup"><span data-stu-id="4d323-112">Windows PowerShell Web Access security is restrictive; users must be granted explicit access to remote computers by using authorization rules.</span></span> <span data-ttu-id="4d323-113">Дополнительные сведения о создании правил авторизации см. в разделе <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access</a> данного руководства.</span><span class="sxs-lookup"><span data-stu-id="4d323-113">For more information about creating authorization rules, see <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Authorization Rules and Security Features of Windows PowerShell Web Access</a> in this guide.</span></span></p></li>
<li><p><span data-ttu-id="4d323-114">У пользователя отсутствует авторизованный доступ к целевому компьютеру.</span><span class="sxs-lookup"><span data-stu-id="4d323-114">The user does not have authorized access to the destination computer.</span></span> <span data-ttu-id="4d323-115">Это определяется списками управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4d323-115">This is determined by access control lists (ACLs).</span></span> <span data-ttu-id="4d323-116">Дополнительные сведения см. в разделе "Вход в Windows PowerShell Web Access" в статье <a href="https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx">Использование веб-консоли Windows PowerShell</a> или в <a href="https://msdn.microsoft.com/library/windows/desktop/ee706585.aspx">блоге группы Windows PowerShell</a>.</span><span class="sxs-lookup"><span data-stu-id="4d323-116">For more information, see “Signing in to Windows PowerShell Web Access” in <a href="https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx">Use the Web-based Windows PowerShell Console</a>, or the <a href="https://msdn.microsoft.com/library/windows/desktop/ee706585.aspx">Windows PowerShell Team Blog</a>.</span></span></p>
<ul>
<li><p><span data-ttu-id="4d323-117">Возможно, удаленное управление Windows PowerShell не включено на целевом компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d323-117">Windows PowerShell remote management might not be enabled on the destination computer.</span></span> <span data-ttu-id="4d323-118">Убедитесь, что оно включено на компьютере, к которому пытается подключиться пользователь.</span><span class="sxs-lookup"><span data-stu-id="4d323-118">Verify that it is enabled on the computer to which the user is trying to connect.</span></span> <span data-ttu-id="4d323-119">Дополнительные сведения см. в разделе "Инструкции по настройке удаленных операций" в описании <a href="https://technet.microsoft.com/library/dd315349.aspx">about_Remote_Requirements</a> в разделах справки "О программе" Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d323-119">For more information, see “How to Configure Your Computer for Remoting” in <a href="https://technet.microsoft.com/library/dd315349.aspx">about_Remote_Requirements</a> in the Windows PowerShell About Help Topics.</span></span></p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="4d323-120">При попытке войти в Windows PowerShell Web Access в окне Internet Explorer пользователи видят страницу <strong>Внутренняя ошибка сервера</strong> или Internet Explorer перестает реагировать на запросы.</span><span class="sxs-lookup"><span data-stu-id="4d323-120">When users try to sign in to Windows PowerShell Web Access in an Internet Explorer window, they are shown an <strong>Internal Server Error</strong> page, or Internet Explorer stops responding.</span></span> <span data-ttu-id="4d323-121">Эта проблема специфична для Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="4d323-121">This issue is specific to Internet Explorer.</span></span></p></td>
<td><p><span data-ttu-id="4d323-122">Она может возникнуть, если пользователь вошел в систему с именем домена, содержащим китайские символы, или если такие символы встречаются в имени сервера шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d323-122">This can occur for users who have signed in with a domain name that contains Chinese characters, or if one or more Chinese characters are part of the gateway server name.</span></span> <span data-ttu-id="4d323-123">Чтобы обойти эту проблему, пользователю нужно <a href="http://ie.microsoft.com/testdrive/info/downloads/Default.html">установить и запустить Internet Explorer 10</a>, а затем выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4d323-123">To work around this issue, the user should <a href="http://ie.microsoft.com/testdrive/info/downloads/Default.html">install and run Internet Explorer 10</a>, and then perform the following steps.</span></span></p>
<ol>
<li><p><span data-ttu-id="4d323-124">Измените <strong>Режим документа</strong> в Internet Explorer на <strong>Стандарты IE10</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-124">Change the Internet Explorer <strong>Document Mode</strong> setting to <strong>IE10 standards</strong>.</span></span></p>
<ol>
<li><p><span data-ttu-id="4d323-125">Нажать клавишу <strong>F12</strong>, чтобы открыть консоль "Средства разработчика".</span><span class="sxs-lookup"><span data-stu-id="4d323-125">Press <strong>F12</strong> to open the Developer Tools console.</span></span></p></li>
<li><p><span data-ttu-id="4d323-126">В Internet Explorer 10 щелкните <strong>Режим браузера</strong> и выберите <strong>Internet Explorer 10</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-126">In Internet Explorer 10, click <strong>Browser Mode</strong>, and then select <strong>Internet Explorer 10</strong>.</span></span></p></li>
<li><p><span data-ttu-id="4d323-127">Щелкните <strong>Режим документа</strong> и выберите <strong>Стандарты IE10</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-127">Click <strong>Document Mode</strong>, and then click <strong>IE10 standards</strong>.</span></span></p></li>
<li><p><span data-ttu-id="4d323-128">Снова нажать клавишу <strong>F12</strong>, чтобы закрыть консоль "Средства разработчика".</span><span class="sxs-lookup"><span data-stu-id="4d323-128">Press <strong>F12</strong> again to close the Developer Tools console.</span></span></p></li>
</ol></li>
<li><p><span data-ttu-id="4d323-129">Отключить автоматическую конфигурацию прокси.</span><span class="sxs-lookup"><span data-stu-id="4d323-129">Disable automatic proxy configuration.</span></span></p>
<ol>
<li><p><span data-ttu-id="4d323-130">В Internet Explorer 10 в щелкните <strong>Сервис</strong> и затем <strong>Свойства браузера</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-130">In Internet Explorer 10, click <strong>Tools</strong>, and then click <strong>Internet Options</strong>.</span></span></p></li>
<li><p><span data-ttu-id="4d323-131">В диалоговом окне <strong>Свойства браузера</strong> на вкладке <strong>Подключения</strong> выберите <strong> Настройка сети</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-131">In the <strong>Internet Options</strong> dialog box, on the <strong>Connections</strong> tab, click <strong>LAN settings</strong>.</span></span></p></li>
<li><p><span data-ttu-id="4d323-132">Снять флажок <strong>Автоматическое определение параметров</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-132">Clear the <strong>Automatically detect settings</strong> check box.</span></span> <span data-ttu-id="4d323-133">Нажать кнопку <strong>ОК</strong>, а затем нажать кнопку <strong>ОК</strong> еще раз, чтобы закрыть диалоговое окно <strong>Свойства браузера</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-133">Click <strong>OK</strong>, and then click <strong>OK</strong> again to close the <strong>Internet Options</strong> dialog box.</span></span></p></li>
</ol></li>
</ol></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="4d323-134">Невозможно подключиться к удаленному компьютеру в рабочей группе</span><span class="sxs-lookup"><span data-stu-id="4d323-134">Cannot connect to a remote workgroup computer</span></span></p></td>
<td><p><span data-ttu-id="4d323-135">Если целевой компьютер входит в рабочую группу, используйте следующий синтаксис, чтобы указать имя пользователя и войти на компьютер: &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em>имя_пользователя</em>&gt;.</span><span class="sxs-lookup"><span data-stu-id="4d323-135">If the destination computer is a member of a workgroup, use the following syntax to provide your user name and sign in to the computer: &lt;<em>workgroup_name</em>&gt;\&lt;<em>user_name</em>&gt;</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="4d323-136">Невозможно найти инструменты управления веб-сервера (IIS), даже если роль была установлена</span><span class="sxs-lookup"><span data-stu-id="4d323-136">Cannot find Web Server (IIS) management tools, even though the role was installed</span></span></p></td>
<td><p><span data-ttu-id="4d323-137">Если вы установили Windows PowerShell Web Access с помощью командлета <span class="code">Install-WindowsFeature</span>, средства управления не устанавливаются, если к командлету добавлен параметр <span class="code">IncludeManagementTools</span>.</span><span class="sxs-lookup"><span data-stu-id="4d323-137">If you installed Windows PowerShell Web Access by using the <span class="code">Install-WindowsFeature</span> cmdlet, management tools are not installed unless the <span class="code">IncludeManagementTools</span> parameter is added to the cmdlet.</span></span> <span data-ttu-id="4d323-138">Например, см. раздел "Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell" в статье <a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">Установка и использование Windows PowerShell Web Access</a>.</span><span class="sxs-lookup"><span data-stu-id="4d323-138">For an example, see “To install Windows PowerShell Web Access by using Windows PowerShell cmdlets” in <a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">Install and Use Windows PowerShell Web Access</a>.</span></span> <span data-ttu-id="4d323-139">Вы можете добавить консоль диспетчера служб IIS и другие нужные инструменты управления IIS, выбрав инструменты в сеансе мастера добавления ролей и функций, который нацелен на сервер шлюза.</span><span class="sxs-lookup"><span data-stu-id="4d323-139">You can add the IIS Manager console and other IIS management tools that you need by selecting the tools in an Add Roles and Features Wizard session that is targeted at the gateway server.</span></span> <span data-ttu-id="4d323-140">Мастер добавления ролей и функций открывается из диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="4d323-140">The Add Roles and Features Wizard is opened from within Server Manager.</span></span></p></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="4d323-141">Веб-сайт Windows PowerShell Web Access недоступен</span><span class="sxs-lookup"><span data-stu-id="4d323-141">The Windows PowerShell Web Access website is not accessible</span></span></p></td>
<td><p><span data-ttu-id="4d323-142">Если включена конфигурация повышенной безопасности в Internet Explorer (IE ESC), можно добавить веб-сайт Windows PowerShell Web Access в список надежных сайтов или отключить IE ESC.</span><span class="sxs-lookup"><span data-stu-id="4d323-142">If Enhanced Security Configuration is enabled in Internet Explorer (IE ESC), you can add the Windows PowerShell Web Access website to the list of trusted sites, or disable IE ESC.</span></span> <span data-ttu-id="4d323-143">Отключить IE ESC можно с помощью плитки <strong>Свойства</strong> на странице <strong>Локальный сервер</strong> в диспетчере серверов.</span><span class="sxs-lookup"><span data-stu-id="4d323-143">You can disable IE ESC in the <strong>Properties</strong> tile on the <strong>Local Server</strong> page in Server Manager.</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="4d323-144">Если сервер шлюза является конечным компьютером и в то же время входит в рабочую группу, при попытке соединения выводится следующее сообщение об ошибке: <strong> Произошел сбой авторизации. Убедитесь, что вы имеете права на подключение к конечному компьютеру</strong>.</span><span class="sxs-lookup"><span data-stu-id="4d323-144">The following error message is displayed while trying to connect when the gateway server is the destination computer, and is also in a workgroup: <strong>An authorization failure occurred. Verify that you are authorized to connect to the destination computer.</strong></span></span></p></td>
<td><p><span data-ttu-id="4d323-145">Когда сервер шлюза также является конечным сервером и входит в рабочую группу, укажите имя пользователя, имя компьютера и имя группы пользователей, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="4d323-145">When the gateway server is also the destination server, and it is in a workgroup, specify the user name, computer name, and user group name as shown in the following table.</span></span> <span data-ttu-id="4d323-146">Не используйте точку (.) в качестве имени компьютера.</span><span class="sxs-lookup"><span data-stu-id="4d323-146">Do not use a dot (.) by itself to represent the computer name.</span></span></p>
<div>
<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th><p><span data-ttu-id="4d323-147">Сценарий</span><span class="sxs-lookup"><span data-stu-id="4d323-147">Scenario</span></span></p></th>
<th><p><span data-ttu-id="4d323-148">Параметр UserName</span><span class="sxs-lookup"><span data-stu-id="4d323-148">UserName Parameter</span></span></p></th>
<th><p><span data-ttu-id="4d323-149">Параметр UserGroup</span><span class="sxs-lookup"><span data-stu-id="4d323-149">UserGroup Parameter</span></span></p></th>
<th><p><span data-ttu-id="4d323-150">Параметр ComputerName</span><span class="sxs-lookup"><span data-stu-id="4d323-150">ComputerName Parameter</span></span></p></th>
<th><p><span data-ttu-id="4d323-151">Параметр ComputerGroup</span><span class="sxs-lookup"><span data-stu-id="4d323-151">ComputerGroup Parameter</span></span></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span data-ttu-id="4d323-152">Сервер шлюза входит в домен</span><span class="sxs-lookup"><span data-stu-id="4d323-152">Gateway server is in a domain</span></span></p></td>
<td><p><span data-ttu-id="4d323-153"><em>имя_сервера</em>\<em>имя_пользователя</em>, Localhost\<em>имя_пользователя</em> или .\<em>имя_пользователя</em></span><span class="sxs-lookup"><span data-stu-id="4d323-153"><em>Server_name</em>\<em>user_name</em>, Localhost\<em>user_name</em>, or .\<em>user_name</em></span></span></p></td>
<td><p><span data-ttu-id="4d323-154"><em>имя_сервера</em>\<em>группа_пользователей</em>, Localhost\<em>группа_пользователей</em> или .\<em>группа_пользователей</em></span><span class="sxs-lookup"><span data-stu-id="4d323-154"><em>Server_name</em>\<em>user_group</em>, Localhost\<em>user_group</em>, or .\<em>user_group</em></span></span></p></td>
<td><p><span data-ttu-id="4d323-155">Полное имя сервера шлюза или Localhost</span><span class="sxs-lookup"><span data-stu-id="4d323-155">Fully qualified name of gateway server, or Localhost</span></span></p></td>
<td><p><span data-ttu-id="4d323-156"><em>имя_сервера</em>\<em>группа_компьютеров</em>, Localhost\<em>группа_компьютеров</em> или .\<em>группа_компьютеров</em></span><span class="sxs-lookup"><span data-stu-id="4d323-156"><em>Server_name</em>\<em>computer_group</em>, Localhost\<em>computer_group</em>, or .\<em>computer_group</em></span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="4d323-157">Сервер шлюза входит в рабочую группу</span><span class="sxs-lookup"><span data-stu-id="4d323-157">Gateway server is in a workgroup</span></span></p></td>
<td><p><span data-ttu-id="4d323-158"><em>имя_сервера</em>\<em>имя_пользователя</em>, Localhost\<em>имя_пользователя</em> или .\<em>имя_пользователя</em></span><span class="sxs-lookup"><span data-stu-id="4d323-158"><em>Server_name</em>\<em>user_name</em>, Localhost\<em>user_name</em>, or .\<em>user_name</em></span></span></p></td>
<td><p><span data-ttu-id="4d323-159"><em>имя_сервера</em>\<em>группа_пользователей</em>, Localhost\<em>группа_пользователей</em> или .\<em>группа_пользователей</em></span><span class="sxs-lookup"><span data-stu-id="4d323-159"><em>Server_name</em>\<em>user_group</em>, Localhost\<em>user_group</em> or .\<em>user_group</em></span></span></p></td>
<td><p><span data-ttu-id="4d323-160">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="4d323-160">Server name</span></span></p></td>
<td><p><span data-ttu-id="4d323-161"><em>имя_сервера</em>\<em>группа_компьютеров</em>, Localhost\<em>группа_компьютеров</em> или .\<em>группа_компьютеров</em></span><span class="sxs-lookup"><span data-stu-id="4d323-161"><em>Server_name</em>\<em>computer_group</em>, Localhost\<em>computer_group</em> or .\<em>computer_group</em></span></span></p></td>
</tr>
</tbody>
</table>
</div>
<p><span data-ttu-id="4d323-162">Войдите на сервер шлюза как на конечный компьютер, используя учетные данные в одном из следующих форматов.</span><span class="sxs-lookup"><span data-stu-id="4d323-162">Sign in to a gateway server as target computer by using credentials formatted as one of the following.</span></span></p>
<ul>
<li><p><span data-ttu-id="4d323-163"><em>имя_сервера</em>\<em>имя_пользователя</em></span><span class="sxs-lookup"><span data-stu-id="4d323-163"><em>Server_name</em>\<em>user_name</em></span></span></p></li>
<li><p><span data-ttu-id="4d323-164">Localhost\<em>имя_пользователя</em></span><span class="sxs-lookup"><span data-stu-id="4d323-164">Localhost\<em>user_name</em></span></span></p></li>
<li><p><span data-ttu-id="4d323-165">.\<em>имя_пользователя</em></span><span class="sxs-lookup"><span data-stu-id="4d323-165">.\<em>user_name</em></span></span></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><span data-ttu-id="4d323-166">Вместо синтаксиса <em>имя_пользователя</em>/<em> имя_компьютера</em>  в правиле авторизации отображается идентификатор безопасности (SID)</span><span class="sxs-lookup"><span data-stu-id="4d323-166">A security identifier (SID) is displayed in an authorization rule instead of the syntax <em>user_name</em>/<em>computer_name</em> </span></span></p></td>
<td><p><span data-ttu-id="4d323-167">Либо правило больше не действительно, либо произошла ошибка запроса к доменным службам Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d323-167">Either the rule is no longer valid, or the Active Directory Domain Services query failed.</span></span> <span data-ttu-id="4d323-168">Правило авторизации недействительно обычно в том случае, если сервер шлюза когда-то входил в рабочую группу, но позднее был присоединен к домену.</span><span class="sxs-lookup"><span data-stu-id="4d323-168">An authorization rule is usually not valid in scenarios where the gateway server was at one time in a workgroup, but was later joined to a domain.</span></span></p></td>
</tr>
<tr class="even">
<td><p><span data-ttu-id="4d323-169">Не удается войти на конечный компьютер, указанный в правилах авторизации под IPv6-адресом с доменом.</span><span class="sxs-lookup"><span data-stu-id="4d323-169">Cannot sign in to a target computer that has been specified in authorization rules as an IPv6 address with a domain.</span></span></p></td>
<td><p><span data-ttu-id="4d323-170">Правила авторизации не поддерживают IPv6-адреса в форме имени домена.</span><span class="sxs-lookup"><span data-stu-id="4d323-170">Authorization rules do not support an IPv6 address in form of a domain name.</span></span> <span data-ttu-id="4d323-171">Чтобы указать конечный компьютер с помощью IPv6-адреса, используйте в правиле авторизации исходный IPv6-адрес (содержащий двоеточия).</span><span class="sxs-lookup"><span data-stu-id="4d323-171">To specify a destination computer by using an IPv6 address, use the original IPv6 address (that contains colons) in the authorization rule.</span></span> <span data-ttu-id="4d323-172">IPv6-адреса в форме имени домена и в числовой форме (с двоеточиями) поддерживаются в качестве имени конечного компьютера на странице входа в Windows PowerShell Web Access, но не в правилах авторизации.</span><span class="sxs-lookup"><span data-stu-id="4d323-172">Both domain and numerical (with colons) IPv6 addresses are supported as the target computer name on the Windows PowerShell Web Access sign-in page, but not in authorization rules.</span></span> <span data-ttu-id="4d323-173">Дополнительные сведения об IPv6-адресах см. в статье <a href="https://technet.microsoft.com/library/cc781672.aspx">Принцип работы IPv6</a>.</span><span class="sxs-lookup"><span data-stu-id="4d323-173">For more information about IPv6 addresses, see <a href="https://technet.microsoft.com/library/cc781672.aspx">How IPv6 Works</a>.</span></span></p></td>
</tr>
</tbody>
</table><span data-ttu-id="4d323-174">

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/dn282395(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="4d323-174">

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">See Also</span></a>
<a href="/en-us/library/dn282395(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="4d323-175">[Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
[Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
[about_Remote_Requirements](https://technet.microsoft.com/library/dd315349.aspx)</span><span class="sxs-lookup"><span data-stu-id="4d323-175">[Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
[Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
[about_Remote_Requirements](https://technet.microsoft.com/library/dd315349.aspx)</span></span>

<span data-ttu-id="4d323-176"><span>Демонстрация:</span> унаследованная защита</span><span class="sxs-lookup"><span data-stu-id="4d323-176"><span>Show:</span> Inherited Protected</span></span>

<span data-ttu-id="4d323-177"><span class="stdr-votetitle">Эта страница была полезной?</span></span><span class="sxs-lookup"><span data-stu-id="4d323-177"><span class="stdr-votetitle">Was this page helpful?</span></span></span>
<span data-ttu-id="4d323-178">Да Нет</span><span class="sxs-lookup"><span data-stu-id="4d323-178">Yes No</span></span>

<span data-ttu-id="4d323-179">Дополнительные отзывы?</span><span class="sxs-lookup"><span data-stu-id="4d323-179">Additional feedback?</span></span>

<span data-ttu-id="4d323-180">Осталось <span class="stdr-count"><span class="stdr-charcnt">1500</span> символов</span> Отправить Пропустить</span><span class="sxs-lookup"><span data-stu-id="4d323-180"><span class="stdr-count"><span class="stdr-charcnt">1500</span> characters remaining</span> Submit Skip this</span></span>

<span data-ttu-id="4d323-181"><span class="stdr-thankyou">Спасибо!</span></span><span class="sxs-lookup"><span data-stu-id="4d323-181"><span class="stdr-thankyou">Thank you!</span></span></span> <span data-ttu-id="4d323-182"><span class="stdr-appreciate">Мы ценим ваши отзывы.</span></span><span class="sxs-lookup"><span data-stu-id="4d323-182"><span class="stdr-appreciate">We appreciate your feedback.</span></span></span>

[<span data-ttu-id="4d323-183">Управление профилем</span><span class="sxs-lookup"><span data-stu-id="4d323-183">Manage Your Profile</span></span>](https://social.technet.microsoft.com/profile)

|

<span data-ttu-id="4d323-184"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a> Отзыв о сайте</span><span class="sxs-lookup"><span data-stu-id="4d323-184"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Site Feedback</a> Site Feedback</span></span>

<span data-ttu-id="4d323-185"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span><span class="sxs-lookup"><span data-stu-id="4d323-185"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span></span>

<span data-ttu-id="4d323-186">Расскажите о своих впечатлениях...</span><span class="sxs-lookup"><span data-stu-id="4d323-186">Tell us about your experience...</span></span>

<span data-ttu-id="4d323-187">Быстро ли загрузилась страница?</span><span class="sxs-lookup"><span data-stu-id="4d323-187">Did the page load quickly?</span></span>

<span data-ttu-id="4d323-188"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="4d323-188"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="4d323-189">Вам нравится дизайн страницы?</span><span class="sxs-lookup"><span data-stu-id="4d323-189">Do you like the page design?</span></span>

<span data-ttu-id="4d323-190"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="4d323-190"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="4d323-191">Расскажите подробнее</span><span class="sxs-lookup"><span data-stu-id="4d323-191">Tell us more</span></span>

-   [<span data-ttu-id="4d323-192">Информационный бюллетень Flash</span><span class="sxs-lookup"><span data-stu-id="4d323-192">Flash Newsletter</span></span>](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [<span data-ttu-id="4d323-193">Контакты</span><span class="sxs-lookup"><span data-stu-id="4d323-193">Contact Us</span></span>](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [<span data-ttu-id="4d323-194">Заявление о конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="4d323-194">Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)
-   |
-   [<span data-ttu-id="4d323-195">Условия использования</span><span class="sxs-lookup"><span data-stu-id="4d323-195">Terms of Use</span></span>](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [<span data-ttu-id="4d323-196">Товарные знаки</span><span class="sxs-lookup"><span data-stu-id="4d323-196">Trademarks</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

<span data-ttu-id="4d323-197">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="4d323-197">© 2016 Microsoft</span></span>

<span data-ttu-id="4d323-198">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="4d323-198">© 2016 Microsoft</span></span>

<span data-ttu-id="4d323-199">Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющимися владельцами такого кода, а не корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4d323-199">Third party scripts and code linked to or referenced from this website are licensed to you by the parties that own such code, not by Microsoft.</span></span> <span data-ttu-id="4d323-200">См. условия использования ASP.NET Ajax CDN — http://www.asp.net/ajaxlibrary/CDN.ashx.</span><span class="sxs-lookup"><span data-stu-id="4d323-200">See ASP.NET Ajax CDN Terms of Use - http://www.asp.net/ajaxlibrary/CDN.ashx.</span></span>
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />

