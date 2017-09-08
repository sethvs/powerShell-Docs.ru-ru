---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "удаление pswawebapplication"
ms.technology: powershell
ms.openlocfilehash: 64d546427e44d7bd284da8f682a7218afbadd0ad
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="uninstall-pswawebapplication"></a>Uninstall-PswaWebApplication

##  <a name="synopsis"></a>КРАТКИЙ ОБЗОР

Удаляет веб-приложение Windows PowerShell® Web Access.

## <a name="syntax"></a>СИНТАКСИС

###  <a name="default"></a>Значение по умолчанию
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>ОПИСАНИЕ

Командлет **Uninstall-PswaWebApplication** удаляет веб-приложение Windows PowerShell и веб-сайт с сервера IIS. Командлет не удаляет службы IIS или другие установленные компоненты, так как они требуются для работы Windows PowerShell.

## <a name="parameters"></a>ПАРАМЕТРЫ

### <a name="-deletetestcertificate"></a>-DeleteTestCertificate

Указывает, что тестовые сертификаты, созданные командлетом **Install\_PswaWebApplication** (с параметром **UseTestCertificate**), удаляются.
Удаляется только тестовый сертификат с тем же именем, что и созданный командлетом **Install-PswaWebApplication**.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | с именем                                |
| Значение по умолчанию                        | верно                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-webapplicationname-ltstringgt"></a>-WebApplicationName &lt;строка&gt;

Указывает имя удаляемого веб-приложения.

|||  
|-|-|
| Псевдонимы                              | отсутствуют                                 |
| Требуется?                            | false                                |
| Указать положение?                            | 1                                    |
| Значение по умолчанию                        | pswa                                 |
| Принимать входные данные конвейера?               | false                                |
| Принимать подстановочные знаки?          | false                                |

### <a name="-websitename-ltstringgt"></a>-WebSiteName &lt;строка&gt;

Задает имя веб-сайта, на котором установлено веб-приложение.

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

Этот командлет не возвращает выходные данные.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1"></a>ПРИМЕР 1

Эта команда удаляет веб-приложение Windows PowerShell.
С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию.

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a>ПРИМЕР 2

Эта команда удаляет веб-приложение Windows PowerShell, а также тестовый сертификат, связанный с приложением.
С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию, включая создание сертификата.

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a>ПРИМЕР 3 {#example-3 .subHeading}

Эта команда удаляет веб-приложение Windows PowerShell, если во время установки были указаны настраиваемый веб-сайт и приложение.
Эта команда удаляет веб-сайт с именем *MySite* и приложение с именем *TestApplication* и указывает, что тестовые сертификаты, связанные с приложением, также удаляются.

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

##  <a name="related-topics"></a>Связанные темы

-  [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
-  [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
-  [Install-PswaWebApplication](install-pswawebapplication.md)
-  [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
-  [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
