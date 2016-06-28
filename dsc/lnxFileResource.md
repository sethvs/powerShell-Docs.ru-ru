---
title: "Ресурс nxFile в DSC для Linux"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 6477ae8575c83fc24150f9502515ff5b82bc8198
ms.openlocfilehash: 2ba44df5dd6c91371cbbfe95d48184a4ff4a7738

---

# Ресурс nxFile в DSC для Linux

Ресурс **nxFile** в настройке требуемого состояния PowerShell предоставляет механизм управления файлами и каталогами на узле Linux.

## Синтаксис

```
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Ensure = <string> { Absent | Present }  ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]

}
```

## Свойства

|  Свойство |  Описание | 
|---|---|
| DestinationPath| Указывает, в каком расположении нужно проверить состояние файла или каталога.| 
| SourcePath| Указывает, откуда нужно скопировать файл или папку. Этот может быть локальный путь или URL-адрес `http/https/ftp`. Удаленные URL-адреса `http/https/ftp` поддерживаются, только если для свойства **Type** выбрано значение file.| 
| Ensure| Определяет, нужно ли проверять существование файла. Чтобы убедиться, что файл существует, укажите для этого свойства значение Present. Чтобы убедиться, что файл не существует, укажите для этого свойства значение Absent. Значение по умолчанию — Present.| 
| Type| Указывает, является ли настраиваемый ресурс каталогом или файлом. Если выбрано значение directory, то ресурс является каталогом, а если значение file, то файлом. Значение по умолчанию — file.| 
| Содержимое| Указывает содержимое файла, например определенную строку.| 
| Контрольная сумма| Определяет тип проверки пары файлов на идентичность. Если свойство **Checksum** не задано, для сравнения используется только имя файла или каталога. Значения: ctime, mtime или md5.| 
| Recurse| Указывает, используются ли вложенные папки. Если свойство имеет значение **$true**, вложенные папки включаются. Значение по умолчанию — **$false**. **Примечание**. Это свойство можно использовать только в том случае, если свойство **Type** имеет значение directory.| 
| Force| Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку. Свойство **Force** позволяет переопределять такие ошибки. Значение по умолчанию — **$false**.| 
| Ссылки| Определяет желаемое поведение символических ссылок. Если для свойства установлено значение follow, символические ссылки отслеживаются, а к целевым объектам применяются действия (например, копирование файла вместо ссылки). Если установлено значение manage, действие применяется к ссылке (например, копирование ссылки). Если установлено значение ignore, символические ссылки игнорируются.| 
| Группа| Имя ресурса **Group** — владельца файла или каталога.| 
| Режим| Указывает нужные разрешения для ресурса в восьмеричной или символьной нотации (например, 777 или rwxrwxrwx). Если используется символьная нотация, не указывайте первый символ, обозначающий каталог или файл.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 

## Дополнительные сведения


Linux и Windows используют разные символы разрыва строки в текстовых файлах по умолчанию, что может привести к непредвиденным результатам при настройке некоторых файлов на компьютере Linux с помощью __nxFile__. Избежать проблем из-за непредвиденных символов разрыва строки при работе с содержанием файла Linux можно разными способами:

Шаг 1. Скопируйте файл из удаленного источника (http, https или ftp): создайте файл с нужным содержанием на компьютере Linux и поместите его на веб- или FTP-сервер, доступный для настраиваемого узла. Определите свойство __SourcePath__ в ресурсе __nxFile__, указав URL-адрес файла на веб- или FTP-сервере.

```
Import-DSCResource -Module nx
Node $Node
{
nxFile resolvConf
{
    SourcePath = "http://10.185.85.11/conf/resolv.conf"
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    
}
        
}
```


Шаг 2. Прочтите содержимое файла в сценарии PowerShell с помощью командлета [Get-Content](https://technet.microsoft.com/en-us/library/hh849787.aspx), настроив с помощью свойства __$OFS__ использование символа разрыва строки Linux.


```
Import-DSCResource -Module nx
Node $Node
{
$OFS = "`n"
$Contents = Get-Content C:\temp\resolv.conf

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = "$Contents"
}

}
```


Шаг 3. Воспользуйтесь функцией PowerShell для замены символов разрыва строки в Windows на символы разрыва строки в Linux.

```
Function LinuxString($inputStr){
    $outputStr = $inputStr.Replace("`r`n","`n")
    $ouputStr += "`n"
    Return $outputStr
}

Import-DSCResource -Module nx
Node $Node
{

$Contents = @'
search contoso.com
domain contoso.com
nameserver 10.185.85.11
'@

$Contents = LinuxString $Contents

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = $Contents
    
}
}
```

## Пример

В следующем примере проверяется существование каталога `/opt/mydir` и файла с указанным содержимым в этом каталоге.

```
Import-DSCResource -Module nx 

Node $node {
nxFile DirectoryExample
{
   Ensure = "Present"
   DestinationPath = "/opt/mydir"
   Type = "Directory"
}

nxFile FileExample
{
    Ensure = "Present"
    Destinationpath = "/opt/mydir/myfile"
    Contents=@"
#!/bin/bash`necho "hello world"`n
"@ 
    Mode = “755”
    DependsOn = "[nxFile]DirectoryExample"
} 
}
```




<!--HONumber=Jun16_HO4-->


