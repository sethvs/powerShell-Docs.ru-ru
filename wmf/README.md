---
title: Windows Management Framework (WMF)
ms.date: 2016-05-16
keywords: PowerShell, WMF
description: 
ms.topic: article
author: keithb
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: eacd33d2a0a92977a3990132e23eef9871a7f0dc
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="windows-management-framework"></a><span data-ttu-id="99a9d-103">Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="99a9d-103">Windows Management Framework</span></span>

<span data-ttu-id="99a9d-104">Windows Management Framework (WMF) — это механизм доставки, который предоставляет согласованный интерфейс управления различными версиями Windows и Windows Server.</span><span class="sxs-lookup"><span data-stu-id="99a9d-104">Windows Management Framework (WMF) is the delivery mechanism that provides a consistent management interface across the various flavors of Windows and Windows Server.</span></span>
<span data-ttu-id="99a9d-105">Установив WMF, клиенты получают возможность легко обеспечивать взаимодействие внутри различных сочетаний операционных систем в своих средах.</span><span class="sxs-lookup"><span data-stu-id="99a9d-105">With the installation of WMF, customers get a seamless way to interoperate between mixes of OSes in their environment.</span></span>
<span data-ttu-id="99a9d-106">Благодаря платформе WMF обновления функций управления в определенном выпуске Windows или Windows Server становятся доступными для установки в более ранних версиях Windows и Windows Server (как правило, в двух предыдущих версиях).</span><span class="sxs-lookup"><span data-stu-id="99a9d-106">WMF makes the updates to management functionality, in a given release of Windows and Windows Server, available for installation on lower versions (typically, 2 lower versions) of Windows and Windows Server.</span></span>

<span data-ttu-id="99a9d-107">При установке WMF добавляются или обновляются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="99a9d-107">WMF installation adds and/or updates the following features:</span></span>

- <span data-ttu-id="99a9d-108">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="99a9d-108">Windows PowerShell</span></span>
- <span data-ttu-id="99a9d-109">Windows PowerShell Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="99a9d-109">Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="99a9d-110">Интегрированная среда сценариев Windows PowerShell (ISE)</span><span class="sxs-lookup"><span data-stu-id="99a9d-110">Windows PowerShell Integrated Script Environment (ISE)</span></span>
- <span data-ttu-id="99a9d-111">Удаленное управление Windows (WinRM)</span><span class="sxs-lookup"><span data-stu-id="99a9d-111">Windows Remote Management (WinRM)</span></span>
- <span data-ttu-id="99a9d-112">Инструментарий управления Windows (WMI)</span><span class="sxs-lookup"><span data-stu-id="99a9d-112">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="99a9d-113">Веб-службы Windows PowerShell (расширение IIS OData для управления)</span><span class="sxs-lookup"><span data-stu-id="99a9d-113">Windows PowerShell Web Services (Management OData IIS Extension)</span></span>
- <span data-ttu-id="99a9d-114">Инвентаризация программного обеспечения (SIL)</span><span class="sxs-lookup"><span data-stu-id="99a9d-114">Software Inventory Logging (SIL)</span></span>
- <span data-ttu-id="99a9d-115">Поставщик CIM диспетчера сервера</span><span class="sxs-lookup"><span data-stu-id="99a9d-115">Server Manager CIM Provider</span></span>

## <a name="wmf-release-notes"></a><span data-ttu-id="99a9d-116">Заметки о выпуске WMF</span><span class="sxs-lookup"><span data-stu-id="99a9d-116">WMF Release Notes</span></span>
<span data-ttu-id="99a9d-117">Сведения о различных улучшениях в PowerShell и других компонентах определенной версии WMF см. по следующим ссылкам на заметки о выпусках:</span><span class="sxs-lookup"><span data-stu-id="99a9d-117">To learn about various enhancements in PowerShell and other components of a given WMF, please refer to the links below to review the release notes:</span></span>


- [<span data-ttu-id="99a9d-118">WMF 5.1 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="99a9d-118">WMF 5.1 (Preview)</span></span>](5.1/release-notes.md)
- [<span data-ttu-id="99a9d-119">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="99a9d-119">WMF 5.0</span></span>](5.0/releasenotes.md)


## <a name="wmf-availability-across-windows-operating-systems"></a><span data-ttu-id="99a9d-120">Доступность WMF в различных операционных системах Windows</span><span class="sxs-lookup"><span data-stu-id="99a9d-120">WMF Availability Across Windows Operating Systems</span></span>

><span data-ttu-id="99a9d-121">TODO: добавить ссылки на конкретные DLC WMF в заголовок столбца</span><span class="sxs-lookup"><span data-stu-id="99a9d-121">TODO: Add links to specific WMF DLC on the column header</span></span>

