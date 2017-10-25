---
ms.date: 2017-08-23
keywords: "powershell,командлет"
title: "Устранение неполадок с доступом в Windows PowerShell Web Access"
ms.openlocfilehash: 08a9fd286ed8a40e9423deb7d29dc0a8ecf8e5b1
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a><span data-ttu-id="186e9-103">Устранение неполадок с доступом в Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="186e9-103">Troubleshooting Access Problems in Windows PowerShell Web Access</span></span>

<span data-ttu-id="186e9-104">Обновлено: 24 июня 2013 г. (пересмотрено 23 августа 2017 г.)</span><span class="sxs-lookup"><span data-stu-id="186e9-104">Updated: June 24, 2013 (revised August 23, 2017)</span></span>

<span data-ttu-id="186e9-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="186e9-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="186e9-106">В следующем разделе перечислены некоторые часто возникающие проблемы при попытке подключения к удаленному компьютеру с помощью Windows PowerShell Web Access и предложения по разрешению таких проблем.</span><span class="sxs-lookup"><span data-stu-id="186e9-106">The following sections identify some common problems when attempting to connect to a remote computer by using Windows PowerShell Web Access, and includes suggestions for resolving the problems.</span></span>

## <a name="sign-in-failure"></a><span data-ttu-id="186e9-107">Сбой при входе</span><span class="sxs-lookup"><span data-stu-id="186e9-107">Sign-in failure</span></span>

<span data-ttu-id="186e9-108">Сбой может возникать по любой из следующих причин.</span><span class="sxs-lookup"><span data-stu-id="186e9-108">Failure could occur because of any of the following.</span></span>

- <span data-ttu-id="186e9-109">Отсутствуют правило авторизации, которое позволяет пользователю получить доступ к компьютеру, или конкретная конфигурация сеанса на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="186e9-109">An authorization rule that allows the user access to the computer, or a specific session configuration on the remote computer, does not exist.</span></span>

  <span data-ttu-id="186e9-110">Безопасность Windows PowerShell Web Access является ограничивающей. Пользователям необходимо явным образом предоставлять доступ к удаленным компьютерам с помощью правил авторизации.</span><span class="sxs-lookup"><span data-stu-id="186e9-110">Windows PowerShell Web Access security is restrictive; users must be granted explicit access to remote computers by using authorization rules.</span></span>

  <span data-ttu-id="186e9-111">Дополнительные сведения о создании правил авторизации см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="186e9-111">For more information about creating authorization rules, see [Authorization Rules and Security Features of Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).</span></span>

- <span data-ttu-id="186e9-112">У пользователя отсутствует авторизованный доступ к целевому компьютеру.</span><span class="sxs-lookup"><span data-stu-id="186e9-112">The user does not have authorized access to the destination computer.</span></span> <span data-ttu-id="186e9-113">Это определяется списками управления доступом.</span><span class="sxs-lookup"><span data-stu-id="186e9-113">This is determined by access control lists (ACLs).</span></span>

  <span data-ttu-id="186e9-114">Подробнее см. в статье [Вход в систему Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access) или в блоге группы разработчиков Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="186e9-114">For more information, see [Signing in to Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), or the Windows PowerShell Team Blog.</span></span>

