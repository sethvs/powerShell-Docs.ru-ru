---
title:   Ресурс nxUser в DSC для Linux
ms.date:  2016-05-16
keywords:  powershell,DSC
description:  
ms.topic:  article
author:  eslesar
manager:  dongill
ms.prod:  powershell
---

# Ресурс nxUser в DSC для Linux

Ресурс **nxUser** в DSC PowerShell предоставляет механизм управления локальными пользователями на узле Linux.

## Синтаксис

```
nxUser <string> #ResourceName
{
    UserName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ FullName = <string> ]
    [ Description = <string> ]
    [ Password = <string> ]
    [ Disabled = <bool> ]
    [ PasswordChangeRequired = <bool> ]
    [ HomeDirectory = <string> ]
    [ Mode = <string> ]
    [ GroupID = <string> ]
    [ DependsOn = <string[]> ]

}
```

## Свойства

|  Свойство |  Указывает имя учетной записи, для которой требуется обеспечить определенное состояние. | 
|---|---|
| UserName| Указывает, в каком расположении нужно проверить состояние файла или каталога.| 
| Ensure| Указывает, существует ли учетная запись. Присвойте этому свойству значение Present, если учетная запись существует, и Absent, если не существует.| 
| FullName| Строка, содержащая полное имя учетной записи пользователя.| 
| Описание| Описание учетной записи пользователя.| 
| Пароль| Хэш пароля пользователя в соответствующей форме для компьютера с Linux. Обычно это защищенный хэш SHA-256 или SHA-512. В Debian и Ubuntu Linux это значение можно создать с помощью команды mkpasswd. В других дистрибутивах Linux для создания хэша можно использовать метод шифрования криптографической библиотеки Python.| 
| Отключен| Указывает, включено ли правило. Присвойте этому свойству значение **$true**, чтобы отключить учетную запись, и **$false**, чтобы включить ее.| 
| PasswordChangeRequired| Указывает, может ли пользователь изменить пароль. Присвойте этому свойству значение **$true**, чтобы пользователь не мог изменить пароль, и **$false**, чтобы мог. Значение по умолчанию — **$false**. Это свойство применяется только в том случае, если учетная запись пользователя ранее не существовала и находится в процессе создания.| 
| HomeDirectory| Домашний каталог пользователя.| 
| GroupID| ИД основной группы пользователя.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 

## Пример

В следующем примере проверяется, что пользователь monuser существует и является членом группы DBusers.

```
Import-DSCResource -Module nx 

Node $node {
nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}
 
nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"            
}
}
```



<!--HONumber=May16_HO3-->


