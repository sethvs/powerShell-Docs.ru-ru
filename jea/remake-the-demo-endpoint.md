---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "повторное создание демонстрационной конечной точки"
ms.technology: powershell
ms.openlocfilehash: 4a56272b6f995500d443d441f5e03db85dac6f96
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="remake-the-demo-endpoint"></a><span data-ttu-id="276c5-103">Повторное создание демонстрационной конечной точки</span><span class="sxs-lookup"><span data-stu-id="276c5-103">Remake the Demo Endpoint</span></span>
<span data-ttu-id="276c5-104">В этом разделе вы узнаете, как создать точную копию демонстрационной конечной точки, которая использовалась в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="276c5-104">In this section, you will learn how to generate an exact replica of the demo endpoint you used in the above section.</span></span>
<span data-ttu-id="276c5-105">Здесь представлены основные понятия, необходимые для понимания JEA, включая конфигурации сеансов и возможности ролей PowerShell.</span><span class="sxs-lookup"><span data-stu-id="276c5-105">This will introduce core concepts that are necessary to understand JEA, including PowerShell Session Configurations and Role Capabilities.</span></span>

## <a name="powershell-session-configurations"></a><span data-ttu-id="276c5-106">Конфигурации сеансов PowerShell</span><span class="sxs-lookup"><span data-stu-id="276c5-106">PowerShell Session Configurations</span></span>
<span data-ttu-id="276c5-107">При работе JEA в предыдущем разделе вы начали со следующей команды:</span><span class="sxs-lookup"><span data-stu-id="276c5-107">When you used JEA in the above section, you started by running the following command:</span></span>

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEA_Demo -Credential $NonAdminCred
```

<span data-ttu-id="276c5-108">Хотя большинство параметров говорят сами за себя, параметр *ConfigurationName* сначала может показаться противоречивым.</span><span class="sxs-lookup"><span data-stu-id="276c5-108">While most of the parameters are self-explanatory, the *ConfigurationName* parameter may seem confusing at first.</span></span>
<span data-ttu-id="276c5-109">Этот параметр задается в конфигурации сеанса PowerShell, к которому вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="276c5-109">That parameter specified the PowerShell Session Configuration to which you were connecting.</span></span>

<span data-ttu-id="276c5-110">*Конфигурация сеанса PowerShell* — еще один термин для обозначения конечной точки PowerShell.</span><span class="sxs-lookup"><span data-stu-id="276c5-110">*PowerShell Session Configuration* is a fancy term for a PowerShell endpoint.</span></span>
<span data-ttu-id="276c5-111">Это то "место", где пользователи могут подключаться и получать доступ к функциональным возможностям PowerShell.</span><span class="sxs-lookup"><span data-stu-id="276c5-111">It is the figurative "place" where users connect and get access to PowerShell functionality.</span></span>
<span data-ttu-id="276c5-112">В зависимости от настройки конфигурация сеанса может предоставлять подключающимся пользователям различные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="276c5-112">Based on how you set up a Session Configuration, it can provide different functionality to connecting users.</span></span>
<span data-ttu-id="276c5-113">В JEA конфигурации сеансов используются для того, чтобы ограничить PowerShell определенным набором функциональных возможностей и вести работу от имени привилегированной виртуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="276c5-113">For JEA, we use Session Configurations to restrict PowerShell to a limited set of functionality and to run as a privileged virtual account.</span></span>

<span data-ttu-id="276c5-114">На вашем компьютере уже есть несколько зарегистрированных конфигураций сеансов PowerShell, каждая из которых настроена несколько иначе, чем остальные.</span><span class="sxs-lookup"><span data-stu-id="276c5-114">You already have several registered PowerShell Session Configurations on your machine, each set up slightly differently.</span></span>
<span data-ttu-id="276c5-115">Большинство из них входят в состав Windows, но конфигурация сеанса "JEA_Demo" была настроена в разделе [предварительных требований](prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="276c5-115">Most of them come with Windows, but the "JEA_Demo" Session Configuration was set up in the [prerequisites](prerequisites.md) section.</span></span>
<span data-ttu-id="276c5-116">Чтобы увидеть все зарегистрированные конфигурации сеансов, выполните в командной строке администратора PowerShell следующую команду:</span><span class="sxs-lookup"><span data-stu-id="276c5-116">You can see all registered Session Configurations by running the following command in an Administrator PowerShell prompt:</span></span>

```PowerShell
Get-PSSessionConfiguration
```

## <a name="powershell-session-configuration-files"></a><span data-ttu-id="276c5-117">Файлы конфигурации сеансов PowerShell</span><span class="sxs-lookup"><span data-stu-id="276c5-117">PowerShell Session Configuration Files</span></span>
<span data-ttu-id="276c5-118">Новые конфигурации сеансов PowerShell создаются путем регистрации новых *файлов конфигурации сеансов PowerShell*.</span><span class="sxs-lookup"><span data-stu-id="276c5-118">You can make new Session Configurations by registering new *PowerShell Session Configuration Files*.</span></span>
<span data-ttu-id="276c5-119">Файлы конфигурации сеансов имеют расширение PSSC.</span><span class="sxs-lookup"><span data-stu-id="276c5-119">Session Configuration Files have ".pssc" file extensions.</span></span>
<span data-ttu-id="276c5-120">Файл конфигурации сеанса можно создать с помощью командлета New-PSSessionConfigurationFile.</span><span class="sxs-lookup"><span data-stu-id="276c5-120">You can generate Session Configuration Files with the New-PSSessionConfigurationFile cmdlet.</span></span>

<span data-ttu-id="276c5-121">Теперь создадим и зарегистрируем новую конфигурацию сеанса для JEA.</span><span class="sxs-lookup"><span data-stu-id="276c5-121">Next, you are going to create and register a new Session Configuration for JEA.</span></span>

## <a name="generate-and-modify-your-powershell-session-configuration"></a><span data-ttu-id="276c5-122">Создание и изменение конфигурации сеанса PowerShell</span><span class="sxs-lookup"><span data-stu-id="276c5-122">Generate and Modify your PowerShell Session Configuration</span></span>
<span data-ttu-id="276c5-123">Для создания "каркасного" файла конфигурации сеанса PowerShell выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="276c5-123">Run the following command to generate a PowerShell Session Configuration "skeleton" file.</span></span>

```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

