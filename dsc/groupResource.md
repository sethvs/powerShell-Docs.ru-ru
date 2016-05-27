---
title:   Ресурс Group в DSC
ms.date:  2016-05-16
keywords:  powershell,DSC
description:  
ms.topic:  article
author:  eslesar
manager:  dongill
ms.prod:  powershell
---

# Ресурс Group в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс Group в DSC Windows PowerShell предоставляет механизм управления локальными группами на целевом узле.

##Синтаксис##
```
Group [string] #ResourceName
{
    GroupName = [string]
    [ Credential = [PSCredential] ]
    [ Description = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Members = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn = [string[]] ]
}
```

## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| GroupName| Имя группы, для которой требуется обеспечить определенное состояние.| 
| Учетные данные| Учетные данные, необходимые для доступа к удаленным ресурсам. **Примечание**. Учетная запись должна иметь соответствующие разрешения Active Directory для добавления в группу любых нелокальных учетных записей; в противном случае произойдет ошибка.
| Описание| Описание группы.| 
| Ensure| Указывает, существует ли группа. Чтобы убедиться, что группа не существует, укажите для этого свойства значение Absent. Чтобы убедиться, что группа существует, укажите для этого свойства значение Present (используется по умолчанию).| 
| Члены группы| Используйте это свойство для замены текущего членства в группе заданными участниками. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **MembersToExclude** или **MembersToInclude**. Это приведет к ошибке.| 
| MembersToExclude| Это свойство используется для удаления участников из существующего членства в группе. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **Members**. Это приведет к ошибке.| 
| MembersToInclude| Это свойство используется для добавления участников в существующее членство в группе. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **Members**. Это приведет к ошибке.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: "DependsOn = "[ResourceType]ResourceName"".| 

## Пример 1

Следующий пример показывает, как проверить, что группа с именем TestGroup не существует. 

```powershell
Group GroupExample
{
    # This will remove TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
## Пример 2.
Следующий пример демонстрирует добавление пользователя Active Directory в группу локальных администраторов в лабораторной сборке с несколькими компьютерами, в которой уже используется объект PSCredential для учетной записи локального администратора. Поскольку этот объект также используется для учетной записи администратора домена (после повышения роли домена), нам потребуется преобразовать этот существующий объект PSCredential в понятные учетные данные домена, чтобы можно было добавить пользователя домена в группу локальных администраторов на рядовом сервере.

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
     @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'   
      }    
    )
}
                  
$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup
        {
            GroupName='Administrators'   
            Ensure= 'Present'             
            MembersToInclude= "$domain\$($Node.AdminAccount)"
            Credential = $dCredential    
            PsDscRunAsCredential = $DCredential
        }
```



<!--HONumber=May16_HO3-->


