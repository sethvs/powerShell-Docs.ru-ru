---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "от начала до конца — Active Directory"
ms.technology: powershell
ms.openlocfilehash: 3108f5dad96ef54feb3cf559fae38812ed46849c
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="end-to-end---active-directory"></a><span data-ttu-id="91df7-103">От начала до конца — Active Directory</span><span class="sxs-lookup"><span data-stu-id="91df7-103">End to End - Active Directory</span></span>
<span data-ttu-id="91df7-104">Допустим, область применения вашей программы расширилась.</span><span class="sxs-lookup"><span data-stu-id="91df7-104">Imagine the scope of your program has increased.</span></span>
<span data-ttu-id="91df7-105">Теперь вы отвечаете за добавление JEA на контроллеры доменов для выполнения действий Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91df7-105">You are now responsible for adding JEA to Domain Controllers to perform Active Directory actions.</span></span>
<span data-ttu-id="91df7-106">Сотрудники службы поддержки будут использовать JEA для разблокировки учетных записей, сброса паролей и других подобных действий.</span><span class="sxs-lookup"><span data-stu-id="91df7-106">The help desk people are going to use JEA to unlock accounts, reset passwords, and do other similar actions.</span></span>

<span data-ttu-id="91df7-107">Вам необходимо предоставить доступ к совершенно иному набору команд другой группе людей.</span><span class="sxs-lookup"><span data-stu-id="91df7-107">You need to expose a completely new set of commands to a different group of people.</span></span>
<span data-ttu-id="91df7-108">Кроме того, у вас есть ряд уже существующих сценариев Active Directory, доступ к которым нужно предоставить.</span><span class="sxs-lookup"><span data-stu-id="91df7-108">On top of that, you have a bunch of existing Active Directory scripts you need to expose.</span></span>
<span data-ttu-id="91df7-109">В этом разделе вы узнаете, как создать конфигурацию сеанса и возможности роли для этой задачи.</span><span class="sxs-lookup"><span data-stu-id="91df7-109">This section will walk through authoring a Session Configuration and Role Capability for this task.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91df7-110">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="91df7-110">Prerequisites</span></span>
<span data-ttu-id="91df7-111">Для выполнения пошаговых инструкций в этом разделе необходимо работать на контроллере домена.</span><span class="sxs-lookup"><span data-stu-id="91df7-111">To follow this section step-by-step, you'll need to be operating on a domain controller.</span></span>
<span data-ttu-id="91df7-112">Если у вас нет доступа к контроллеру домена, не волнуйтесь.</span><span class="sxs-lookup"><span data-stu-id="91df7-112">If you don't have access to your domain controller, don't worry.</span></span>
<span data-ttu-id="91df7-113">Попробуйте сделать то же самое, работая по другому сценарию или в другой роли, которые вам знакомы.</span><span class="sxs-lookup"><span data-stu-id="91df7-113">Try to follow along with by working against some other scenario or role with which you are familiar.</span></span>
<span data-ttu-id="91df7-114">Если необходимо быстро настроить новый контроллер домена, см. [приложение статьи "Создание контроллера домена"](.\creating-a-domain-controller.md).</span><span class="sxs-lookup"><span data-stu-id="91df7-114">If you want to quickly set up a new domain controller, check out the [Creating a Domain Controller appendix](.\creating-a-domain-controller.md).</span></span>

## <a name="steps-to-make-a-new-role-capability-and-session-configuration"></a><span data-ttu-id="91df7-115">Процедура создания возможностей роли и конфигурации сеанса</span><span class="sxs-lookup"><span data-stu-id="91df7-115">Steps to Make a new Role Capability and Session Configuration</span></span>

<span data-ttu-id="91df7-116">На первый взгляд создание возможностей роли может показаться сложным, но мы разделим эту процедуру на несколько простых шагов:</span><span class="sxs-lookup"><span data-stu-id="91df7-116">Making a new role capability can seem daunting at first, but it can be broken into fairly simple steps:</span></span>

