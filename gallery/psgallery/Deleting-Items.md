---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "Удаление элементов"
ms.openlocfilehash: 00452f9b6625a51e95f3f46dbd66291fa20e17ad
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="deleting-items"></a><span data-ttu-id="78703-103">Удаление элементов</span><span class="sxs-lookup"><span data-stu-id="78703-103">Deleting items</span></span>

<span data-ttu-id="78703-104">Коллекция PowerShell не поддерживает полное удаление элементов, так как это помешает работе пользователей, которым они необходимы для работы.</span><span class="sxs-lookup"><span data-stu-id="78703-104">The PowerShell Gallery does not support permanent deletion of items, because that would break anyone who is depending on it remaining available.</span></span>

<span data-ttu-id="78703-105">Вместо этого элемент из коллекции PowerShell можно исключить — для этого используется страница управления элементами на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="78703-105">Instead, the PowerShell Gallery supports a way to 'unlist' an item, which can be done in the item management page on the web site.</span></span> <span data-ttu-id="78703-106">Исключенный элемент больше не будет отображаться в результатах поиска и списках элементов ни в коллекции PowerShell, ни при использовании команд PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="78703-106">When an item is unlisted, it no longer shows up in search and in any item listing, both on the PowerShell Gallery and using PowerShellGet commands.</span></span> <span data-ttu-id="78703-107">При этом он будет доступен для загрузки при указании точной версии, что обеспечит сохранение работоспособности автоматических скриптов.</span><span class="sxs-lookup"><span data-stu-id="78703-107">However, it remains downloadable by specifying its exact version, which is what allows the automated scripts to continue working.</span></span>

<span data-ttu-id="78703-108">Если возникнет исключительная ситуация и нужно будет удалить какой-либо элемент, это можно сделать вручную через рабочую группу, ответственную за коллекцию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78703-108">If you run into an exceptional situation where you think one of your items must be deleted, this can be handled manually by the PowerShell Gallery team.</span></span> <span data-ttu-id="78703-109">Например, уважительной причиной для удаления элемента может стать нарушение авторских прав или если он включает потенциально вредоносное содержимое.</span><span class="sxs-lookup"><span data-stu-id="78703-109">For example, if there is a copyright infringement issue, or potentially harmful content, that could be a valid reason to delete it.</span></span> <span data-ttu-id="78703-110">В этом случае необходимо отправить запрос в службу поддержки через [коллекцию PowerShell] (http://www.PowerShellGallery.com).</span><span class="sxs-lookup"><span data-stu-id="78703-110">You should submit a support request through [PowerShell Gallery] (http://www.PowerShellGallery.com) in that case.</span></span>

