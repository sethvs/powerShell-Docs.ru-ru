---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "пример шаблона с описанием известной проблемы или ограничения"
ms.openlocfilehash: b93393b2c84e76a301e6406d1388e82e95a2959c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
><span data-ttu-id="9f9e7-103">Примечание. Предоставьте предложенное описательное название и краткое описание.</span><span class="sxs-lookup"><span data-stu-id="9f9e7-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="9f9e7-104">Пример. Ложные ошибки ExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="9f9e7-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="9f9e7-105">В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.</span><span class="sxs-lookup"><span data-stu-id="9f9e7-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="9f9e7-106">Разрешение</span><span class="sxs-lookup"><span data-stu-id="9f9e7-106">Resolution</span></span>

<span data-ttu-id="9f9e7-107">Чтобы устранить проблему, задайте для **ExecutionPolicy** значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):</span><span class="sxs-lookup"><span data-stu-id="9f9e7-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

