---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 0c450d765531c18c0b73c5c64262e9895f92068a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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