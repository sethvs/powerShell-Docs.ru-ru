---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea,powershell,безопасность"
title: "Возможности ролей JEA"
ms.openlocfilehash: 10f5f390daccbb012be6ee7272041e777810ee12
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="jea-role-capabilities"></a><span data-ttu-id="b2c17-103">Возможности ролей JEA</span><span class="sxs-lookup"><span data-stu-id="b2c17-103">JEA Role Capabilities</span></span>

> <span data-ttu-id="b2c17-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b2c17-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="b2c17-105">При создании конечной точки JEA потребуется определить одну или несколько "возможностей ролей", описывающих, *что именно* пользователь может сделать в сеансе JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-105">When creating a JEA endpoint, you will need to define one or more "role capabilities" which describe *what* someone can do in a JEA session.</span></span>
<span data-ttu-id="b2c17-106">Возможность роли — это файл данных PowerShell с расширением PSRC, содержащий все командлеты, функции, поставщики и внешние программы, которые должны быть доступны для подключающихся пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2c17-106">A role capability is a PowerShell data file with the .psrc extension that lists all the cmdlets, functions, providers, and external programs that should be made available to connecting users.</span></span>

<span data-ttu-id="b2c17-107">В этом разделе описывается создание файла возможностей ролей PowerShell для пользователей JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-107">This topic describes how to create a PowerShell role capability file for your JEA users.</span></span>

## <a name="determine-which-commands-to-allow"></a><span data-ttu-id="b2c17-108">Определение разрешаемых команд</span><span class="sxs-lookup"><span data-stu-id="b2c17-108">Determine which commands to allow</span></span>

<span data-ttu-id="b2c17-109">Прежде всего, при создании файла возможности роли нужно определить, к чему именно потребуется доступ пользователям, которым назначена эта роль.</span><span class="sxs-lookup"><span data-stu-id="b2c17-109">The first step when creating a role capability file is to consider what the users who are assigned the role will need access to.</span></span>
<span data-ttu-id="b2c17-110">Этот процесс сбора требований может занять некоторое время, однако он крайне важен.</span><span class="sxs-lookup"><span data-stu-id="b2c17-110">This requirements gathering process can take a while, but it is a very important process.</span></span>
<span data-ttu-id="b2c17-111">Предоставление пользователям доступа к слишком малому набору командлетов и функций может помешать их нормальной работе.</span><span class="sxs-lookup"><span data-stu-id="b2c17-111">Giving users access to too few cmdlets and functions can prevent them from getting their job done.</span></span>
<span data-ttu-id="b2c17-112">Разрешение доступа к слишком большому числу командлетов и функций может предоставить пользователям более широкие возможности, чем подразумевалось вами, что ослабит защиту вашей системы.</span><span class="sxs-lookup"><span data-stu-id="b2c17-112">Allowing access to too many cmdlets and functions can lead to users doing more than you intended with their implicit admin privileges, weakening your security stance.</span></span>

<span data-ttu-id="b2c17-113">То, как вы будете это делать, зависит от вашей организации и целей, однако приведенные ниже советы помогут придерживаться правильного направления.</span><span class="sxs-lookup"><span data-stu-id="b2c17-113">How you go about this process will depend on your organization and goals, however the following tips can help ensure you're on the right path.</span></span>

1. <span data-ttu-id="b2c17-114">**Определите**, какие команды пользователи применяют для выполнения поставленных задач.</span><span class="sxs-lookup"><span data-stu-id="b2c17-114">**Identify** the commands users are using to get their jobs done.</span></span> <span data-ttu-id="b2c17-115">Для этого можно опросить ИТ-специалистов, проверить сценарии автоматизации либо проанализировать журналы или записи сеансов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2c17-115">This may involve surveying IT staff, checking automation scripts, or analyzing PowerShell session transcripts or logs.</span></span>
2. <span data-ttu-id="b2c17-116">По возможности **замените** используемые программы командной строки на эквиваленты PowerShell, чтобы сделать аудит и настройку JEA максимально удобными.</span><span class="sxs-lookup"><span data-stu-id="b2c17-116">**Update** use of command line tools to PowerShell equivalents, where possible, for the best auditing and JEA customization experience.</span></span> <span data-ttu-id="b2c17-117">Внешние программы не поддерживают такую детальную настройку ограничений, как собственные командлеты PowerShell и функции в JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-117">External programs cannot be constrained as granularly as native PowerShell cmdlets and functions in JEA.</span></span>
3. <span data-ttu-id="b2c17-118">При необходимости **ограничьте** область действия командлетов, разрешив только отдельные параметры и их значения.</span><span class="sxs-lookup"><span data-stu-id="b2c17-118">**Restrict** the scope of the cmdlets if necessary to only allow specific parameters or parameter values.</span></span> <span data-ttu-id="b2c17-119">Это особенно важно в том случае, если пользователям нужно разрешить управлять лишь частью системы.</span><span class="sxs-lookup"><span data-stu-id="b2c17-119">This is particularly important if users should only be able to manage part of a system.</span></span>
4. <span data-ttu-id="b2c17-120">**Создайте** настраиваемые функции на замену сложным командам или командам, которые трудно ограничить в JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-120">**Create** custom functions to replace complex commands or commands which are difficult to constrain in JEA.</span></span> <span data-ttu-id="b2c17-121">Простая функция, включающая в себя сложную команду или применяющая дополнительную логику проверки, повышает уровень контроля и упрощает работу администраторов и конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2c17-121">A simple function that wraps a complex command or applies additional validation logic can offer additional control for admins and end-user simplicity.</span></span>
5. <span data-ttu-id="b2c17-122">**Проверьте** полученный список допустимых команд на соответствие потребностям пользователей или служб автоматизации и при необходимости скорректируйте его.</span><span class="sxs-lookup"><span data-stu-id="b2c17-122">**Test** the scoped list of allowable commands with your users and/or automation services and adjust as necessary.</span></span>

