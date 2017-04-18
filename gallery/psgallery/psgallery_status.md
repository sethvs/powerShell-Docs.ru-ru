---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psgallery_состояние"
ms.technology: powershell
ms.openlocfilehash: 1886715c4b948e4bc59a51fb96d54b56b5b5afed
ms.sourcegitcommit: 809e4f1bdf218b283e84438151030bfa94ca956d
translationtype: HT
---
<a name="powershell-gallery-status"></a>Состояние коллекции PowerShell
=========================

## <a name="04112017---users-unable-to-log-in"></a>11.04.2017 — пользователям не удается войти

__Сводка влияния__: некоторым пользователям не удается войти в коллекцию PowerShell с помощью учетных записей Azure AD. Группа эксплуатации коллекции PowerShell изучает эту проблему. Проблема не влияет на пользователей с учетными записями Майкрософт (те, с доменами наподобие Outlook.com, Live.com и т. д.). 
 
__Основная причина__: подлежит уточнению  

__Дальнейшие действия__: мы работаем с командой Azure AD, чтобы определить причину проблемы. 

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a>27.03.2017 — устранено. Не видны отдельные страницы модулей и скриптов

__Сводка по влиянию__. Прямые ссылки на отдельные страницы модулей и скриптов на сайте https://www.powershellgallery.com были недоступны. Это было актуально для всех регионов. Это не повлияло на командлеты PowerShellGet: Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Scirpt по-прежнему работали.

__Причина__. Инженеры определили причину как проблему при включении кнопок социальных сетей (например, Facebook) на страницу.  

__Решение__. Инженеры исправили проблему, отключив сведения о числе подключений через Facebook.

__Дальнейшие действия__. Мы открыли обращение о внутреннем отслеживании, чтобы исправить использование API Facebook.

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a>15.12.2016 — не удается отправить сообщения электронной почты через веб-сайт PowerShellGallery

__Сводка по влиянию__. Между 13.12.2016 и 15.12.2016 все сообщения, отправленные через функции "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", не были получены администраторами коллекции PowerShell.  
__Первопричина__. Инженеры выявили, что причина состояла в проблеме проверки подлинности на SMTP-сервере.  
__Решение__. Инженеры смогли устранить проблему проверки подлинности и восстановить подключение к SMTP-серверу.  
__Дальнейшие действия__. Если вы использовали ссылки "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", чтобы отправить почту по адресу cgadmin@microsoft.com в это время, и не получили ответа, повторите попытку. Приносим извинения за причиненные неудобства.  



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a>10.08.2016 — устранена ошибка: не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com.

__Сводка влияния__. С 05.08.2016 по 10.08.2016 клиентам не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com или использовать функцию "Обратная связь".  
__Первопричина__. Инженеры выявили, что причина состояла в изменении конфигурации учетной записи электронной почты.  
__Решение__. Инженеры устранили проблему в конфигурации.  
__Дальнейшие действия__. Если вы использовали ссылку "Обратная связь" или отправляли почту по адресу cgadmin@microsoft.com в это время и не получили ответа, повторите попытку. Благодарим за терпение.



## <a name="7132016---download-items-failed"></a>13.07.2016 — сбой скачивания элементов

__Сводка влияния__. С 11.07.2016 по 13.07.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell. Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.

```PowerShell
PS C:\> Install-Module xStorage 
PackageManagement\Install-Package : Package 'xStorage' failed to be installed because: 
End of Central Directory record could not be found. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1375 char:21 + ... 
$null = PackageManagement\Install-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + CategoryInfo : InvalidResult: 
(xStorage:String) [Install-Package], Exception + FullyQualifiedErrorId : Package '{0}' 
failed to be installed because: {1},Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage 
```

__Предварительная первопричина__. Инженеры выявили проблему в сети доставки содержимого Azure (CDN), развернутой для коллекции PowerShell 11.07.2016.  
__Устранение рисков__. Инженеры отключили Azure CDN в коллекции PowerShell.  
__Дальнейшие действия__. Мы находимся в процессе поиска первопричины и разрабатываем решение, чтобы предотвратить появление проблемы в будущем.


## <a name="5192016---download-items-failed"></a>19.05.2016 — сбой скачивания элементов
__Сводка влияния__. С 17.05.2016 по 19.05.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell. Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.

```PowerShell
VERBOSE: Hash for package 'AzureRM.OperationalInsights' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='AzureRM.OperationalInsights', version='1.0.8',
destination='C:\Users\jbritt\AppData\Local\Temp\2\1741355729'
WARNING: Package 'AzureRM.OperationalInsights' failed to be installed because: 
End of Central Directory record could not be found. 
WARNING: Dependent Package 'AzureRM.OperationalInsights' failed to install. 
WARNING: Package 'AzureRM' failed to install. 
VERBOSE: Module 'AzureRM.Network' was saved successfully. 
VERBOSE: Saving the dependency module 'AzureRM.NotificationHubs' with version '1.0.8' for the 
module 'AzureRM'. 
VERBOSE: Module 'AzureRM.NotificationHubs' was saved successfully. 
PackageManagement\Save-Package : Unable to save the module 'AzureRM'. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1187 char:21 + 
$null = PackageManagement\Save-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + 
CategoryInfo : InvalidOperation: (Microsoft.Power...ets.SavePackage:SavePackage) 
[Save-Package], Exception + FullyQualifiedErrorId : ProviderFailToDownloadFile,
Microsoft.PowerShell.PackageManagement.Cmdlets.SavePackage 
```

__Предварительная первопричина__. Инженеры обнаружили сбой в базовом поставщике сети доставки содержимого Azure (CDN), развернутой для коллекции PowerShell 17.05.2016.  
__Устранение рисков__. Инженеры отключили Azure CDN в коллекции PowerShell.  
__Дальнейшие действия__. Мы находимся в процессе поиска первопричины и разрабатываем решение, чтобы предотвратить появление проблемы в будущем.

