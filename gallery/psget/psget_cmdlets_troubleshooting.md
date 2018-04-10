---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: psget_устранение_проблем_с_командлетами
ms.openlocfilehash: bc49dc78b8205d1194ddfe4bdca98b3e681860bd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="ebd64-103">Как разрешить проблему "ПРЕДУПРЕЖДЕНИЕ. Не удалось скачать пакет "имя вашего пакета""?</span><span class="sxs-lookup"><span data-stu-id="ebd64-103">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>




<span data-ttu-id="ebd64-104">Нам известно, что на некоторых компьютерах командлеты Install-Module и Update-Module могут завершаться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="ebd64-104">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="ebd64-105">По результатам нашего расследования это связано с сетевым подключением.</span><span class="sxs-lookup"><span data-stu-id="ebd64-105">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="ebd64-106">Недавно мы обновили поставщик NuGet, чтобы он смог надежно скачивать пакеты.</span><span class="sxs-lookup"><span data-stu-id="ebd64-106">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="ebd64-107">Выполните описанные ниже инструкции, чтобы установить последнюю сборку поставщика NuGet, а затем установите или обновите свой модуль.</span><span class="sxs-lookup"><span data-stu-id="ebd64-107">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="ebd64-108">Для примера возьмем модуль Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd64-108">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```