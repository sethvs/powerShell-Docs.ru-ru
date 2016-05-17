---
title:   Ресурс nxService в DSC для Linux
ms.date:  2016-05-16
keywords:  powershell,DSC
description:  
ms.topic:  article
author:  eslesar
manager:  dongill
ms.prod:  powershell
---

# Ресурс nxService в DSC для Linux

Ресурс **nxService** в настройке требуемого состояния PowerShell предоставляет механизм управления службами на узле Linux.

## Синтаксис

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | system }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## Свойства
|  Свойство |  Описание | 
|---|---|
| Название| Указывает имя службы или управляющей программы, которую нужно настроить.| 
| Контроллер| Указывает тип контроллера для использования при настройке службы.| 
| Включен| Указывает, запускается ли служба во время загрузки.| 
| State| Указывает, запущена ли служба. Установите для этого свойства значение Stopped, чтобы служба не выполнялась. Установите для этого свойства значение Running, чтобы служба выполнялась.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 


## Дополнительные сведения

Ресурс **nxService** не создает определение или сценарий службы, если они не существуют. Ресурс **nxFile** настройки требуемого состояния PowerShell можно использовать для управления существованием или содержанием сценария или файла определения службы.

## Пример

В следующем примере показана конфигурация службы httpd (для HTTP-сервера Apache), зарегистрированной на контроллере службы **SystemD**.

```
Import-DSCResource -Module nx 

Node $node {
#Apache Service
nxService ApacheService 
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```



<!--HONumber=May16_HO3-->