1.  <span data-ttu-id="91df7-117">Определить включаемые задачи.</span><span class="sxs-lookup"><span data-stu-id="91df7-117">Identify the tasks you need to enable</span></span>
2.  <span data-ttu-id="91df7-118">Ограничить эти задачи при необходимости.</span><span class="sxs-lookup"><span data-stu-id="91df7-118">Restrict those tasks as necessary</span></span>
3.  <span data-ttu-id="91df7-119">Убедиться, что они работают с JEA.</span><span class="sxs-lookup"><span data-stu-id="91df7-119">Confirm they work with JEA</span></span>
4.  <span data-ttu-id="91df7-120">Поместить их в файл возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="91df7-120">Put them in a Role Capability file</span></span>
5.  <span data-ttu-id="91df7-121">Зарегистрировать конфигурацию сеанса, предоставляющую возможности роли.</span><span class="sxs-lookup"><span data-stu-id="91df7-121">Register a Session Configuration that exposes that Role Capability</span></span>

## <a name="step-1-identify-what-needs-to-be-exposed"></a><span data-ttu-id="91df7-122">Шаг 1. Определение необходимых задач</span><span class="sxs-lookup"><span data-stu-id="91df7-122">Step 1: Identify What Needs to Be Exposed</span></span>
<span data-ttu-id="91df7-123">Прежде чем создавать возможности роли или конфигурацию сеанса, необходимо определить все задачи, которые пользователи должны будут выполнять через конечную точку JEA, а также порядок их выполнения с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91df7-123">Before you make a new Role Capability or Session Configuration, you need to identify all of the things users will need to do through the JEA endpoint, as well as how to do them through PowerShell.</span></span>
<span data-ttu-id="91df7-124">Для этого необходимо провести большую работу по сбору и изучению требований.</span><span class="sxs-lookup"><span data-stu-id="91df7-124">This will involve a fair amount of requirement gathering and research.</span></span>
<span data-ttu-id="91df7-125">То, как вы будете это делать, зависит от вашей организации и целей.</span><span class="sxs-lookup"><span data-stu-id="91df7-125">How you go about this process will depend on your organization and goals.</span></span>
<span data-ttu-id="91df7-126">Важно понимать, что на практике сбор и анализ требований составляют критически важную часть работы.</span><span class="sxs-lookup"><span data-stu-id="91df7-126">It is important to call out requirement gathering and research as a critical part of the real world process.</span></span>
<span data-ttu-id="91df7-127">Это, вероятно, самый сложный этап в процессе внедрения JEA.</span><span class="sxs-lookup"><span data-stu-id="91df7-127">This may be the most difficult step in the process of adopting JEA.</span></span>

