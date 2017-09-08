---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "командлеты web access"
ms.technology: powershell
ms.openlocfilehash: ac8717c2aa97d0482b4d88f1b57d621d7ff47535
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="windows-powershell-web-access-cmdlets"></a><span data-ttu-id="2821e-103">Командлеты Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="2821e-103">Windows PowerShell Web Access Cmdlets</span></span>

<span data-ttu-id="2821e-104">В этом справочнике приводится описание и синтаксис всех командлетов, относящихся к Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="2821e-104">This reference provides cmdlet descriptions and syntax for all Windows PowerShell® Web Access-specific cmdlets.</span></span> <span data-ttu-id="2821e-105">Командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.</span><span class="sxs-lookup"><span data-stu-id="2821e-105">It lists the cmdlets in alphabetical order based on the verb at the beginning of the cmdlet.</span></span>

## <a name="add-pswaauthorizationruleadd-pswaauthorizationrulemd"></a>[<span data-ttu-id="2821e-106">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2821e-106">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)

<span data-ttu-id="2821e-107">Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="2821e-107">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="get-pswaauthorizationruleget-pswaauthorizationrulemd"></a>[<span data-ttu-id="2821e-108">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2821e-108">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)

<span data-ttu-id="2821e-109">Возвращает набор правил авторизации Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="2821e-109">Returns a set of the Windows PowerShell Web Access authorization rules.</span></span>

## <a name="install-pswawebapplicationinstall-pswawebapplicationmd"></a>[<span data-ttu-id="2821e-110">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="2821e-110">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)

<span data-ttu-id="2821e-111">Настраивает веб-приложение Windows PowerShell Web Access в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="2821e-111">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="remove-pswaauthorizationruleremove-pswaauthorizationrulemd"></a>[<span data-ttu-id="2821e-112">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2821e-112">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)

<span data-ttu-id="2821e-113">Удаляет указанное правило авторизации из Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="2821e-113">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="test-pswaauthorizationruletest-pswaauthorizationrulemd"></a>[<span data-ttu-id="2821e-114">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2821e-114">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)

<span data-ttu-id="2821e-115">Проверяет правила авторизации, чтобы гарантировать, что запрос на доступ конкретного пользователя, компьютера или конечной точки авторизован.</span><span class="sxs-lookup"><span data-stu-id="2821e-115">Tests authorization rules to validate that a particular user, computer, endpoint access request is authorized.</span></span>

## <a name="uninstall-pswawebapplicationuninstall-pswawebapplicationmd"></a>[<span data-ttu-id="2821e-116">Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="2821e-116">Uninstall-PswaWebApplication</span></span>](uninstall-pswawebapplication.md)

<span data-ttu-id="2821e-117">Удаляет веб-приложение Windows PowerShell Web Access с сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="2821e-117">Uninstalls the Windows PowerShell web application from IIS.</span></span>

><span data-ttu-id="2821e-118">**Примечание**.</span><span class="sxs-lookup"><span data-stu-id="2821e-118">**Note**:</span></span>
>
><span data-ttu-id="2821e-119">Для получения списка всех доступных командлетов используйте командлет</span><span class="sxs-lookup"><span data-stu-id="2821e-119">To list all the cmdlets that are available, use the:</span></span>
>
> <span data-ttu-id="2821e-120">`Get-Command –Module PowerShellWebAccess`.</span><span class="sxs-lookup"><span data-stu-id="2821e-120">`Get-Command –Module PowerShellWebAccess` cmdlet.</span></span>

<span data-ttu-id="2821e-121">Дополнительные сведения о любых командлетах или их синтаксисе можно получить, выполнив</span><span class="sxs-lookup"><span data-stu-id="2821e-121">For more information about, or for the syntax of, any of the cmdlets, use:</span></span>  
<span data-ttu-id="2821e-122">`Get-Help `*&lt;командлет&gt;*,</span><span class="sxs-lookup"><span data-stu-id="2821e-122">`Get-Help `*&lt;cmdlet name&gt;*</span></span>  
<span data-ttu-id="2821e-123">где *&lt;командлет&gt;* — это имя командлета, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="2821e-123">where *&lt;cmdlet name&gt;* is the name of the cmdlet that you want to research.</span></span>

<span data-ttu-id="2821e-124">Для получения дополнительных сведений запустите любой и следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="2821e-124">For more detailed information, you can run any of the following cmdlets:</span></span>

-  <span data-ttu-id="2821e-125">`Get-Help `*&lt;командлет&gt;*` -Detailed`</span><span class="sxs-lookup"><span data-stu-id="2821e-125">`Get-Help `*&lt;cmdlet name&gt;*` -Detailed`</span></span>
-  <span data-ttu-id="2821e-126">`Get-Help `*&lt;командлет&gt;*` -Examples`</span><span class="sxs-lookup"><span data-stu-id="2821e-126">`Get-Help `*&lt;cmdlet name&gt;*` -Examples`</span></span>
-  <span data-ttu-id="2821e-127">`Get-Help `*&lt;командлет&gt;*` -Full`</span><span class="sxs-lookup"><span data-stu-id="2821e-127">`Get-Help `*&lt;cmdlet name&gt;*` -Full`</span></span>

### <a name="more-information"></a><span data-ttu-id="2821e-128">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="2821e-128">More Information</span></span>

<span data-ttu-id="2821e-129">Дополнительные сведения о PowerShell Web Access см. в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="2821e-129">For more information about PowerShell Web Access, see the following:</span></span>

-   [<span data-ttu-id="2821e-130">Установка и использование Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="2821e-130">Install and Use Windows PowerShell Web Access</span></span>](../install-and-use-windows-powershell-web-access.md)

