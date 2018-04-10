---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Выполнение удаленных команд
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: eb9f0ce0102de13d4fcd1d51f0e9174e9d5c340c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="running-remote-commands"></a><span data-ttu-id="2fa13-103">Выполнение удаленных команд</span><span class="sxs-lookup"><span data-stu-id="2fa13-103">Running Remote Commands</span></span>

<span data-ttu-id="2fa13-104">Вы можете запускать команды на одном или сотнях компьютеров одной командой Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fa13-104">You can run commands on one or hundreds of computers with a single Windows PowerShell command.</span></span> <span data-ttu-id="2fa13-105">Windows PowerShell поддерживает удаленное вычисление с помощью разных технологий, включая WMI, RPC и WS-Management.</span><span class="sxs-lookup"><span data-stu-id="2fa13-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

## <a name="remoting-in-powershell-core"></a><span data-ttu-id="2fa13-106">Удаленное взаимодействие в PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="2fa13-106">Remoting in PowerShell Core</span></span>

<span data-ttu-id="2fa13-107">PowerShell Core, более новый выпуск PowerShell для Windows, macOS и Linux, поддерживает инструментарий WMI, WS-Management и удаленное взаимодействие SSH.</span><span class="sxs-lookup"><span data-stu-id="2fa13-107">PowerShell Core, the newer edition of PowerShell on Windows, macOS, and Linux, supports WMI, WS-Management, and SSH remoting.</span></span>
<span data-ttu-id="2fa13-108">(RPC больше не поддерживается.)</span><span class="sxs-lookup"><span data-stu-id="2fa13-108">(RPC is no longer supported.)</span></span>

<span data-ttu-id="2fa13-109">Дополнительные сведения о настройке см. в указанных ниже разделах:</span><span class="sxs-lookup"><span data-stu-id="2fa13-109">For more information on setting this up, see:</span></span>