> <span data-ttu-id="276c5-124">**Совет.** По умолчанию каркасный файл включает только основные настройки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="276c5-124">**TIP:** Only the most common configuration settings are included in the skeleton file by default.</span></span>
> <span data-ttu-id="276c5-125">Чтобы включить в создаваемый PSSC-файл все применимые настройки, используйте параметр `-Full`.</span><span class="sxs-lookup"><span data-stu-id="276c5-125">Use the `-Full` parameter to include all applicable settings in the generated PSSC.</span></span>

<span data-ttu-id="276c5-126">Откройте файл в интегрированной среде сценариев PowerShell или в любом удобном текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="276c5-126">Open the file in PowerShell ISE, or your favorite text editor.</span></span>

```PowerShell
ise "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

<span data-ttu-id="276c5-127">Измените в нем следующие поля, указав приведенные ниже значения (не забудьте указать собственную группу безопасности без прав администратора).</span><span class="sxs-lookup"><span data-stu-id="276c5-127">Update the following fields in the file with the values below (remember to substitute in your own non-administrator security group):</span></span>

```PowerShell
# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: # RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{'CONTOSO\JEA_NonAdmin_Operator' = @{ RoleCapabilities =  'Maintenance' }}
```

<span data-ttu-id="276c5-128">Вот что означает каждая из этих записей:</span><span class="sxs-lookup"><span data-stu-id="276c5-128">Here is what each of those entries mean:</span></span>

1.  <span data-ttu-id="276c5-129">Поле *SessionType* определяет предустановленные параметры по умолчанию для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="276c5-129">The *SessionType* field defines preset default settings to use with this endpoint.</span></span>
<span data-ttu-id="276c5-130">*RestrictedRemoteServer* определяет минимальный набор параметров, необходимых для удаленного управления.</span><span class="sxs-lookup"><span data-stu-id="276c5-130">*RestrictedRemoteServer* defines the minimal settings necessary for remote management.</span></span>
<span data-ttu-id="276c5-131">По умолчанию конечная точка *RestrictedRemoteServer* имеет параметры Get-Command, Get-FormatData, Select-Object, Get-Help, Measure-Object, Exit-PSSession, Clear-Host и Out-Default.</span><span class="sxs-lookup"><span data-stu-id="276c5-131">By default, a *RestrictedRemoteServer* endpoint will expose Get-Command, Get-FormatData, Select-Object, Get-Help, Measure-Object, Exit-PSSession, Clear-Host, and Out-Default.</span></span>
<span data-ttu-id="276c5-132">Она устанавливает для параметра *ExecutionPolicy* значение *RemoteSigned*, а для параметра *LanguageMode* значение *NoLanguage*.</span><span class="sxs-lookup"><span data-stu-id="276c5-132">It will set the *ExecutionPolicy* to *RemoteSigned*, and the *LanguageMode* to *NoLanguage*.</span></span>
<span data-ttu-id="276c5-133">По итогам применения этих параметров создается минимальная безопасная основа для настройки конечной точки.</span><span class="sxs-lookup"><span data-stu-id="276c5-133">The net effect of these settings is a secure and minimal starting point for configuring your endpoint.</span></span>

2.  <span data-ttu-id="276c5-134">Поле *RoleDefinitions* назначает возможности ролей для отдельных групп.</span><span class="sxs-lookup"><span data-stu-id="276c5-134">The *RoleDefinitions* field assigns Role Capabilities to specific groups.</span></span>
<span data-ttu-id="276c5-135">Оно определяет, какие действия разрешает выполнять привилегированная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="276c5-135">It defines who can do what as a privileged account.</span></span>
<span data-ttu-id="276c5-136">В этом поле можно указать функциональные возможности, которые будут предоставлены подключившемуся пользователю в зависимости от членства в группах.</span><span class="sxs-lookup"><span data-stu-id="276c5-136">With this field, you can specify the functionality available to any connecting user based on group membership.</span></span>
<span data-ttu-id="276c5-137">Это основные функциональные возможности элемента RBAC в JEA.</span><span class="sxs-lookup"><span data-stu-id="276c5-137">This is the core of JEA's RBAC functionality.</span></span>
<span data-ttu-id="276c5-138">В этом примере членам группы "Contoso\JEA_NonAdmin_Operator" предоставляются возможности роли "Maintenance".</span><span class="sxs-lookup"><span data-stu-id="276c5-138">In this example, you are exposing the pre-made "Maintenance" RoleCapability to members of the "Contoso\JEA_NonAdmin_Operator" group.</span></span>

3.  <span data-ttu-id="276c5-139">Поле *RunAsVirtualAccount* означает, что PowerShell следует запустить от имени виртуальной учетной записи в этой конечной точке.</span><span class="sxs-lookup"><span data-stu-id="276c5-139">The *RunAsVirtualAccount* field indicates that PowerShell should "run as" a Virtual Account at this endpoint.</span></span>
<span data-ttu-id="276c5-140">По умолчанию виртуальная учетная запись входит во встроенную группу администраторов.</span><span class="sxs-lookup"><span data-stu-id="276c5-140">By default, the Virtual Account is a member of the built in Administrators group.</span></span>
<span data-ttu-id="276c5-141">На контроллере домена она также по умолчанию входит в группу администраторов домена.</span><span class="sxs-lookup"><span data-stu-id="276c5-141">On a domain controller, it is also a member of the Domain Administrators group by default.</span></span>
<span data-ttu-id="276c5-142">Далее в этом руководстве вы узнаете, как настроить права доступа для виртуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="276c5-142">Later in this guide, you will learn how to customize the privileges of the Virtual Account.</span></span>

4.  <span data-ttu-id="276c5-143">Поле *TranscriptDirectory* определяет, где будут сохраняться созданные детализированные записи PowerShell с "подсматриванием" после каждого удаленного сеанса.</span><span class="sxs-lookup"><span data-stu-id="276c5-143">The *TranscriptDirectory* field defines where "over-the-shoulder" PowerShell transcripts are saved after each remote session.</span></span>
<span data-ttu-id="276c5-144">Эти записи позволяют отслеживать, какие действия были выполнены в каждом сеансе.</span><span class="sxs-lookup"><span data-stu-id="276c5-144">These transcripts allow you to inspect the actions taken in each session in a readable way.</span></span>
<span data-ttu-id="276c5-145">Дополнительные сведения о записях PowerShell см. в этой [записи в блоге](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).</span><span class="sxs-lookup"><span data-stu-id="276c5-145">For more information about PowerShell transcripts, check out this [blog post](http://blogs.msdn.com/b/powershell/archive/2015/06/09/powershell-the-blue-team.aspx).</span></span>
<span data-ttu-id="276c5-146">Примечание. В обычные журналы событий Windows также записываются данные о том, какие команды каждый пользователь выполнил в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="276c5-146">Note: regular Windows Eventing also captures information about what each user ran with PowerShell.</span></span>
<span data-ttu-id="276c5-147">При этом записи, создаваемые здесь, более удобны для чтения.</span><span class="sxs-lookup"><span data-stu-id="276c5-147">Transcripts are just a bit more readable.</span></span>

<span data-ttu-id="276c5-148">Наконец, сохраните изменения в *JEADemo2.pssc*.</span><span class="sxs-lookup"><span data-stu-id="276c5-148">Finally, save your changes to *JEADemo2.pssc*.</span></span>

## <a name="apply-the-powershell-session-configuration"></a><span data-ttu-id="276c5-149">Применение конфигурации сеанса PowerShell</span><span class="sxs-lookup"><span data-stu-id="276c5-149">Apply the PowerShell Session Configuration</span></span>

<span data-ttu-id="276c5-150">Для создания конечной точки из файла конфигурации сеанса необходимо зарегистрировать файл.</span><span class="sxs-lookup"><span data-stu-id="276c5-150">To create an endpoint from a Session Configuration file, you need to register the file.</span></span>
<span data-ttu-id="276c5-151">При этом требуется несколько фрагментов данных:</span><span class="sxs-lookup"><span data-stu-id="276c5-151">This requires a few pieces of information:</span></span>

1. <span data-ttu-id="276c5-152">Путь к файлу конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="276c5-152">The path to the Session Configuration file.</span></span>
2. <span data-ttu-id="276c5-153">Имя зарегистрированной конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="276c5-153">The name of your registered Session Configuration.</span></span> <span data-ttu-id="276c5-154">Это то же имя, которое пользователи указывают как значение параметра "ConfigurationName" при подключении конечной точки к `Enter-PSSession` или `New-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="276c5-154">This is the same name users provide to the "ConfigurationName" parameter when they connect to your endpoint with `Enter-PSSession` or `New-PSSession`.</span></span>