| <span data-ttu-id="99a9d-122">Версия операционной системы</span><span class="sxs-lookup"><span data-stu-id="99a9d-122">Operating System Version</span></span> | [<span data-ttu-id="99a9d-123">Предварительная версия WMF 5.1*</span><span class="sxs-lookup"><span data-stu-id="99a9d-123">WMF 5.1 Preview*</span></span>]() | [<span data-ttu-id="99a9d-124">WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="99a9d-124">WMF 5.0</span></span>]() | [<span data-ttu-id="99a9d-125">WMF 4.0</span><span class="sxs-lookup"><span data-stu-id="99a9d-125">WMF 4.0</span></span>]() |  [<span data-ttu-id="99a9d-126">WMF 3.0</span><span class="sxs-lookup"><span data-stu-id="99a9d-126">WMF 3.0</span></span>]() | [<span data-ttu-id="99a9d-127">WMF (2.0)</span><span class="sxs-lookup"><span data-stu-id="99a9d-127">WMF (2.0)</span></span>]() |
| ------------------------ | ----------- | ----------- | ----------- | ------------ |  ------------- |
| <span data-ttu-id="99a9d-128">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="99a9d-128">Windows Server 2016</span></span> | <span data-ttu-id="99a9d-129">Входит в комплект поставки *</span><span class="sxs-lookup"><span data-stu-id="99a9d-129">Ships in-box*</span></span> | <span data-ttu-id="99a9d-130">Входит в комплект поставки *</span><span class="sxs-lookup"><span data-stu-id="99a9d-130">Ships in-box*</span></span> |  |  |  |
| <span data-ttu-id="99a9d-131">Windows 10</span><span class="sxs-lookup"><span data-stu-id="99a9d-131">Windows 10</span></span> | <span data-ttu-id="99a9d-132">Входит в комплект поставки *</span><span class="sxs-lookup"><span data-stu-id="99a9d-132">Ships in-box*</span></span> | <span data-ttu-id="99a9d-133">Входит в комплект поставки *</span><span class="sxs-lookup"><span data-stu-id="99a9d-133">Ships in-box*</span></span>  | | | |  
| <span data-ttu-id="99a9d-134">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="99a9d-134">Windows Server 2012 R2</span></span>| <span data-ttu-id="99a9d-135">??</span><span class="sxs-lookup"><span data-stu-id="99a9d-135">??</span></span> | <span data-ttu-id="99a9d-136">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-136">Yes</span></span> | <span data-ttu-id="99a9d-137">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-137">Ships in-box</span></span> |  |  |
| <span data-ttu-id="99a9d-138">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="99a9d-138">Windows 8.1</span></span> | <span data-ttu-id="99a9d-139">??</span><span class="sxs-lookup"><span data-stu-id="99a9d-139">??</span></span> | <span data-ttu-id="99a9d-140">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-140">Yes</span></span> |  <span data-ttu-id="99a9d-141">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-141">Ships in-box</span></span> |  |  |
| <span data-ttu-id="99a9d-142">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="99a9d-142">Windows Server 2012</span></span> | <span data-ttu-id="99a9d-143">??</span><span class="sxs-lookup"><span data-stu-id="99a9d-143">??</span></span> | <span data-ttu-id="99a9d-144">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-144">Yes</span></span> | <span data-ttu-id="99a9d-145">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-145">Yes</span></span> |  <span data-ttu-id="99a9d-146">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-146">Ships in-box</span></span> | |
| <span data-ttu-id="99a9d-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="99a9d-147">Windows 8</span></span> |  |  |  | <span data-ttu-id="99a9d-148">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-148">Ships in-box</span></span> | |
| <span data-ttu-id="99a9d-149">Windows Server 2008 R2 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="99a9d-149">Windows Server 2008 R2 SP1</span></span> | <span data-ttu-id="99a9d-150">??</span><span class="sxs-lookup"><span data-stu-id="99a9d-150">??</span></span> | <span data-ttu-id="99a9d-151">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-151">Yes</span></span> | <span data-ttu-id="99a9d-152">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-152">Yes</span></span> |  <span data-ttu-id="99a9d-153">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-153">Yes</span></span>| <span data-ttu-id="99a9d-154">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-154">Ships in-box</span></span> |
| <span data-ttu-id="99a9d-155">Windows 7 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="99a9d-155">Windows 7 SP1</span></span>  | <span data-ttu-id="99a9d-156">??</span><span class="sxs-lookup"><span data-stu-id="99a9d-156">??</span></span> | <span data-ttu-id="99a9d-157">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-157">Yes</span></span> | <span data-ttu-id="99a9d-158">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-158">Yes</span></span> | <span data-ttu-id="99a9d-159">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-159">Yes</span></span> | <span data-ttu-id="99a9d-160">Входит в комплект поставки</span><span class="sxs-lookup"><span data-stu-id="99a9d-160">Ships in-box</span></span> |
| <span data-ttu-id="99a9d-161">Windows Server 2008 с пакетом обновления 2 (SP2)</span><span class="sxs-lookup"><span data-stu-id="99a9d-161">Windows Server 2008 SP2</span></span> | | | | <span data-ttu-id="99a9d-162">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-162">Yes</span></span> | <span data-ttu-id="99a9d-163">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-163">Yes</span></span> |
| <span data-ttu-id="99a9d-164">Windows Vista</span><span class="sxs-lookup"><span data-stu-id="99a9d-164">Windows Vista</span></span> | | | | | <span data-ttu-id="99a9d-165">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-165">Yes</span></span> |
| <span data-ttu-id="99a9d-166">Windows Server 2003</span><span class="sxs-lookup"><span data-stu-id="99a9d-166">Windows Server 2003</span></span>| | | |  | <span data-ttu-id="99a9d-167">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-167">Yes</span></span> |
| <span data-ttu-id="99a9d-168">Windows XP</span><span class="sxs-lookup"><span data-stu-id="99a9d-168">Windows XP</span></span> | | | |  | <span data-ttu-id="99a9d-169">Да</span><span class="sxs-lookup"><span data-stu-id="99a9d-169">Yes</span></span> |

><span data-ttu-id="99a9d-170">TODO: объяснить значение значка * в приведенной выше таблице</span><span class="sxs-lookup"><span data-stu-id="99a9d-170">TODO: Explain * in the above table</span></span>
