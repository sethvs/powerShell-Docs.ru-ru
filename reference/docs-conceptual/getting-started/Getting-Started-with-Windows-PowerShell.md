---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Начало работы с Windows PowerShell
ms.assetid: b0e2ad92-875f-421d-b612-f624e644aa69
ms.openlocfilehash: d8f1a416c1618040311ec0ea3b98b28aa432bcf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="getting-started-with-windows-powershell"></a><span data-ttu-id="388de-103">Начало работы с Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="388de-103">Getting Started with Windows PowerShell</span></span>
<span data-ttu-id="388de-104">Windows PowerShell — это оболочка командной строки Windows, предназначенная специально для системных администраторов.</span><span class="sxs-lookup"><span data-stu-id="388de-104">Windows PowerShell is a Windows command-line shell designed especially for system administrators.</span></span> <span data-ttu-id="388de-105">Windows PowerShell содержит интерактивное приглашение и среду сценариев, которые можно использовать отдельно или вместе.</span><span class="sxs-lookup"><span data-stu-id="388de-105">Windows PowerShell includes an interactive prompt and a scripting environment that can be used independently or in combination.</span></span>

<span data-ttu-id="388de-106">В отличие от большинства оболочек, которые принимают и возвращают текст, Windows PowerShell основана на среде CLR .NET Framework и платформе .NET Framework и принимает и возвращает объекты .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="388de-106">Unlike most shells, which accept and return text, Windows PowerShell is built on top of the .NET Framework common language runtime (CLR) and the .NET Framework, and accepts and returns .NET Framework objects.</span></span> <span data-ttu-id="388de-107">Это фундаментальное изменение в среде предоставляет совершенно новые средства и методы для настройки Windows и управления ей.</span><span class="sxs-lookup"><span data-stu-id="388de-107">This fundamental change in the environment brings entirely new tools and methods to the management and configuration of Windows.</span></span>

<span data-ttu-id="388de-108">В Windows PowerShell введено понятие командлета — встроенной в оболочку простой программы командной строки, выполняющей одну функцию.</span><span class="sxs-lookup"><span data-stu-id="388de-108">Windows PowerShell introduces the concept of a cmdlet (pronounced "command-let"), a simple, single-function command-line tool built into the shell.</span></span> <span data-ttu-id="388de-109">Каждый командлет можно использовать отдельно, но все их возможности раскрываются именно при совместном использовании для выполнения сложных задач.</span><span class="sxs-lookup"><span data-stu-id="388de-109">You can use each cmdlet separately, but their power is realized when you use these simple tools in combination to perform complex tasks.</span></span> <span data-ttu-id="388de-110">Windows PowerShell содержит более ста основных командлетов, кроме того, можно создавать собственные командлеты и использовать их совместно с другими пользователями.</span><span class="sxs-lookup"><span data-stu-id="388de-110">Windows PowerShell includes more than one hundred basic core cmdlets, and you can write your own cmdlets and share them with other users.</span></span>

<span data-ttu-id="388de-111">Как и многие другие оболочки, Windows PowerShell предоставляет доступ к файловой системе на компьютере.</span><span class="sxs-lookup"><span data-stu-id="388de-111">Like many shells, Windows PowerShell gives you access to the file system on the computer.</span></span> <span data-ttu-id="388de-112">Кроме того, *поставщики* Windows PowerShell позволяют получить доступ к другим хранилищам данных, например реестру и хранилищам сертификатов цифровой подписи, так же легко, как и к файловой системе.</span><span class="sxs-lookup"><span data-stu-id="388de-112">In addition, Windows PowerShell *providers* enable you to access other data stores, such as the registry and the digital signature certificate stores, as easily as you access the file system.</span></span>

<span data-ttu-id="388de-113">Это руководство по началу работы содержит вводные сведения о Windows PowerShell — язык, командлеты, поставщики и использование объектов.</span><span class="sxs-lookup"><span data-stu-id="388de-113">This Getting Started guide provides an introduction to Windows PowerShell: the language, the cmdlets, the providers, and the use of objects.</span></span>

<span data-ttu-id="388de-114">Содержание раздела:</span><span class="sxs-lookup"><span data-stu-id="388de-114">In this topic:</span></span>

- [<span data-ttu-id="388de-115">Требования Windows PowerShell к системе</span><span class="sxs-lookup"><span data-stu-id="388de-115">Windows PowerShell System Requirements</span></span>](../setup/Windows-PowerShell-System-Requirements.md)

- [<span data-ttu-id="388de-116">Установка Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="388de-116">Installing Windows PowerShell</span></span>](../setup/Installing-Windows-PowerShell.md)

- [<span data-ttu-id="388de-117">Запуск Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="388de-117">Starting Windows PowerShell</span></span>](../setup/Starting-Windows-PowerShell.md)

- [<span data-ttu-id="388de-118">Подготовка к использованию Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="388de-118">Getting Ready to Use Windows PowerShell</span></span>](Getting-Ready-to-Use-Windows-PowerShell.md)