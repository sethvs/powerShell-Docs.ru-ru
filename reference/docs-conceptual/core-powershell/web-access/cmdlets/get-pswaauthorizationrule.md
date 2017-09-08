---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "получение pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: 43997320ec7ab779b2061a0af88f97db0b7e93d6
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="get-pswaauthorizationrule"></a>Get-PswaAuthorizationRule

##  <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Возвращает набор правил авторизации Windows PowerShell® Web Access.

##  <a name="syntax"></a>Синтаксис

###  <a name="id"></a>ID
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

###  <a name="name"></a>Название
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Командлет **Get-PswaAuthorizationRule** возвращает набор правил авторизации Windows PowerShell® Web Access.
Если не заданы параметры **Id** или **RuleName**, этот командлет перечисляет все правила. Параметр **Id** можно использовать для фильтрации результатов.

## <a name="parameters"></a>ПАРАМЕТРЫ

### <a name="-idltint32gt"></a>-Id&lt;Int32\[\]&gt;

Указывает идентификаторы (ID) правил, которые должен получить этот командлет. Если идентификаторы не указаны, этот командлет возвращает все правила авторизации.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue, ByPropertyName)       |
| Принимать подстановочные знаки?          | false                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;строка\[\]&gt;

Указывает имена правил авторизации для получения. Этот параметр возвращает все правила, имена которых точно соответствуют именам правил в строках этого массива.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue, ByPropertyName)       |
| Принимать подстановочные знаки?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.
Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>ВХОДНЫЕ ДАННЫЕ

###  <a name="int"></a>int\[\]

Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.

###  <a name="string"></a>String\[\]

Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.

##  <a name="outputs"></a>ВЫХОДНЫЕ ДАННЫЕ

###  <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Этот командлет создает объект PswaAuthorizationRule в качестве выходных данных.


## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

Этот пример получает все правила.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a>ПРИМЕР 2

Этот пример получает правило с идентификатором *2*.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a>ПРИМЕР 3 {#example-3 .subHeading}

В этом примере показано, как командлет принимает значение из конвейера.
В этот командлет передаются идентификатор и имя правила.

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

##  <a name="related-topics"></a>Связанные темы

-  [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
-  [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
-  [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
-  [Install-PswaWebApplication](install-pswawebapplication.md)
