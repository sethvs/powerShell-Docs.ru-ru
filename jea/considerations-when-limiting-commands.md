---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "рекомендации по ограничениям команд"
ms.technology: powershell
ms.openlocfilehash: 0b4396ee130d99c42f613c1b79193c236ad472e7
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
### <a name="considerations-when-limiting-commands"></a><span data-ttu-id="6c115-103">Рекомендации по ограничениям команд</span><span class="sxs-lookup"><span data-stu-id="6c115-103">Considerations When Limiting Commands</span></span>
<span data-ttu-id="6c115-104">На этом этапе необходимо обратить внимание на один важный момент.</span><span class="sxs-lookup"><span data-stu-id="6c115-104">There is one important point to make about this step.</span></span>
<span data-ttu-id="6c115-105">Все возможности, предоставляемые через JEA, находятся в областях, ограниченных правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6c115-105">It is critical that all capabilities exposed through JEA are located in administrator-restricted areas.</span></span>
<span data-ttu-id="6c115-106">Пользователи без прав не должны иметь возможность изменять используемые сценарии через конечные точки JEA.</span><span class="sxs-lookup"><span data-stu-id="6c115-106">Non-administrator users should not have the capability to modify the scripts used through JEA endpoints.</span></span>

<span data-ttu-id="6c115-107">Кроме того, ни в коем случае нельзя предоставлять пользователям JEA возможность перезаписывать конфигурации JEA и сценарии из разрешенного списка во время сеансов JEA.</span><span class="sxs-lookup"><span data-stu-id="6c115-107">On a related note, it is critical that you do not give JEA users the ability to overwrite JEA configurations and whitelisted scripts within their JEA sessions.</span></span>
<span data-ttu-id="6c115-108">Будьте особенно внимательны, предоставляя доступ к таким командам, как `Copy-Item`.</span><span class="sxs-lookup"><span data-stu-id="6c115-108">Be extremely careful when exposing commands like `Copy-Item`!</span></span>

