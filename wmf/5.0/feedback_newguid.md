---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: bb2e7b99d14c790bdd3df2f5c729275b96a659fc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="new-guid"></a><span data-ttu-id="343cc-102">New-Guid</span><span class="sxs-lookup"><span data-stu-id="343cc-102">New-Guid</span></span>
<span data-ttu-id="343cc-103">Часто в сценарии (или при создании ресурсов DSC) требуется уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="343cc-103">Often script (or perhaps writing a DSC resource), you have the need for a unique identifier.</span></span> <span data-ttu-id="343cc-104">Здесь можно использовать GUID, для создания которых достаточно вызвать класс Guid платформы .NET Framework, однако наличие командлета делает этот процесс более очевидным и удобным для конечных пользователей, которые еще не знакомы с данным классом .NET Framework:</span><span class="sxs-lookup"><span data-stu-id="343cc-104">GUIDs work well, and it is easy to call the .NET Framework Guid class to generate one, but having a cmdlet makes this more discoverable for end users who are not already familiar with the .NET Framework class:</span></span>

<span data-ttu-id="343cc-105">PS C:\\&gt; New-Guid</span><span class="sxs-lookup"><span data-stu-id="343cc-105">PS C:\\&gt; New-Guid</span></span>

<span data-ttu-id="343cc-106">GUID</span><span class="sxs-lookup"><span data-stu-id="343cc-106">Guid</span></span>

----

<span data-ttu-id="343cc-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span><span class="sxs-lookup"><span data-stu-id="343cc-107">e19d6ea5-3cc2-4db9-8095-0cdaed5a703d</span></span>

