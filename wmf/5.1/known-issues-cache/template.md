---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
title: пример шаблона с описанием известной проблемы или ограничения
ms.openlocfilehash: cecf31127aaa1942471877a2056230ab592bd095
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
><span data-ttu-id="008f4-103">Примечание. Предоставьте предложенное описательное название и краткое описание.</span><span class="sxs-lookup"><span data-stu-id="008f4-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="008f4-104">Пример. Ложные ошибки ExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="008f4-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="008f4-105">В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.</span><span class="sxs-lookup"><span data-stu-id="008f4-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="008f4-106">Разрешение</span><span class="sxs-lookup"><span data-stu-id="008f4-106">Resolution</span></span>

<span data-ttu-id="008f4-107">Чтобы устранить проблему, задайте для **ExecutionPolicy** значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):</span><span class="sxs-lookup"><span data-stu-id="008f4-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```