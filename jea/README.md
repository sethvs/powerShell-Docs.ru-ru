---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "файл README"
ms.technology: powershell
ms.openlocfilehash: b0ef4ff685b82e1a4e9ab83a45736720df7b39a2
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="just-enough-administration"></a><span data-ttu-id="afd1a-103">Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="afd1a-103">Just Enough Administration</span></span>
<span data-ttu-id="afd1a-104">Just Enough Administration (JEA) — это технология безопасности, позволяющая делегировать администрирование в отношении всего, чем можно управлять через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd1a-104">Just Enough Administration (JEA) is a security technology that enables delegated administration for anything that can be managed with PowerShell.</span></span>
<span data-ttu-id="afd1a-105">JEA позволяет сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="afd1a-105">With JEA, you can:</span></span>
- <span data-ttu-id="afd1a-106">**Уменьшить число администраторов на компьютерах**, используя виртуальные учетные записи, которые допускают выполнение привилегированных действий от имени обычных пользователей.</span><span class="sxs-lookup"><span data-stu-id="afd1a-106">**Reduce the number of administrators on your machines** by leveraging virtual accounts that perform privileged actions on behalf of regular users.</span></span>
- <span data-ttu-id="afd1a-107">**Ограничить доступные пользователям действия**, указав, какие командлеты, функции и внешние команды могут выполнять пользователи.</span><span class="sxs-lookup"><span data-stu-id="afd1a-107">**Limit what users can do** by specifying which cmdlets, functions, and external commands they can run.</span></span>
- <span data-ttu-id="afd1a-108">**Лучше понять, что делают ваши пользователи**, используя детализированные записи с "подсматриванием" для команд, выполняемых пользователем за время сеанса.</span><span class="sxs-lookup"><span data-stu-id="afd1a-108">**Better understand what your users are doing** with "over the shoulder" transcriptions that show you exactly what commands a user executed during a session.</span></span>

<span data-ttu-id="afd1a-109">**Почему это важно?**</span><span class="sxs-lookup"><span data-stu-id="afd1a-109">**Why is this important?**</span></span>  
<span data-ttu-id="afd1a-110">Рассмотрим распространенный сценарий, когда DNS-серверы размещены совместно с контроллерами домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afd1a-110">Consider the common scenario where your DNS servers are co-located with your Active Directory Domain Controllers.</span></span>
<span data-ttu-id="afd1a-111">Администраторам DNS требуются привилегии локального администратора для устранения проблем с DNS-сервером, но для этого их необходимо включить в высокопривилегированную группу безопасности администраторов домена.</span><span class="sxs-lookup"><span data-stu-id="afd1a-111">Your DNS administrators need to have local administrator privileges to fix issues with the DNS server, but in order to do so you have to make them members of the highly privileged "Domain Admins" security group.</span></span>
<span data-ttu-id="afd1a-112">При этом они получат контроль над всем доменом и доступ ко всем ресурсам на соответствующем компьютере.</span><span class="sxs-lookup"><span data-stu-id="afd1a-112">This approach effectively gives DNS Administrators control over your whole domain and access to all resources on that machine.</span></span>

<span data-ttu-id="afd1a-113">При наличии JEA вы можете настроить для администраторов DNS роль, предоставляющую им доступ только к командам, которые нужны им для работы.</span><span class="sxs-lookup"><span data-stu-id="afd1a-113">With JEA in place, you can configure a role for your DNS administrators that gives them access to all the commands they need to get their job done, but nothing more.</span></span>
<span data-ttu-id="afd1a-114">Это означает, что вы можете предоставить соответствующие права доступа для восстановления поврежденного кэша DNS без случайного предоставления прав доступа к Active Directory или на просмотр файловой системы, или на запуск потенциально опасных сценариев.</span><span class="sxs-lookup"><span data-stu-id="afd1a-114">This means you can provide the appropriate access to repair a poisoned DNS cache without unintentionally giving them rights to Active Directory, or to browse the file system, or run potentially dangerous scripts.</span></span>
<span data-ttu-id="afd1a-115">Более того, если в сеансе JEA настроено использование одноразовых привилегированных виртуальных учетных записей, ваши администраторы DNS смогут подключаться к серверу с помощью *непривилегированных* учетных данных и при этом выполнять привилегированные команды.</span><span class="sxs-lookup"><span data-stu-id="afd1a-115">Better yet, when the JEA session is configured to use one-time privileged virtual accounts, your DNS administrators can connect to the server using *unprivileged* credentials and still be able to run privileged commands.</span></span>

