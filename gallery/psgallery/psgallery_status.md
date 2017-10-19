---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "psgallery_состояние"
ms.openlocfilehash: af6111d3c511273571bd978c6d0e7447726c2917
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
<a name="powershell-gallery-status"></a>Состояние коллекции PowerShell
=========================
## <a name="10102017---powershell-gallery-unavailable-for-2-hours-101017"></a>10.10.2017 коллекция PowerShell была недоступна в течение двух часов.

__Сводка об инциденте.__ 10.10.2017 около 17:00 (по тихоокеанскому времени) в работе коллекции PowerShell возникла высокая задержка, которая привела к временным проблемам с подключением. Для устранения этой проблемы веб-сайт на два часа был переведен в автономный режим (начиная примерно с 22:00 по тихоокеанскому времени). Работа веб-сайта была возобновлена незадолго до полуночи 10.10.2017. 
 
__Основная причина.__ Причина высокой задержки все еще выясняется.

__Решение.__ Для решения проблемы веб-службы были переведены в автономный режим. Затем их работа была возобновлена. 

__Дальнейшие действия.__ Причина неполадки все еще выясняется.

## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a>01.06.2017. Развертывание в службу автоматизации Azure сейчас недоступно

__Сводка по влиянию.__ Сейчас развертывание элементов с зависимостями из коллекции PowerShell в службу автоматизации Azure недоступно.  Импорт элементов из коллекции PowerShell изнутри службы автоматизации Azure все еще доступен.  
 
__Основная причина.__ Элементы с зависимостями от других элементов, ранее развернутые в службу автоматизации Azure, не будут развертываться в эту службу. Инженеры обнаружили проблему с тем, как создаются шаблоны ARM для элементов с зависимостями для функции развертывания в службу автоматизации Azure.

__Решение.__ Инженеры работают над устранением проблемы.  Текущее решение для пользователей — импортировать элемент из коллекции PowerShell изнутри службы автоматизации Azure. 

__Дальнейшие действия.__ Инженеры вскоре выпустят исправление.  Тем временем используйте рекомендуемое решение. 


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a>11.04.2017 г. — пользователи не могут выполнить вход с помощью учетных записей Azure Active Directory (AAD)

__Сводка по влиянию__. Некоторым пользователям не удалось выполнить вход в коллекцию PowerShell с помощью учетных записей Azure AD. 
 
__Причина__. Во время обновления было пропущено изменение параметра для безопасного взаимодействия с AAD. В процессе тестирования с целью обнаружения изменений определенные типы учетных записей AAD не использовались, что не повлияло на развертывание.

__Решение__. Инженерам удалось определить упущенный параметр, и проблема была устранена. 

__Дальнейшие действия__. Планируется последующая доработка тестирования для расширения набора типов учетных записей AAD.

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

__Сводка по влиянию__. С 05.08.2016 по 10.08.2016 клиентам не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com или использовать функцию "Обратная связь".  
__Первопричина__. Инженеры выявили, что причина состояла в изменении конфигурации учетной записи электронной почты.  
__Решение__. Инженеры устранили проблему в конфигурации.  
__Дальнейшие действия__. Если вы использовали ссылку "Обратная связь" или отправляли почту по адресу cgadmin@microsoft.com в это время и не получили ответа, повторите попытку. Благодарим за терпение.



## <a name="7132016---download-items-failed"></a>13.07.2016 — сбой скачивания элементов

__Сводка по влиянию__. С 11.07.2016 по 13.07.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell. Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.

```powershell
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
__Сводка по влиянию__. С 17.05.2016 по 19.05.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell. Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.

```powershell
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

