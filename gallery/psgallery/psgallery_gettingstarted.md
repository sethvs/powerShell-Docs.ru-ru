---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psgallery_начало_работы"
ms.technology: powershell
ms.openlocfilehash: 4c06d1ebd4417da4bd58e3536d123f8285ba189e
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="get-started-with-the-powershell-gallery"></a>Приступая к работе с коллекцией PowerShell

## <a name="what-is-the-powershell-gallery"></a>Что такое коллекция PowerShell?

Коллекция PowerShell — это центральный репозиторий для хранения содержимого PowerShell.
В ней можно найти полезные модули PowerShell с командами и ресурсы настройки требуемого состояния (DSC). Здесь также представлены скрипты PowerShell, некоторые из которых могут содержать рабочие процессы PowerShell. Они описывают набор задач и реализуют конвейер для их выполнения.
Некоторые из этих элементов созданы корпорацией Майкрософт, а другие — сообществом PowerShell.

## <a name="requirements"></a>Требования

Для скачивания элементов из коллекции PowerShell требуется модуль [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409). Модуль PowerShellGet можно найти в перечисленных ниже источниках. Входить в систему для скачивания элементов из коллекции PowerShell необязательно.

-   [Windows 10](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409)
-   [Windows Management Framework 5.0](http://go.microsoft.com/fwlink/?LinkId=398175)
-   [Установщик MSI (для PowerShell 3 и 4)](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

Чтобы PowerShellGet работал с коллекцией PowerShell, требуется [поставщик NuGet](http://go.microsoft.com/fwlink/?LinkId=722208). При первом запуске PowerShellGet вам будет предложено установить поставщик NuGet автоматически, если поставщик NuGet не находится в одном из следующих расположений:

-   $env:ProgramFiles\\PackageManagement\\ProviderAssemblies;
-   $env:LOCALAPPDATA\\PackageManagement\\ProviderAssemblies.

Или же вы можете выполнить команду **Install-PackageProvider -Name NuGet -Force**, чтобы автоматизировать скачивание и установку поставщика NuGet.

  
Если ваша версия NuGet младше 2.8.5.201, вам необходимо выполнить следующие командлеты PowerShell для установки последней версии NuGet и переключения на нее.

1.  Install-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force
2.  Import-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force
3.  Удалите старую версию NuGet из папки, указанной выше.

Дополнительные сведения см. на веб-сайте <http://oneget.org/>.

  
Примечание. Из-за изменений в форматах упаковки мы рекомендуем установить последнюю версию PowerShellGet и PackageManagement для установки недавно обновленных компонентов. PowerShellGet включен в Windows 10. Подробности см. [здесь](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409).
PowerShellGet также включен в платформу Windows Management Framework (WMF) 5.0, которую можно скачать [здесь](http://go.microsoft.com/fwlink/?LinkId=398175).

## <a name="discovering-items-from-the-powershell-gallery"></a>Обнаружение элементов в коллекции PowerShell

Найти элементы в коллекции PowerShell можно при помощи элемента управления **Поиск** на сайте или просмотрев страницы "Модули" и "Скрипты". Найти элементы в коллекции PowerShell можно также при помощи командлетов [**Find-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Find-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) (в зависимости от типа искомого) с параметром **-Repository PSGallery**.

Для фильтрации результатов поиска в коллекции используются параметры [Find-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [Find-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).

- Name
- AllVersions
- MinimumVersion
- RequiredVersion
- Tag
- Includes
- DscResource
- RoleCapability
- Команда
- Фильтр

Если вас интересуют только определенные ресурсы DSC в коллекции, выполните командлет [**Find-DscResource**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
[**Find-DscResource**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) возвращает данные о ресурсах DSC, содержащихся в коллекции. Поскольку ресурсы DSC всегда являются частью модуля, вам по-прежнему потребуется выполнить командлет [Install-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409), чтобы установить их.

## <a name="learning-about-items-in-the-powershell-gallery"></a>Изучение элементов в коллекции PowerShell

Когда вы нашли элемент, который вас интересует, о нем можно узнать больше. Для этого можно изучить страницу конкретного элемента в коллекции. На ней представлены все метаданные, переданные вместе с элементом. Эти метаданные предоставляются автором элемента и не проверяются корпорацией Майкрософт. Владелец элемента тесно связан с учетной записью в коллекции, используемой для публикации элемента, поэтому ориентироваться на нее — более надежно, чем на информацию в поле "Автор".

Если вы нашли элемент, который по вашему мнению опубликован с нарушениями, щелкните** Сообщить о нарушении** на странице этого элемента.

При использовании командлетов [Find-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) или [Find-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) эти данные можно доступны в возвращенном объекте PSGetModuleInfo. Например, команда [**Find-Module -Name PSReadLine -Repository PSGallery | Get-Member**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) возвращает данные о модуле PSReadLine в коллекции.

## <a name="downloading-items-from-the-powershell-gallery"></a>Скачивание элементов из коллекции PowerShell

При скачивании элементов из коллекции PowerShell рекомендуется использовать следующий процесс.

### <a name="inspect"></a>Изучение

Чтобы скачать элемент из коллекции для изучения, выполните командлет [**Save-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) или [**Save-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) в зависимости от типа элемента. Так вы сможете сохранить элемент локально без установки и проверить его содержимое. Не забудьте удалить элемент, сохраненный вручную.

Некоторые из этих элементов созданы корпорацией Майкрософт, а другие — сообществом PowerShell. Корпорация Майкрософт рекомендует ознакомиться с содержимым и кодом элементов в этой коллекции перед их установкой.

Если вы нашли элемент, который по вашему мнению опубликован с нарушениями, щелкните** Сообщить о нарушении** на странице этого элемента.

### <a name="install"></a>Установка

Чтобы установить элемент из коллекции для использования, выполните командлет [**Install-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) или [**Install-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) в зависимости от типа элемента.

По умолчанию [Install-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) устанавливает модуль в папку $env:ProgramFiles\\WindowsPowerShell\\Modules. Для выполнения этой операции необходима учетная запись администратора. Если добавить параметр **-Scope CurrentUser**, модуль будет установлен в папку $env:USERPROFILE\\Documents\\WindowsPowerShell\\Modules.

По умолчанию [Install-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) устанавливает скрипты в папку $env:ProgramFiles\\WindowsPowerShell\\Scripts. Для выполнения этой операции необходима учетная запись администратора. Если добавить параметр **-Scope CurrentUser**, скрипт будет установлен в папку $env:USERPROFILE\\Documents\\WindowsPowerShell\\Scripts.

По умолчанию командлеты [Install-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) and [Install-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) устанавливают последнюю версию элемента. Чтобы установить более раннюю версию элемента, добавьте параметр **-RequiredVersion**.

### <a name="deploy"></a>Развертывание

Чтобы развернуть элемент из коллекции PowerShell в службе автоматизации Azure, нажмите кнопку **Развернуть в службе автоматизации Azure** на странице подробностей об элементе. После этого вы будете перенаправлены на портал управления Azure, на который нужно войти с использованием учетных данных учетной записи Azure. Обратите внимание, что развертывание элементов с зависимостями приводит к развертыванию всех зависимостей в службе автоматизации Azure. Кнопку "Развернуть в службе автоматизации Azure" можно отключить, добавив тег **AzureAutomationNotSupported** в метаданные элемента.

Подробности о службе автоматизации Azure см. на [сайте службы автоматизации Azure](http://azure.microsoft.com/en-us/services/automation/).

## <a name="updating-items-from-the-powershell-gallery"></a>Обновление элементов из коллекции PowerShell

Чтобы обновить элементы, установленные из коллекции PowerShell, выполните командлет [Update-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) или [Update-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409). При запуске без дополнительных параметров [Update-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) пытается обновить каждый модуль, установленный командлетом [Install-Module](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
Чтобы выборочно обновить модули, добавьте параметр **-Name**.

Аналогично при запуске без дополнительных параметров [Update-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) пытается обновить каждый скрипт, установленный командлетом [Install-Script](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
Чтобы выборочно обновить скрипты, добавьте параметр **-Name**.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>Перечисление элементов, установленных из коллекции PowerShell

Чтобы узнать, какие модули вы установили из коллекции PowerShell, выполните командлет [**Get-InstalledModule**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409). Эта команда перечисляет все модули в системе, установленные непосредственно из коллекции PowerShell.

Аналогично, чтобы узнать, какие скрипты были установлены из коллекции PowerShell, выполните командлет [**Get-InstalledScript**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409). Эта команда перечисляет все скрипты в системе, установленные непосредственно из коллекции PowerShell.

