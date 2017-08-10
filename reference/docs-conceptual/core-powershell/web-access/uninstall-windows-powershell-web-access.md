---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Удаление Windows PowerShell Web Access"
ms.openlocfilehash: 7231d5eadceda8e3b28d9a81c2b5dcbe43680ff2
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
#  <a name="uninstall-windows-powershell-web-access"></a><span data-ttu-id="47c86-103">Удаление Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="47c86-103">Uninstall Windows PowerShell Web Access</span></span>

<span data-ttu-id="47c86-104">Обновлено: 24 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="47c86-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="47c86-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="47c86-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="47c86-106">Выполните процедуры в этом разделе, чтобы удалить веб-сайт и приложение Windows PowerShell Web Access с сервера шлюза, который работает под управлением Windows Server 2012 R2 или Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="47c86-106">Follow steps in this topic to delete the Windows PowerShell Web Access website and application from the gateway server that is running either Windows Server 2012 R2 or Windows Server 2012.</span></span> <span data-ttu-id="47c86-107">Прежде чем начать, известите пользователей веб-консоли, что вы удаляете веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="47c86-107">Before you begin, notify users of the web-based console that you are removing the website.</span></span>

<a href="" id="BKMK_uninstall"></a>

------------------------------------------------------------------------

<span data-ttu-id="47c86-108">Перед удалением Windows PowerShell Web Access с сервера шлюза выполните командлет <span class="code">Uninstall-PswaWebApplication</span>, чтобы удалить веб-сайт и веб-приложения Windows PowerShell Web Access, или используйте процедуру диспетчера служб IIS [Удаление веб-сайта и веб-приложений Windows PowerShell Web Access](#BKMK_delsite).</span><span class="sxs-lookup"><span data-stu-id="47c86-108">Before you uninstall Windows PowerShell Web Access from the gateway server, either run the <span class="code">Uninstall-PswaWebApplication</span> cmdlet to remove the website and Windows PowerShell Web Access web applications, or use the IIS Manager procedure, [To delete the Windows PowerShell Web Access website and web applications by using IIS Manager](#BKMK_delsite).</span></span>

<span data-ttu-id="47c86-109">Удаление Windows PowerShell Web Access не приводит к удалению IIS или любых других компонентов, которые были установлены автоматически, поскольку они требуются для выполнения Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="47c86-109">Uninstalling Windows PowerShell Web Access does not uninstall IIS or any other features that were installed automatically because Windows PowerShell Web Access requires them to run.</span></span> <span data-ttu-id="47c86-110">В процессе удаления остаются установленными компоненты, от которых зависит Windows PowerShell Web Access. Вы можете удалить эти компоненты при необходимости.</span><span class="sxs-lookup"><span data-stu-id="47c86-110">The uninstallation process leaves features installed upon which Windows PowerShell Web Access was dependent; you can uninstall those features separately if needed.</span></span>

<span data-ttu-id="47c86-111"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Рекомендуемое (быстрое) удаление</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="47c86-111"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Recommended (quick) uninstallation</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="47c86-112">В этом разделе приводятся процедуры для удаления веб-приложения Windows PowerShell Web Access и компонента Windows PowerShell Web Access с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c86-112">Procedures in this section help you uninstall both the Windows PowerShell Web Access web application and the Windows PowerShell Web Access feature by using Windows PowerShell cmdlets.</span></span>

###

<span data-ttu-id="47c86-113"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Удаление веб-приложения</span></a></span><span class="sxs-lookup"><span data-stu-id="47c86-113"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 1: Delete the web application</span></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="47c86-114">Если вы задали настраиваемое имя веб-сайта, добавьте параметр <span class="code">WebsiteName</span> в команду и укажите имя веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="47c86-114">If you have specified your own, custom website name, add the <span class="code">WebsiteName</span> parameter to your command, and specify the website name.</span></span> <span data-ttu-id="47c86-115">Если использовалось настраиваемое веб-приложение (не приложение **pswa** по умолчанию), добавьте параметр <span class="code">WebApplicationName</span> в команду и укажите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="47c86-115">If you have used a custom web application (not the default application, **pswa**, add the <span class="code">WebApplicationName</span> parameter to your command, and specify the name of the web application.</span></span>

#### <a name="to-delete-the-website-and-web-applications-by-using-the-uninstall-pswawebapplication-cmdlet"></a><span data-ttu-id="47c86-116">Удаление веб-сайта и веб-приложений с помощью командлета Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="47c86-116">To delete the website and web applications by using the Uninstall-PswaWebApplication cmdlet</span></span>

1.  <span data-ttu-id="47c86-117">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47c86-117">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="47c86-118">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.</span><span class="sxs-lookup"><span data-stu-id="47c86-118">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="47c86-119">На **начальном** экране Windows щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="47c86-119">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2.  <span data-ttu-id="47c86-120">Введите **Uninstall-PswaWebApplication** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="47c86-120">Type **Uninstall-PswaWebApplication**, and then press **Enter**.</span></span>

3.  <span data-ttu-id="47c86-121">Если используется тестовый сертификат, добавьте в командлет параметр <span class="code">DeleteTestCertificate</span>, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="47c86-121">If you are using a test certificate, add the <span class="code">DeleteTestCertificate</span> parameter to the cmdlet, as shown in the following example.</span></span>

    [<span data-ttu-id="47c86-122">Copy</span><span class="sxs-lookup"><span data-stu-id="47c86-122">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_28147344-ab2f-49e7-b1c2-6dbe649d4366'); "Копировать в буфер обмена".)

        Uninstall-PswaWebApplication -DeleteTestCertificate

###

<span data-ttu-id="47c86-123"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Удаление Windows PowerShell Web Access</span></a></span><span class="sxs-lookup"><span data-stu-id="47c86-123"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 2: Uninstall Windows PowerShell Web Access</span></a></span></span>

------------------------------------------------------------------------

#### <a name="to-uninstall-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a><span data-ttu-id="47c86-124">Удаление Windows PowerShell Web Access с помощью командлетов Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="47c86-124">To uninstall Windows PowerShell Web Access by using Windows PowerShell cmdlets</span></span>

1.  <span data-ttu-id="47c86-125">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="47c86-125">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span> <span data-ttu-id="47c86-126">Если сеанс уже открыт, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="47c86-126">If a session is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="47c86-127">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="47c86-127">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="47c86-128">На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="47c86-128">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

2.  <span data-ttu-id="47c86-129">Введите следующую команду и нажмите клавишу **ВВОД**, где *computer_name* представляет удаленный сервер, с которого требуется удалить Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="47c86-129">Type the following, and then press **Enter**, where *computer_name* represents a remote server from which you want to remove Windows PowerShell Web Access.</span></span> <span data-ttu-id="47c86-130">Параметр <span class="code">-Restart</span> автоматически перезагружает целевые серверы, если это требуется при удалении.</span><span class="sxs-lookup"><span data-stu-id="47c86-130">The <span class="code">-Restart</span> parameter automatically restarts destination servers if required by the removal.</span></span>

    [<span data-ttu-id="47c86-131">Copy</span><span class="sxs-lookup"><span data-stu-id="47c86-131">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_7b534520-f292-471f-89e3-a1079c03e369'); "Копировать в буфер обмена".)

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    <span data-ttu-id="47c86-132">Чтобы удалить роли и компоненты с автономного виртуального жесткого диска (VHD), необходимо добавить оба параметра — <span class="code">-ComputerName</span> и <span class="code">-VHD</span>.</span><span class="sxs-lookup"><span data-stu-id="47c86-132">To remove roles and features from an offline VHD, you must add both the <span class="code">-ComputerName</span> parameter and the <span class="code">-VHD</span> parameter.</span></span> <span data-ttu-id="47c86-133">Параметр <span class="code">-ComputerName</span> содержит имя сервера, на котором следует подключить виртуальный жесткий диск, а параметр <span class="code">-VHD</span> — путь к VHD-файлу на указанном сервере.</span><span class="sxs-lookup"><span data-stu-id="47c86-133">The <span class="code">-ComputerName</span> parameter contains the name of the server on which to mount the VHD, and the <span class="code">-VHD</span> parameter contains the path to the VHD file on the specified server.</span></span>

    [<span data-ttu-id="47c86-134">Copy</span><span class="sxs-lookup"><span data-stu-id="47c86-134">Copy</span></span>](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_5d8f91ee-b91a-4653-b7df-e745187fd72d'); "Копировать в буфер обмена".)

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

3.  <span data-ttu-id="47c86-135">После завершения удаления Windows PowerShell Web Access откройте для проверки страницу **Все серверы** в диспетчере серверов, выберите сервер, с которого был удален компонент, и просмотрите плитку **Роли и компоненты** на странице для выбранного сервера.</span><span class="sxs-lookup"><span data-stu-id="47c86-135">When removal is finished, verify that you removed Windows PowerShell Web Access by opening the **All Servers** page in Server Manager, selecting a server from which you removed the feature, and viewing the **Roles and Features** tile on the page for the selected server.</span></span> <span data-ttu-id="47c86-136">Можно также выполнить командлет <span class="code">Get-WindowsFeature</span>, адресованный выбранному серверу (Get-WindowsFeature -ComputerName &lt;*имя_компьютера*&gt;), чтобы просмотреть список ролей и компонентов, установленных на сервере.</span><span class="sxs-lookup"><span data-stu-id="47c86-136">You can also run the <span class="code">Get-WindowsFeature</span> cmdlet targeted at the selected server (Get-WindowsFeature -ComputerName &lt;*computer_name*&gt;) to view a list of roles and features that are installed on the server.</span></span>

<span data-ttu-id="47c86-137"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Настраиваемое удаление</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="47c86-137"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Custom uninstallation</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="47c86-138">В этом разделе приводятся процедуры для удаления веб-приложения Windows PowerShell Web Access и компонента Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов в диспетчере серверов и на консоли диспетчера служб IIS.</span><span class="sxs-lookup"><span data-stu-id="47c86-138">Procedures in this section help you uninstall both the Windows PowerShell Web Access web application and the Windows PowerShell Web Access feature by using the Remove Roles and Features Wizard in Server Manager, and the IIS Manager console.</span></span>

###

<span data-ttu-id="47c86-139"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Удаление веб-приложения</span></a></span><span class="sxs-lookup"><span data-stu-id="47c86-139"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 1: Delete the web application</span></a></span></span>

------------------------------------------------------------------------

#### <a name="to-delete-the-windows-powershell-web-access-website-and-web-applications-by-using-iis-manager"></a><span data-ttu-id="47c86-140">Удаление веб-сайта Windows PowerShell Web Access и веб-приложений с помощью диспетчера служб IIS</span><span class="sxs-lookup"><span data-stu-id="47c86-140">To delete the Windows PowerShell Web Access website and web applications by using IIS Manager</span></span>

1.  <span data-ttu-id="47c86-141">Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="47c86-141">Open the IIS Manager console by doing one of the following.</span></span> <span data-ttu-id="47c86-142">Если консоль уже открыта, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="47c86-142">If it is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="47c86-143">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="47c86-143">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="47c86-144">В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="47c86-144">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="47c86-145">На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="47c86-145">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="47c86-146">Щелкните ярлык, когда он появится в списке результатов **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="47c86-146">Click the shortcut when it is displayed in the **Apps** results.</span></span>

2.  <span data-ttu-id="47c86-147">В области дерева диспетчера служб IIS выберите веб-сайт, на котором выполняется веб-приложение Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="47c86-147">In the IIS Manager tree pane, select the website that is running the Windows PowerShell Web Access web application.</span></span>

3.  <span data-ttu-id="47c86-148">В области **Действия** в разделе **Управление веб-сайтом** щелкните **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="47c86-148">In the **Actions** pane, under **Manage Website**, click **Stop**.</span></span>

4.  <span data-ttu-id="47c86-149">В области дерева щелкните правой кнопкой мыши веб-приложение на веб-сайте, на котором выполняется веб-приложение Windows PowerShell Web Access, а затем выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="47c86-149">In the tree pane, right-click the web application in the website that is running the Windows PowerShell Web Access web application, and then click **Remove**.</span></span>

5.  <span data-ttu-id="47c86-150">В области дерева выберите **Пулы приложений**, выберите папку пула приложений Windows PowerShell Web Access, щелкните **Остановить** в области **Действия**, а затем щелкните **Удалить** в области содержимого.</span><span class="sxs-lookup"><span data-stu-id="47c86-150">In the tree pane, select **Application Pools**, select the Windows PowerShell Web Access application pool folder, click **Stop** in the **Actions** pane, and then click **Remove** in the content pane.</span></span>

6.  <span data-ttu-id="47c86-151">Закройте диспетчер IIS.</span><span class="sxs-lookup"><span data-stu-id="47c86-151">Close IIS Manager.</span></span>

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span data-ttu-id="47c86-152"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание.</span></span><span class="sxs-lookup"><span data-stu-id="47c86-152"><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Note </span></span></span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><span data-ttu-id="47c86-153">Сертификат не удаляется при этой операции удаления.</span><span class="sxs-lookup"><span data-stu-id="47c86-153">The certificate is not deleted during uninstallation.</span></span> <span data-ttu-id="47c86-154">Если вы создали самозаверяющий сертификат или использовали тестовый сертификат и хотите удалить его, удалите сертификат в диспетчере служб IIS.</span><span class="sxs-lookup"><span data-stu-id="47c86-154">If you created a self-signed certificate or used a test certificate and want to remove it, delete the certificate in IIS Manager.</span></span></p></td>
    </tr>
    </tbody>
    </table>

###

<span data-ttu-id="47c86-155"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Удаление Windows PowerShell Web Access</span></a></span><span class="sxs-lookup"><span data-stu-id="47c86-155"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Step 2: Uninstall Windows PowerShell Web Access</span></a></span></span>

------------------------------------------------------------------------

#### <a name="to-uninstall-windows-powershell-web-access-by-using-the-remove-roles-and-features-wizard"></a><span data-ttu-id="47c86-156">Удаление Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов</span><span class="sxs-lookup"><span data-stu-id="47c86-156">To uninstall Windows PowerShell Web Access by using the Remove Roles and Features Wizard</span></span>

1.  <span data-ttu-id="47c86-157">Если диспетчер серверов уже открыт, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="47c86-157">If Server Manager is already open, go on to the next step.</span></span> <span data-ttu-id="47c86-158">Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="47c86-158">If Server Manager is not already open, open it by doing one of the following.</span></span>

    -   <span data-ttu-id="47c86-159">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="47c86-159">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span>

    -   <span data-ttu-id="47c86-160">На **начальном** экране в Windows выберите **Диспетчер серверов**.</span><span class="sxs-lookup"><span data-stu-id="47c86-160">On the Windows **Start** screen, click **Server Manager**.</span></span>

2.  <span data-ttu-id="47c86-161">В меню **Управление** выберите команду **Удалить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="47c86-161">On the **Manage** menu, click **Remove Roles and Features**.</span></span>

3.  <span data-ttu-id="47c86-162">На странице **Выбор целевого сервера** выберите сервер или виртуальный жесткий диск, с которого следует удалить компонент.</span><span class="sxs-lookup"><span data-stu-id="47c86-162">On the **Select destination server** page, select the server or offline VHD from which you want to remove the feature.</span></span> <span data-ttu-id="47c86-163">Чтобы выбрать автономный виртуальный жесткий диск, сначала выберите сервер, на котором будет подключен виртуальный жесткий диск, а затем выберите VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="47c86-163">To select an offline VHD, first select the server on which to mount the VHD, and then select the VHD file.</span></span> <span data-ttu-id="47c86-164">Выбрав конечный сервер, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="47c86-164">After you have selected the destination server, click **Next**.</span></span>

4.  <span data-ttu-id="47c86-165">Еще раз щелкните **Далее**, чтобы пропустить страницу **Удаление компонентов**.</span><span class="sxs-lookup"><span data-stu-id="47c86-165">Click **Next** again to skip to the **Remove features** page.</span></span>

5.  <span data-ttu-id="47c86-166">Снимите флажок **Windows PowerShell Web Access** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="47c86-166">Clear the check box for **Windows PowerShell Web Access**, and then click **Next**.</span></span>

6.  <span data-ttu-id="47c86-167">На странице **Подтверждение удаления компонентов** щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="47c86-167">On the **Confirm removal selections** page, click **Remove**.</span></span>

<span data-ttu-id="47c86-168"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span><span class="sxs-lookup"><span data-stu-id="47c86-168"><a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">See Also</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a></span></span>

------------------------------------------------------------------------

<span data-ttu-id="47c86-169">[Установка и использование Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[Справка IIS Manager 7.0](https://technet.microsoft.com/library/cc732664.aspx)</span><span class="sxs-lookup"><span data-stu-id="47c86-169">[Install and Use Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[IIS Manager 7.0 Help](https://technet.microsoft.com/library/cc732664.aspx)</span></span>

<span data-ttu-id="47c86-170"><span>Демонстрация:</span> унаследованная защита</span><span class="sxs-lookup"><span data-stu-id="47c86-170"><span>Show:</span> Inherited Protected</span></span>

<span data-ttu-id="47c86-171"><span class="stdr-votetitle">Эта страница была полезной?</span></span><span class="sxs-lookup"><span data-stu-id="47c86-171"><span class="stdr-votetitle">Was this page helpful?</span></span></span>
<span data-ttu-id="47c86-172">Да Нет</span><span class="sxs-lookup"><span data-stu-id="47c86-172">Yes No</span></span>

<span data-ttu-id="47c86-173">Дополнительные отзывы?</span><span class="sxs-lookup"><span data-stu-id="47c86-173">Additional feedback?</span></span>

<span data-ttu-id="47c86-174">Осталось <span class="stdr-count"><span class="stdr-charcnt">1500</span> символов</span> Отправить Пропустить</span><span class="sxs-lookup"><span data-stu-id="47c86-174"><span class="stdr-count"><span class="stdr-charcnt">1500</span> characters remaining</span> Submit Skip this</span></span>

<span data-ttu-id="47c86-175"><span class="stdr-thankyou">Спасибо!</span></span><span class="sxs-lookup"><span data-stu-id="47c86-175"><span class="stdr-thankyou">Thank you!</span></span></span> <span data-ttu-id="47c86-176"><span class="stdr-appreciate">Мы ценим ваши отзывы.</span></span><span class="sxs-lookup"><span data-stu-id="47c86-176"><span class="stdr-appreciate">We appreciate your feedback.</span></span></span>

[<span data-ttu-id="47c86-177">Управление профилем</span><span class="sxs-lookup"><span data-stu-id="47c86-177">Manage Your Profile</span></span>](https://social.technet.microsoft.com/profile)

|

<span data-ttu-id="47c86-178"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a> Отзыв о сайте</span><span class="sxs-lookup"><span data-stu-id="47c86-178"><a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Site Feedback</a> Site Feedback</span></span>

<span data-ttu-id="47c86-179"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span><span class="sxs-lookup"><span data-stu-id="47c86-179"><a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a></span></span>

<span data-ttu-id="47c86-180">Расскажите о своих впечатлениях...</span><span class="sxs-lookup"><span data-stu-id="47c86-180">Tell us about your experience...</span></span>

<span data-ttu-id="47c86-181">Быстро ли загрузилась страница?</span><span class="sxs-lookup"><span data-stu-id="47c86-181">Did the page load quickly?</span></span>

<span data-ttu-id="47c86-182"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="47c86-182"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="47c86-183">Вам нравится дизайн страницы?</span><span class="sxs-lookup"><span data-stu-id="47c86-183">Do you like the page design?</span></span>

<span data-ttu-id="47c86-184"><span> Да<span> </span></span> <span> Нет<span> </span></span></span><span class="sxs-lookup"><span data-stu-id="47c86-184"><span> Yes<span> </span></span> <span> No<span> </span></span></span></span>

<span data-ttu-id="47c86-185">Расскажите подробнее</span><span class="sxs-lookup"><span data-stu-id="47c86-185">Tell us more</span></span>

-   [<span data-ttu-id="47c86-186">Информационный бюллетень Flash</span><span class="sxs-lookup"><span data-stu-id="47c86-186">Flash Newsletter</span></span>](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [<span data-ttu-id="47c86-187">Контакты</span><span class="sxs-lookup"><span data-stu-id="47c86-187">Contact Us</span></span>](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [<span data-ttu-id="47c86-188">Заявление о конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="47c86-188">Privacy Statement</span></span>](https://privacy.microsoft.com/privacystatement)
-   |
-   [<span data-ttu-id="47c86-189">Условия использования</span><span class="sxs-lookup"><span data-stu-id="47c86-189">Terms of Use</span></span>](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [<span data-ttu-id="47c86-190">Товарные знаки</span><span class="sxs-lookup"><span data-stu-id="47c86-190">Trademarks</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

<span data-ttu-id="47c86-191">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="47c86-191">© 2016 Microsoft</span></span>

<span data-ttu-id="47c86-192">© Корпорация Майкрософт (Microsoft Corporation), 2016 г.</span><span class="sxs-lookup"><span data-stu-id="47c86-192">© 2016 Microsoft</span></span>

<span data-ttu-id="47c86-193">Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющимися владельцами такого кода, а не корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="47c86-193">Third party scripts and code linked to or referenced from this website are licensed to you by the parties that own such code, not by Microsoft.</span></span> <span data-ttu-id="47c86-194">См. условия использования ASP.NET Ajax CDN — http://www.asp.net/ajaxlibrary/CDN.ashx.</span><span class="sxs-lookup"><span data-stu-id="47c86-194">See ASP.NET Ajax CDN Terms of Use - http://www.asp.net/ajaxlibrary/CDN.ashx.</span></span>
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />

