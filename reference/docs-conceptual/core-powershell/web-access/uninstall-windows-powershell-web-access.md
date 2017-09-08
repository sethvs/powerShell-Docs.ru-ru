---
ms.date: 2017-08-23
keywords: "powershell,командлет"
title: "Удаление Windows PowerShell Web Access"
ms.openlocfilehash: 6b75eadb7264d7478fb3c9bc2b2ff355772ef4c2
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="uninstall-windows-powershell-web-access"></a><span data-ttu-id="ee068-103">Удаление Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="ee068-103">Uninstall Windows PowerShell Web Access</span></span>

<span data-ttu-id="ee068-104">Обновлено: 24 июня 2013 г.</span><span class="sxs-lookup"><span data-stu-id="ee068-104">Updated: June 24, 2013</span></span>

<span data-ttu-id="ee068-105">Область применения: Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ee068-105">Applies To: Windows Server 2012 R2, Windows Server 2012</span></span>

<span data-ttu-id="ee068-106">В этом разделе приведена процедура удаления веб-сайта Windows PowerShell Web Access и соответствующего приложения с сервера шлюза, где они установлены.</span><span class="sxs-lookup"><span data-stu-id="ee068-106">The steps in this topic remove the Windows PowerShell Web Access website and corresponding application from the gateway server where it is installed.</span></span>

## <a name="notify-users"></a><span data-ttu-id="ee068-107">Уведомить пользователей</span><span class="sxs-lookup"><span data-stu-id="ee068-107">Notify users</span></span>

<span data-ttu-id="ee068-108">Прежде чем начать, известите пользователей веб-консоли, что вы удаляете веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ee068-108">Before you begin, notify users of the web-based console that you are removing the website.</span></span>


<span data-ttu-id="ee068-109">Перед удалением Windows PowerShell Web Access с сервера шлюза выполните командлет `Uninstall-PswaWebApplication`, чтобы удалить веб-сайт и веб-приложения Windows PowerShell Web Access, или используйте процедуру диспетчера служб IIS [Удаление веб-сайта и веб-приложений Windows PowerShell Web Access]().</span><span class="sxs-lookup"><span data-stu-id="ee068-109">Before you uninstall Windows PowerShell Web Access from the gateway server, either run the `Uninstall-PswaWebApplication` cmdlet to remove the website and Windows PowerShell Web Access web applications, or use the IIS Manager procedure, [to delete the windows powershell web access website and web applications by using iis manager]().</span></span>

<span data-ttu-id="ee068-110">Удаление Windows PowerShell Web Access не приводит к удалению IIS или любых других компонентов, которые были установлены автоматически, поскольку они требуются для выполнения Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="ee068-110">Uninstalling Windows PowerShell Web Access does not uninstall IIS or any other features that were installed automatically because Windows PowerShell Web Access requires them to run.</span></span> <span data-ttu-id="ee068-111">В процессе удаления остаются установленными компоненты, от которых зависит Windows PowerShell Web Access. Вы можете удалить эти компоненты при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ee068-111">The uninstallation process leaves features installed upon which Windows PowerShell Web Access was dependent; you can uninstall those features separately if needed.</span></span>

## <a name="recommended-quick-uninstallation"></a><span data-ttu-id="ee068-112">Рекомендуемое (быстрое) удаление</span><span class="sxs-lookup"><span data-stu-id="ee068-112">Recommended (quick) uninstallation</span></span>

<span data-ttu-id="ee068-113">Процедуры этого раздела используются для удаления:</span><span class="sxs-lookup"><span data-stu-id="ee068-113">Procedures in this section help you uninstall both:</span></span>

- <span data-ttu-id="ee068-114">веб-приложения Windows PowerShell Web Access и</span><span class="sxs-lookup"><span data-stu-id="ee068-114">the Windows PowerShell Web Access web application, and</span></span>
- <span data-ttu-id="ee068-115">компонента Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="ee068-115">the Windows PowerShell Web Access feature</span></span>
 
<span data-ttu-id="ee068-116">с помощью командлетов Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee068-116">by using Windows PowerShell cmdlets.</span></span>

### <a name="step-1-delete-the-web-application-using-cmdlets"></a><span data-ttu-id="ee068-117">Шаг 1. Удаление веб-приложения с помощью командлетов</span><span class="sxs-lookup"><span data-stu-id="ee068-117">Step 1: Delete the web application using cmdlets</span></span>

