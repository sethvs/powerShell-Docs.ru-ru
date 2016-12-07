---
title: "Ресурс User в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 84ed3408cfef1dbc99f6f3147ae36be09bca67e4
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
#<a name="dsc-user-resource"></a>Ресурс User в DSC#

 
>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0


Ресурс __User__ в DSC Windows PowerShell предоставляет механизм управления локальными учетными записями на целевом узле.


##<a name="syntax"></a>Синтаксис##

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   | 
|---|---| 
| UserName| Указывает имя учетной записи, для которой требуется обеспечить определенное состояние.| 
| Описание| Указывает описание учетной записи пользователя.| 
| Отключен| Указывает, включена ли учетная запись. Присвойте этому свойству значение __$true__, чтобы отключить учетную запись, и __$false__, чтобы включить ее.| 
| Ensure| Указывает, существует ли учетная запись. Присвойте этому свойству значение Present, если учетная запись существует, и Absent, если не существует.| 
| FullName| Представляет строку с полным именем для учетной записи пользователя.| 
| Пароль| Указывает пароль для этой учетной записи. | 
| PasswordChangeNotAllowed| Указывает, может ли пользователь изменить пароль. Присвойте этому свойству значение __$true__, чтобы пользователь не мог изменить пароль, и __$false__, чтобы мог. Значение по умолчанию — __$false__.| 
| PasswordChangeRequired| Указывает, требуется ли смена пароля при следующем входе пользователя в систему. Присвойте этому свойству значение __$true__, если пользователь должен изменить пароль. По умолчанию используется значение __$true__.| 
| PasswordNeverExpires| Указывает, может ли истечь срок действия пароля. Присвойте этому свойству значение __$true__, чтобы срок действия пароля никогда не истекал, и __$false__ в противном случае. Значение по умолчанию — __$false__.| 
| DependsOn | Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Пример

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = “[Group]GroupExample" # Configures GroupExample first
}
```