<span data-ttu-id="276c5-155">Чтобы зарегистрировать конфигурацию сеанса на локальном компьютере, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="276c5-155">To register the Session Configuration on your local machine, run the following command:</span></span>

```PowerShell
Register-PSSessionConfiguration -Name 'JEADemo2' -Path "$env:ProgramData\JEAConfiguration\JEADemo2.pssc"
```

<span data-ttu-id="276c5-156">Все готово.</span><span class="sxs-lookup"><span data-stu-id="276c5-156">Congratulations!</span></span> <span data-ttu-id="276c5-157">Вы настроили конечную точку JEA.</span><span class="sxs-lookup"><span data-stu-id="276c5-157">You have set up your JEA endpoint.</span></span>

## <a name="test-out-your-endpoint"></a><span data-ttu-id="276c5-158">Тестирование конечной точки</span><span class="sxs-lookup"><span data-stu-id="276c5-158">Test Out Your Endpoint</span></span>
<span data-ttu-id="276c5-159">Повторите шаги, указанные в разделе [Использование JEA](using-jea.md), с новой конечной точкой, чтобы убедиться в том, что она работает, как предполагалось.</span><span class="sxs-lookup"><span data-stu-id="276c5-159">Re-run the steps listed in the [Using JEA](using-jea.md) section against your new endpoint to confirm it is operating as intended.</span></span>
<span data-ttu-id="276c5-160">Задавая имя конфигурации в команде `Enter-PSSession`, используйте имя новой конечной точки (JEADemo2).</span><span class="sxs-lookup"><span data-stu-id="276c5-160">Be sure to use the new endpoint name (JEADemo2) when providing the configuration name to `Enter-PSSession`.</span></span>

