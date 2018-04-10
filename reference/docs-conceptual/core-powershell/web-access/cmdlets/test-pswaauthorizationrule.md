---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: проверка pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: ed6d56b2f3c4ee4ac410cdaadda312bffe506ee9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="test-pswaauthorizationrule"></a>Test-PswaAuthorizationRule

## <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.

## <a name="syntax"></a>СИНТАКСИС

### <a name="computername"></a>имя_компьютера
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a>ConnectionUri
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Командлет **Test-PswaAuthorizationRule** проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.
Этот командлет также можно использовать для тестирования правил авторизации, чтобы гарантировать, что запрос на доступ конкретного пользователя, компьютера или конечной точки авторизован.
По умолчанию этот командлет проверяет все правила в файле авторизации.
Тем не менее можно указать набор правил для проверки.

Этот командлет можно использовать для устранения неполадок проверки подлинности.

Параметры для этого командлета соответствуют полям на странице входа Windows PowerShell® Web Access.

## <a name="parameters"></a>ПАРАМЕТРЫ

### <a name="-computername-ltstringgt"></a>-ComputerName &lt;строка&gt;

Задает имя проверяемого компьютера.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-configurationname-ltstringgt"></a>-ConfigurationName &lt;строка&gt;

Указывает имя конфигурации сеанса Windows PowerShell (также известной как конечная точка или пространство выполнения) для проверки.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | 3                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-connectionuri-lturigt"></a>-ConnectionUri &lt;Uri&gt;

Указывает URI подключения для проверки.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 2                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-credential-ltpscredentialgt"></a>-Credential &lt;PSCredential&gt;

Указывает объект **PSCredential** для учетной записи пользователя, который предполагается использовать для проверки правил авторизации Windows PowerShell Web Access. Если этот параметр не добавлен, командлет будет использовать учетную запись текущего пользователя. Чтобы получить объект **PSCredential**, который требуется для удаленной проверки правил авторизации, запустите командлет [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936).

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Rule &lt;PswaAuthorizationRule\[\]&gt;

Задает набор правил для проверки. Если этот параметр не указан, командлет проверяет соответствие всем правилам авторизации.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | True (ByValue)                       |
| Принимать подстановочные знаки?          | false                                |

### <a name="-username-ltstringgt"></a>-UserName &lt;строка&gt;

Задает имя проверяемого пользователя.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | верно                                 |
| Указать положение?                            | 1                                    |
| Значение по умолчанию                        | отсутствуют                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.
Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>ВХОДНЫЕ ДАННЫЕ

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Этот командлет принимает в качестве входных данных массив объектов PswaAuthorizationRule.

## <a name="outputs"></a>ВЫХОДНЫЕ ДАННЫЕ

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Этот командлет создает массив объектов PswaAuthorizationRule в качестве выходных данных.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

В этом примере проверяются все правила авторизации, чтобы отобразить все правила, позволяющие пользователю *contoso\\mhanson* подключаться к компьютеру *srv2* и использовать конфигурацию сеанса Windows PowerShell с именем *test*.

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a>ПРИМЕР 2

В этом примере проверяются все правила авторизации, чтобы узнать, какие правила авторизации применяются к пользователю *contoso\\mhanson*.

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a>Связанные темы

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Install-PswaWebApplication](install-pswawebapplication.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)