## <a name="availability"></a><span data-ttu-id="afd1a-116">доступность;</span><span class="sxs-lookup"><span data-stu-id="afd1a-116">Availability</span></span>
<span data-ttu-id="afd1a-117">JEA разрабатывается параллельно с будущим выпуском Windows Server 2016; в предыдущих версиях Windows эта служба доступна вместе с обновлениями Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="afd1a-117">JEA is being developed in parallel to Windows Server 2016, and is available on older versions of Windows through Windows Management Framework updates.</span></span>
<span data-ttu-id="afd1a-118">Текущая версия JEA доступна на следующих платформах:</span><span class="sxs-lookup"><span data-stu-id="afd1a-118">The current release of JEA is available on the following platforms:</span></span>

<span data-ttu-id="afd1a-119">**Windows Server**</span><span class="sxs-lookup"><span data-stu-id="afd1a-119">**Windows Server**</span></span>
- <span data-ttu-id="afd1a-120">Windows Server 2016 Technical Preview 4 и более поздние версии</span><span class="sxs-lookup"><span data-stu-id="afd1a-120">Windows Server 2016 Technical Preview 4 and higher</span></span>
- <span data-ttu-id="afd1a-121">Windows Server 2012 R2, 2012 и 2008 R2\* с установленным пакетом [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395)</span><span class="sxs-lookup"><span data-stu-id="afd1a-121">Windows Server 2012 R2, 2012, and 2008 R2\* with [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) installed</span></span>

<span data-ttu-id="afd1a-122">**Клиент Windows**</span><span class="sxs-lookup"><span data-stu-id="afd1a-122">**Windows Client**</span></span>
- <span data-ttu-id="afd1a-123">Windows 10 с установленным ноябрьским обновлением (1511)</span><span class="sxs-lookup"><span data-stu-id="afd1a-123">Windows 10 with the November Update (1511) installed</span></span>
- <span data-ttu-id="afd1a-124">Windows Server 8.1, 8 и 7\* с установленным пакетом [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395)</span><span class="sxs-lookup"><span data-stu-id="afd1a-124">Windows 8.1, 8, and 7\* with [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) installed</span></span>

<span data-ttu-id="afd1a-125">\* Поддержка виртуальных учетных записей пользователей в сеансах JEA в Windows Server 2008 R2 или Windows 7 сейчас недоступна.</span><span class="sxs-lookup"><span data-stu-id="afd1a-125">\* Support for virtual accounts in JEA sessions is currently not available on Windows Server 2008 R2 or Windows 7.</span></span>


## <a name="explore-the-experience-guide"></a><span data-ttu-id="afd1a-126">Изучите руководство по работе</span><span class="sxs-lookup"><span data-stu-id="afd1a-126">Explore the experience guide</span></span>
<span data-ttu-id="afd1a-127">Готовы узнать, как создать, развернуть и использовать собственную конечную точку JEA?</span><span class="sxs-lookup"><span data-stu-id="afd1a-127">Ready to learn how to author, deploy, and use your own JEA endpoint?</span></span>

<span data-ttu-id="afd1a-128">Это руководство поможет вам быстро начать работу с предварительно созданной конечной точкой JEA и получить представление о работе с точки зрения конечного пользователя. В нем также описано создание конечной точки с нуля, чтобы показать конфигурации сеансов и возможности ролей.</span><span class="sxs-lookup"><span data-stu-id="afd1a-128">This guide gets you started quickly with a pre-built JEA endpoint to get an idea of what the end-user experience is like, then walks you through recreating an endpoint from scratch to help demonstrate concepts like session configurations and Role Capabilities.</span></span>