1. <span data-ttu-id="ee068-118">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee068-118">Do one of the following to open a Windows PowerShell session.</span></span>

    -   <span data-ttu-id="ee068-119">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.</span><span class="sxs-lookup"><span data-stu-id="ee068-119">On the Windows desktop, right-click **Windows PowerShell** on the taskbar.</span></span>

    -   <span data-ttu-id="ee068-120">На **начальном** экране Windows щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ee068-120">On the Windows **Start** screen, click **Windows PowerShell**.</span></span>

2. <span data-ttu-id="ee068-121">Введите `Uninstall-PswaWebApplication` и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ee068-121">Type `Uninstall-PswaWebApplication`, and then press **Enter**.</span></span>
   1. <span data-ttu-id="ee068-122">Если вы задали настраиваемое имя веб-сайта, добавьте параметр `-WebsiteName` в команду и укажите имя веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ee068-122">If you have specified your own, custom website name, add the `-WebsiteName` parameter to your command, and specify the website name.</span></span>

        `Uninstall-PswaWebApplication -WebsiteName <web-site-name>`
   1. <span data-ttu-id="ee068-123">Если использовалось настраиваемое веб-приложение (не приложение **pswa** по умолчанию), добавьте параметр `-WebApplicationName` в команду и укажите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ee068-123">If you have used a custom web application (not the default application, **pswa**, add the `-WebApplicationName` parameter to your command, and specify the name of the web application.</span></span>

        `Uninstall-PswaWebApplication -WebApplicationName <web-application-name>`
   1. <span data-ttu-id="ee068-124">Если используется тестовый сертификат, добавьте в командлет параметр `DeleteTestCertificate`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ee068-124">If you are using a test certificate, add the `DeleteTestCertificate` parameter to the cmdlet, as shown in the following example.</span></span>

        `Uninstall-PswaWebApplication -DeleteTestCertificate`

### <a name="step-2-uninstall-windows-powershell-web-access-using-cmdlets"></a><span data-ttu-id="ee068-125">Шаг 2. Удаление Windows PowerShell Web Access с помощью командлетов</span><span class="sxs-lookup"><span data-stu-id="ee068-125">Step 2: Uninstall Windows PowerShell Web Access using cmdlets</span></span>

1.  <span data-ttu-id="ee068-126">Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="ee068-126">Do one of the following to open a Windows PowerShell session with elevated user rights.</span></span> <span data-ttu-id="ee068-127">Если сеанс уже открыт, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="ee068-127">If a session is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="ee068-128">На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="ee068-128">On the Windows desktop, right-click **Windows PowerShell** on the taskbar, and then click **Run as Administrator**.</span></span>

    -   <span data-ttu-id="ee068-129">На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите команду **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="ee068-129">On the Windows **Start** screen, right-click **Windows PowerShell**, and then click **Run as Administrator**.</span></span>

1. <span data-ttu-id="ee068-130">Введите следующую команду и нажмите клавишу **ВВОД**, где *computer_name* представляет удаленный сервер, с которого требуется удалить Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="ee068-130">Type the following, and then press **Enter**, where *computer_name* represents a remote server from which you want to remove Windows PowerShell Web Access.</span></span> <span data-ttu-id="ee068-131">Параметр `-Restart` автоматически перезапускает целевые серверы, если это требуется при удалении.</span><span class="sxs-lookup"><span data-stu-id="ee068-131">The `-Restart` parameter automatically restarts destination servers if required by the removal.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    <span data-ttu-id="ee068-132">Чтобы удалить роли и компоненты с автономного виртуального жесткого диска (VHD), необходимо добавить оба параметра, `-ComputerName` и `-VHD`.</span><span class="sxs-lookup"><span data-stu-id="ee068-132">To remove roles and features from an offline VHD, you must add both the `-ComputerName` parameter and the `-VHD` parameter.</span></span> <span data-ttu-id="ee068-133">Параметр `-ComputerName` содержит имя сервера, на котором следует подключить виртуальный жесткий диск, а параметр `-VHD` — путь к VHD-файлу на указанном сервере.</span><span class="sxs-lookup"><span data-stu-id="ee068-133">The `-ComputerName` parameter contains the name of the server on which to mount the VHD, and the `-VHD` parameter contains the path to the VHD file on the specified server.</span></span>

        Uninstall-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -Restart

