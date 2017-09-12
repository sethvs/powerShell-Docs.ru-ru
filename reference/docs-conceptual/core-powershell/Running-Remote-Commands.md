---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Выполнение удаленных команд"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: c3bf002e7a3daa5afc8219dd846145808eef3c9b
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="running-remote-commands"></a><span data-ttu-id="f1338-103">Выполнение удаленных команд</span><span class="sxs-lookup"><span data-stu-id="f1338-103">Running Remote Commands</span></span>
<span data-ttu-id="f1338-104">Вы можете запускать команды на одном или сотнях компьютеров одной командой Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1338-104">You can run commands on one or hundreds of computers with a single Windows PowerShell command.</span></span> <span data-ttu-id="f1338-105">Windows PowerShell поддерживает удаленное вычисление с помощью разных технологий, включая WMI, RPC и WS-Management.</span><span class="sxs-lookup"><span data-stu-id="f1338-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

## <a name="remoting-without-configuration"></a><span data-ttu-id="f1338-106">Удаленное взаимодействие без настройки</span><span class="sxs-lookup"><span data-stu-id="f1338-106">Remoting Without Configuration</span></span>
<span data-ttu-id="f1338-107">Многие командлеты Windows PowerShell имеют параметр ComputerName, который позволяет собирать данные и изменять параметры одного или нескольких удаленных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="f1338-107">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="f1338-108">Они используют различные способы связи, многие из которых работают во всех операционных системах Windows, которые Windows PowerShell поддерживает без необходимости какой-либо настройки.</span><span class="sxs-lookup"><span data-stu-id="f1338-108">They use a variety of communication technologies and many work on all Windows operating systems that Windows PowerShell supports without any special configuration.</span></span>

<span data-ttu-id="f1338-109">В эти командлеты входят следующие:</span><span class="sxs-lookup"><span data-stu-id="f1338-109">These cmdlets include:</span></span>