```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName JEADemo2 -Credential $NonAdminCred
```

## <a name="key-concepts"></a><span data-ttu-id="276c5-161">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="276c5-161">Key Concepts</span></span>
<span data-ttu-id="276c5-162">**Конфигурация сеанса PowerShell**: иногда называется *конечной точкой PowerShell*; это то "место", где пользователи могут подключаться к PowerShell и получать доступ к его функциональным возможностям.</span><span class="sxs-lookup"><span data-stu-id="276c5-162">**PowerShell Session Configuration**: Sometimes referred to as *PowerShell Endpoint*, this is the figurative "place" where users connect and get access to PowerShell functionality.</span></span>
<span data-ttu-id="276c5-163">Чтобы получить список конфигураций сеансов, зарегистрированных в системе, выполните команду `Get-PSSessionConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="276c5-163">You can list the registered Session Configurations on your system by running `Get-PSSessionConfiguration`.</span></span>
<span data-ttu-id="276c5-164">При определенной настройке конфигурацию сеанса PowerShell можно назвать *конечной точкой JEA*.</span><span class="sxs-lookup"><span data-stu-id="276c5-164">When configured in a specific way, a PowerShell Session Configuration can be called a *JEA Endpoint*.</span></span>

<span data-ttu-id="276c5-165">**Файл конфигурации сеанса PowerShell (PSSC)**: файл, который, будучи зарегистрированным, определяет параметры конфигурации сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="276c5-165">**PowerShell Session Configuration File (.pssc)**: A file that, when registered, defines settings for a PowerShell Session Configuration.</span></span>
<span data-ttu-id="276c5-166">Он содержит спецификации для ролей пользователей, которые могут подключаться к конечной точке, виртуальную запись, с использованием которой он запускается, и многое другое.</span><span class="sxs-lookup"><span data-stu-id="276c5-166">It contains specifications for user roles that can connect to the endpoint, the "run as" Virtual Account, and more.</span></span>     

<span data-ttu-id="276c5-167">**Определения ролей**: поле в файле конфигурации сеанса, задающее возможности ролей, предоставляемые подключающимся пользователям.</span><span class="sxs-lookup"><span data-stu-id="276c5-167">**Role Definitions**: The field in a Session Configuration File that defines the Role Capabilities granted to connecting users.</span></span>
<span data-ttu-id="276c5-168">Оно определяет, *кому* и *какие* действия разрешает выполнять привилегированная учетная запись.</span><span class="sxs-lookup"><span data-stu-id="276c5-168">It defines *who* can do *what* as a privileged account.</span></span>
<span data-ttu-id="276c5-169">Это основные функциональные возможности RBAC в JEA.</span><span class="sxs-lookup"><span data-stu-id="276c5-169">This is the core of JEA's RBAC capabilities.</span></span>

<span data-ttu-id="276c5-170">**SessionType**: поле в файле конфигурации сеанса, представляющее параметры по умолчанию для конфигурации сеанса.</span><span class="sxs-lookup"><span data-stu-id="276c5-170">**SessionType**: A field in a Session Configuration File that represents default settings for a Session Configuration.</span></span>
<span data-ttu-id="276c5-171">У конечных точек JEA оно должно иметь значение RestrictedRemoteServer.</span><span class="sxs-lookup"><span data-stu-id="276c5-171">For JEA endpoints, this must be set to RestrictedRemoteServer.</span></span>

<span data-ttu-id="276c5-172">**PowerShell Transcript**: файл, содержащий представление сеанса PowerShell с "подсматриванием".</span><span class="sxs-lookup"><span data-stu-id="276c5-172">**PowerShell Transcript**: A file containing an "over-the-shoulder" view of a PowerShell session.</span></span>
<span data-ttu-id="276c5-173">В PowerShell можно настроить создание записей сеансов JEA с помощью поля TranscriptDirectory.</span><span class="sxs-lookup"><span data-stu-id="276c5-173">You can set PowerShell to generate transcripts for JEA sessions using the TranscriptDirectory field.</span></span>
<span data-ttu-id="276c5-174">Дополнительные сведения о записях см. в этой [записи в блоге](https://technet.microsoft.com/en-us/magazine/ff687007.aspx).</span><span class="sxs-lookup"><span data-stu-id="276c5-174">For more information on transcripts, check out this [blog post](https://technet.microsoft.com/en-us/magazine/ff687007.aspx).</span></span>