1. <span data-ttu-id="ee068-134">После завершения удаления Windows PowerShell Web Access откройте для проверки страницу **Все серверы** в диспетчере серверов, выберите сервер, с которого был удален компонент, и просмотрите плитку **Роли и компоненты** на странице для выбранного сервера.</span><span class="sxs-lookup"><span data-stu-id="ee068-134">When removal is finished, verify that you removed Windows PowerShell Web Access by opening the **All Servers** page in Server Manager, selecting a server from which you removed the feature, and viewing the **Roles and Features** tile on the page for the selected server.</span></span>

    <span data-ttu-id="ee068-135">Можно также выполнить командлет `Get-WindowsFeature`, нацеленный на выбранный сервер (Get-WindowsFeature-ComputerName &lt;*имя_компьютера*&gt;), чтобы просмотреть список ролей и компонентов, установленных на сервере.</span><span class="sxs-lookup"><span data-stu-id="ee068-135">You can also run the `Get-WindowsFeature` cmdlet targeted at the selected server (Get-WindowsFeature -ComputerName &lt;*computer_name*&gt;) to view a list of roles and features that are installed on the server.</span></span>

## <a name="custom-uninstallation"></a><span data-ttu-id="ee068-136">Настраиваемое удаление</span><span class="sxs-lookup"><span data-stu-id="ee068-136">Custom uninstallation</span></span>

<span data-ttu-id="ee068-137">В этом разделе приводятся процедуры для удаления веб-приложения Windows PowerShell Web Access и компонента Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов в диспетчере серверов и на консоли диспетчера служб IIS.</span><span class="sxs-lookup"><span data-stu-id="ee068-137">Procedures in this section help you uninstall both the Windows PowerShell Web Access web application and the Windows PowerShell Web Access feature by using the Remove Roles and Features Wizard in Server Manager, and the IIS Manager console.</span></span>

### <a name="step-1-delete-the-web-application-using-iis-manager"></a><span data-ttu-id="ee068-138">Шаг 1. Удаление веб-приложения с помощью диспетчера IIS</span><span class="sxs-lookup"><span data-stu-id="ee068-138">Step 1: Delete the web application using IIS Manager</span></span>


1. <span data-ttu-id="ee068-139">Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="ee068-139">Open the IIS Manager console by doing one of the following.</span></span> <span data-ttu-id="ee068-140">Если консоль уже открыта, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="ee068-140">If it is already open, go on to the next step.</span></span>

    -   <span data-ttu-id="ee068-141">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="ee068-141">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span> <span data-ttu-id="ee068-142">В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="ee068-142">On the **Tools** menu in Server Manager, click **Internet Information Services (IIS) Manager**.</span></span>

    -   <span data-ttu-id="ee068-143">На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**.</span><span class="sxs-lookup"><span data-stu-id="ee068-143">On the Windows **Start** screen, type any part of the name **Internet Information Services (IIS) Manager**.</span></span> <span data-ttu-id="ee068-144">Щелкните ярлык, когда он появится в списке результатов **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="ee068-144">Click the shortcut when it is displayed in the **Apps** results.</span></span>

1. <span data-ttu-id="ee068-145">В области дерева диспетчера служб IIS выберите веб-сайт, на котором выполняется веб-приложение Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="ee068-145">In the IIS Manager tree pane, select the website that is running the Windows PowerShell Web Access web application.</span></span>

1. <span data-ttu-id="ee068-146">В области **Действия** в разделе **Управление веб-сайтом** щелкните **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="ee068-146">In the **Actions** pane, under **Manage Website**, click **Stop**.</span></span>

1. <span data-ttu-id="ee068-147">В области дерева щелкните правой кнопкой мыши веб-приложение на веб-сайте, на котором выполняется веб-приложение Windows PowerShell Web Access, а затем выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="ee068-147">In the tree pane, right-click the web application in the website that is running the Windows PowerShell Web Access web application, and then click **Remove**.</span></span>

1. <span data-ttu-id="ee068-148">В области дерева выберите **Пулы приложений**, выберите папку пула приложений Windows PowerShell Web Access, щелкните **Остановить** в области **Действия**, а затем щелкните **Удалить** в области содержимого.</span><span class="sxs-lookup"><span data-stu-id="ee068-148">In the tree pane, select **Application Pools**, select the Windows PowerShell Web Access application pool folder, click **Stop** in the **Actions** pane, and then click **Remove** in the content pane.</span></span>

