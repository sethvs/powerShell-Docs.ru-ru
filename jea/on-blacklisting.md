---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "о запрещенных списках"
ms.technology: powershell
ms.openlocfilehash: e823cc0b130500fb7ea60e65acf27f90ad3f3802
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
### <a name="on-blacklisting"></a><span data-ttu-id="19257-103">О запрещенных списках</span><span class="sxs-lookup"><span data-stu-id="19257-103">On Blacklisting</span></span>
<span data-ttu-id="19257-104">Познакомившись с JEA, вы можете задуматься о том, можно ли добавлять команды в запрещенный список.</span><span class="sxs-lookup"><span data-stu-id="19257-104">After playing around with JEA, you may be wondering if it is possible to blacklist commands.</span></span>
<span data-ttu-id="19257-105">Эта потребность понятна, но сейчас ее реализация в JEA не планируется по следующим причинам.</span><span class="sxs-lookup"><span data-stu-id="19257-105">This is an understandable request, but it is not currently planned for JEA for the following reasons:</span></span>

1.  <span data-ttu-id="19257-106">Мы разработали JEA для того, чтобы операторы получали доступ только к тем действиям, которые им необходимы.</span><span class="sxs-lookup"><span data-stu-id="19257-106">We designed JEA to limit operators to only the actions they need to do.</span></span>
<span data-ttu-id="19257-107">Запрещенный список имеет противоположное назначение.</span><span class="sxs-lookup"><span data-stu-id="19257-107">A blacklist is the opposite.</span></span>

2.  <span data-ttu-id="19257-108">Авторы команд PowerShell не разрабатывали свои команды для JEA.</span><span class="sxs-lookup"><span data-stu-id="19257-108">PowerShell command authors did not design PowerShell commands with the JEA in mind.</span></span>
<span data-ttu-id="19257-109">Сразу после установки Windows Server 2016 предоставляет около 1520 команд.</span><span class="sxs-lookup"><span data-stu-id="19257-109">On a fresh install of Windows Server 2016, there are about 1520 commands immediately available.</span></span>
<span data-ttu-id="19257-110">Модели угроз для этих команд не учитывают вероятность того, что пользователь будет вести работу от имени более привилегированной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="19257-110">The threat models for these commands did not include the possibility that a user would be running commands as a more privileged account.</span></span>
<span data-ttu-id="19257-111">Например, некоторые команды по своему назначению позволяют внедрять код (например, Add-Type и Invoke-Command в основном модуле PowerShell).</span><span class="sxs-lookup"><span data-stu-id="19257-111">For example, certain commands allow for code injection by design (e.g. Add-Type and Invoke-Command in the core PowerShell module).</span></span>
<span data-ttu-id="19257-112">JEA может предупредить вас при предоставлении доступа к некоторым известным нам командам, но мы не проверяли остальные команды в Windows в соответствии с новой моделью угрозы.</span><span class="sxs-lookup"><span data-stu-id="19257-112">JEA can warn you when you expose the specific commands we know about, but we have not re-assessed every other command in Windows based on the new threat model.</span></span>
<span data-ttu-id="19257-113">Необходимо понимать возможности команд, к которым вы предоставляете доступ через JEA.</span><span class="sxs-lookup"><span data-stu-id="19257-113">You must understand the capabilities of the commands you exposing through JEA.</span></span>  

3.  <span data-ttu-id="19257-114">Кроме того, даже если бы среда JEA блокировала все команды, уязвимые для внедрения кода, нет никаких гарантий того, что злоумышленник не сможет выполнить действие из запрещенного списка с помощью другой аналогичной команды.</span><span class="sxs-lookup"><span data-stu-id="19257-114">Furthermore, even if JEA blocked all commands with code-injection vulnerabilities, there is no guarantee that a malicious user would not be able to carry out a blacklisted action with another related command.</span></span>
<span data-ttu-id="19257-115">Если вы не понимаете, к каким командам предоставляете доступ, то не сможете гарантировать невозможность того или иного действия.</span><span class="sxs-lookup"><span data-stu-id="19257-115">Unless you understand all of the commands that you are exposing, it is impossible for you to guarantee that a certain action is not possible.</span></span>
<span data-ttu-id="19257-116">Именно вы должны понимать, к каким командам предоставляете доступ, независимо от того, используется ли в них запрещенный или разрешенный список.</span><span class="sxs-lookup"><span data-stu-id="19257-116">The burden is on you to understand what commands you are exposing, whether they are using a whitelist or a blacklist.</span></span>
<span data-ttu-id="19257-117">Состав команд, которые остались бы доступны при использовании запрещенного списка, контролировать нельзя, поэтому вместо этого в JEA применяются разрешенные списки.</span><span class="sxs-lookup"><span data-stu-id="19257-117">The number of commands a blacklist would expose is unmanageable, so JEA is implemented using whitelists instead.</span></span>