<span data-ttu-id="b2c17-123">Важно помнить, что команды в сеансе JEA часто запускаются с правами администратора (или иными повышенными правами).</span><span class="sxs-lookup"><span data-stu-id="b2c17-123">It is important to remember that commands in a JEA session are often run with admin (or otherwise elevated) privileges.</span></span>
<span data-ttu-id="b2c17-124">Важно тщательно отбирать доступные команды, чтобы конечная точка JEA не позволяла подключающемуся пользователю повысить свои права.</span><span class="sxs-lookup"><span data-stu-id="b2c17-124">Careful selection of available commands is important to ensure the JEA endpoint does not allow the connecting user to elevate their permissions.</span></span>
<span data-ttu-id="b2c17-125">Ниже приведено несколько примеров команд, которые в состоянии без ограничений быть использованы злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="b2c17-125">Below are some examples of commands that can be used maliciously if allowed in an unconstrained state.</span></span>
<span data-ttu-id="b2c17-126">Обратите внимание, что этот список не является исчерпывающим и служит лишь отправной точкой для дальнейших действий.</span><span class="sxs-lookup"><span data-stu-id="b2c17-126">Note that this is not an exhaustive list and should only be used as a cautionary starting point.</span></span>

### <a name="examples-of-potentially-dangerous-commands"></a><span data-ttu-id="b2c17-127">Примеры потенциально опасных команд</span><span class="sxs-lookup"><span data-stu-id="b2c17-127">Examples of potentially dangerous commands</span></span>

<span data-ttu-id="b2c17-128">Риск</span><span class="sxs-lookup"><span data-stu-id="b2c17-128">Risk</span></span> | <span data-ttu-id="b2c17-129">Пример</span><span class="sxs-lookup"><span data-stu-id="b2c17-129">Example</span></span> | <span data-ttu-id="b2c17-130">Связанные команды</span><span class="sxs-lookup"><span data-stu-id="b2c17-130">Related commands</span></span>
-----|---------|-----------------
<span data-ttu-id="b2c17-131">Предоставление прав администратора подключающемуся пользователю для обхода JEA</span><span class="sxs-lookup"><span data-stu-id="b2c17-131">Granting the connecting user admin privileges to bypass JEA</span></span> | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | <span data-ttu-id="b2c17-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span><span class="sxs-lookup"><span data-stu-id="b2c17-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span></span>
<span data-ttu-id="b2c17-133">Выполнение произвольного кода, например вредоносных программ, эксплойтов или пользовательских сценариев для обхода защиты</span><span class="sxs-lookup"><span data-stu-id="b2c17-133">Running arbitrary code, such as malware, exploits, or custom scripts to bypass protections</span></span> | `Start-Process -FilePath '\\san\share\malware.exe'` | <span data-ttu-id="b2c17-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span><span class="sxs-lookup"><span data-stu-id="b2c17-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span></span>

## <a name="create-a-role-capability-file"></a><span data-ttu-id="b2c17-135">Создание файла возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="b2c17-135">Create a role capability file</span></span>

<span data-ttu-id="b2c17-136">Вы можете создать новый файл возможности роли с помощью командлета [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile).</span><span class="sxs-lookup"><span data-stu-id="b2c17-136">You can create a new PowerShell role capability file with the [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) cmdlet.</span></span>

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

<span data-ttu-id="b2c17-137">Полученный файл можно открыть в текстовом редакторе и изменить, чтобы разрешить нужные команды для роли.</span><span class="sxs-lookup"><span data-stu-id="b2c17-137">The resulting role capability file can be opened in a text editor and modified to allow the desired commands for the role.</span></span>
<span data-ttu-id="b2c17-138">Справочная документация PowerShell содержит несколько примеров того, как можно настроить такой файл.</span><span class="sxs-lookup"><span data-stu-id="b2c17-138">The PowerShell help documentation contains several examples of how you can configure the file.</span></span>

### <a name="allowing-powershell-cmdlets-and-functions"></a><span data-ttu-id="b2c17-139">Разрешение функций и командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2c17-139">Allowing PowerShell cmdlets and functions</span></span>