1.  <span data-ttu-id="afd1a-129">[Введение](introduction.md) </span><span class="sxs-lookup"><span data-stu-id="afd1a-129">[Introduction](introduction.md) </span></span>  
<span data-ttu-id="afd1a-130">Вкратце рассмотрим, почему JEA — это важно.</span><span class="sxs-lookup"><span data-stu-id="afd1a-130">Briefly review why you should care about JEA</span></span>

2.  [<span data-ttu-id="afd1a-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="afd1a-131">Prerequisites</span></span>](prerequisites.md)  
<span data-ttu-id="afd1a-132">Настроим среду.</span><span class="sxs-lookup"><span data-stu-id="afd1a-132">Explains how to set up your environment</span></span>

3.  [<span data-ttu-id="afd1a-133">Использование JEA</span><span class="sxs-lookup"><span data-stu-id="afd1a-133">Using JEA</span></span>](using-jea.md)  
<span data-ttu-id="afd1a-134">Начнем с изучения работы оператора с JEA.</span><span class="sxs-lookup"><span data-stu-id="afd1a-134">Helps you start by understanding the operator experience of using JEA</span></span>

4.  [<span data-ttu-id="afd1a-135">Новая демоверсия</span><span class="sxs-lookup"><span data-stu-id="afd1a-135">Remake the Demo</span></span>](remake-the-demo-endpoint.md)  
<span data-ttu-id="afd1a-136">Создадим конфигурацию сеанса JEA с нуля.</span><span class="sxs-lookup"><span data-stu-id="afd1a-136">Create a JEA Session Configuration from scratch</span></span>

5.  [<span data-ttu-id="afd1a-137">Возможности ролей</span><span class="sxs-lookup"><span data-stu-id="afd1a-137">Role Capabilities</span></span>](role-capabilities.md)  
<span data-ttu-id="afd1a-138">Узнаем, как настраивать возможности JEA, используя файлы возможностей ролей.</span><span class="sxs-lookup"><span data-stu-id="afd1a-138">Learn about how to customize JEA capabilities with Role Capability Files</span></span>

6.  [<span data-ttu-id="afd1a-139">Сквозной — Active Directory</span><span class="sxs-lookup"><span data-stu-id="afd1a-139">End to End - Active Directory</span></span>](end-to-end---active-directory.md)  
<span data-ttu-id="afd1a-140">Создадим новую конечную точку для управления Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afd1a-140">Make a whole new endpoint for managing Active Directory</span></span>

7.  [<span data-ttu-id="afd1a-141">Обслуживание и развертывание на нескольких компьютерах</span><span class="sxs-lookup"><span data-stu-id="afd1a-141">Multi-machine Deployment and Maintenance</span></span>](multi-machine-deployment-and-maintenance.md)  
<span data-ttu-id="afd1a-142">Узнаем, как меняется процесс развертывания и создания при изменении масштаба.</span><span class="sxs-lookup"><span data-stu-id="afd1a-142">Discover how deployment and authoring changes with scale</span></span>

8.  [<span data-ttu-id="afd1a-143">Отчеты о JEA</span><span class="sxs-lookup"><span data-stu-id="afd1a-143">Reporting on JEA</span></span>](reporting-on-jea.md)  
<span data-ttu-id="afd1a-144">Узнаем, как вести аудит и формировать отчеты по всем действиям и инфраструктуре JEA.</span><span class="sxs-lookup"><span data-stu-id="afd1a-144">Discover how to audit and report on all JEA actions and infrastructure</span></span>

9.  <span data-ttu-id="afd1a-145">Приложения</span><span class="sxs-lookup"><span data-stu-id="afd1a-145">Appendixes</span></span>
  - [<span data-ttu-id="afd1a-146">Основные понятия, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="afd1a-146">Key Concepts Used Throughout This Guide</span></span>](key-concepts-used-throughout-this-guide.md)  
  -  [<span data-ttu-id="afd1a-147">Создание контроллера домена</span><span class="sxs-lookup"><span data-stu-id="afd1a-147">Creating a Domain Controller</span></span>](creating-a-domain-controller.md)  
  -  [<span data-ttu-id="afd1a-148">О запрещенных списках</span><span class="sxs-lookup"><span data-stu-id="afd1a-148">On Blacklisting</span></span>](on-blacklisting.md)  
  -  [<span data-ttu-id="afd1a-149">Рекомендации по ограничениям команд</span><span class="sxs-lookup"><span data-stu-id="afd1a-149">Considerations When Limiting Commands</span></span>](considerations-when-limiting-commands.md)  
  -  [<span data-ttu-id="afd1a-150">Распространенные проблемы возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="afd1a-150">Common Role Capability Pitfalls</span></span>](common-role-capability-pitfalls.md)

## <a name="start-authoring-your-own-jea-endpoints"></a><span data-ttu-id="afd1a-151">Начните создавать свои собственные конечные точки JEA</span><span class="sxs-lookup"><span data-stu-id="afd1a-151">Start authoring your own JEA endpoints</span></span>
<span data-ttu-id="afd1a-152">Создать конечную точку JEA легко — вам нужна только система с JEA и текстовый редактор (например, интегрированная среда сценариев PowerShell).</span><span class="sxs-lookup"><span data-stu-id="afd1a-152">It's easy to author a JEA endpoint -- all you need is a JEA-enabled system and a text editor (like PowerShell ISE).</span></span>
<span data-ttu-id="afd1a-153">Начать лучше всего с каркасных файлов, используя [`New-PSRoleCapabilityFile -Path <path>`](https://technet.microsoft.com/library/mt631422.aspx) и [`New-PSSessionConfigurationFile -Path <Path>`](https://technet.microsoft.com/library/mt631422.aspx) без других аргументов.</span><span class="sxs-lookup"><span data-stu-id="afd1a-153">One helpful tip to get started is to create skeleton files using [`New-PSRoleCapabilityFile -Path <path>`](https://technet.microsoft.com/library/mt631422.aspx) and [`New-PSSessionConfigurationFile -Path <Path>`](https://technet.microsoft.com/library/mt631422.aspx) without any other arguments.</span></span>
<span data-ttu-id="afd1a-154">Эти каркасные файлы содержат все необходимые поля конфигурации, а также полезные комментарии о том, для чего можно использовать каждое поле.</span><span class="sxs-lookup"><span data-stu-id="afd1a-154">These skeleton files contain all of the applicable configuration fields along with helpful comments to explain what each field can be used for.</span></span>

<span data-ttu-id="afd1a-155">Чтобы дополнительно упростить создание конечных точек JEA, воспользуйтесь [вспомогательным приложением инструментария JEA](http://blogs.technet.com/b/privatecloud/archive/2015/12/20/introducing-the-updated-jea-helper-tool.aspx), графический пользовательский интерфейс которого позволяет создавать файлы конфигурации сеансов и возможностей ролей.</span><span class="sxs-lookup"><span data-stu-id="afd1a-155">To make authoring JEA endpoints even easier, check out the [JEA Toolkit Helper](http://blogs.technet.com/b/privatecloud/archive/2015/12/20/introducing-the-updated-jea-helper-tool.aspx) which provides a GUI with which you can author Session Configuration and Role Capability files.</span></span>
<span data-ttu-id="afd1a-156">Оно поддерживает даже создание возможностей ролей на основе журналов PowerShell, позволяя начать с команд, которыми пользователи регулярно пользуются в своей работе.</span><span class="sxs-lookup"><span data-stu-id="afd1a-156">It even supports generating Role Capabilities based on PowerShell logs to start you off with the commands your users regularly run to get their jobs done.</span></span>