### <a name="find-resources"></a><span data-ttu-id="91df7-128">Поиск ресурсов</span><span class="sxs-lookup"><span data-stu-id="91df7-128">Find Resources</span></span>
<span data-ttu-id="91df7-129">Во время исследовательской работы при создании конечной точки управления Active Directory вам могут пригодиться следующие интернет-ресурсы:</span><span class="sxs-lookup"><span data-stu-id="91df7-129">Here is a set of online resources that might have come up in your research on creating an Active Directory management endpoint:</span></span>
-   [<span data-ttu-id="91df7-130">Обзор Active Directory PowerShell</span><span class="sxs-lookup"><span data-stu-id="91df7-130">Active Directory PowerShell Overview</span></span>](http://blogs.msdn.com/b/adpowershell/archive/2009/03/05/active-directory-powershell-overview.aspx)
-   [<span data-ttu-id="91df7-131">Руководство по PowerShell для Active Directory</span><span class="sxs-lookup"><span data-stu-id="91df7-131">CMD to PowerShell Guide for Active Directory</span></span>](http://blogs.technet.com/b/ashleymcglone/archive/2013/01/02/free-download-cmd-to-powershell-guide-for-ad.aspx)

### <a name="make-a-list"></a><span data-ttu-id="91df7-132">Составление списка</span><span class="sxs-lookup"><span data-stu-id="91df7-132">Make a List</span></span>
<span data-ttu-id="91df7-133">В остальной части этого раздела вы будете работать с указанными ниже десятью действиями.</span><span class="sxs-lookup"><span data-stu-id="91df7-133">Here is a set of ten actions that you will be working from in the remainder of this section.</span></span>
<span data-ttu-id="91df7-134">Помните, что это просто пример, и требования вашей организации могут отличаться:</span><span class="sxs-lookup"><span data-stu-id="91df7-134">Keep in mind this is simply an example, your organizations requirements may be different:</span></span>

|<span data-ttu-id="91df7-135">Действие</span><span class="sxs-lookup"><span data-stu-id="91df7-135">Action</span></span>                                                         |<span data-ttu-id="91df7-136">Команда PowerShell</span><span class="sxs-lookup"><span data-stu-id="91df7-136">PowerShell Command</span></span>                                             |
|---------------------------------------------------------------|---------------------------------------------------------------|
|<span data-ttu-id="91df7-137">Разблокирование учетной записи</span><span class="sxs-lookup"><span data-stu-id="91df7-137">Account Unlock</span></span>                                                 |`Unlock-ADAccount`                                             |
|<span data-ttu-id="91df7-138">Сброс пароля</span><span class="sxs-lookup"><span data-stu-id="91df7-138">Password Reset</span></span>                                                 |<span data-ttu-id="91df7-139">`Set-ADAccountPassword` и `Set-ADUser -ChangePasswordAtLogon`</span><span class="sxs-lookup"><span data-stu-id="91df7-139">`Set-ADAccountPassword` and `Set-ADUser -ChangePasswordAtLogon`</span></span>|
|<span data-ttu-id="91df7-140">Изменение должности пользователя</span><span class="sxs-lookup"><span data-stu-id="91df7-140">Change a User's Title</span></span>                                          |`Set-ADUser -Title`                                            |  
|<span data-ttu-id="91df7-141">Поиск заблокированных, отключенных, неактивных и других учетных записей AD</span><span class="sxs-lookup"><span data-stu-id="91df7-141">Find AD Accounts that are locked out, disabled, inactive, etc.</span></span> |`Search-ADAccount`                                             |
|<span data-ttu-id="91df7-142">Добавление пользователя в группу</span><span class="sxs-lookup"><span data-stu-id="91df7-142">Add User to Group</span></span>                                              |`Add-ADGroupMember -Identity (with whitelist) -Members`        |
|<span data-ttu-id="91df7-143">Удаление пользователя из группы</span><span class="sxs-lookup"><span data-stu-id="91df7-143">Remove User from Group</span></span>                                         |`Remove-ADGroupMember -Identity (with whitelist) -Members`     |
|<span data-ttu-id="91df7-144">Включение учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="91df7-144">Enable a user account</span></span>                                          |`Enable-ADAccount`                                             |
|<span data-ttu-id="91df7-145">Удаление учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="91df7-145">Disable a user account</span></span>                                         |`Disable-ADAccount`                                            |

## <a name="step-2-restrict-tasks-as-necessary"></a><span data-ttu-id="91df7-146">Шаг 2. Ограничение задач при необходимости</span><span class="sxs-lookup"><span data-stu-id="91df7-146">Step 2: Restrict Tasks as Necessary</span></span>

<span data-ttu-id="91df7-147">Теперь, когда у вас есть список действий, продумайте возможности каждой команды.</span><span class="sxs-lookup"><span data-stu-id="91df7-147">Now that you have your list of actions, you need to think through the capabilities of each command.</span></span>
<span data-ttu-id="91df7-148">Это нужно сделать по двум причинам.</span><span class="sxs-lookup"><span data-stu-id="91df7-148">There are two important reasons to do this:</span></span>

1.  <span data-ttu-id="91df7-149">Пользователям очень легко предоставить больше возможностей, чем планировалось.</span><span class="sxs-lookup"><span data-stu-id="91df7-149">It is easy to give users more capabilities than you intend.</span></span>
<span data-ttu-id="91df7-150">Например, `Set-ADUser` — невероятно мощная и гибкая команда.</span><span class="sxs-lookup"><span data-stu-id="91df7-150">For example, `Set-ADUser` is an incredibly powerful and flexible command.</span></span>
<span data-ttu-id="91df7-151">Не все ее возможности стоит предоставлять пользователям службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="91df7-151">You may not want to expose everything it can do to help desk users.</span></span>  

2.  <span data-ttu-id="91df7-152">Хуже того, существует возможность предоставлять доступ к командам, позволяющим пользователям обходить ограничения JEA.</span><span class="sxs-lookup"><span data-stu-id="91df7-152">Even worse, it's possible to expose commands that allow users to escape JEA's restrictions.</span></span>
<span data-ttu-id="91df7-153">В этом случае JEA перестает служить рубежом безопасности.</span><span class="sxs-lookup"><span data-stu-id="91df7-153">If this happens, JEA ceases to function as a security boundary.</span></span>
<span data-ttu-id="91df7-154">Будьте внимательны при выборе команд.</span><span class="sxs-lookup"><span data-stu-id="91df7-154">Please be careful when selecting commands.</span></span>
<span data-ttu-id="91df7-155">Например, команда Invoke-Expression позволит пользователям выполнять код без ограничений.</span><span class="sxs-lookup"><span data-stu-id="91df7-155">For example, Invoke-Expression will allow users to run unrestricted code.</span></span>
<span data-ttu-id="91df7-156">Дополнительное обсуждение этой темы см. в разделе "Рекомендации по ограничению команд".</span><span class="sxs-lookup"><span data-stu-id="91df7-156">For more discussion on this topic, check out the Considerations When Restricting Commands section.</span></span>

<span data-ttu-id="91df7-157">Просмотрев все команды, вы можете добавить следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="91df7-157">After reviewing each command, you decide to restrict the following:</span></span>

1.  <span data-ttu-id="91df7-158">`Set-ADUser` может выполняться только с параметром "-Title";</span><span class="sxs-lookup"><span data-stu-id="91df7-158">`Set-ADUser` should only be allowed to run with the -Title parameter</span></span>

2.  <span data-ttu-id="91df7-159">`Add-ADGroupMember` и `Remove-ADGroupMember` могут работать только с определенными группами.</span><span class="sxs-lookup"><span data-stu-id="91df7-159">`Add-ADGroupMember` and `Remove-ADGroupMember` should only work with certain groups</span></span>

### <a name="step-3-confirm-the-tasks-work-with-jea"></a><span data-ttu-id="91df7-160">Шаг 3. Контроль работы задач с JEA</span><span class="sxs-lookup"><span data-stu-id="91df7-160">Step 3: Confirm the Tasks Work with JEA</span></span>
<span data-ttu-id="91df7-161">Фактически в ограниченной среде JEA эти командлеты можно оптимизировать.</span><span class="sxs-lookup"><span data-stu-id="91df7-161">Actually using those cmdlets may not be straightforward in the restricted JEA environment.</span></span>
<span data-ttu-id="91df7-162">JEA выполняется в режиме *NoLanguage*, что, помимо прочего, не дает пользователям применять переменные.</span><span class="sxs-lookup"><span data-stu-id="91df7-162">JEA runs in *NoLanguage* mode which, among other things, prevents users from using variables.</span></span>
<span data-ttu-id="91df7-163">Для удобства конечных пользователей необходимо проверить несколько моментов.</span><span class="sxs-lookup"><span data-stu-id="91df7-163">In order to ensure that end users have a smooth experience, it's important to check for a few things.</span></span>

<span data-ttu-id="91df7-164">Возьмем, например, команду `Set-ADAccountPassword`.</span><span class="sxs-lookup"><span data-stu-id="91df7-164">As an example, consider `Set-ADAccountPassword`.</span></span>
<span data-ttu-id="91df7-165">Параметр -NewPassword требует защищенной строки.</span><span class="sxs-lookup"><span data-stu-id="91df7-165">The -NewPassword parameter requires a secure string.</span></span>
<span data-ttu-id="91df7-166">Часто пользователи создают защищенную строку и передают ее как переменную (как показано ниже):</span><span class="sxs-lookup"><span data-stu-id="91df7-166">Often, users create a secure string and pass it in as a variable (as below):</span></span>

```PowerShell
$newPassword = Read-Host -Prompt "Specify a new password" -AsSecureString
Set-ADAccountPassword -Identity mollyd -NewPassword $newPassword -Reset
```

<span data-ttu-id="91df7-167">Но режим *NoLanguage* не позволяет использовать переменные.</span><span class="sxs-lookup"><span data-stu-id="91df7-167">However, *NoLanguage* mode prevents the usage of variables.</span></span>
<span data-ttu-id="91df7-168">Это ограничение можно обойти двумя способами.</span><span class="sxs-lookup"><span data-stu-id="91df7-168">You can get around this restriction in two ways:</span></span>

1.  <span data-ttu-id="91df7-169">Вы можете потребовать, чтобы пользователи выполняли команду без назначения переменных.</span><span class="sxs-lookup"><span data-stu-id="91df7-169">You can require users run the command without assigning variables.</span></span>
<span data-ttu-id="91df7-170">Сделать это легко, но операторам будет крайне затруднительно работать с конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="91df7-170">This is easy to configure, but can be painful for the operators using the endpoint.</span></span>
<span data-ttu-id="91df7-171">Кто захочет вводить эти данные каждый раз при сбросе пароля?</span><span class="sxs-lookup"><span data-stu-id="91df7-171">Who wants to type this out every time you reset a password?</span></span>
```PowerShell
Set-ADAccountPassword -Identity mollyd -NewPassword (Read-Host -Prompt "Specify a new password" -AsSecureString) -Reset
```

2.  <span data-ttu-id="91df7-172">Сложный код можно заключить в сценарий или функцию, которые будут предоставлены конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="91df7-172">You can wrap the complexity in a script or a function that you expose to end users.</span></span>
<span data-ttu-id="91df7-173">Предоставленные сценарии и функции будут выполняться в неограниченном контексте; вы можете написать функции, которые будут использовать переменные и вызывать другие команды без каких-либо трудностей.</span><span class="sxs-lookup"><span data-stu-id="91df7-173">Scripts and functions that you expose run in an unrestricted context; you can write functions that use variables and call other commands without any issue.</span></span>
<span data-ttu-id="91df7-174">Такой подход упрощает работу пользователя, предотвращает ошибки, сокращает необходимую степень понимания PowerShell и препятствует непреднамеренному предоставлению доступа к лишним функциям.</span><span class="sxs-lookup"><span data-stu-id="91df7-174">This approach simplifies the end user experience, prevents errors, reduces required PowerShell knowledge, and reduces unintentionally exposing excess functionality.</span></span>
<span data-ttu-id="91df7-175">Единственный недостаток — стоимость разработки и обслуживания функции.</span><span class="sxs-lookup"><span data-stu-id="91df7-175">The only downside is the cost of authoring and maintaining the function.</span></span>

### <a name="aside-adding-a-function-to-your-module"></a><span data-ttu-id="91df7-176">Шаг в сторону: добавление функции в модуль</span><span class="sxs-lookup"><span data-stu-id="91df7-176">Aside: Adding a Function to your Module</span></span>
<span data-ttu-id="91df7-177">Выберем второй подход и напишем функцию PowerShell `Reset-ContosoUserPassword`.</span><span class="sxs-lookup"><span data-stu-id="91df7-177">Taking approach #2, you are going to write a PowerShell function called `Reset-ContosoUserPassword`.</span></span>
<span data-ttu-id="91df7-178">Эта функция будет делать все, что должно происходить при сбросе пароля пользователя.</span><span class="sxs-lookup"><span data-stu-id="91df7-178">This function is going to do everything that needs to happen when you reset a user's password.</span></span>
<span data-ttu-id="91df7-179">В вашей организации она может включать сложные, замысловатые действия.</span><span class="sxs-lookup"><span data-stu-id="91df7-179">In your organization, this may involve doing fancy and complicated things.</span></span>
<span data-ttu-id="91df7-180">Так как это лишь пример, ваша команда сбросит пароль и потребует, чтобы пользователь изменил пароль при входе в систему.</span><span class="sxs-lookup"><span data-stu-id="91df7-180">Because this is just an example, your command will just reset the password and require the user change the password at logon.</span></span>
<span data-ttu-id="91df7-181">Мы добавим ее в модуль Contoso_AD_Module, который вы создали в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="91df7-181">We will put it in the Contoso_AD_Module module you made in the last section.</span></span>

1. <span data-ttu-id="91df7-182">В интегрированной среде сценариев PowerShell откройте файл Contoso_AD_Module.psm1.</span><span class="sxs-lookup"><span data-stu-id="91df7-182">In PowerShell ISE, open "Contoso_AD_Module.psm1"</span></span>
```PowerShell
ise 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\Contoso_AD_Module.psm1'
```

2. <span data-ttu-id="91df7-183">Нажмите клавиши CTRL+J, чтобы открыть меню фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="91df7-183">Press Crtl+J to open the snippets menu.</span></span>

3. <span data-ttu-id="91df7-184">Найдите в списке слово "функция" и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="91df7-184">Key down until you find "function" and press enter.</span></span>
<span data-ttu-id="91df7-185">Будет создан каркас для функции.</span><span class="sxs-lookup"><span data-stu-id="91df7-185">This puts up a super basic skeleton of a function.</span></span>

4. <span data-ttu-id="91df7-186">Измените имя функции на Reset-ContosoUserPassword.</span><span class="sxs-lookup"><span data-stu-id="91df7-186">Rename the function "Reset-ContosoUserPassword".</span></span>  

5. <span data-ttu-id="91df7-187">Измените имя одного из параметров на Identity и удалите второй.</span><span class="sxs-lookup"><span data-stu-id="91df7-187">Rename one of the parameters "Identity" and delete the second.</span></span>

6. <span data-ttu-id="91df7-188">Скопируйте следующий код в тело функции.</span><span class="sxs-lookup"><span data-stu-id="91df7-188">Copy the following into the body of the function.</span></span>
```PowerShell
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
```

7. <span data-ttu-id="91df7-189">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="91df7-189">Save the file.</span></span>
<span data-ttu-id="91df7-190">Должен получиться код следующего вида:</span><span class="sxs-lookup"><span data-stu-id="91df7-190">You should end up with something that looks like this:</span></span>
```PowerShell
function Reset-ContosoUserPassword ($Identity)
{
# Get the new password
$NewPassword = Read-Host -Prompt "Enter a new password" -AsSecureString
# Reset the password
Set-ADAccountPassword -Identity $Identity -NewPassword $NewPassword -Reset
# Require the user to reset at next logon
Set-ADUser -Identity $Identity -ChangePasswordAtLogon
}
```
<span data-ttu-id="91df7-191">Теперь пользователи смогут просто вызвать команду `Reset-ContosoUserPassword` — им не придется запоминать синтаксис для создания безопасной строки.</span><span class="sxs-lookup"><span data-stu-id="91df7-191">Now, your users can simply call `Reset-ContosoUserPassword` and not have to remember the syntax to create a secure string inline.</span></span>

## <a name="step-4-edit-the-role-capability-file"></a><span data-ttu-id="91df7-192">Шаг 4. Изменение файла с возможностями роли</span><span class="sxs-lookup"><span data-stu-id="91df7-192">Step 4: Edit the Role Capability File</span></span>
<span data-ttu-id="91df7-193">В разделе [Создание возможности роли](./role-capabilities.md#role-capability-creation) был создан пустой файл возможности роли.</span><span class="sxs-lookup"><span data-stu-id="91df7-193">In the [Role Capability Creation](./role-capabilities.md#role-capability-creation) section, you created a blank Role Capability file.</span></span>
<span data-ttu-id="91df7-194">В этом разделе мы заполним его значениями.</span><span class="sxs-lookup"><span data-stu-id="91df7-194">In this section, you will fill in the values in that file.</span></span>

<span data-ttu-id="91df7-195">Сначала откройте файл возможностей роли в интегрированной среде сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91df7-195">Start by opening the role capability file in PowerShell ISE.</span></span>
```PowerShell
ise 'C:\Program Files\WindowsPowerShell\Modules\Contoso_AD_Module\RoleCapabilities\ADHelpDesk.psrc'
```
<span data-ttu-id="91df7-196">Внесите в файл следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="91df7-196">Update the file with the following changes:</span></span>
```PowerShell
# OLD: VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }
VisibleCmdlets =
    'Unlock-ADAccount',
    'Search-ADAccount',
    'Enable-ADAccount',
    'Disable-ADAccount',
    @{ Name = 'Set-ADUser'; Parameters = @{ Name = 'Title'; ValidateSet = 'Manager', 'Engineer' }},
    @{ Name = 'Add-ADGroupMember'; Parameters =
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}},
    @{ Name = 'Remove-ADGroupMember'; Parameters =
        @{Name = 'Identity'; ValidateSet = 'TestGroup'},
        @{Name = 'Members'}}

# OLD: VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }
VisibleFunctions = 'Reset-ContosoUserPassword'
```

<span data-ttu-id="91df7-197">При этом необходимо обратить внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="91df7-197">There are a few things to note about the above:</span></span>
1.  <span data-ttu-id="91df7-198">PowerShell попытается автоматически загрузить модули, необходимые для ваших возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="91df7-198">PowerShell will attempt to auto-load the modules needed for your Role Capability.</span></span>
<span data-ttu-id="91df7-199">Если этого не происходит, явно перечислите имена модулей в поле "ModulesToImport".</span><span class="sxs-lookup"><span data-stu-id="91df7-199">You may need to explicitly list module names in the "ModulesToImport" field if you notice problems with a module not being autoloaded.</span></span>

2.  <span data-ttu-id="91df7-200">Если вы не уверены, является ли команда командлетом или функцией, выполните `Get-Command` и проверьте свойство CommandType.</span><span class="sxs-lookup"><span data-stu-id="91df7-200">If you aren't sure if a command is a cmdlet or a function, run `Get-Command` and look at the "CommandType" property</span></span>

3.  <span data-ttu-id="91df7-201">ValidatePattern позволяет ограничить аргументы параметра с помощью регулярного выражения, если определить набор допустимых значений непросто.</span><span class="sxs-lookup"><span data-stu-id="91df7-201">The ValidatePattern allows you to use a regular expression to restrict parameter arguments if it is not easy to define a set of allowable values.</span></span>
<span data-ttu-id="91df7-202">Определить ValidatePattern и ValidateSet для отдельного параметра одновременно невозможно.</span><span class="sxs-lookup"><span data-stu-id="91df7-202">You cannot define both a ValidatePattern and ValidateSet for a single parameter.</span></span>

## <a name="step-5-register-a-new-session-configuration"></a><span data-ttu-id="91df7-203">Шаг 5. Регистрация новой конфигурации сеанса</span><span class="sxs-lookup"><span data-stu-id="91df7-203">Step 5: Register a new Session Configuration</span></span>
<span data-ttu-id="91df7-204">Далее создадим новый файл конфигурации сеанса, который будет предоставлять возможности роли членам группы AD "JEA_NonAdmin_HelpDesk".</span><span class="sxs-lookup"><span data-stu-id="91df7-204">Next, you will create a new session configuration file that will expose your Role Capability to members of the "JEA_NonAdmin_HelpDesk" AD group.</span></span>

<span data-ttu-id="91df7-205">Для начала создайте и откройте пустой файл конфигурации сеанса в интегрированной среде сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91df7-205">Start by creating and opening a new blank Session Configuration file in PowerShell ISE.</span></span>
```PowerShell
New-PSSessionConfigurationFile -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
ise "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
```
<span data-ttu-id="91df7-206">Измените значения следующих полей в PSSC-файле.</span><span class="sxs-lookup"><span data-stu-id="91df7-206">Modify the following fields in the PSSC file.</span></span>
<span data-ttu-id="91df7-207">Если вы работаете в собственной среде, замените "CONTOSO\JEA_NonAdmins_Helpdesk" на имя собственного пользователя или группы без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="91df7-207">If you are working in your own environment, you should replace "CONTOSO\JEA_NonAdmins_Helpdesk" with your own non-administrator user or group.</span></span>
```PowerShell
# OLD: Description = ''
Description = 'An endpoint for Active Directory tasks.'

# OLD: SessionType = 'Default'
SessionType = 'RestrictedRemoteServer'

# OLD: TranscriptDirectory = 'C:\Transcripts\'
TranscriptDirectory = "C:\ProgramData\JEAConfiguration\Transcripts"

# OLD: RunAsVirtualAccount = $true
RunAsVirtualAccount = $true

# OLD: RoleDefinitions = @{ 'CONTOSO\SqlAdmins' = @{ RoleCapabilities = 'SqlAdministration' }; 'CONTOSO\ServerMonitors' = @{ VisibleCmdlets = 'Get-Process' } }
RoleDefinitions = @{ 'CONTOSO\JEA_NonAdmin_HelpDesk' = @{ RoleCapabilities =  'ADHelpDesk' }}
```
<span data-ttu-id="91df7-208">Сохранение и регистрация конфигурации сеанса</span><span class="sxs-lookup"><span data-stu-id="91df7-208">Save and register the Session Configuration</span></span>
```PowerShell
Register-PSSessionConfiguration -Name ADHelpDesk -Path "$env:ProgramData\JEAConfiguration\HelpDeskDemo.pssc"
```
## <a name="test-it-out"></a><span data-ttu-id="91df7-209">Тестирование</span><span class="sxs-lookup"><span data-stu-id="91df7-209">Test It Out!</span></span>
<span data-ttu-id="91df7-210">Получите учетные данные пользователя без прав администратора:</span><span class="sxs-lookup"><span data-stu-id="91df7-210">Get your non-administrator user credentials:</span></span>
```PowerShell
$HelpDeskCred = Get-Credential
```
<span data-ttu-id="91df7-211">Если вы выполнили указания из раздела [Настройка пользователей и групп](creating-a-domain-controller.md#set-up-users-and-groups), это будут следующие учетные данные:</span><span class="sxs-lookup"><span data-stu-id="91df7-211">If you followed the [Set Up Users and Groups](creating-a-domain-controller.md#set-up-users-and-groups) section, the credentials will be:</span></span>
-   <span data-ttu-id="91df7-212">Имя пользователя: HelpDeskUser</span><span class="sxs-lookup"><span data-stu-id="91df7-212">Username = "HelpDeskUser"</span></span>
-   <span data-ttu-id="91df7-213">Пароль: pa$$w0rd</span><span class="sxs-lookup"><span data-stu-id="91df7-213">Password = "pa$$w0rd"</span></span>

<span data-ttu-id="91df7-214">Установите удаленное подключение к конечной точке ADHelpdesk, используя учетные данные без прав администратора:</span><span class="sxs-lookup"><span data-stu-id="91df7-214">Remote into the ADHelpdesk endpoint using the non-admin credential:</span></span>
```PowerShell
Enter-PSSession -ComputerName . -ConfigurationName ADHelpDesk -Credential $HelpDeskCred
```
<span data-ttu-id="91df7-215">Используйте команду Set-ADUser для сброса должности пользователя.</span><span class="sxs-lookup"><span data-stu-id="91df7-215">Use Set-ADUser to reset a user's title.</span></span>
```PowerShell
Set-ADUser -Identity OperatorUser -Title Engineer
```
<span data-ttu-id="91df7-216">Убедитесь, что должность изменилась.</span><span class="sxs-lookup"><span data-stu-id="91df7-216">Verify that the title has changed.</span></span>
```PowerShell
Get-ADUser -Identity OperatorUser -Property Title
```
<span data-ttu-id="91df7-217">Теперь используйте команду Add-ADGroupMember, чтобы добавить пользователя в TestGroup.</span><span class="sxs-lookup"><span data-stu-id="91df7-217">Now, use Add-ADGroupMember to add a user to the TestGroup.</span></span>
<span data-ttu-id="91df7-218">Примечание. Группа TestGroup должна быть создана заранее.</span><span class="sxs-lookup"><span data-stu-id="91df7-218">Note: make sure you've created the TestGroup beforehand.</span></span>
```PowerShell
Add-ADGroupMember TestGroup -Member OperatorUser -Verbose
```
<span data-ttu-id="91df7-219">Завершите сеанс:</span><span class="sxs-lookup"><span data-stu-id="91df7-219">Exit the session:</span></span>
```PowerShell
Exit-PSSession
```
## <a name="key-concepts"></a><span data-ttu-id="91df7-220">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="91df7-220">Key Concepts</span></span>
<span data-ttu-id="91df7-221">**Режим без языка**: когда PowerShell работает в режиме без языка (NoLanguage), пользователи могут выполнять только команды, но не могут использовать какие-либо элементы языка.</span><span class="sxs-lookup"><span data-stu-id="91df7-221">**NoLanguage Mode**: When PowerShell is in "NoLanguage" mode, users may only run commands; they cannot use any language elements.</span></span>
<span data-ttu-id="91df7-222">Чтобы получить дополнительные сведения, запустите `Get-Help about_Language_Modes`.</span><span class="sxs-lookup"><span data-stu-id="91df7-222">For more information, run `Get-Help about_Language_Modes`.</span></span>

<span data-ttu-id="91df7-223">**Функции PowerShell**: функции PowerShell — это элементы кода PowerShell, которые можно вызывать по имени.</span><span class="sxs-lookup"><span data-stu-id="91df7-223">**PowerShell Functions**: PowerShell functions are bits of PowerShell code that you can call by name.</span></span>
<span data-ttu-id="91df7-224">Чтобы получить дополнительные сведения, запустите `Get-Help about_Functions`.</span><span class="sxs-lookup"><span data-stu-id="91df7-224">For more information, run `Get-Help about_Functions`.</span></span>

<span data-ttu-id="91df7-225">**ValidateSet или ValidatePattern**: предоставляя доступ к команде, вы можете ограничить действительные аргументы для определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="91df7-225">**ValidateSet/ValidatePattern**: When exposing a command, you can restrict valid arguments for specific parameters.</span></span>
<span data-ttu-id="91df7-226">ValidateSet — это конкретный список допустимых аргументов.</span><span class="sxs-lookup"><span data-stu-id="91df7-226">A ValidateSet is a specific list of valid arguments.</span></span>
<span data-ttu-id="91df7-227">ValidatePattern — это регулярное выражение, которому должны соответствовать аргументы для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="91df7-227">A ValidatePattern is a regular expression that the arguments for that parameter must match.</span></span>

