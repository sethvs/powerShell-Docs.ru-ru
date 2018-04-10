---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: установка pswawebapplication
ms.technology: powershell
ms.openlocfilehash: c7f7768a41b6784d8c29afa1fccf0b855160b777
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Настраивает веб-приложение Windows PowerShell® Web Access в IIS.

## <a name="syntax"></a>СИНТАКСИС

### <a name="default"></a>Значение по умолчанию
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Командлет **Install-PswaWebApplication** настраивает веб-приложение Windows PowerShell Web Access. Этот командлет устанавливает веб-приложение, связывает его с веб-сайтом и при необходимости создает тестовый сертификат SSL с помощью параметра **useTestCertificate**. Для обеспечения безопасности веб-администраторам не следует использовать тестовый сертификат для рабочей среды.

## <a name="parameters"></a>ПАРАМЕТРЫ

### <a name="-usetestcertificate"></a>-UseTestCertificate

Указывает, что создается тестовый сертификат. Если этот параметр имеет значение true, то командлет создает тестовый сертификат и настраивает веб-приложение Windows PowerShell Web Access для использования сертификата для HTTPS-запросов. Если этот параметр имеет значение false, то ни сертификат, ни привязка не создаются. Задайте значение false, если для Windows PowerShell Web Access используется другой сертификат.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | верно                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-webapplicationnameltstringgt"></a>-WebApplicationName&lt;строка&gt;

Указывает имя веб-приложения. Отображается как последняя часть URL-адреса Windows PowerShell Web Access.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | 1                                    |
| Значение по умолчанию                        | pswa                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-websitenameltstringgt"></a>-WebSiteName&lt;строка&gt;

Задает имя веб-сайта веб-сервера (IIS) для установки этого веб-приложения Windows PowerShell Web Access.

|||
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | Веб-сайт по умолчанию                     |
| Принимать входные данные конвейера?               | false                                |
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

Показывает, что произойдет при запуске командлета.
Командлет не запущен.

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

Этот командлет не принимает входные данные.

## <a name="outputs"></a>ВЫХОДНЫЕ ДАННЫЕ

Этот командлет не создает выходные данные.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

В этом примере выполняется установка веб-приложения PSWA с использованием значений по умолчанию для параметров **WebApplicationName** (*pswa*) и **WebSiteName** (*веб-сайт по умолчанию*).

```
Install-PswaWebApplication
```

### <a name="example-2"></a>ПРИМЕР 2

В этом примере выполняется установка веб-приложения PSWA с тестовым сертификатом и со значениями по умолчанию для параметров **WebApplicationName** и **WebSiteName**.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Связанные темы

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)