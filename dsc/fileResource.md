---
title: "Ресурс File в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: df9bb0362e82757ed1580cc4ace27735414a3e6d
ms.openlocfilehash: 8c8fb7a40c066b048e1a54a741f4953e6b5a47b6

---

# Ресурс File в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс File в DSC Windows PowerShell предоставляет механизм управления файлами и папками на целевом узле.

>**Примечание**. Если свойство **MatchSource** имеет значение **$false** (значение по умолчанию), копируемое содержимое будет кэшироваться при первом применении конфигурации. 
>При последующем применении конфигурации файлы и папки в пути, указанном в параметре **SourcePath**, не будут проверяться на наличие обновлений. Если вы хотите, чтобы файлы и папки в **SourcePath** проверялись на наличие обновлений при каждом применении конфигурации, установите для свойства **MatchSource** значение **$true**. 

## Синтаксис
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ] 
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ] 
    [ MatchSource = [bool] ]
}
```

## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| DestinationPath| Указывает, в каком расположении нужно проверить состояние файла или каталога.| 
| Атрибуты| Указывает требуемое состояние атрибутов для целевого файла или папки.| 
| Контрольная сумма| Указывает тип контрольной суммы для использования при проверке двух файлов на идентичность. Если свойство __Checksum__ не задано, для сравнения используется только имя файла или каталога. Допустимые значения: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.| 
| Содержимое| Указывает содержимое файла, например определенную строку.| 
| Учетные данные| Указывает учетные данные, необходимые для доступа к ресурсам (например, к исходным файлам), если такой доступ является обязательным.| 
| Ensure| Указывает, существует ли файл или каталог. Чтобы убедиться, что файл или каталог не существует, укажите для этого свойства значение Absent. Чтобы убедиться, что файл или каталог существует, укажите для этого свойства значение Present. Значение по умолчанию — Present.| 
| Force| Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку. Свойство Force позволяет переопределять такие ошибки. Значение по умолчанию — __$false__.| 
| Recurse| Указывает, используются ли вложенные папки. Если свойство имеет значение __$true__, вложенные папки включаются. Значение по умолчанию — __$false__. **Примечание**. Это свойство можно использовать только в том случае, если свойство Type имеет значение Directory.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| SourcePath| Указывает, откуда нужно скопировать файл или папку.| 
| Type| Указывает, является ли настраиваемый ресурс каталогом или файлом. Если выбрано значение Directory, то ресурс является каталогом, а если значение File, то файлом. Значение по умолчанию — File.| 
| MatchSource| Если используется значение по умолчанию __$false__, все файлы в источнике (например, файлы A, B и C) добавляются в папку назначения при первом применении конфигурации. Если в источник добавляется новый файл (D), он не будет добавлен в папку назначения даже при последующем повторном применении конфигурации. Если используется значение __$true__, при каждом применении конфигурации в папку назначения будут добавляться все найденные новые файлы (в нашем примере это файл D). Значение по умолчанию — **$false**.| 

## Пример

В представленном ниже примере показано, как использовать ресурс файла, чтобы проверить наличие каталога `C:\Users\Public\Documents\DSCDemo\DemoSource` (вместе со всеми подкаталогами) с исходного компьютера (например, опрашивающего сервера) на целевом узле. Кроме того, по завершении настройки в журнал записывается сообщение и указывается оператор, гарантирующий запуск операции проверки файла перед операцией записи в журнал.

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"    
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```




<!--HONumber=Jul16_HO2-->