<span data-ttu-id="b2c17-140">Чтобы разрешить пользователям запускать функции или командлеты PowerShell, добавьте имя функции или командлета в поле VisibleFunctions или VisbibleCmdlets.</span><span class="sxs-lookup"><span data-stu-id="b2c17-140">To authorize users to run PowerShell cmdlets or functions, add the cmdlet or function name to the VisbibleCmdlets or VisibleFunctions fields.</span></span>
<span data-ttu-id="b2c17-141">Если вы не уверены, является ли команда командлетом или функцией, выполните `Get-Command <name>` и проверьте свойство CommandType в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b2c17-141">If you aren't sure whether a command is a cmdlet or function, you can run `Get-Command <name>` and check the "CommandType" property in the output.</span></span>

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

<span data-ttu-id="b2c17-142">Иногда область действия командлета или функции слишком широка для потребностей пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2c17-142">Sometimes the scope of a specific cmdlet or function is too broad for your users' needs.</span></span>
<span data-ttu-id="b2c17-143">Например, администратору DNS, скорее всего, потребуется только доступ для перезапуска службы DNS.</span><span class="sxs-lookup"><span data-stu-id="b2c17-143">A DNS admin, for example, probably only needs access to restart the DNS service.</span></span>
<span data-ttu-id="b2c17-144">В мультитенантной среде, где клиентам предоставляется доступ к средствам самостоятельного управления, эти клиенты должны быть в состоянии управлять только собственными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="b2c17-144">In a multi-tenant environment where tenants are granted access to self-service management tools, tenants should be limited to managing with their own resources.</span></span>
<span data-ttu-id="b2c17-145">В этих случаях можно ограничить доступные параметры из командлета или функции.</span><span class="sxs-lookup"><span data-stu-id="b2c17-145">For these cases, you can restrict which parameters are exposed from the cmdlet or function.</span></span>

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

