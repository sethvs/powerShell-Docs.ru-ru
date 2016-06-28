---
title: "Ресурс nxArchive в DSC для Linux"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 6477ae8575c83fc24150f9502515ff5b82bc8198
ms.openlocfilehash: 2edbc1d11dfc7c84369430688a8b0d773277e864

---

# Ресурс nxArchive в DSC для Linux

Ресурс **nxArchive** в DSC PowerShell предоставляет механизм распаковки файлов архивов (TAR, ZIP) в указанную папку на узле с Linux.

## Синтаксис

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## Свойства

|  Свойство |  Описание | 
|---|---|
| SourcePath| Указывает исходный путь для файла архива. Это должен быть файл в формате TAR, ZIP или TAR.GZ. | 
| DestinationPath| Указывает, куда будет извлечено содержимое архива.| 
| Контрольная сумма| Указывает тип для использования при определении факта обновления исходного архива. Значения: ctime, mtime или md5. Значение по умолчанию — md5.| 
| Force| Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку. Свойство **Force** позволяет переопределять такие ошибки. Значение по умолчанию — **$false**.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| Ensure| Указывает необходимость проверки того, существует ли содержимое архива в **папке назначения**. Чтобы убедиться, что содержимое существует, укажите для этого свойства значение Present. Чтобы убедиться, что содержимое не существует, укажите для этого свойства значение Absent. Значение по умолчанию — Present.| 

## Пример

В следующем примере показано, как использовать ресурс **nxArchive**, чтобы убедиться, что содержимое архивного файла с именем `website.tar` существует и извлекается в указанную папку.

```
Import-DSCResource -Module nx 

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
} 
```




<!--HONumber=Jun16_HO4-->