1. <span data-ttu-id="ee068-149">Закройте диспетчер IIS.</span><span class="sxs-lookup"><span data-stu-id="ee068-149">Close IIS Manager.</span></span>

> <span data-ttu-id="ee068-150">![Предупреждение](images/SecurityNote.jpeg)**Note**.</span><span class="sxs-lookup"><span data-stu-id="ee068-150">![Warning note](images/SecurityNote.jpeg)**Note**:</span></span>
>
> <span data-ttu-id="ee068-151">Сертификат не удаляется при этой операции удаления.</span><span class="sxs-lookup"><span data-stu-id="ee068-151">The certificate is not deleted during uninstallation.</span></span> 
>
> <span data-ttu-id="ee068-152">Если вы создали самозаверяющий сертификат или использовали тестовый сертификат и хотите удалить его, удалите сертификат в диспетчере служб IIS.</span><span class="sxs-lookup"><span data-stu-id="ee068-152">If you created a self-signed certificate or used a test certificate and want to remove it, delete the certificate in IIS Manager.</span></span> 

### <a name="step-2-uninstall-windows-powershell-web-access-using-the-remove-roles-and-features-wizard"></a><span data-ttu-id="ee068-153">Шаг 2. Удаление Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов</span><span class="sxs-lookup"><span data-stu-id="ee068-153">Step 2: Uninstall Windows PowerShell Web Access using the Remove Roles and Features Wizard</span></span>

1. <span data-ttu-id="ee068-154">Если диспетчер серверов уже открыт, переходите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="ee068-154">If Server Manager is already open, go on to the next step.</span></span> <span data-ttu-id="ee068-155">Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="ee068-155">If Server Manager is not already open, open it by doing one of the following.</span></span>

    -   <span data-ttu-id="ee068-156">На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.</span><span class="sxs-lookup"><span data-stu-id="ee068-156">On the Windows desktop, start Server Manager by clicking **Server Manager** in the Windows taskbar.</span></span>

    -   <span data-ttu-id="ee068-157">На **начальном** экране в Windows выберите **Диспетчер серверов**.</span><span class="sxs-lookup"><span data-stu-id="ee068-157">On the Windows **Start** screen, click **Server Manager**.</span></span>

1. <span data-ttu-id="ee068-158">В меню **Управление** выберите команду **Удалить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="ee068-158">On the **Manage** menu, click **Remove Roles and Features**.</span></span>

1. <span data-ttu-id="ee068-159">На странице **Выбор целевого сервера** выберите сервер или виртуальный жесткий диск, с которого следует удалить компонент.</span><span class="sxs-lookup"><span data-stu-id="ee068-159">On the **Select destination server** page, select the server or offline VHD from which you want to remove the feature.</span></span> <span data-ttu-id="ee068-160">Чтобы выбрать автономный виртуальный жесткий диск, сначала выберите сервер, на котором будет подключен виртуальный жесткий диск, а затем выберите VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="ee068-160">To select an offline VHD, first select the server on which to mount the VHD, and then select the VHD file.</span></span> <span data-ttu-id="ee068-161">Выбрав конечный сервер, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ee068-161">After you have selected the destination server, click **Next**.</span></span>

1. <span data-ttu-id="ee068-162">Еще раз щелкните **Далее**, чтобы пропустить страницу **Удаление компонентов**.</span><span class="sxs-lookup"><span data-stu-id="ee068-162">Click **Next** again to skip to the **Remove features** page.</span></span>

1. <span data-ttu-id="ee068-163">Снимите флажок **Windows PowerShell Web Access** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ee068-163">Clear the check box for **Windows PowerShell Web Access**, and then click **Next**.</span></span>

1. <span data-ttu-id="ee068-164">На странице **Подтверждение удаления компонентов** щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="ee068-164">On the **Confirm removal selections** page, click **Remove**.</span></span>

## <a name="see-also"></a><span data-ttu-id="ee068-165">См. также</span><span class="sxs-lookup"><span data-stu-id="ee068-165">See Also</span></span>

- [<span data-ttu-id="ee068-166">Установка и использование Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="ee068-166">Install and Use Windows PowerShell Web Access</span></span>](install-and-use-windows-powershell-web-access.md)
- [<span data-ttu-id="ee068-167">Справка по диспетчеру IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="ee068-167">IIS Manager 7.0 Help</span></span>](https://technet.microsoft.com/library/cc732664.aspx)