<span data-ttu-id="b2c17-146">В более сложных сценариях может потребоваться ограничить значения, которые можно задать для этих параметров.</span><span class="sxs-lookup"><span data-stu-id="b2c17-146">In more advanced scenarios, you may also need to restrict which values someone can supply to these parameters.</span></span>
<span data-ttu-id="b2c17-147">Возможности ролей позволяют задать набор допустимых значений или шаблон регулярного выражения, по которому оценивается, разрешены ли указанные входные данные.</span><span class="sxs-lookup"><span data-stu-id="b2c17-147">Role capabilities let you define a set of allowed values or a regular expression pattern that is evaluated to determine if a given input is allowed.</span></span>

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> <span data-ttu-id="b2c17-148">[Общие параметры PowerShell](https://technet.microsoft.com/en-us/library/hh847884.aspx) всегда разрешены, даже если ограничить доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="b2c17-148">The [common PowerShell parameters](https://technet.microsoft.com/en-us/library/hh847884.aspx) are always allowed, even if you restrict the available parameters.</span></span>
> <span data-ttu-id="b2c17-149">Их не следует явно указывать в поле "Parameters".</span><span class="sxs-lookup"><span data-stu-id="b2c17-149">You should not explicitly list them in the Parameters field.</span></span>

<span data-ttu-id="b2c17-150">В следующей таблице описаны различные способы настройки видимого командлета или видимой функции.</span><span class="sxs-lookup"><span data-stu-id="b2c17-150">The table below describes the various ways you can customize a visible cmdlet or function.</span></span>
<span data-ttu-id="b2c17-151">Вы можете комбинировать любые приведенные ниже примеры в поле "VisibleCmdlets".</span><span class="sxs-lookup"><span data-stu-id="b2c17-151">You can mix and match any of the below in the VisibleCmdlets field.</span></span>

<span data-ttu-id="b2c17-152">Пример</span><span class="sxs-lookup"><span data-stu-id="b2c17-152">Example</span></span>                                                                                      | <span data-ttu-id="b2c17-153">Вариант использования</span><span class="sxs-lookup"><span data-stu-id="b2c17-153">Use case</span></span>
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="b2c17-154">`'My-Func'` или `@{ Name = 'My-Func' }`</span><span class="sxs-lookup"><span data-stu-id="b2c17-154">`'My-Func'` or `@{ Name = 'My-Func' }`</span></span>                                                       | <span data-ttu-id="b2c17-155">Разрешает пользователю выполнить `My-Func` без каких-либо ограничений для параметров.</span><span class="sxs-lookup"><span data-stu-id="b2c17-155">Allows the user to run `My-Func` without any restrictions on the parameters.</span></span>
`'MyModule\My-Func'`                                                                         | <span data-ttu-id="b2c17-156">Разрешает пользователю выполнить `My-Func` из модуля `MyModule` без каких-либо ограничений для параметров.</span><span class="sxs-lookup"><span data-stu-id="b2c17-156">Allows the user to run `My-Func` from the module `MyModule` without any restrictions on the parameters.</span></span>
`'My-*'`                                                                                     | <span data-ttu-id="b2c17-157">Разрешает пользователю выполнить любой командлет или функцию с командой `My`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-157">Allows the user to run any cmdlet or function with the verb `My`.</span></span>
`'*-Func'`                                                                                   | <span data-ttu-id="b2c17-158">Разрешает пользователю выполнить любой командлет или функцию с существительным `Func`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-158">Allows the user to run any cmdlet or function with the noun `Func`.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | <span data-ttu-id="b2c17-159">Разрешает пользователю выполнить `My-Func` с параметрами `Param1` и (или) `Param2`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-159">Allows the user to run `My-Func` with the `Param1` and/or `Param2` parameters.</span></span> <span data-ttu-id="b2c17-160">Для параметров можно задать любое значение.</span><span class="sxs-lookup"><span data-stu-id="b2c17-160">Any value can be supplied to the parameters.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | <span data-ttu-id="b2c17-161">Разрешает пользователю выполнить `My-Func` с параметром `Param1`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-161">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="b2c17-162">Для параметра можно задать только значение "Value1" или "Value2".</span><span class="sxs-lookup"><span data-stu-id="b2c17-162">Only "Value1" and "Value2" can be supplied to the parameter.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | <span data-ttu-id="b2c17-163">Разрешает пользователю выполнить `My-Func` с параметром `Param1`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-163">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="b2c17-164">Для параметра можно задать любое значение, начинающееся с "contoso".</span><span class="sxs-lookup"><span data-stu-id="b2c17-164">Any value starting with "contoso" can be supplied to the parameter.</span></span>


> [!WARNING]
> <span data-ttu-id="b2c17-165">Для обеспечения наилучшей безопасности при определении видимых командлетов или функций рекомендуется не использовать подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="b2c17-165">For best security practices, it is not recommended to use wildcards when defining visible cmdlets or functions.</span></span>
> <span data-ttu-id="b2c17-166">Вместо этого следует явно указать каждую надежную команду, чтобы убедиться, что не будут случайно разрешены никакие другие команды, которые используют такую же схему именования.</span><span class="sxs-lookup"><span data-stu-id="b2c17-166">Instead, you should explicitly list each trusted command to ensure no other commands that share the same naming scheme are unintentionally authorized.</span></span>

<span data-ttu-id="b2c17-167">Вы не можете применить ValidatePattern и ValidateSet для одного командлета или одной функции.</span><span class="sxs-lookup"><span data-stu-id="b2c17-167">You cannot apply both a ValidatePattern and ValidateSet to the same cmdlet or function.</span></span>

<span data-ttu-id="b2c17-168">В противном случае ValidatePattern переопределит ValidateSet.</span><span class="sxs-lookup"><span data-stu-id="b2c17-168">If you do, the ValidatePattern will override the ValidateSet.</span></span>

<span data-ttu-id="b2c17-169">Дополнительные сведения о ValidatePattern см. в [этой записи блога *Hey, Scripting Guy!*](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) и справочных материалах о [регулярных выражениях PowerShell](https://technet.microsoft.com/en-us/library/hh847880.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2c17-169">For more information about ValidatePattern, check out [this *Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) and the [PowerShell Regular Expressions](https://technet.microsoft.com/en-us/library/hh847880.aspx) reference content.</span></span>

### <a name="allowing-external-commands-and-powershell-scripts"></a><span data-ttu-id="b2c17-170">Разрешение внешних команд и сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2c17-170">Allowing external commands and PowerShell scripts</span></span>

<span data-ttu-id="b2c17-171">Чтобы разрешить пользователям запускать исполняемые файлы и сценарии PowerShell (PS1) в сеансе JEA, нужно добавить полный путь к каждой программы в поле "VisibleExternalCommands".</span><span class="sxs-lookup"><span data-stu-id="b2c17-171">To allow users to run executables and PowerShell scripts (.ps1) in a JEA session, you have to add the full path to each program in the VisibleExternalCommands field.</span></span>

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

<span data-ttu-id="b2c17-172">Рекомендуется по возможности использовать командлеты или функции PowerShell, эквивалентные любым внешним исполняемым файлам, которые вы разрешаете, так как для этих функций и командлетов PowerShell вы можете управлять разрешенными параметрами.</span><span class="sxs-lookup"><span data-stu-id="b2c17-172">It is advised, where possible, to use PowerShell cmdlet/function equivalents of any external executables you authorize since you have control over which parameters are allowed with PowerShell cmdlets/functions.</span></span>

<span data-ttu-id="b2c17-173">Многие исполняемые файлы дают возможность считать текущее состояние и затем изменить его, просто указав различные параметры.</span><span class="sxs-lookup"><span data-stu-id="b2c17-173">Many executables allow you to both read the current state and then change it just by providing different parameters.</span></span>

<span data-ttu-id="b2c17-174">Например, рассмотрим роль администратора файлового сервера, который хочет проверить, какие сетевые папки размещаются на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b2c17-174">For example, consider the role of a file server admin who wants to check which network shares are hosted by the local machine.</span></span>
<span data-ttu-id="b2c17-175">Один из способов проверки заключается в использовании `net share`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-175">One way to check is to use `net share`.</span></span>
<span data-ttu-id="b2c17-176">Однако разрешение использования net.exe очень опасно, так как администратор может легко воспользоваться этой командой для получения прав администратора с помощью `net group Administrators unprivilegedjeauser /add`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-176">However, allowing net.exe is very dangerous becuase the admin could just as easily use the command to gain admin privileges with `net group Administrators unprivilegedjeauser /add`.</span></span>
<span data-ttu-id="b2c17-177">Лучше разрешить командлет [Get-SmbShare](https://technet.microsoft.com/en-us/library/jj635704.aspx), которой дает тот же результат, но имеет гораздо более ограниченную область действия.</span><span class="sxs-lookup"><span data-stu-id="b2c17-177">A better approach is to allow [Get-SmbShare](https://technet.microsoft.com/en-us/library/jj635704.aspx) which achieves the same result but has a much more limited scope.</span></span>

<span data-ttu-id="b2c17-178">Делая внешние команды доступными для пользователей в сеансе JEA, всегда указывайте полный путь к исполняемому файлу, чтобы вместо него не запускалась другая (и потенциально вредоносная) программа с таким же именем, размещенная в другом месте.</span><span class="sxs-lookup"><span data-stu-id="b2c17-178">When making external commands available to users in a JEA session, always specify the complete path to the executable to ensure a similarly named (and potentially malicous) program placed elsewhere on the system does not get executed instead.</span></span>

### <a name="allowing-access-to-powershell-providers"></a><span data-ttu-id="b2c17-179">Разрешение доступа к поставщикам PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2c17-179">Allowing access to PowerShell providers</span></span>

<span data-ttu-id="b2c17-180">По умолчанию в сеансах JEA нет доступных поставщиков PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2c17-180">By default, no PowerShell providers are available in JEA sessions.</span></span>

<span data-ttu-id="b2c17-181">Это в первую очередь служит для снижения риска раскрытия конфиденциальной информации и параметров конфигурации подключающемуся пользователю.</span><span class="sxs-lookup"><span data-stu-id="b2c17-181">This is primarily to reduce the risk of sensitive information and configuration settings being disclosed to the connecting user.</span></span>

<span data-ttu-id="b2c17-182">При необходимости доступ к поставщикам PowerShell можно разрешить с помощью команды `VisibleProviders`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-182">When necessary, you can allow access to the PowerShell providers using the `VisibleProviders` command.</span></span>
<span data-ttu-id="b2c17-183">Для просмотра полного списка поставщиков запустите `Get-PSProvider`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-183">For a full list of providers, run `Get-PSProvider`.</span></span>

```powershell
VisibleProviders = 'Registry'
```

<span data-ttu-id="b2c17-184">Для простых задач, которым требуется доступ к файловой системе, реестру, хранилищу сертификатов, или других конфиденциальных поставщиков можно также написать настраиваемую функцию, которая работает с поставщиком от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="b2c17-184">For simple tasks that require access to the file system, registry, certificate store, or other sensitive providers, you can also consider writing a custom function that works with the provider on the user's behalf.</span></span>
<span data-ttu-id="b2c17-185">К функциям, командлетам и внешним программам, доступным в сеансе JEA, не применяются те же ограничения, что и для JEA, то есть они могут по умолчанию получить доступ к любому поставщику.</span><span class="sxs-lookup"><span data-stu-id="b2c17-185">Functions, cmdlets, and external programs that are available in a JEA session are not subject to the same constraints as JEA -- they can access any provider by default.</span></span>
<span data-ttu-id="b2c17-186">В случаях, когда требуется скопировать файлы из конечной точки JEA или на нее, рассмотрите возможность использования [диска пользователя](session-configurations.md#user-drive).</span><span class="sxs-lookup"><span data-stu-id="b2c17-186">Also consider using the [user drive](session-configurations.md#user-drive) when copying files to/from a JEA endpoint is required.</span></span>

### <a name="creating-custom-functions"></a><span data-ttu-id="b2c17-187">Создание настраиваемых функций</span><span class="sxs-lookup"><span data-stu-id="b2c17-187">Creating custom functions</span></span>

<span data-ttu-id="b2c17-188">В файле возможностей роли можно создать настраиваемые функции, чтобы упростить выполнение сложных задач для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2c17-188">You can author custom functions in a role capability file to simplify complex tasks for your end users.</span></span>
<span data-ttu-id="b2c17-189">Настраиваемые функции также удобны, когда требуется расширенная логика проверки для значений параметров командлета.</span><span class="sxs-lookup"><span data-stu-id="b2c17-189">Custom functions are also useful when you require advanced validation logic for cmdlet parameter values.</span></span>
<span data-ttu-id="b2c17-190">Вы можете составлять простые функции в поле **FunctionDefinitions**:</span><span class="sxs-lookup"><span data-stu-id="b2c17-190">You can write simple functions in the **FunctionDefinitions** field:</span></span>

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending | Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="b2c17-191">Не забудьте добавить имя настраиваемых функций в поле **VisibleFunctions**, чтобы пользователи JEA могли запускать их.</span><span class="sxs-lookup"><span data-stu-id="b2c17-191">Don't forget to add the name of your custom functions to the **VisibleFunctions** field so they can be run by the JEA users.</span></span>


<span data-ttu-id="b2c17-192">Основная часть (блок сценария) настраиваемых функций запускается в языковом режиме по умолчанию для данной системы, и на нее не налагаются ограничения языка JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-192">The body (script block) of custom functions runs in the default language mode for the system and is not subject to JEA's language constraints.</span></span>
<span data-ttu-id="b2c17-193">Это означает, что функции имеют доступ к файловой системе и реестру и могут запускать команды, которые не были сделаны видимыми в файле возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="b2c17-193">This means that functions can access the file system and registry, and run commands that were not made visible in the role capability file.</span></span>
<span data-ttu-id="b2c17-194">Примите меры, чтобы избежать выполнения произвольного кода при использовании параметров и передачи вводимых пользователем данных напрямую в такие командлеты, как `Invoke-Expression`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-194">Take care to avoid allowing arbitrary code to be run when using parameters and avoid piping user input directly into cmdlets like `Invoke-Expression`.</span></span>

<span data-ttu-id="b2c17-195">В приведенном выше примере можно заметить, что полное имя модуля (FQMN) `Microsoft.PowerShell.Utility\Select-Object` было использовано вместо сокращенного `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="b2c17-195">In the above example, you will notice that the fully qualified module name (FQMN) `Microsoft.PowerShell.Utility\Select-Object` was used instead of the shorthand `Select-Object`.</span></span>
<span data-ttu-id="b2c17-196">Функции, определенные в файлах возможностей роли, по-прежнему подчиняются области действия сеансов JEA, что включает в себя функции прокси-сервера, создаваемые JEA для ограничения существующих команд.</span><span class="sxs-lookup"><span data-stu-id="b2c17-196">Functions defined in role capability files are still subject to the scope of JEA sessions, which includes the proxy functions JEA creates to constrain existing commands.</span></span>

<span data-ttu-id="b2c17-197">По умолчанию Select-Object является ограниченным командлетом во всех сеансах JEA, который не позволяет выбрать произвольные свойства для объектов.</span><span class="sxs-lookup"><span data-stu-id="b2c17-197">Select-Object is a default, constrained cmdlet in all JEA sessions that doesn't allow you to select arbitrary properties on objects.</span></span>
<span data-ttu-id="b2c17-198">Чтобы использовать Select-Object без ограничений в функциях, требуется явно запросить полную реализацию, указав полное имя модуля.</span><span class="sxs-lookup"><span data-stu-id="b2c17-198">To use the unconstrained Select-Object in functions, you must explicitly request the full implementation by specifying the FQMN.</span></span>
<span data-ttu-id="b2c17-199">Любой ограниченный командлет в сеансе JEA будет демонстрировать одинаковое поведение при вызове из функции в соответствии с [приоритетом команд](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2c17-199">Any constrained cmdlet in a JEA session will exhibit the same behavior when invoked from a function, in line with PowerShell's [command precedence](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span></span>

<span data-ttu-id="b2c17-200">При наличии множества настраиваемых функций может быть проще поместить их в [модуль сценария PowerShell](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="b2c17-200">If you are writing a lot of custom functions, it may be easier to put them in a [PowerShell Script Module](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span></span>
<span data-ttu-id="b2c17-201">Затем можно сделать эти функции видимыми в сеансе JEA с помощью поля "VisibleFunctions", как и в случае со встроенными и сторонними модулями.</span><span class="sxs-lookup"><span data-stu-id="b2c17-201">You can then make those functions visible in the JEA session using the VisibleFunctions field like you would with built-in and third party modules.</span></span>

## <a name="place-role-capabilities-in-a-module"></a><span data-ttu-id="b2c17-202">Помещение возможностей ролей в модуль</span><span class="sxs-lookup"><span data-stu-id="b2c17-202">Place role capabilities in a module</span></span>

<span data-ttu-id="b2c17-203">Чтобы среда PowerShell обнаружила файл возможности ролей, его следует поместить в папку "RoleCapabilities" в модуле PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2c17-203">In order for PowerShell to find a role capability file, it must be stored in a "RoleCapabilities" folder in a PowerShell module.</span></span>
<span data-ttu-id="b2c17-204">Этот модуль может храниться в любой папке, включенной в переменную среды `$env:PSModulePath`, однако не следует помещать его в папку System32 (которая зарезервирована для встроенных модулей) либо в папку, где не являющиеся доверенными подключающиеся пользователи могут изменить его.</span><span class="sxs-lookup"><span data-stu-id="b2c17-204">The module can be stored in any folder included in the `$env:PSModulePath` environment variable, however you should not place it in System32 (reserved for built-in modules) or a folder where the untrusted, connecting users could modify the files.</span></span>
<span data-ttu-id="b2c17-205">Ниже приведен пример создания базового модуля сценария PowerShell с именем *ContosoJEA* в папке "Program Files".</span><span class="sxs-lookup"><span data-stu-id="b2c17-205">Below is an example of creating a basic PowerShell script module called *ContosoJEA* in the "Program Files" path.</span></span>

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest. At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

<span data-ttu-id="b2c17-206">В разделе [Основные сведения о модуле PowerShell](https://msdn.microsoft.com/en-us/library/dd878324.aspx) приведены дополнительные сведения о модулях PowerShell, манифестах модуля и переменной среды PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="b2c17-206">See [Understanding a PowerShell Module](https://msdn.microsoft.com/en-us/library/dd878324.aspx) for more information about PowerShell modules, module manifests, and the PSModulePath environment variable.</span></span>

## <a name="updating-role-capabilities"></a><span data-ttu-id="b2c17-207">Изменение возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="b2c17-207">Updating role capabilities</span></span>


<span data-ttu-id="b2c17-208">Файл возможностей ролей можно изменить в любое время, просто сохранив изменения в нем.</span><span class="sxs-lookup"><span data-stu-id="b2c17-208">You can update a role capability file at any time by simply saving changes to the role capability file.</span></span>
<span data-ttu-id="b2c17-209">Все новые сеансы JEA, запущенные после изменения возможности роли, будут использовать обновленные возможности.</span><span class="sxs-lookup"><span data-stu-id="b2c17-209">Any new JEA sessions started after the role capability has been updated will reflect the revised capabilities.</span></span>

<span data-ttu-id="b2c17-210">Именно поэтому так важно управлять доступом к папке возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="b2c17-210">This is why controlling access to the role capabilities folder is so important.</span></span>
<span data-ttu-id="b2c17-211">Изменять файлы возможностей ролей должно быть разрешено только наиболее надежным администраторам.</span><span class="sxs-lookup"><span data-stu-id="b2c17-211">Only highly trusted administrators should be able to change role capability files.</span></span>
<span data-ttu-id="b2c17-212">Если пользователь, не являющийся доверенным, может изменять файлы возможностей ролей, он легко сможет получить доступ к командлетам, повышающим его права.</span><span class="sxs-lookup"><span data-stu-id="b2c17-212">If an untrusted user can change role capability files, they can easily give themselves access to cmdlets which allow them to elevate their privileges.</span></span>


<span data-ttu-id="b2c17-213">Администраторам, желающим заблокировать доступ к возможностям ролей, следует убедиться, что учетная запись Local System имеет доступ на чтение к файлам возможностей ролей и содержащим их модулям.</span><span class="sxs-lookup"><span data-stu-id="b2c17-213">For administrators looking to lock down access to the role capabilities, ensure Local System has read access to the role capability files and containing modules.</span></span>

## <a name="how-role-capabilities-are-merged"></a><span data-ttu-id="b2c17-214">Способ слияния возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="b2c17-214">How role capabilities are merged</span></span>

<span data-ttu-id="b2c17-215">При входе в сеанс JEA пользователям может предоставляться доступ к нескольким возможностям ролей в зависимости от сопоставлений ролей в [файле конфигурации сеанса](session-configurations.md).</span><span class="sxs-lookup"><span data-stu-id="b2c17-215">Users can be granted access to multiple role capabilities when they enter a JEA session depending on the role mappings in the [session configuration file](session-configurations.md).</span></span>
<span data-ttu-id="b2c17-216">В этом случае JEA пытается предоставить такому пользователю *наиболее широкий* набор команд, разрешенных для любой из этих ролей.</span><span class="sxs-lookup"><span data-stu-id="b2c17-216">When this happens, JEA tries to give the user the *most permissive* set of commands allowed by any of the roles.</span></span>

<span data-ttu-id="b2c17-217">**VisibleCmdlets и VisibleFunctions**</span><span class="sxs-lookup"><span data-stu-id="b2c17-217">**VisibleCmdlets and VisibleFunctions**</span></span>

<span data-ttu-id="b2c17-218">Наиболее сложная логика слияния затрагивает командлеты и функции, параметры и значения параметров которых могут быть ограничены в JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-218">The most complex merge logic affects cmdlets and functions, which can have their parameters and parameter values limited in JEA.</span></span>

<span data-ttu-id="b2c17-219">Действуют следующие правила:</span><span class="sxs-lookup"><span data-stu-id="b2c17-219">The rules are as follows:</span></span>

1. <span data-ttu-id="b2c17-220">Если командлет является видимым всего в одной роли, он отображается для пользователя с любыми применимыми ограничениями параметров.</span><span class="sxs-lookup"><span data-stu-id="b2c17-220">If a cmdlet is only made visible in one role, it will be visible to the user with any applicable parameter constraints.</span></span>
2. <span data-ttu-id="b2c17-221">Если командлет является видимым в нескольких ролях, каждая из которых налагает на него схожие ограничения, он отображается пользователю с такими ограничениями.</span><span class="sxs-lookup"><span data-stu-id="b2c17-221">If a cmdlet is made visible in more than one role, and each role has the same constraints on the cmdlet, the cmdlet will be visible to the user with those constraints.</span></span>
3. <span data-ttu-id="b2c17-222">Если командлет является видимым в нескольких ролях, каждая из которых разрешает иной набор параметров, пользователю отображается как командлет, так и все параметры, определенные для каждой роли.</span><span class="sxs-lookup"><span data-stu-id="b2c17-222">If a cmdlet is made visible in more than one role, and each role allows a different set of parameters, the cmdlet and all of the parameters defined across every role will be visible to the user.</span></span> <span data-ttu-id="b2c17-223">Если одна роль не имеет ограничений для параметров, будет разрешены все параметры.</span><span class="sxs-lookup"><span data-stu-id="b2c17-223">If one role doesn't have constraints on the parameters, all parameters will be allowed.</span></span>
4. <span data-ttu-id="b2c17-224">Если одна роль определяет набор или шаблон проверок для параметра командлета, а другая разрешает параметр, но не ограничивает его значения, набор или шаблон проверок будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="b2c17-224">If one role defines a validate set or validate pattern for a cmdlet parameter, and the other role allows the parameter but does not constrain the parameter values, the validate set or pattern will be ignored.</span></span>
5. <span data-ttu-id="b2c17-225">Если набор проверок определен для одного параметра командлета в нескольких ролях, все значения из всех наборов проверок будут разрешены.</span><span class="sxs-lookup"><span data-stu-id="b2c17-225">If a validate set is defined for the same cmdlet parameter in more than one role, all values from all validate sets will be allowed.</span></span>
6. <span data-ttu-id="b2c17-226">Если шаблон проверок определен для одного параметра командлета в нескольких ролях, будут разрешены все значения, соответствующие любому из шаблонов.</span><span class="sxs-lookup"><span data-stu-id="b2c17-226">If a validate pattern is defined for the same cmdlet parameter in more than one role, any values that match any of the patterns will be allowed.</span></span>
7. <span data-ttu-id="b2c17-227">Если набор проверок определен в одной или нескольких ролях и шаблон проверок определен в другой роли для того же параметра командлета, набор проверок игнорируется, а к оставшимся шаблонам проверок применяется правило (6).</span><span class="sxs-lookup"><span data-stu-id="b2c17-227">If a validate set is defined in one or more roles, and a validate pattern is defined in another role for the same cmdlet parameter, the validate set is ignored and rule (6) applies to the remaining validate patterns.</span></span>

<span data-ttu-id="b2c17-228">Ниже приведен пример объединения ролей согласно этим правилам:</span><span class="sxs-lookup"><span data-stu-id="b2c17-228">Below is an example of how roles are merged according to these rules:</span></span>

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service'; Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permisisons for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service is ignored becuase of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```



<span data-ttu-id="b2c17-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span><span class="sxs-lookup"><span data-stu-id="b2c17-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span></span>

<span data-ttu-id="b2c17-230">Все другие поля в файле роли возможностей ролей просто добавляются в совокупный набор допустимых внешних команд, псевдонимов, поставщиков и сценариев запуска.</span><span class="sxs-lookup"><span data-stu-id="b2c17-230">All other fields in the role capability file are simply added to a cumulative set of allowable external commands, aliases, providers, and startup scripts.</span></span>
<span data-ttu-id="b2c17-231">Команда, псевдоним, поставщик или сценарий, доступные в одной возможности роли, будут доступны пользователю JEA.</span><span class="sxs-lookup"><span data-stu-id="b2c17-231">Any command, alias, provider, or script available in one role capability will be available to the JEA user.</span></span>

<span data-ttu-id="b2c17-232">Внимательно следите за тем, чтобы комбинированный набор поставщиков из одной возможности роли и командлеты, функции и команды из другой не разрешали подключающимся пользователям непреднамеренный доступ к системным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="b2c17-232">Be careful to ensure that the combined set of providers from one role capability and cmdlets/functions/commands from another do not allow connecting users unintentional access to system resources.</span></span>
<span data-ttu-id="b2c17-233">Например, если одна роль разрешает командлет `Remove-Item`, а другая разрешает поставщик `FileSystem`, существует риск того, что пользователь JEA удалит произвольные файлы на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b2c17-233">For example, if one role allows the `Remove-Item` cmdlet and another allows the `FileSystem` provider, you are at risk of a JEA user deleting arbitrary files on your computer.</span></span>
<span data-ttu-id="b2c17-234">Дополнительные сведения об определении действующих разрешений пользователей см. в [разделе об аудите JEA](audit-and-report.md).</span><span class="sxs-lookup"><span data-stu-id="b2c17-234">Additional information about identifying users' effective permissions can be found in the [auditing JEA topic](audit-and-report.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2c17-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2c17-235">Next steps</span></span>

- [<span data-ttu-id="b2c17-236">Создание файла конфигурации сеанса</span><span class="sxs-lookup"><span data-stu-id="b2c17-236">Create a session configuration file</span></span>](session-configurations.md)

