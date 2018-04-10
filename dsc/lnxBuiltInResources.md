---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Встроенные ресурсы настройки требуемого состояния для Linux
ms.openlocfilehash: 77617b72584f39c46fc4b9eb67235378bbfc19aa
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a><span data-ttu-id="03a64-103">Встроенные ресурсы настройки требуемого состояния для Linux</span><span class="sxs-lookup"><span data-stu-id="03a64-103">Built-In Desired State Configuration Resources for Linux</span></span>

<span data-ttu-id="03a64-104">Ресурсы — это строительные блоки, которые можно использовать для написания сценария настройки требуемого состояния (DSC) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="03a64-104">Resources are building blocks that you can use to write a PowerShell Desired State Configuration (DSC) script.</span></span> <span data-ttu-id="03a64-105">DSC для Linux поставляется с набором встроенных возможностей для настройки ресурсов, таких как файлы и папки, пакеты, переменные среды, службы и процессы.</span><span class="sxs-lookup"><span data-stu-id="03a64-105">DSC for Linux comes with a set of built-in functionality for configuring resources such as files and folders, packages, environment variables, and services and processes.</span></span>

## <a name="built-in-resources"></a><span data-ttu-id="03a64-106">Встроенные ресурсы</span><span class="sxs-lookup"><span data-stu-id="03a64-106">Built-in resources</span></span>

<span data-ttu-id="03a64-107">Список ресурсов и ссылки на статьи, в которых они рассматриваются подробно.</span><span class="sxs-lookup"><span data-stu-id="03a64-107">The following table provides a list of these resources and links to topics that describe them in detail.</span></span>

* <span data-ttu-id="03a64-108">Ресурс [nxArchive](lnxArchiveResource.md) — предоставляет механизм распаковки файлов архива в формате TAR или ZIP в заданную папку.</span><span class="sxs-lookup"><span data-stu-id="03a64-108">[nxArchive Resource](lnxArchiveResource.md)--Provides a mechanism to unpack archive (.tar, .zip) files at a specific path.</span></span>
* <span data-ttu-id="03a64-109">Ресурс [nxEnvironment](lnxEnvironmentResource.md) — управляет переменными среды на целевых узлах.</span><span class="sxs-lookup"><span data-stu-id="03a64-109">[nxEnvironment Resource](lnxEnvironmentResource.md)--Manages environment variables on target nodes.</span></span>
* <span data-ttu-id="03a64-110">Ресурс [nxFile](lnxFileResource.md) — управляет файлами и каталогами Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-110">[nxFile Resource](lnxFileResource.md)--Manages Linux files and directories.</span></span>
* <span data-ttu-id="03a64-111">Ресурс [nxFileLine](lnxFileLineResource.md) — управляет отдельными строками в файле Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-111">[nxFileLine Resource](lnxFileLineResource.md)--Manages individual lines in a Linux file.</span></span>
* <span data-ttu-id="03a64-112">Ресурс [nxGroup](lnxGroupResource.md) — управляет локальными группами Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-112">[nxGroup Resource](lnxGroupResource.md)--Manages local Linux groups.</span></span>
* <span data-ttu-id="03a64-113">Ресурс [nxPackage](lnxPackageResource.md) — управляет пакетами на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-113">[nxPackage Resource](lnxPackageResource.md)--Manages packages on Linux nodes.</span></span>
* <span data-ttu-id="03a64-114">Ресурс [nxScript](lnxScriptResource.md) — запускает сценарии на целевых узлах.</span><span class="sxs-lookup"><span data-stu-id="03a64-114">[nxScript Resource](lnxScriptResource.md)--Runs scripts on target nodes.</span></span>
* <span data-ttu-id="03a64-115">Ресурс [nxService](lnxServiceResource.md) — управляет службами Linux (управляющими программами или "демонами").</span><span class="sxs-lookup"><span data-stu-id="03a64-115">[nxService Resource](lnxServiceResource.md)--Manages Linux services (daemons).</span></span>
* <span data-ttu-id="03a64-116">Ресурс [nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md) — управляет открытыми SSH-ключами для пользователей Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-116">[nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Manages public ssh keys for a Linux user.</span></span>
* <span data-ttu-id="03a64-117">Ресурс [nxUser](lnxUserResource.md) — управляет локальными пользователями Linux.</span><span class="sxs-lookup"><span data-stu-id="03a64-117">[nxUser Resource](lnxUserResource.md)--Manages local Linux users.</span></span>