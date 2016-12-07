# <a name="archive-cmdlets"></a>Командлеты Archive

Два новых командлета **Compress-Archive** и **Expand-Archive** позволяют сжимать и распаковывать ZIP-файлы.

## <a name="compress-archive"></a>Compress-Archive
Командлет **Compress-Archive** создает новый файл архива из указанных файлов. Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения. Файл архива можно сжать с помощью алгоритма, указанного в параметре **-CompressionLevel**.
```PowerShell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>] 
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Expand-Archive
Командлет **Expand-Archive** извлекает файлы из указанного файла архива. Файл архива позволяет упаковать и при необходимости сжать несколько файлов в один для упрощения обработки и хранения.
```PowerShell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
