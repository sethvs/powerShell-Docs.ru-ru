---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурсы DSC
ms.openlocfilehash: e393c8fe2e1ba8d68ba9aa1b656d1e5ebfad30e8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-resources"></a><span data-ttu-id="6a3c6-103">Ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="6a3c6-103">DSC Resources</span></span>

><span data-ttu-id="6a3c6-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6a3c6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6a3c6-105">Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC.</span><span class="sxs-lookup"><span data-stu-id="6a3c6-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="6a3c6-106">В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).</span><span class="sxs-lookup"><span data-stu-id="6a3c6-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="6a3c6-107">Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="6a3c6-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="6a3c6-108">Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a3c6-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

<span data-ttu-id="6a3c6-109">Описание ресурсов DSC см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="6a3c6-109">The following topics describe DSC resources:</span></span>

- [<span data-ttu-id="6a3c6-110">Встроенные ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="6a3c6-110">Built-In DSC resources</span></span>](builtInResource.md)
- [<span data-ttu-id="6a3c6-111">Встроенные пользовательские ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="6a3c6-111">Build custom DSC resources</span></span>](authoringResource.md)
- [<span data-ttu-id="6a3c6-112">Встроенные ресурсы DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="6a3c6-112">Built-In DSC resources for Linux</span></span>](lnxBuiltInResources.md)