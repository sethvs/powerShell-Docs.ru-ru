---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "распространенные проблемы возможностей ролей"
ms.technology: powershell
ms.openlocfilehash: 8e928ec07ef98b2ec8186a27d3aefa1450a3a424
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
### <a name="common-role-capability-pitfalls"></a><span data-ttu-id="70307-103">Распространенные проблемы возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="70307-103">Common Role Capability Pitfalls</span></span>
<span data-ttu-id="70307-104">При самостоятельной работе вы можете столкнуться с несколькими распространенными проблемами.</span><span class="sxs-lookup"><span data-stu-id="70307-104">You may run into a few common pitfalls if you go through this process yourself.</span></span>
<span data-ttu-id="70307-105">Вот краткое руководство по тому, как выявлять и устранять такие проблемы при изменении или создании новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="70307-105">Here is a quick guide explaining how to identify and remediate these issues when modifying or creating a new endpoint:</span></span>

#### <a name="functions-vs-cmdlets"></a><span data-ttu-id="70307-106">Функции. Командлеты</span><span class="sxs-lookup"><span data-stu-id="70307-106">Functions vs. Cmdlets</span></span>
<span data-ttu-id="70307-107">Команды PowerShell, написанные в PowerShell, являются функциями PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70307-107">PowerShell commands written in PowerShell are PowerShell functions.</span></span>
<span data-ttu-id="70307-108">Команды PowerShell, написанные как специализированные классы .NET, являются командлетами PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70307-108">PowerShell commands written as specialized .NET classes are PowerShell cmdlets.</span></span>
<span data-ttu-id="70307-109">Тип команды можно проверить, выполнив `Get-Command`.</span><span class="sxs-lookup"><span data-stu-id="70307-109">You can check the command type by running `Get-Command`.</span></span>

#### <a name="visibleproviders"></a><span data-ttu-id="70307-110">VisibleProviders</span><span class="sxs-lookup"><span data-stu-id="70307-110">VisibleProviders</span></span>
<span data-ttu-id="70307-111">Вам потребуется предоставить доступ ко всем поставщикам, необходимым для ваших команд.</span><span class="sxs-lookup"><span data-stu-id="70307-111">You will need to expose any providers your commands need.</span></span>
<span data-ttu-id="70307-112">Чаще всего используется поставщик FileSystem, но может потребоваться доступ и к другим поставщикам, таким как Registry.</span><span class="sxs-lookup"><span data-stu-id="70307-112">The most common is the FileSystem provider, but you may also need to expose others, like the Registry provider.</span></span>
<span data-ttu-id="70307-113">Вводные сведения о поставщиках см. в записи в блоге [Эй, сценарист](http://blogs.technet.com/b/heyscriptingguy/archive/2015/04/20/find-and-use-windows-powershell-providers.aspx).</span><span class="sxs-lookup"><span data-stu-id="70307-113">For an introduction to providers, check out this [Hey, Scripting Guy blog post](http://blogs.technet.com/b/heyscriptingguy/archive/2015/04/20/find-and-use-windows-powershell-providers.aspx).</span></span>
<span data-ttu-id="70307-114">Будьте внимательны, предоставляя доступ к поставщикам: зачастую лучше определить собственную функцию, которая будет работать с соответствующими базовыми поставщиками, чем напрямую предоставлять доступ к поставщику в сеансе JEA.</span><span class="sxs-lookup"><span data-stu-id="70307-114">Be careful when exposing providers -- often, it is better to define your own function that works with the underlying providers than to directly expose the provider in a JEA session.</span></span>
<span data-ttu-id="70307-115">Таким образом вы можете дать пользователям возможность работать с файлами, разделами реестра и т. д., но при этом сохраните контроль над тем, с **какими** из них они могут работать, используя настраиваемую логику проверки.</span><span class="sxs-lookup"><span data-stu-id="70307-115">This way, you can still allow users to work with files, registry keys, etc. but retain control over **which** files and registry keys they can work with using custom validation logic.</span></span>

