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
# <a name="archive-cmdlets"></a>Командлеты Archive

Два новых командлета **Compress-Archive** и **Expand-Archive** позволяют сжимать и распаковывать ZIP-файлы.

## <a name="compress-archive"></a>Compress-Archive
Командлет **Compress-Archive** создает новый файл архива из указанных файлов. Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения. Файл архива можно сжать с помощью алгоритма, указанного в параметре **-CompressionLevel**.
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Expand-Archive
Командлет **Expand-Archive** извлекает файлы из указанного файла архива. Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения.
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```