- <span data-ttu-id="186e9-115">Возможно, удаленное управление Windows PowerShell не включено на целевом компьютере.</span><span class="sxs-lookup"><span data-stu-id="186e9-115">Windows PowerShell remote management might not be enabled on the destination computer.</span></span>

  <span data-ttu-id="186e9-116">Убедитесь, что удаленное управление включено на компьютере, к которому пытается подключиться пользователь.</span><span class="sxs-lookup"><span data-stu-id="186e9-116">Verify remote management is enabled on the computer to which the user is trying to connect.</span></span>

  <span data-ttu-id="186e9-117">Дополнительные сведения см. в разделе [Настройка удаленного управления компьютером](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span><span class="sxs-lookup"><span data-stu-id="186e9-117">For more information, see [How to Configure Your Computer for Remoting](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).</span></span>

## <a name="internal-server-error"></a><span data-ttu-id="186e9-118">Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="186e9-118">Internal Server Error</span></span>

<span data-ttu-id="186e9-119">При попытке войти в Windows PowerShell Web Access в окне Internet Explorer пользователи видят страницу **Внутренняя ошибка сервера** или *Internet Explorer* перестает реагировать на запросы.</span><span class="sxs-lookup"><span data-stu-id="186e9-119">When users try to sign in to Windows PowerShell Web Access in an Internet Explorer window, they are shown an **Internal Server Error** page, or *Internet Explorer* stops responding.</span></span>

<span data-ttu-id="186e9-120">Эта проблема специфична для Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="186e9-120">This issue is specific to Internet Explorer.</span></span>

### <a name="possible-cause"></a><span data-ttu-id="186e9-121">Возможная причина</span><span class="sxs-lookup"><span data-stu-id="186e9-121">Possible cause</span></span>

<span data-ttu-id="186e9-122">Она может возникнуть, если пользователь вошел в систему с именем домена, содержащим китайские символы, или если такие символы встречаются в имени сервера шлюза.</span><span class="sxs-lookup"><span data-stu-id="186e9-122">This can occur for users who have signed in with a domain name that contains Chinese characters, or if one or more Chinese characters are part of the gateway server name.</span></span>

#### <a name="workaround"></a><span data-ttu-id="186e9-123">Обходной путь</span><span class="sxs-lookup"><span data-stu-id="186e9-123">Workaround</span></span>

1. <span data-ttu-id="186e9-124">[Установите и запустите Internet Explorer 10](http://ie.microsoft.com/testdrive/info/downloads/Default.html).</span><span class="sxs-lookup"><span data-stu-id="186e9-124">[Install and run Internet Explorer 10](http://ie.microsoft.com/testdrive/info/downloads/Default.html)</span></span>
1. <span data-ttu-id="186e9-125">Измените **Режим документа** в Internet Explorer на *стандартный IE10*.</span><span class="sxs-lookup"><span data-stu-id="186e9-125">Change Internet Explorer **Document Mode** setting to *IE10* standards.</span></span>
   1. <span data-ttu-id="186e9-126">Нажмите клавишу **F12**, чтобы открыть консоль "Средства разработчика".</span><span class="sxs-lookup"><span data-stu-id="186e9-126">Press **F12** to open the Developer Tools console</span></span>
   1. <span data-ttu-id="186e9-127">В Internet Explorer 10 щелкните **Режим браузера** и выберите *Internet Explorer 10*.</span><span class="sxs-lookup"><span data-stu-id="186e9-127">In Internet Explorer 10, click **Browser Mode**, and then select *Internet Explorer 10*.</span></span>
   1. <span data-ttu-id="186e9-128">Щелкните **Режим документа** и выберите *стандартный IE10*.</span><span class="sxs-lookup"><span data-stu-id="186e9-128">Click **Document Mode**, and then click *IE10* standards.</span></span>
   1. <span data-ttu-id="186e9-129">Снова нажать клавишу **F12**, чтобы закрыть консоль "Средства разработчика".</span><span class="sxs-lookup"><span data-stu-id="186e9-129">Press **F12** again to close the Developer Tools console.</span></span>
1. <span data-ttu-id="186e9-130">Отключите автоматическую настройку прокси-сервера в Internet Explorer 10.</span><span class="sxs-lookup"><span data-stu-id="186e9-130">Disable automatic proxy configuration in Internet Explorer 10.</span></span>
   1. <span data-ttu-id="186e9-131">В меню **Сервис**выберите пункт **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="186e9-131">Click **Tools**, and then click **Internet Options**.</span></span>
   1. <span data-ttu-id="186e9-132">В диалоговом окне **Свойства браузера** на вкладке **Подключения** выберите  **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="186e9-132">In the **Internet Options** dialog box, on the **Connections** tab, click **LAN settings**.</span></span>
   1. <span data-ttu-id="186e9-133">Снять флажок **Автоматическое определение параметров**.</span><span class="sxs-lookup"><span data-stu-id="186e9-133">Clear the **Automatically detect settings** check box.</span></span> <span data-ttu-id="186e9-134">Нажать кнопку **ОК**, а затем нажать кнопку **ОК** еще раз, чтобы закрыть диалоговое окно *Свойства браузера*.</span><span class="sxs-lookup"><span data-stu-id="186e9-134">Click **OK**, and then click **OK** again to close the *Internet Options* dialog box.</span></span>

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a><span data-ttu-id="186e9-135">Невозможно подключиться к удаленному компьютеру в рабочей группе</span><span class="sxs-lookup"><span data-stu-id="186e9-135">Cannot connect to a remote workgroup computer</span></span>

<span data-ttu-id="186e9-136">Если целевой компьютер является членом рабочей группы, используйте следующий синтаксис, чтобы указать имя пользователя и войти на компьютер: `<workgroup_name>\<user_name>`</span><span class="sxs-lookup"><span data-stu-id="186e9-136">If the destination computer is a member of a workgroup, use the following syntax to provide your user name and sign in to the computer: `<workgroup_name>\<user_name>`</span></span>

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a><span data-ttu-id="186e9-137">Невозможно найти инструменты управления веб-сервера (IIS), даже если роль была установлена</span><span class="sxs-lookup"><span data-stu-id="186e9-137">Cannot find Web Server (IIS) management tools, even though the role was installed</span></span>

<span data-ttu-id="186e9-138">При установке Windows PowerShell Web Access с помощью командлета `Install-WindowsFeature` средства управления не устанавливаются, если в командлет не был добавлен параметр `-IncludeManagementTools`.</span><span class="sxs-lookup"><span data-stu-id="186e9-138">If you installed Windows PowerShell Web Access by using the `Install-WindowsFeature` cmdlet, management tools are not installed unless the `-IncludeManagementTools` parameter is added to the cmdlet.</span></span>

<span data-ttu-id="186e9-139">Например, см. раздел [Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="186e9-139">For an example, see [To install Windows PowerShell Web Access by using Windows PowerShell cmdlets](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).</span></span>

<span data-ttu-id="186e9-140">Вы можете добавить консоль диспетчера служб IIS и другие нужные средства управления IIS, выбрав инструменты в сеансе **мастера добавления ролей и компонентов**, который нацелен на сервер шлюза.</span><span class="sxs-lookup"><span data-stu-id="186e9-140">You can add the IIS Manager console, and other IIS management tools that you need, by selecting the tools in an **Add Roles and Features Wizard** session that is targeted at the gateway server.</span></span>
<span data-ttu-id="186e9-141">Мастер добавления ролей и функций открывается из диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="186e9-141">The Add Roles and Features Wizard is opened from within Server Manager.</span></span>

## <a name="windows-powershell-web-access-website-is-not-accessible"></a><span data-ttu-id="186e9-142">Веб-сайт Windows PowerShell Web Access недоступен</span><span class="sxs-lookup"><span data-stu-id="186e9-142">Windows PowerShell Web Access website is not accessible</span></span>

<span data-ttu-id="186e9-143">Если включена конфигурация повышенной безопасности в Internet Explorer (IE ESC), можно добавить веб-сайт Windows PowerShell Web Access в список надежных сайтов.</span><span class="sxs-lookup"><span data-stu-id="186e9-143">If Enhanced Security Configuration is enabled in Internet Explorer (IE ESC), you can add the Windows PowerShell Web Access website to the list of trusted sites.</span></span>

<span data-ttu-id="186e9-144">Менее предпочтительный способ (из-за угрозы безопасности) — отключить IE ESC.</span><span class="sxs-lookup"><span data-stu-id="186e9-144">A less recommended approach, due to security risks, is to disable IE ESC.</span></span>
<span data-ttu-id="186e9-145">Отключить IE ESC можно с помощью плитки "Свойства" на странице "Локальный сервер" в диспетчере серверов.</span><span class="sxs-lookup"><span data-stu-id="186e9-145">You can disable IE ESC in the Properties tile on the Local Server page in Server Manager.</span></span>

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a><span data-ttu-id="186e9-146">Произошел сбой авторизации.</span><span class="sxs-lookup"><span data-stu-id="186e9-146">An authorization failure occurred.</span></span> <span data-ttu-id="186e9-147">Убедитесь, что вы имеете права на подключение к конечному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="186e9-147">Verify that you are authorized to connect to the destination computer.</span></span>

<span data-ttu-id="186e9-148">Если сервер шлюза является конечным компьютером и в то же время входит в рабочую группу, при попытке подключения выводится указанное выше сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="186e9-148">The above error message is displayed while trying to connect when the gateway server is the destination computer, and is also in a workgroup.</span></span>

<span data-ttu-id="186e9-149">Когда сервер шлюза также является конечным сервером и входит в рабочую группу, укажите имя пользователя, имя компьютера и имя группы пользователей.</span><span class="sxs-lookup"><span data-stu-id="186e9-149">When the gateway server is also the destination server, and it is in a workgroup, specify the user name, computer name, and user group name.</span></span>
<span data-ttu-id="186e9-150">Не используйте точку (.) в качестве имени компьютера.</span><span class="sxs-lookup"><span data-stu-id="186e9-150">Do not use a dot (.) by itself to represent the computer name.</span></span>

### <a name="scenarios-and-proper-values"></a><span data-ttu-id="186e9-151">Ситуации и соответствующие значения</span><span class="sxs-lookup"><span data-stu-id="186e9-151">Scenarios and proper values</span></span>

#### <a name="all-cases"></a><span data-ttu-id="186e9-152">Все ситуации</span><span class="sxs-lookup"><span data-stu-id="186e9-152">All cases</span></span>

<span data-ttu-id="186e9-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="186e9-153">Parameter</span></span> | <span data-ttu-id="186e9-154">Значение</span><span class="sxs-lookup"><span data-stu-id="186e9-154">Value</span></span>
-- | --
<span data-ttu-id="186e9-155">UserName</span><span class="sxs-lookup"><span data-stu-id="186e9-155">UserName</span></span> | <span data-ttu-id="186e9-156">Имя\_сервера\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-156">Server\_name\\user\_name</span></span><br/><span data-ttu-id="186e9-157">Localhost\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-157">Localhost\\user\_name</span></span><br/><span data-ttu-id="186e9-158">.\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-158">.\\user\_name</span></span>
<span data-ttu-id="186e9-159">UserGroup</span><span class="sxs-lookup"><span data-stu-id="186e9-159">UserGroup</span></span> | <span data-ttu-id="186e9-160">имя\_сервера\\группа\_пользователей</span><span class="sxs-lookup"><span data-stu-id="186e9-160">Server\_name\\user\_group</span></span><br/><span data-ttu-id="186e9-161">Localhost\\группа\_пользователей</span><span class="sxs-lookup"><span data-stu-id="186e9-161">Localhost\\user\_group</span></span><br/><span data-ttu-id="186e9-162">.\\группа\_пользователей</span><span class="sxs-lookup"><span data-stu-id="186e9-162">.\\user\_group</span></span>
<span data-ttu-id="186e9-163">ComputerGroup</span><span class="sxs-lookup"><span data-stu-id="186e9-163">ComputerGroup</span></span> | <span data-ttu-id="186e9-164">имя\_сервера\\группа\_компьютеров</span><span class="sxs-lookup"><span data-stu-id="186e9-164">Server\_name\\computer\_group</span></span><br/><span data-ttu-id="186e9-165">Localhost\\группа\_компьютеров</span><span class="sxs-lookup"><span data-stu-id="186e9-165">Localhost\\computer\_group</span></span><br/><span data-ttu-id="186e9-166">.\\группа\_компьютеров</span><span class="sxs-lookup"><span data-stu-id="186e9-166">.\\computer\_group</span></span>

#### <a name="gateway-server-is-in-a-domain"></a><span data-ttu-id="186e9-167">Сервер шлюза входит в домен</span><span class="sxs-lookup"><span data-stu-id="186e9-167">Gateway server is in a domain</span></span>

<span data-ttu-id="186e9-168">Параметр</span><span class="sxs-lookup"><span data-stu-id="186e9-168">Parameter</span></span> | <span data-ttu-id="186e9-169">Значение</span><span class="sxs-lookup"><span data-stu-id="186e9-169">Value</span></span>
-- | --
<span data-ttu-id="186e9-170">имя_компьютера</span><span class="sxs-lookup"><span data-stu-id="186e9-170">ComputerName</span></span> | <span data-ttu-id="186e9-171">Полное имя сервера шлюза или Localhost</span><span class="sxs-lookup"><span data-stu-id="186e9-171">Fully qualified name of gateway server, or Localhost</span></span>

#### <a name="gateway-server-is-in-a-workgroup"></a><span data-ttu-id="186e9-172">Сервер шлюза входит в рабочую группу</span><span class="sxs-lookup"><span data-stu-id="186e9-172">Gateway server is in a workgroup</span></span>

<span data-ttu-id="186e9-173">Параметр</span><span class="sxs-lookup"><span data-stu-id="186e9-173">Parameter</span></span> | <span data-ttu-id="186e9-174">Значение</span><span class="sxs-lookup"><span data-stu-id="186e9-174">Value</span></span>
-- | --
<span data-ttu-id="186e9-175">имя_компьютера</span><span class="sxs-lookup"><span data-stu-id="186e9-175">ComputerName</span></span> | <span data-ttu-id="186e9-176">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="186e9-176">Server name</span></span>

### <a name="gateway-credentials"></a><span data-ttu-id="186e9-177">Учетные данные шлюза</span><span class="sxs-lookup"><span data-stu-id="186e9-177">Gateway credentials</span></span>

<span data-ttu-id="186e9-178">Войдите на сервер шлюза как на конечный компьютер, используя учетные данные в одном из следующих форматов.</span><span class="sxs-lookup"><span data-stu-id="186e9-178">Sign in to a gateway server as target computer by using credentials formatted as one of the following.</span></span>

- <span data-ttu-id="186e9-179">Имя\_сервера\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-179">Server\_name\\user\_name</span></span>
- <span data-ttu-id="186e9-180">Localhost\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-180">Localhost\\user\_name</span></span>
- <span data-ttu-id="186e9-181">.\\имя\_пользователя</span><span class="sxs-lookup"><span data-stu-id="186e9-181">.\\user\_name</span></span>

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a><span data-ttu-id="186e9-182">В правиле авторизации отображается идентификатор безопасности (SID)</span><span class="sxs-lookup"><span data-stu-id="186e9-182">A security identifier (SID) is displayed in an authorization rule</span></span>

<span data-ttu-id="186e9-183">Вместо синтаксиса "имя\_пользователя/имя\_компьютера" в правиле авторизации отображается идентификатор безопасности (SID).</span><span class="sxs-lookup"><span data-stu-id="186e9-183">A security identifier (SID) is displayed in an authorization rule instead of the syntax user\_name/computer\_name.</span></span>

<span data-ttu-id="186e9-184">Либо правило больше не действительно, либо произошла ошибка запроса к доменным службам Active Directory.</span><span class="sxs-lookup"><span data-stu-id="186e9-184">Either the rule is no longer valid, or the Active Directory Domain Services query failed.</span></span>
<span data-ttu-id="186e9-185">Правило авторизации недействительно обычно в том случае, если сервер шлюза когда-то входил в рабочую группу, но позднее был присоединен к домену.</span><span class="sxs-lookup"><span data-stu-id="186e9-185">An authorization rule is usually not valid in scenarios where the gateway server was at one time in a workgroup, but was later joined to a domain</span></span>

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a><span data-ttu-id="186e9-186">Не удается войти с правилом, задающим IPv6-адрес в формате имени домена</span><span class="sxs-lookup"><span data-stu-id="186e9-186">Cannot sign in with rule as an IPv6 address with a domain</span></span>

<span data-ttu-id="186e9-187">Не удается войти на конечный компьютер, указанный в правилах авторизации под IPv6-адресом с доменом.</span><span class="sxs-lookup"><span data-stu-id="186e9-187">Cannot sign in to a target computer that has been specified in authorization rules as an IPv6 address with a domain.</span></span>

<span data-ttu-id="186e9-188">Правила авторизации не поддерживают IPv6-адреса в форме имени домена.</span><span class="sxs-lookup"><span data-stu-id="186e9-188">Authorization rules do not support an IPv6 address in form of a domain name.</span></span>

<span data-ttu-id="186e9-189">Чтобы указать конечный компьютер с помощью IPv6-адреса, используйте в правиле авторизации исходный IPv6-адрес (содержащий двоеточия).</span><span class="sxs-lookup"><span data-stu-id="186e9-189">To specify a destination computer by using an IPv6 address, use the original IPv6 address (that contains colons) in the authorization rule.</span></span>
<span data-ttu-id="186e9-190">IPv6-адреса в форме имени домена и в числовой форме (с двоеточиями) поддерживаются в качестве имени конечного компьютера на странице входа в Windows PowerShell Web Access, но не в правилах авторизации.</span><span class="sxs-lookup"><span data-stu-id="186e9-190">Both domain and numerical (with colons) IPv6 addresses are supported as the target computer name on the Windows PowerShell Web Access sign-in page, but not in authorization rules.</span></span> 

<span data-ttu-id="186e9-191">Дополнительные сведения об IPv6-адресах см. в статье [Принцип работы IPv6](https://technet.microsoft.com/en-us/library/cc781672(v=ws.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="186e9-191">For more information about IPv6 addresses, see [How IPv6 Works](https://technet.microsoft.com/en-us/library/cc781672(v=ws.10).aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="186e9-192">См. также</span><span class="sxs-lookup"><span data-stu-id="186e9-192">See Also</span></span>

- <span data-ttu-id="186e9-193">[Правила авторизации и компоненты безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="186e9-193">[Authorization Rules and Security Features of Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)</span></span>
- <span data-ttu-id="186e9-194">[Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span><span class="sxs-lookup"><span data-stu-id="186e9-194">[Use the Web-based Windows PowerShell Console](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)</span></span>
- [<span data-ttu-id="186e9-195">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="186e9-195">about_Remote_Requirements</span></span>](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)
