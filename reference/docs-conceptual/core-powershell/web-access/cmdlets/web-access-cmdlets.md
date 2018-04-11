---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: командлеты web access
ms.technology: powershell
ms.openlocfilehash: 6930fd6a08de69078576fb0d0fbabb04e05d0814
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="windows-powershell-web-access-cmdlets"></a><span data-ttu-id="d4fec-103">Командлеты Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="d4fec-103">Windows PowerShell Web Access Cmdlets</span></span>

<span data-ttu-id="d4fec-104">В этом справочнике приводится описание и синтаксис всех командлетов, относящихся к Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="d4fec-104">This reference provides cmdlet descriptions and syntax for all Windows PowerShell® Web Access-specific cmdlets.</span></span> <span data-ttu-id="d4fec-105">Командлеты перечисляются в алфавитном порядке по команде в начале имени командлета.</span><span class="sxs-lookup"><span data-stu-id="d4fec-105">It lists the cmdlets in alphabetical order based on the verb at the beginning of the cmdlet.</span></span>

## <a name="add-pswaauthorizationruleadd-pswaauthorizationrulemd"></a>[<span data-ttu-id="d4fec-106">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d4fec-106">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)

<span data-ttu-id="d4fec-107">Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="d4fec-107">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="get-pswaauthorizationruleget-pswaauthorizationrulemd"></a>[<span data-ttu-id="d4fec-108">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d4fec-108">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)

<span data-ttu-id="d4fec-109">Возвращает набор правил авторизации Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d4fec-109">Returns a set of the Windows PowerShell Web Access authorization rules.</span></span>

## <a name="install-pswawebapplicationinstall-pswawebapplicationmd"></a>[<span data-ttu-id="d4fec-110">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="d4fec-110">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)

<span data-ttu-id="d4fec-111">Настраивает веб-приложение Windows PowerShell Web Access в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="d4fec-111">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="remove-pswaauthorizationruleremove-pswaauthorizationrulemd"></a>[<span data-ttu-id="d4fec-112">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d4fec-112">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)

<span data-ttu-id="d4fec-113">Удаляет указанное правило авторизации из Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d4fec-113">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="test-pswaauthorizationruletest-pswaauthorizationrulemd"></a>[<span data-ttu-id="d4fec-114">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d4fec-114">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)

<span data-ttu-id="d4fec-115">Проверяет правила авторизации, чтобы гарантировать, что запрос на доступ конкретного пользователя, компьютера или конечной точки авторизован.</span><span class="sxs-lookup"><span data-stu-id="d4fec-115">Tests authorization rules to validate that a particular user, computer, endpoint access request is authorized.</span></span>

## <a name="uninstall-pswawebapplicationuninstall-pswawebapplicationmd"></a>[<span data-ttu-id="d4fec-116">Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="d4fec-116">Uninstall-PswaWebApplication</span></span>](uninstall-pswawebapplication.md)

<span data-ttu-id="d4fec-117">Удаляет веб-приложение Windows PowerShell Web Access с сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="d4fec-117">Uninstalls the Windows PowerShell web application from IIS.</span></span>

><span data-ttu-id="d4fec-118">**Примечание**.</span><span class="sxs-lookup"><span data-stu-id="d4fec-118">**Note**:</span></span>
>
><span data-ttu-id="d4fec-119">Для получения списка всех доступных командлетов используйте командлет</span><span class="sxs-lookup"><span data-stu-id="d4fec-119">To list all the cmdlets that are available, use the:</span></span>
>
> <span data-ttu-id="d4fec-120">`Get-Command –Module PowerShellWebAccess`.</span><span class="sxs-lookup"><span data-stu-id="d4fec-120">`Get-Command –Module PowerShellWebAccess` cmdlet.</span></span>

<span data-ttu-id="d4fec-121">Дополнительные сведения о любых командлетах или их синтаксисе можно получить, выполнив `Get-Help `*&lt;cmdlet name&gt;*, где *&lt;cmdlet name&gt;* указывает командлет, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="d4fec-121">For more information about, or for the syntax of, any of the cmdlets, use: `Get-Help `*&lt;cmdlet name&gt;* where *&lt;cmdlet name&gt;* is the name of the cmdlet that you want to research.</span></span>

<span data-ttu-id="d4fec-122">Для получения дополнительных сведений запустите любой и следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="d4fec-122">For more detailed information, you can run any of the following cmdlets:</span></span>

- <span data-ttu-id="d4fec-123">`Get-Help `*&lt;командлет&gt;*` -Detailed`</span><span class="sxs-lookup"><span data-stu-id="d4fec-123">`Get-Help `*&lt;cmdlet name&gt;*` -Detailed`</span></span>
- <span data-ttu-id="d4fec-124">`Get-Help `*&lt;командлет&gt;*` -Examples`</span><span class="sxs-lookup"><span data-stu-id="d4fec-124">`Get-Help `*&lt;cmdlet name&gt;*` -Examples`</span></span>
- <span data-ttu-id="d4fec-125">`Get-Help `*&lt;командлет&gt;*` -Full`</span><span class="sxs-lookup"><span data-stu-id="d4fec-125">`Get-Help `*&lt;cmdlet name&gt;*` -Full`</span></span>

### <a name="more-information"></a><span data-ttu-id="d4fec-126">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="d4fec-126">More Information</span></span>

<span data-ttu-id="d4fec-127">Дополнительные сведения о PowerShell Web Access см. в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="d4fec-127">For more information about PowerShell Web Access, see the following:</span></span>

- [<span data-ttu-id="d4fec-128">Установка и использование Windows PowerShell Web Access</span><span class="sxs-lookup"><span data-stu-id="d4fec-128">Install and Use Windows PowerShell Web Access</span></span>](../install-and-use-windows-powershell-web-access.md)