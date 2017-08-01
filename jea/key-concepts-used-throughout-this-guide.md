---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "основные понятия, используемые в этом руководстве"
ms.technology: powershell
ms.openlocfilehash: 873ab19fdf43ec4ac41cc546aa94b64fbc607984
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="key-concepts-used-throughout-this-guide"></a><span data-ttu-id="d2cb7-103">Основные понятия, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="d2cb7-103">Key Concepts Used Throughout This Guide</span></span>
<span data-ttu-id="d2cb7-104">**Что такое JEA?**</span><span class="sxs-lookup"><span data-stu-id="d2cb7-104">**What exactly is JEA?**</span></span>

<span data-ttu-id="d2cb7-105">JEA — это расширение [ограниченных конечных точек](http://blogs.technet.com/b/heyscriptingguy/archive/2014/03/31/introduction-to-powershell-endpoints.aspx) PowerShell, которое добавляет определения внутри ролей, виртуальные учетные записи и ряд других улучшений, упрощающих защиту конечных точек управления.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-105">JEA is an extension of PowerShell [constrained endpoints](http://blogs.technet.com/b/heyscriptingguy/archive/2014/03/31/introduction-to-powershell-endpoints.aspx) that adds in role definitions, virtual accounts, and several other improvements to make it even easier to lock down your management endpoints.</span></span>
<span data-ttu-id="d2cb7-106">Конечная точка JEA состоит из файла конфигурации сеанса PowerShell, а также файлов возможностей ролей.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-106">A JEA endpoint consists of a PowerShell Session Configuration file and one or more Role Capability files.</span></span>

<span data-ttu-id="d2cb7-107">**Что такое файлы конфигурации сеансов и возможностей ролей?**</span><span class="sxs-lookup"><span data-stu-id="d2cb7-107">**What are Session Configuration and Role Capability files?**</span></span>

<span data-ttu-id="d2cb7-108">Файлы конфигурации сеансов PowerShell (PSSC) определяют, *кто* может подключаться к конечной точке PowerShell и *как* она будет настроена.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-108">PowerShell Session Configuration files (.pssc) define *who* can connect to a PowerShell endpoint and *how* it is configured.</span></span>
<span data-ttu-id="d2cb7-109">В этих файлах пользователи и группы безопасности сопоставляются с определенными ролями управления и настраиваются такие глобальные параметры, как виртуальные учетные записи и политики записи.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-109">This is where you would map users and security groups to specific management roles and configure global settings like virtual accounts and transcription policies.</span></span>
<span data-ttu-id="d2cb7-110">Файлы конфигурации сеансов зависят от конкретного компьютера, что позволяет вам при желании контролировать доступ отдельно на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-110">Session configuration files are specific to each machine, which allows you to control access on a per-machine basis if desired.</span></span>

<span data-ttu-id="d2cb7-111">Файлы возможностей ролей (PSRC) определяют, *что* могут делать в системе пользователи, которым назначена роль.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-111">PowerShell Role Capability files (.psrc) define *what* users belonging to a role are able to do on the system.</span></span>
<span data-ttu-id="d2cb7-112">С их помощью можно ограничить командлеты, функции, поставщики и внешние программы, доступные пользователю в сеансе JEA.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-112">Here, you can restrict which cmdlets, functions, providers, and external programs a user may use in their JEA session.</span></span>
<span data-ttu-id="d2cb7-113">Зачастую файлы возможностей ролей универсальны и не привязаны жестко к предоставляемой роли (администратор DNS, служба поддержки 1 уровня, аудит с инвентаризацией только для чтения и т. д.) и принадлежат к модулям PowerShell, что позволяет использовать их повторно в своей среде и передавать другим.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-113">Role Capability files are often generic for the role being served (DNS admin, level 1 helpdesk, read-only inventory auditing, etc.) and belong to PowerShell modules, making it easy to share them across your environment and with others.</span></span>

<span data-ttu-id="d2cb7-114">**Как JEA использует виртуальные учетные записи?**</span><span class="sxs-lookup"><span data-stu-id="d2cb7-114">**How does JEA leverage virtual accounts?**</span></span>

<span data-ttu-id="d2cb7-115">В файле конфигурации сеанса PowerShell можно настроить сеансы JEA таким образом, чтобы использовались виртуальные учетные записи запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-115">In the PowerShell Session Configuration file, you can configure JEA sessions to use virtual "run as" accounts.</span></span>
<span data-ttu-id="d2cb7-116">Виртуальные учетные записи — это одноразовые привилегированные учетные записи, создаваемые для определенного подключенного пользователя в соответствующем сеансе, в контексте которого выполняются команды пользователя.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-116">Virtual accounts are one-time privileged accounts spun up for the specific connecting user in that specific session under which context the user's commands are executed.</span></span>
<span data-ttu-id="d2cb7-117">Виртуальные учетные записи по умолчанию относятся к локальной группе безопасности "Администраторы", но при желании их можно настроить таким образом, чтобы они относились только к указанным вами группам безопасности.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-117">Virtual accounts belong to the local "Administrators" security group by default, but can optionally be configured to only belong to security groups you specify.</span></span>

<span data-ttu-id="d2cb7-118">**Удаленное взаимодействие PowerShell**: удаленное взаимодействие PowerShell позволяет выполнять команды PowerShell с удаленных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-118">**PowerShell Remoting**: PowerShell remoting allows you to run PowerShell commands against remote machines.</span></span>
<span data-ttu-id="d2cb7-119">Можно работать с одного или нескольких компьютеров и использовать временные или постоянные подключения.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-119">You can operate against one or many computers, and use either temporary or persistent connections.</span></span>
<span data-ttu-id="d2cb7-120">В этой демонстрации вы устанавливаете удаленное подключение к локальному компьютеру через интерактивный сеанс.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-120">In this demo, you remoted into your local machine with an interactive session.</span></span>
<span data-ttu-id="d2cb7-121">JEA ограничивает функциональные возможности, доступные через службу удаленного взаимодействия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-121">JEA restricts the functionality available through PowerShell remoting.</span></span>
<span data-ttu-id="d2cb7-122">Чтобы получить дополнительные сведения об удаленном взаимодействии PowerShell, выполните `Get-Help about_Remote`.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-122">For more information about PowerShell remoting, run `Get-Help about_Remote`.</span></span>

<span data-ttu-id="d2cb7-123">**Пользователь запуска от имени**: при использовании JEA пользователь без прав администратора работает от имени привилегированной виртуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-123">**"RunAs" User**: When using JEA, a non-administrator "runs as" a privileged "Virtual Account."</span></span>
<span data-ttu-id="d2cb7-124">Виртуальная учетная запись действует только во время удаленного сеанса.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-124">The Virtual Account only lasts the duration of the remote session.</span></span>
<span data-ttu-id="d2cb7-125">Иными словами, она создается при подключении пользователя к конечной точке и удаляется, когда пользователь завершает сеанс.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-125">That is to say, it is created when a user connects to the endpoint, and destroyed when the user ends the session.</span></span>
<span data-ttu-id="d2cb7-126">По умолчанию виртуальная учетная запись входит в локальную группу администраторов.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-126">By default, the Virtual Account is a member of the local Administrators group.</span></span>
<span data-ttu-id="d2cb7-127">На контроллере домена он входит в группу администраторов домена.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-127">On a domain controller, it is a member of Domain Admins.</span></span>
<span data-ttu-id="d2cb7-128">Виртуальные учетные записи являются локальными для компьютера, на котором они были созданы, и не имеют разрешений за его пределами.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-128">Virtual Accounts are local to the machine on which they are created, and do not have permissions outside of that machine.</span></span>
<span data-ttu-id="d2cb7-129">Это означает, что они не зарегистрированы в Active Directory (им не назначен RID).</span><span class="sxs-lookup"><span data-stu-id="d2cb7-129">This means that they are not registered in Active Directory (no RID is assigned).</span></span>
<span data-ttu-id="d2cb7-130">Кроме того, если разрешенная команда или сценарий пытаются получить доступ к ресурсам за пределами локального компьютера, они будут обращаться к этим ресурсам, используя удостоверение компьютера, а не виртуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-130">Additionally, if an allowed command/script tries to access resources outside of the local machine, it will be accessing those resources under the machine's identity, not the Virtual Account identity.</span></span>

<span data-ttu-id="d2cb7-131">**Подключенный пользователь**: пользователь без прав администратора, который подключается к конечной точке JEA и которому назначаются роли.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-131">**"Connected" User**: The non-administrator user who connects to the JEA endpoint and to whom roles are assigned.</span></span>
<span data-ttu-id="d2cb7-132">Все команды этого пользователя выполняются в контексте пользователя запуска от имени или виртуальной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d2cb7-132">Any commands this user runs are run under the context of the RunAs User or virtual account.</span></span>

