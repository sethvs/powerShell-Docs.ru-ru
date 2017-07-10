---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс Group в DSC"
ms.openlocfilehash: 6fb6c5f9593687d7204ff31fddd9bca978ed2707
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="dsc-group-resource" class="xliff"></a>
# Ресурс Group в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс Group в DSC Windows PowerShell предоставляет механизм управления локальными группами на целевом узле.

<a id="syntax" class="xliff"></a>
## Синтаксис
```
Group [string] #ResourceName
{
    GroupName          = [string]
    [ Credential       = [PSCredential] ]
    [ Description      = [string[]] ]
    [ Ensure           = [string] { Absent | Present }  ]
    [ Members          = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn        = [string[]] ]
}
```

<a id="properties" class="xliff"></a>
## Свойства

|  Свойство  |  Описание   | 
|---|---| 
| GroupName| Имя группы, для которой требуется обеспечить определенное состояние.| 
| Учетные данные| Учетные данные, необходимые для доступа к удаленным ресурсам. **Примечание**. Учетная запись должна иметь соответствующие разрешения Active Directory на добавление в группу любых нелокальных учетных записей. Иначе во время выполнения конфигурации на целевом узле произойдет ошибка.  
| Описание| Описание группы.| 
| Ensure| Указывает, существует ли группа. Чтобы убедиться, что группа не существует, укажите для этого свойства значение Absent. Чтобы убедиться, что группа существует, укажите для этого свойства значение Present (используется по умолчанию).| 
| Члены группы| Используйте это свойство для замены текущего членства в группе заданными участниками. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **MembersToExclude** или **MembersToInclude**. Это приводит к ошибке.| 
| MembersToExclude| Это свойство используется для удаления участников из существующего членства в группе. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **Members**. Это приводит к ошибке.| 
| MembersToInclude| Это свойство используется для добавления участников в существующее членство в группе. Значение этого свойства хранится в массиве строк в формате *домен*\\*имя_пользователя*. Если вы задали это свойство в конфигурации, не используйте свойство **Members**. Это приведет к ошибке.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: "DependsOn = "[ResourceType]ResourceName"".| 

<a id="example-1" class="xliff"></a>
## Пример 1

Следующий пример показывает, как проверить, что группа с именем TestGroup не существует. 

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
<a id="example-2" class="xliff"></a>
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

<a id="example-3" class="xliff"></a>
## Пример 3
В примере ниже показано, как настроить локальную группу TigerTeamAdmins на сервере TigerTeamSource.Contoso.Com, чтобы она не содержала определенную учетную запись домена Contoso\JerryG.  

```powershell

Configuration SecureTigerTeamSrouce 
{
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'
  
  Node TigerTeamSource.Contoso.Com {
  Group TigerTeamAdmins
    {
       GroupName        = 'TigerTeamAdmins'   
       Ensure           = 'Absent'             
       MembersToInclude = "Contoso\JerryG"
    }
  }
}
```

