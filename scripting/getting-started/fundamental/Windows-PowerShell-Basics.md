---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Основы Windows PowerShell"
ms.assetid: 6b3cbbc8-060c-4877-b00b-7300dbbe4e28
ms.openlocfilehash: f8a520f1fbe97737c7d0c2acab0129f88b5ed425
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="windows-powershell-basics"></a><span data-ttu-id="ccb00-103">Основы Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccb00-103">Windows PowerShell Basics</span></span>
<span data-ttu-id="ccb00-104">В графических пользовательских интерфейсах используются общие концепции, знакомые большинству пользователей.</span><span class="sxs-lookup"><span data-stu-id="ccb00-104">Graphical user interfaces use some basic concepts that are well known to most computer users.</span></span> <span data-ttu-id="ccb00-105">Пользователи полагаются на эти привычные интерфейсы для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="ccb00-105">Users rely on the familiarity of those interfaces to accomplish tasks.</span></span> <span data-ttu-id="ccb00-106">Операционные системы предлагают пользователю графическое представление элементов, которые можно просматривать, при этом раскрывающиеся меню обычно используются для доступа к конкретной функциональности, а контекстные меню — к контекстной функциональности.</span><span class="sxs-lookup"><span data-stu-id="ccb00-106">Operating systems present users with a graphical representation of items that can be browsed, usually with drop-down menus for accessing specific functionality and context menus for accessing context-specific functionality.</span></span>

<span data-ttu-id="ccb00-107">Интерфейс командной строки (CLI), такой как Windows PowerShell, должен использовать другой подход для предоставления информации, так как в нем нет меню или графических систем, чтобы помочь пользователю.</span><span class="sxs-lookup"><span data-stu-id="ccb00-107">A command-line interface (CLI), such as Windows PowerShell, must use a different approach to expose information, because it does not have menus or graphical systems to help the user.</span></span> <span data-ttu-id="ccb00-108">Для использования команд необходимо знать их имена.</span><span class="sxs-lookup"><span data-stu-id="ccb00-108">You need to know command names before you can use them.</span></span> <span data-ttu-id="ccb00-109">Хотя можно вводить сложные команды, эквивалентные функциям в среде графического пользовательского интерфейса, необходимо ознакомиться с наиболее распространенными командами и их параметрами.</span><span class="sxs-lookup"><span data-stu-id="ccb00-109">Although you can type complex commands that are equivalent to the features in a GUI environment, you must become familiar with commonly-used commands and command parameters.</span></span>

<span data-ttu-id="ccb00-110">В большинстве интерфейсов командной строки нет шаблонов, помогающих пользователю освоить интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ccb00-110">Most CLIs do not have patterns that can help the user to learn the interface.</span></span> <span data-ttu-id="ccb00-111">Поскольку интерфейсы CLI были первыми оболочками операционных систем, многие имена команд и параметров выбирались произвольно.</span><span class="sxs-lookup"><span data-stu-id="ccb00-111">Because CLIs were the first operating system shells, many command names and parameter names were selected arbitrarily.</span></span> <span data-ttu-id="ccb00-112">Предпочтение отдавалось лаконичным, а не понятным именам.</span><span class="sxs-lookup"><span data-stu-id="ccb00-112">Terse command names were generally chosen over clear ones.</span></span> <span data-ttu-id="ccb00-113">Хотя справочные системы и стандарты проектирования команд интегрированы в большинство интерфейсов CLI, они обычно рассчитаны на совместимость с самыми ранними командами. Поэтому набор команд формируется согласно решениям, принятым десятилетия назад.</span><span class="sxs-lookup"><span data-stu-id="ccb00-113">Although help systems and command design standards are integrated into most CLIs, they have been generally designed for compatibility with the earliest commands, so the command set is still shaped by decisions made decades ago.</span></span>

<span data-ttu-id="ccb00-114">Windows PowerShell ориентирована на использование имеющихся у пользователей знаний об интерфейсах CLI.</span><span class="sxs-lookup"><span data-stu-id="ccb00-114">Windows PowerShell was designed to take advantage of a user's historic knowledge of CLIs.</span></span> <span data-ttu-id="ccb00-115">В этой главе мы рассмотрим некоторые основные средства и концепции, помогающие быстро освоить Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb00-115">In this chapter, we will talk about some basic tools and concepts that you can use to learn Windows PowerShell quickly.</span></span> <span data-ttu-id="ccb00-116">в том числе:</span><span class="sxs-lookup"><span data-stu-id="ccb00-116">They include:</span></span>

-   <span data-ttu-id="ccb00-117">Использование Get-Command</span><span class="sxs-lookup"><span data-stu-id="ccb00-117">Using Get-Command</span></span>

-   <span data-ttu-id="ccb00-118">Использование команд Cmd.exe и UNIX</span><span class="sxs-lookup"><span data-stu-id="ccb00-118">Using Cmd.exe and UNIX commands</span></span>

-   <span data-ttu-id="ccb00-119">Использование внешних команд</span><span class="sxs-lookup"><span data-stu-id="ccb00-119">Using External Commands</span></span>

-   <span data-ttu-id="ccb00-120">Использование Tab-Completion</span><span class="sxs-lookup"><span data-stu-id="ccb00-120">Using Tab-Completion</span></span>

-   <span data-ttu-id="ccb00-121">Использование Get-Help</span><span class="sxs-lookup"><span data-stu-id="ccb00-121">Using Get-Help</span></span>

