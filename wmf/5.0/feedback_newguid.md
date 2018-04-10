---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 91c115c7f0553cd5edf7fecf04e6a5c71c0a1aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="new-guid"></a><span data-ttu-id="02ecc-102">New-Guid</span><span class="sxs-lookup"><span data-stu-id="02ecc-102">New-Guid</span></span>
<span data-ttu-id="02ecc-103">Часто в сценарии (или при создании ресурсов DSC) требуется уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="02ecc-103">Often script (or perhaps writing a DSC resource), you have the need for a unique identifier.</span></span> <span data-ttu-id="02ecc-104">Здесь можно использовать GUID, для создания которых достаточно вызвать класс Guid платформы .NET Framework, однако наличие командлета делает этот процесс более очевидным и удобным для конечных пользователей, которые еще не знакомы с данным классом .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="02ecc-104">GUIDs work well, and it is easy to call the .NET Framework Guid class to generate one, but having a cmdlet makes this more discoverable for end users who are not already familiar with the .NET Framework class:</span></span>

<span data-ttu-id="02ecc-105">PS C:\\&gt; New-Guid</span><span class="sxs-lookup"><span data-stu-id="02ecc-105">PS C:\\&gt; New-Guid</span></span>

<span data-ttu-id="02ecc-106">GUID</span><span class="sxs-lookup"><span data-stu-id="02ecc-106">Guid</span></span>

----

<span data-ttu-id="02ecc-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span><span class="sxs-lookup"><span data-stu-id="02ecc-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span></span>