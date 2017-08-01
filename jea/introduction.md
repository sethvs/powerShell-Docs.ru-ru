---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "введение"
ms.technology: powershell
ms.openlocfilehash: 71264d1001228249d9f2bb0f72473e9761170bf0
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="introduction"></a><span data-ttu-id="5513b-103">Введение</span><span class="sxs-lookup"><span data-stu-id="5513b-103">Introduction</span></span>

##  <a name="motivation"></a><span data-ttu-id="5513b-104">**Причины для использования**</span><span class="sxs-lookup"><span data-stu-id="5513b-104">**Motivation**</span></span>  
<span data-ttu-id="5513b-105">Предоставляя кому-либо привилегированный доступ к своим системам, вы полагаетесь на этого человека.</span><span class="sxs-lookup"><span data-stu-id="5513b-105">When you grant someone privileged access to your systems, you extend your trust boundary to that person.</span></span>
<span data-ttu-id="5513b-106">Это риск, и администраторы всегда находятся под угрозой.</span><span class="sxs-lookup"><span data-stu-id="5513b-106">This is a risk -- administrators are an attack surface.</span></span>
<span data-ttu-id="5513b-107">Внутренние атаки и кража учетных данных реальны и распространены.</span><span class="sxs-lookup"><span data-stu-id="5513b-107">Insider attacks and stolen credentials are both real and common.</span></span>

##  <a name="not-a-new-problem"></a><span data-ttu-id="5513b-108">**Проблема не нова**</span><span class="sxs-lookup"><span data-stu-id="5513b-108">**Not a new problem**</span></span>  
<span data-ttu-id="5513b-109">Вероятно, вы уже знакомы с принципом минимальных полномочий или использовали ту или иную форму управления доступом на основе ролей в приложениях, предоставляющих такую возможность.</span><span class="sxs-lookup"><span data-stu-id="5513b-109">You are probably very familiar with the principle of least privilege, and you might use some form of role-based access control (RBAC) with applications that provide it.</span></span>
<span data-ttu-id="5513b-110">В то же время эффективность и управляемость таких решений часто ограничены из-за широкой области их применения и неточности.</span><span class="sxs-lookup"><span data-stu-id="5513b-110">However, the effectiveness and manageability of these solutions are often limited by their broad scope and imprecision.</span></span>
<span data-ttu-id="5513b-111">Кроме того, в RBAC есть пробелы.</span><span class="sxs-lookup"><span data-stu-id="5513b-111">Furthermore, there are gaps in RBAC coverage.</span></span>
<span data-ttu-id="5513b-112">Например, в Windows привилегированный доступ — это по сути двухпозиционный переключатель, вынуждающий предоставлять ненужные разрешения при добавлении пользователей в группу администраторов.</span><span class="sxs-lookup"><span data-stu-id="5513b-112">For example, in Windows, privileged access is largely a binary switch, forcing you to give unnecessary permissions when adding users to the Administrators group.</span></span>

##  <a name="just-enough-administration-jea"></a><span data-ttu-id="5513b-113">**Just Enough Administration (JEA)**</span><span class="sxs-lookup"><span data-stu-id="5513b-113">**Just Enough Administration (JEA)**</span></span> 
<span data-ttu-id="5513b-114">Предоставляет RBAC-платформу управления доступом на основе ролей через удаленное взаимодействие PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5513b-114">Provides a role-based access control (RBAC) platform through PowerShell Remoting.</span></span>
<span data-ttu-id="5513b-115">*С ее помощью отдельные пользователи могут выполнять определенные задачи администрирования на серверах, не получая права администраторов.*</span><span class="sxs-lookup"><span data-stu-id="5513b-115">*It allows specific users to perform specific administrative tasks on servers without giving them administrator rights.*</span></span>
<span data-ttu-id="5513b-116">Это позволяет заполнять пробелы между существующими решениями RBAC и упрощает управление соответствующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="5513b-116">This allows you to fill in the gaps between your existing RBAC solutions, and simplifies management of those settings.</span></span>

