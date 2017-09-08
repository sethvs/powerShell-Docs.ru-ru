---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "удаление pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: d316cb98efc730ed3e99f6a5dac2b969e3437129
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="remove-pswaauthorizationrule"></a>Remove-PswaAuthorizationRule

##  <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Удаляет указанное правило авторизации из Windows PowerShell® Web Access.

## <a name="syntax"></a>СИНТАКСИС

###  <a name="id"></a>Id
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a>Правило
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Удаляет указанное правило авторизации из Windows PowerShell Web Access.

## <a name="parameters"></a>ПАРАМЕТРЫ

### <a name="-force"></a>-Force

Запуск командлета без запроса на подтверждение. По умолчанию командлет запрашивает подтверждение, прежде чем продолжить работу.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-id-ltint32gt"></a>-Id &lt;Int32\[\]&gt;

Указывает идентификаторы (ID) одного или нескольких удаляемых правил.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue, ByPropertyName)       |
| Принимать подстановочные знаки?          | false                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Rule &lt;PswaAuthorizationRule\[\]&gt;

Указывает правила, которые необходимо удалить.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue)                       |
| Принимать подстановочные знаки?          | false                                |

### <a name="-confirm"></a>-Confirm

Запрос на подтверждение перед выполнением командлета.

|||  
|-|-|
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | false                                |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-whatif"></a>-WhatIf

Показывает, что произойдет при запуске командлета. Командлет не запущен.

|||  
|-|-|
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | false                                |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.
Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>ВХОДНЫЕ ДАННЫЕ

###  <a name="int"></a>int\[\]

Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.

###  <a name="pswaauthorizationrule"></a>PswaAuthorizationRule\[\]

Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.

##  <a name="outputs"></a>ВЫХОДНЫЕ ДАННЫЕ

Этот командлет не создает выходные данные.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

Этот пример удаляет правило авторизации с идентификатором *2*.

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a>ПРИМЕР 2 {#example-2 .subHeading}

Этот пример удаляет все правила авторизации, а также требует подтверждения пользователя.

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

##  <a name="related-topics"></a>Связанные темы

-  [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
-  [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
-  [Install-PswaWebApplication](install-pswawebapplication.md)
-  [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
