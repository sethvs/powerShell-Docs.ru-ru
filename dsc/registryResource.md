---
title: "Ресурс Registry в DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: d94f178fb75d15b12268ad783f78183ceba9f2b3
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-registry-resource"></a>Ресурс Registry в DSC

> Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурс **Registry** в DSC Windows PowerShell предоставляет механизм управления разделами и значениями реестра на целевом узле.

## <a name="syntax"></a>Синтаксис

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a>Свойства
|  Свойство  |  Описание   | 
|---|---| 
| Клавиши| Указывает путь к разделу реестра, для которого требуется обеспечить определенное состояние. Этот путь должен включать куст.| 
| ValueName| Указывает имя значения реестра.| 
| Ensure| Указывает, существует ли ключ и значение. Для этого укажите для этого свойства значение Present. Чтобы они не существовали, укажите для этого свойства значение Absent. Значение по умолчанию — Present.| 
| Force| Если указанный раздел реестра присутствует, __Force__ перезаписывает его новым значением.| 
| Hex| Указывает, будут ли данные выражены в шестнадцатеричном формате. Если свойство задано, данные значения DWORD/QWORD будут представлены в шестнадцатеричном формате. Недопустимо для других типов. Значение по умолчанию — __$false__.| 
| DependsOn| Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса. Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.| 
| ValueData| Данные для значения реестра.| 
| ValueType| Указывает тип значения. Поддерживаемые типы: 
<ul><li>строка (REG_SZ);</li>


<li>двоичный файл (REG-BINARY);</li>


<li>Dword, 32-разрядный (REG_DWORD);</li>


<li>Qword, 64-разрядный (REG_QWORD);</li>


<li>несколько строк (REG_MULTI_SZ);</li>


<li>расширяемая строка (REG_EXPAND_SZ).</li></ul>

## <a name="example"></a>Пример
В этом примере гарантируется, что ключ с именем ExampleKey присутствует в кусте **HKEY\_LOCAL\_MACHINE**.
```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

>**Примечание.**. Для изменения настройки реестра в кусте **HKEY\_CURRENT\_USER** требуется запустить конфигурацию с использованием учетных данных пользователя, а не системных.
>Вы можете использовать свойство **PsDscRunAsCredential**, чтобы указать учетные данные пользователя для конфигурации. Пример см. в статье [Запуск DSC с использованием учетных данных пользователя](runAsUser.md).