- [<span data-ttu-id="f1338-110">Restart-Computer</span><span class="sxs-lookup"><span data-stu-id="f1338-110">Restart-Computer</span></span>](https://technet.microsoft.com/en-us/library/dd315301.aspx)

- [<span data-ttu-id="f1338-111">Test-Connection</span><span class="sxs-lookup"><span data-stu-id="f1338-111">Test-Connection</span></span>](https://technet.microsoft.com/en-us/library/dd315259.aspx)

- [<span data-ttu-id="f1338-112">Clear-EventLog</span><span class="sxs-lookup"><span data-stu-id="f1338-112">Clear-EventLog</span></span>](https://technet.microsoft.com/en-us/library/dd347552.aspx)

- [<span data-ttu-id="f1338-113">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="f1338-113">Get-EventLog</span></span>](https://technet.microsoft.com/en-us/library/dd315250.aspx)

- [<span data-ttu-id="f1338-114">Get-HotFix</span><span class="sxs-lookup"><span data-stu-id="f1338-114">Get-HotFix</span></span>](https://technet.microsoft.com/en-us/library/e1ef636f-5170-4675-b564-199d9ef6f101)

 -   [<span data-ttu-id="f1338-115">Get-Process</span><span class="sxs-lookup"><span data-stu-id="f1338-115">Get-Process</span></span>](https://technet.microsoft.com/en-us/library/dd347630.aspx)

- [<span data-ttu-id="f1338-116">Get-Service</span><span class="sxs-lookup"><span data-stu-id="f1338-116">Get-Service</span></span>](https://technet.microsoft.com/en-us/library/dd347591.aspx)

- [<span data-ttu-id="f1338-117">Set-Service</span><span class="sxs-lookup"><span data-stu-id="f1338-117">Set-Service</span></span>](https://technet.microsoft.com/en-us/library/dd315324.aspx)

- [<span data-ttu-id="f1338-118">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="f1338-118">Get-WinEvent</span></span>](https://technet.microsoft.com/en-us/library/dd315358.aspx)

- [<span data-ttu-id="f1338-119">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="f1338-119">Get-WmiObject</span></span>](https://technet.microsoft.com/en-us/library/dd315295.aspx)

<span data-ttu-id="f1338-120">Обычно командлеты, которые поддерживают удаленное взаимодействие без специальной настройки, имеют параметр ComputerName, но не имеют параметра Session.</span><span class="sxs-lookup"><span data-stu-id="f1338-120">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and do not have the Session parameter.</span></span> <span data-ttu-id="f1338-121">Чтобы найти эти командлеты в сеансе, введите:</span><span class="sxs-lookup"><span data-stu-id="f1338-121">To find these cmdlets in your session, type:</span></span>

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="f1338-122">Служба удаленного взаимодействия Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1338-122">Windows PowerShell Remoting</span></span>
<span data-ttu-id="f1338-123">Служба удаленного взаимодействия Windows PowerShell, использующая протокол WS-Management, позволяет запустить любую команду Windows PowerShell на одном или нескольких удаленных компьютерах.</span><span class="sxs-lookup"><span data-stu-id="f1338-123">Windows PowerShell remoting, which uses the WS-Management protocol, lets you run any Windows PowerShell command on one or many remote computers.</span></span> <span data-ttu-id="f1338-124">С ее помощью можно устанавливать постоянные подключения, запускать интерактивные сеансы 1:1 и сценарии на нескольких компьютерах.</span><span class="sxs-lookup"><span data-stu-id="f1338-124">It lets you establish persistent connections, start 1:1 interactive sessions, and run scripts on multiple computers.</span></span>

<span data-ttu-id="f1338-125">Чтобы использовать службу удаленного взаимодействия Windows PowerShell, удаленный компьютер должен быть настроен для удаленного управления.</span><span class="sxs-lookup"><span data-stu-id="f1338-125">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span> <span data-ttu-id="f1338-126">Дополнительные сведения, в том числе инструкции, см. в разделе [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-126">For more information, including instructions, see [About Remote Requirements](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span></span>

<span data-ttu-id="f1338-127">После настройки службы удаленного взаимодействия Windows PowerShell вам станут доступны многие стратегии удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="f1338-127">After you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span> <span data-ttu-id="f1338-128">В остальной части этого документа перечислены только некоторые из них.</span><span class="sxs-lookup"><span data-stu-id="f1338-128">The remainder of this document lists just a few of them.</span></span> <span data-ttu-id="f1338-129">Дополнительные сведения см. в разделах [about_Remote](https://technet.microsoft.com/en-us/library/dd347744.aspx) и [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-129">For more information, see [About Remote](https://technet.microsoft.com/en-us/library/dd347744.aspx) and [About Remote FAQ](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="f1338-130">Запуск интерактивного сеанса</span><span class="sxs-lookup"><span data-stu-id="f1338-130">Start an Interactive Session</span></span>
<span data-ttu-id="f1338-131">Чтобы запустить интерактивный сеанс с одним удаленным компьютером, используйте командлет [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-131">To start an interactive session with a single remote computer, use the [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx) cmdlet.</span></span> <span data-ttu-id="f1338-132">Например, чтобы запустить интерактивный сеанс с удаленным компьютером Server01, введите:</span><span class="sxs-lookup"><span data-stu-id="f1338-132">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```
Enter-PSSession Server01
```

<span data-ttu-id="f1338-133">В командной строке отобразится имя компьютера, к которому вы подключены.</span><span class="sxs-lookup"><span data-stu-id="f1338-133">The command prompt changes to display the name of the computer to which you are connected.</span></span> <span data-ttu-id="f1338-134">В дальнейшем все команды, введенные в командной строке, будут запускаться на удаленном компьютере, а результаты отобразятся на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1338-134">From then on, any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="f1338-135">Чтобы завершить интерактивный сеанс, введите:</span><span class="sxs-lookup"><span data-stu-id="f1338-135">To end the interactive session, type:</span></span>

```
Exit-PSSession
```

<span data-ttu-id="f1338-136">Дополнительные сведения о командлетах Enter-PSSession и Exit-PSSession см. в статьях [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx) и [Exit-PSSession](https://technet.microsoft.com/en-us/library/dd315322.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-136">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see [Enter-PSSession](https://technet.microsoft.com/en-us/library/dd315384.aspx) and [Exit-PSSession](https://technet.microsoft.com/en-us/library/dd315322.aspx).</span></span>

### <a name="run-a-remote-command"></a><span data-ttu-id="f1338-137">Выполнение удаленной команды</span><span class="sxs-lookup"><span data-stu-id="f1338-137">Run a Remote Command</span></span>
<span data-ttu-id="f1338-138">Чтобы выполнить любую команду на одном или нескольких удаленных компьютеров, используйте командлет [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-138">To run any command on one or many remote computers, use the [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx) cmdlet.</span></span>
<span data-ttu-id="f1338-139">Например, чтобы выполнить команду [Get-UICulture](https://technet.microsoft.com/en-us/library/dd347742.aspx) на удаленных компьютерах Server01 и Server02, введите:</span><span class="sxs-lookup"><span data-stu-id="f1338-139">For example, to run a [Get-UICulture](https://technet.microsoft.com/en-us/library/dd347742.aspx) command on the Server01 and Server02 remote computers, type:</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="f1338-140">Выходные данные будут возвращены на ваш компьютер.</span><span class="sxs-lookup"><span data-stu-id="f1338-140">The output is returned to your computer.</span></span>

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
<span data-ttu-id="f1338-141">Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462).</span><span class="sxs-lookup"><span data-stu-id="f1338-141">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462).</span></span>

### <a name="run-a-script"></a><span data-ttu-id="f1338-142">Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="f1338-142">Run a Script</span></span>
<span data-ttu-id="f1338-143">Чтобы запустить сценарий на одном или нескольких удаленных компьютерах, используйте параметр FilePath командлета Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="f1338-143">To run a script on one or many remote computers, use the FilePath parameter of the Invoke-Command cmdlet.</span></span> <span data-ttu-id="f1338-144">Сценарий должен быть включен или доступен для локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="f1338-144">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="f1338-145">Результаты будут возвращены на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="f1338-145">The results are returned to your local computer.</span></span>

<span data-ttu-id="f1338-146">Например, следующая команда выполняет сценарий DiskCollect.ps1 на удаленных компьютерах Server01 и Server02.</span><span class="sxs-lookup"><span data-stu-id="f1338-146">For example, the following command runs the DiskCollect.ps1 script on the Server01 and Server02 remote computers.</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

<span data-ttu-id="f1338-147">Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-147">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://technet.microsoft.com/en-us/library/dd347578.aspx).</span></span>

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="f1338-148">Установка постоянного подключения</span><span class="sxs-lookup"><span data-stu-id="f1338-148">Establish a Persistent Connection</span></span>
<span data-ttu-id="f1338-149">Чтобы выполнить ряд связанных команд с общими данными, создайте сеанс на удаленном компьютере, а затем используйте командлет Invoke-Command для выполнения команд в созданном сеансе.</span><span class="sxs-lookup"><span data-stu-id="f1338-149">To run a series of related commands that share data, create a session on the remote computer and then use the Invoke-Command cmdlet to run commands in the session that you create.</span></span> <span data-ttu-id="f1338-150">Чтобы создать удаленный сеанс, используйте командлет New-PSSession.</span><span class="sxs-lookup"><span data-stu-id="f1338-150">To create a remote session, use the New-PSSession cmdlet.</span></span>

<span data-ttu-id="f1338-151">Например, следующая команда создает удаленный сеанс на компьютере Server01 и другой удаленный сеанс на компьютере Server02.</span><span class="sxs-lookup"><span data-stu-id="f1338-151">For example, the following command creates a remote session on the Server01 computer and another remote session on the Server02 computer.</span></span> <span data-ttu-id="f1338-152">Она сохраняет объекты сеанса в переменной $s.</span><span class="sxs-lookup"><span data-stu-id="f1338-152">It saves the session objects in the $s variable.</span></span>

```
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="f1338-153">После установки сеансов в них можно выполнить любую команду.</span><span class="sxs-lookup"><span data-stu-id="f1338-153">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="f1338-154">Так как сеансы являются постоянными, вы можете собирать данные в одной команде и использовать их в последующей.</span><span class="sxs-lookup"><span data-stu-id="f1338-154">And because the sessions are persistent, you can collect data in one command and use it in a subsequent command.</span></span>

<span data-ttu-id="f1338-155">Например, следующая команда выполняет команду Get-Hotfix в сеансах в переменной $s и сохраняет результаты в переменной $h.</span><span class="sxs-lookup"><span data-stu-id="f1338-155">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="f1338-156">Переменная $h создается в каждом сеансе в $s, но она не существует в локальном сеансе.</span><span class="sxs-lookup"><span data-stu-id="f1338-156">The $h variable is created in each of the sessions in $s, but it does not exist in the local session.</span></span>

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="f1338-157">Теперь данные в переменной $h можно использовать в последующих командах, таких как следующая.</span><span class="sxs-lookup"><span data-stu-id="f1338-157">Now you can use the data in the $h variable in subsequent commands, such as the following one.</span></span> <span data-ttu-id="f1338-158">Результаты отобразятся на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1338-158">The results are displayed on the local computer.</span></span>

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="f1338-159">Расширенная служба удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="f1338-159">Advanced Remoting</span></span>
<span data-ttu-id="f1338-160">Это и есть служба удаленного взаимодействия Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1338-160">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="f1338-161">Используя командлеты, установленные с Windows PowerShell, можно установить и настроить удаленные сеансы с локальных и удаленных компьютеров, создать настраиваемые и ограниченные сеансы, разрешить пользователям импортировать команды из удаленного сеанса, которые могут неявно выполняться в удаленном сеансе, настроить безопасность удаленного сеанса и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f1338-161">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="f1338-162">Для упрощения настройки в PowerShell включен поставщик WSMan.</span><span class="sxs-lookup"><span data-stu-id="f1338-162">To facilitate remote configuration, Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="f1338-163">Диск WSMAN:, созданный поставщиком, позволяет перемещаться по иерархии параметров конфигурации на локальном и удаленном компьютерах.</span><span class="sxs-lookup"><span data-stu-id="f1338-163">The WSMAN: drive that the provider creates lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>
<span data-ttu-id="f1338-164">Дополнительные сведения о поставщике WSMan см. в разделах [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) и [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx) или введите команду Get-Help wsman в консоли Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1338-164">For more information about the WSMan provider, see  [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) and [About WS-Management Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx), or in the Windows PowerShell console, type "Get-Help wsman".</span></span>

<span data-ttu-id="f1338-165">Дополнительная информация:</span><span class="sxs-lookup"><span data-stu-id="f1338-165">For more information, see:</span></span>
- [<span data-ttu-id="f1338-166">Часто задаваемые вопросы об удаленном взаимодействии</span><span class="sxs-lookup"><span data-stu-id="f1338-166">About Remote FAQ</span></span>](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [<span data-ttu-id="f1338-167">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1338-167">Register-PSSessionConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dd819496.aspx)
- <span data-ttu-id="f1338-168">[Import-PSSession](https://technet.microsoft.com/en-us/library/dd347575.aspx)</span><span class="sxs-lookup"><span data-stu-id="f1338-168">[Import-PSSession](https://technet.microsoft.com/en-us/library/dd347575.aspx).</span></span> 

<span data-ttu-id="f1338-169">Справку по ошибкам службы удаленного взаимодействия см. в статье [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1338-169">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="f1338-170">См. также</span><span class="sxs-lookup"><span data-stu-id="f1338-170">See Also</span></span>
- [<span data-ttu-id="f1338-171">about_Remote</span><span class="sxs-lookup"><span data-stu-id="f1338-171">about_Remote</span></span>](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="f1338-172">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="f1338-172">about_Remote_FAQ</span></span>](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="f1338-173">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="f1338-173">about_Remote_Requirements</span></span>](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="f1338-174">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f1338-174">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="f1338-175">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="f1338-175">about_PSSessions</span></span>](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="f1338-176">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="f1338-176">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="f1338-177">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="f1338-177">Invoke-Command</span></span>](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)
- [<span data-ttu-id="f1338-178">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="f1338-178">Import-PSSession</span></span>](https://technet.microsoft.com/en-us/library/048c115e-a6fb-4e0d-8cea-c5ca24630c9d)
- [<span data-ttu-id="f1338-179">New-PSSession</span><span class="sxs-lookup"><span data-stu-id="f1338-179">New-PSSession</span></span>](https://technet.microsoft.com/en-us/library/59452f12-a11d-4558-99ea-e6ca6ad5ffd3)
- [<span data-ttu-id="f1338-180">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1338-180">Register-PSSessionConfiguration</span></span>](https://technet.microsoft.com/en-us/library/af68867a-d201-4b19-a1de-594015ed8a25)
- [<span data-ttu-id="f1338-181">Поставщик WSMan</span><span class="sxs-lookup"><span data-stu-id="f1338-181">WSMan Provider</span></span>](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