* <span data-ttu-id="2fa13-110">[Удаленное взаимодействие через SSH в PowerShell Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="2fa13-110">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
* <span data-ttu-id="2fa13-111">[Удаленное взаимодействие через WSMan в PowerShell Core][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="2fa13-111">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="remoting-without-configuration"></a><span data-ttu-id="2fa13-112">Удаленное взаимодействие без настройки</span><span class="sxs-lookup"><span data-stu-id="2fa13-112">Remoting Without Configuration</span></span>

<span data-ttu-id="2fa13-113">Многие командлеты Windows PowerShell имеют параметр ComputerName, который позволяет собирать данные и изменять параметры одного или нескольких удаленных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="2fa13-113">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="2fa13-114">Они используют различные способы связи, многие из которых работают во всех операционных системах Windows, которые Windows PowerShell поддерживает без необходимости какой-либо настройки.</span><span class="sxs-lookup"><span data-stu-id="2fa13-114">They use a variety of communication technologies and many work on all Windows operating systems that Windows PowerShell supports without any special configuration.</span></span>

<span data-ttu-id="2fa13-115">В эти командлеты входят следующие:</span><span class="sxs-lookup"><span data-stu-id="2fa13-115">These cmdlets include:</span></span>

* [<span data-ttu-id="2fa13-116">Restart-Computer</span><span class="sxs-lookup"><span data-stu-id="2fa13-116">Restart-Computer</span></span>](https://go.microsoft.com/fwlink/?LinkId=821625)
* [<span data-ttu-id="2fa13-117">Test-Connection</span><span class="sxs-lookup"><span data-stu-id="2fa13-117">Test-Connection</span></span>](https://go.microsoft.com/fwlink/?LinkId=821646)
* [<span data-ttu-id="2fa13-118">Clear-EventLog</span><span class="sxs-lookup"><span data-stu-id="2fa13-118">Clear-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821568)
* [<span data-ttu-id="2fa13-119">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="2fa13-119">Get-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821585)
* [<span data-ttu-id="2fa13-120">Get-HotFix</span><span class="sxs-lookup"><span data-stu-id="2fa13-120">Get-HotFix</span></span>](https://go.microsoft.com/fwlink/?LinkId=821586)
* [<span data-ttu-id="2fa13-121">Get-Process</span><span class="sxs-lookup"><span data-stu-id="2fa13-121">Get-Process</span></span>](https://go.microsoft.com/fwlink/?linkid=821590)
* [<span data-ttu-id="2fa13-122">Get-Service</span><span class="sxs-lookup"><span data-stu-id="2fa13-122">Get-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821593)
* [<span data-ttu-id="2fa13-123">Set-Service</span><span class="sxs-lookup"><span data-stu-id="2fa13-123">Set-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821633)
* [<span data-ttu-id="2fa13-124">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="2fa13-124">Get-WinEvent</span></span>](https://go.microsoft.com/fwlink/?linkid=821529)
* [<span data-ttu-id="2fa13-125">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="2fa13-125">Get-WmiObject</span></span>](https://go.microsoft.com/fwlink/?LinkId=821595)

<span data-ttu-id="2fa13-126">Обычно командлеты, которые поддерживают удаленное взаимодействие без специальной настройки, имеют параметр ComputerName, но не имеют параметра Session.</span><span class="sxs-lookup"><span data-stu-id="2fa13-126">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and do not have the Session parameter.</span></span> <span data-ttu-id="2fa13-127">Чтобы найти эти командлеты в сеансе, введите:</span><span class="sxs-lookup"><span data-stu-id="2fa13-127">To find these cmdlets in your session, type:</span></span>

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="2fa13-128">Служба удаленного взаимодействия Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fa13-128">Windows PowerShell Remoting</span></span>

<span data-ttu-id="2fa13-129">Служба удаленного взаимодействия Windows PowerShell, использующая протокол WS-Management, позволяет запустить любую команду Windows PowerShell на одном или нескольких удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="2fa13-129">Windows PowerShell remoting, which uses the WS-Management protocol, lets you run any Windows PowerShell command on one or many remote computers.</span></span> <span data-ttu-id="2fa13-130">С ее помощью можно устанавливать постоянные подключения, запускать интерактивные сеансы 1:1 и сценарии на нескольких компьютерах.</span><span class="sxs-lookup"><span data-stu-id="2fa13-130">It lets you establish persistent connections, start 1:1 interactive sessions, and run scripts on multiple computers.</span></span>

<span data-ttu-id="2fa13-131">Чтобы использовать службу удаленного взаимодействия Windows PowerShell, удаленный компьютер должен быть настроен для удаленного управления.</span><span class="sxs-lookup"><span data-stu-id="2fa13-131">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span> <span data-ttu-id="2fa13-132">Дополнительные сведения, в том числе инструкции, см. в разделе [about_Remote_Requirements](https://technet.microsoft.com/library/dd315349.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa13-132">For more information, including instructions, see [About Remote Requirements](https://technet.microsoft.com/library/dd315349.aspx).</span></span>

<span data-ttu-id="2fa13-133">После настройки службы удаленного взаимодействия Windows PowerShell вам станут доступны многие стратегии удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="2fa13-133">After you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span> <span data-ttu-id="2fa13-134">В остальной части этого документа перечислены только некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="2fa13-134">The remainder of this document lists just a few of them.</span></span> <span data-ttu-id="2fa13-135">Дополнительные сведения см. в разделах [about_Remote](https://technet.microsoft.com/library/dd347744.aspx) и [about_Remote_FAQ](https://technet.microsoft.com/library/dd347744.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa13-135">For more information, see [About Remote](https://technet.microsoft.com/library/dd347744.aspx) and [About Remote FAQ](https://technet.microsoft.com/library/dd347744.aspx).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="2fa13-136">Запуск интерактивного сеанса</span><span class="sxs-lookup"><span data-stu-id="2fa13-136">Start an Interactive Session</span></span>

<span data-ttu-id="2fa13-137">Чтобы запустить интерактивный сеанс с одним удаленным компьютером, используйте командлет [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477).</span><span class="sxs-lookup"><span data-stu-id="2fa13-137">To start an interactive session with a single remote computer, use the [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) cmdlet.</span></span>
<span data-ttu-id="2fa13-138">Например, чтобы запустить интерактивный сеанс с удаленным компьютером Server01, введите:</span><span class="sxs-lookup"><span data-stu-id="2fa13-138">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```powershell
Enter-PSSession Server01
```

<span data-ttu-id="2fa13-139">В командной строке отобразится имя компьютера, к которому вы подключены.</span><span class="sxs-lookup"><span data-stu-id="2fa13-139">The command prompt changes to display the name of the computer to which you are connected.</span></span> <span data-ttu-id="2fa13-140">В дальнейшем все команды, введенные в командной строке, будут запускаться на удаленном компьютере, а результаты отобразятся на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2fa13-140">From then on, any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="2fa13-141">Чтобы завершить интерактивный сеанс, введите:</span><span class="sxs-lookup"><span data-stu-id="2fa13-141">To end the interactive session, type:</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="2fa13-142">Дополнительные сведения о командлетах Enter-PSSession и Exit-PSSession см. в статьях [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) и [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span><span class="sxs-lookup"><span data-stu-id="2fa13-142">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) and [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span></span>

### <a name="run-a-remote-command"></a><span data-ttu-id="2fa13-143">Выполнение удаленной команды</span><span class="sxs-lookup"><span data-stu-id="2fa13-143">Run a Remote Command</span></span>

<span data-ttu-id="2fa13-144">Чтобы выполнить любую команду на одном или нескольких удаленных компьютеров, используйте командлет [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="2fa13-144">To run any command on one or many remote computers, use the [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) cmdlet.</span></span>
<span data-ttu-id="2fa13-145">Например, чтобы выполнить команду [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) на удаленных компьютерах Server01 и Server02, введите:</span><span class="sxs-lookup"><span data-stu-id="2fa13-145">For example, to run a [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) command on the Server01 and Server02 remote computers, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="2fa13-146">Выходные данные будут возвращены на ваш компьютер.</span><span class="sxs-lookup"><span data-stu-id="2fa13-146">The output is returned to your computer.</span></span>

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

<span data-ttu-id="2fa13-147">Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="2fa13-147">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="run-a-script"></a><span data-ttu-id="2fa13-148">Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="2fa13-148">Run a Script</span></span>

<span data-ttu-id="2fa13-149">Чтобы запустить сценарий на одном или нескольких удаленных компьютерах, используйте параметр FilePath командлета Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="2fa13-149">To run a script on one or many remote computers, use the FilePath parameter of the Invoke-Command cmdlet.</span></span> <span data-ttu-id="2fa13-150">Сценарий должен быть включен или доступен для локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="2fa13-150">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="2fa13-151">Результаты будут возвращены на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="2fa13-151">The results are returned to your local computer.</span></span>

<span data-ttu-id="2fa13-152">Например, следующая команда выполняет сценарий DiskCollect.ps1 на удаленных компьютерах Server01 и Server02.</span><span class="sxs-lookup"><span data-stu-id="2fa13-152">For example, the following command runs the DiskCollect.ps1 script on the Server01 and Server02 remote computers.</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

<span data-ttu-id="2fa13-153">Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="2fa13-153">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="2fa13-154">Установка постоянного подключения</span><span class="sxs-lookup"><span data-stu-id="2fa13-154">Establish a Persistent Connection</span></span>

<span data-ttu-id="2fa13-155">Чтобы выполнить ряд связанных команд с общими данными, создайте сеанс на удаленном компьютере, а затем используйте командлет Invoke-Command для выполнения команд в созданном сеансе.</span><span class="sxs-lookup"><span data-stu-id="2fa13-155">To run a series of related commands that share data, create a session on the remote computer and then use the Invoke-Command cmdlet to run commands in the session that you create.</span></span> <span data-ttu-id="2fa13-156">Чтобы создать удаленный сеанс, используйте командлет New-PSSession.</span><span class="sxs-lookup"><span data-stu-id="2fa13-156">To create a remote session, use the New-PSSession cmdlet.</span></span>

<span data-ttu-id="2fa13-157">Например, следующая команда создает удаленный сеанс на компьютере Server01 и другой удаленный сеанс на компьютере Server02.</span><span class="sxs-lookup"><span data-stu-id="2fa13-157">For example, the following command creates a remote session on the Server01 computer and another remote session on the Server02 computer.</span></span> <span data-ttu-id="2fa13-158">Она сохраняет объекты сеанса в переменной $s.</span><span class="sxs-lookup"><span data-stu-id="2fa13-158">It saves the session objects in the $s variable.</span></span>

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="2fa13-159">После установки сеансов в них можно выполнить любую команду.</span><span class="sxs-lookup"><span data-stu-id="2fa13-159">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="2fa13-160">Так как сеансы являются постоянными, вы можете собирать данные в одной команде и использовать их в последующей.</span><span class="sxs-lookup"><span data-stu-id="2fa13-160">And because the sessions are persistent, you can collect data in one command and use it in a subsequent command.</span></span>

<span data-ttu-id="2fa13-161">Например, следующая команда выполняет команду Get-Hotfix в сеансах в переменной $s и сохраняет результаты в переменной $h.</span><span class="sxs-lookup"><span data-stu-id="2fa13-161">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="2fa13-162">Переменная $h создается в каждом сеансе в $s, но она не существует в локальном сеансе.</span><span class="sxs-lookup"><span data-stu-id="2fa13-162">The $h variable is created in each of the sessions in $s, but it does not exist in the local session.</span></span>

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="2fa13-163">Теперь данные в переменной $h можно использовать в последующих командах, таких как следующая.</span><span class="sxs-lookup"><span data-stu-id="2fa13-163">Now you can use the data in the $h variable in subsequent commands, such as the following one.</span></span> <span data-ttu-id="2fa13-164">Результаты отобразятся на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2fa13-164">The results are displayed on the local computer.</span></span>

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="2fa13-165">Расширенная служба удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="2fa13-165">Advanced Remoting</span></span>

<span data-ttu-id="2fa13-166">Это и есть служба удаленного взаимодействия Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fa13-166">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="2fa13-167">Используя командлеты, установленные с Windows PowerShell, можно установить и настроить удаленные сеансы с локальных и удаленных компьютеров, создать настраиваемые и ограниченные сеансы, разрешить пользователям импортировать команды из удаленного сеанса, которые могут неявно выполняться в удаленном сеансе, настроить безопасность удаленного сеанса и многое другое.</span><span class="sxs-lookup"><span data-stu-id="2fa13-167">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="2fa13-168">Для упрощения настройки в PowerShell включен поставщик WSMan.</span><span class="sxs-lookup"><span data-stu-id="2fa13-168">To facilitate remote configuration, Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="2fa13-169">Диск WSMAN:, созданный поставщиком, позволяет перемещаться по иерархии параметров конфигурации на локальном и удаленном компьютерах.</span><span class="sxs-lookup"><span data-stu-id="2fa13-169">The WSMAN: drive that the provider creates lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>
<span data-ttu-id="2fa13-170">Дополнительные сведения о поставщике WSMan см. в разделах [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) и [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx) или введите команду Get-Help wsman в консоли Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fa13-170">For more information about the WSMan provider, see  [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) and [About WS-Management Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx), or in the Windows PowerShell console, type "Get-Help wsman".</span></span>

<span data-ttu-id="2fa13-171">Дополнительная информация:</span><span class="sxs-lookup"><span data-stu-id="2fa13-171">For more information, see:</span></span>

- [<span data-ttu-id="2fa13-172">Часто задаваемые вопросы об удаленном взаимодействии</span><span class="sxs-lookup"><span data-stu-id="2fa13-172">About Remote FAQ</span></span>](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [<span data-ttu-id="2fa13-173">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="2fa13-173">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="2fa13-174">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="2fa13-174">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="2fa13-175">Справку по ошибкам службы удаленного взаимодействия см. в статье [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fa13-175">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="2fa13-176">См. также</span><span class="sxs-lookup"><span data-stu-id="2fa13-176">See Also</span></span>

- [<span data-ttu-id="2fa13-177">about_Remote</span><span class="sxs-lookup"><span data-stu-id="2fa13-177">about_Remote</span></span>](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="2fa13-178">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="2fa13-178">about_Remote_FAQ</span></span>](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="2fa13-179">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="2fa13-179">about_Remote_Requirements</span></span>](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="2fa13-180">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="2fa13-180">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="2fa13-181">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="2fa13-181">about_PSSessions</span></span>](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="2fa13-182">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="2fa13-182">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="2fa13-183">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="2fa13-183">Invoke-Command</span></span>](https://go.microsoft.com/fwlink/?LinkId=821493)
- [<span data-ttu-id="2fa13-184">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="2fa13-184">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="2fa13-185">New-PSSession</span><span class="sxs-lookup"><span data-stu-id="2fa13-185">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="2fa13-186">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="2fa13-186">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="2fa13-187">Поставщик WSMan</span><span class="sxs-lookup"><span data-stu-id="2fa13-187">WSMan Provider</span></span>](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md