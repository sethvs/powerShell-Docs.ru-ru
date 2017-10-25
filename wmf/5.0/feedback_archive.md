---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 7ad4a00f7beba0de70696d88cd5448c7c638c50c
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2017
---
# <a name="archive-cmdlets"></a><span data-ttu-id="2e74d-102">Командлеты Archive</span><span class="sxs-lookup"><span data-stu-id="2e74d-102">Archive cmdlets</span></span>

<span data-ttu-id="2e74d-103">Два новых командлета **Compress-Archive** и **Expand-Archive** позволяют сжимать и распаковывать ZIP-файлы.</span><span class="sxs-lookup"><span data-stu-id="2e74d-103">Two new cmdlets, **Compress-Archive** and **Expand-Archive**, let you compress and expand ZIP files.</span></span>

## <a name="compress-archive"></a><span data-ttu-id="2e74d-104">Compress-Archive</span><span class="sxs-lookup"><span data-stu-id="2e74d-104">Compress-Archive</span></span>
<span data-ttu-id="2e74d-105">Командлет **Compress-Archive** создает новый файл архива из указанных файлов.</span><span class="sxs-lookup"><span data-stu-id="2e74d-105">The **Compress-Archive** cmdlet creates a new archive file from specified files.</span></span> <span data-ttu-id="2e74d-106">Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения.</span><span class="sxs-lookup"><span data-stu-id="2e74d-106">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span> <span data-ttu-id="2e74d-107">Файл архива можно сжать с помощью алгоритма, указанного в параметре **-CompressionLevel**.</span><span class="sxs-lookup"><span data-stu-id="2e74d-107">An archive file can be compressed by using a compression algorithm specified in the **-CompressionLevel** parameter.</span></span>
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a><span data-ttu-id="2e74d-108">Expand-Archive</span><span class="sxs-lookup"><span data-stu-id="2e74d-108">Expand-Archive</span></span>
<span data-ttu-id="2e74d-109">Командлет **Expand-Archive** извлекает файлы из указанного файла архива.</span><span class="sxs-lookup"><span data-stu-id="2e74d-109">The **Expand-Archive** cmdlet extracts files from a specified archive file.</span></span> <span data-ttu-id="2e74d-110">Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения.</span><span class="sxs-lookup"><span data-stu-id="2e74d-110">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span>
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```

