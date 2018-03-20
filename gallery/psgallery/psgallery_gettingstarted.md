---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "psgallery_начало_работы"
ms.openlocfilehash: 2117712b0081db4a21f8480b458a499ed84dc512
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
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

- `$env:ProgramFiles\PackageManagement\ProviderAssemblies`
- `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies`

Кроме того, можно выполнить `Install-PackageProvider -Name NuGet -Force` для автоматизации скачивания и установки поставщика NuGet.

  
Если ваша версия NuGet младше 2.8.5.201, вам необходимо выполнить следующие командлеты PowerShell для установки последней версии NuGet и переключения на нее.

1.  `Install-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
2.  `Import-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
3.  Удалите старую версию NuGet из папки, указанной выше.

Дополнительные сведения см. в разделе <http://oneget.org/>.

  
Примечание. Из-за изменений в форматах упаковки мы рекомендуем установить последнюю версию PowerShellGet и PackageManagement для установки недавно обновленных компонентов. PowerShellGet включен в Windows 10. Подробности см. [здесь](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409).
PowerShellGet также включен в платформу Windows Management Framework (WMF) 5.0, которую можно скачать [здесь](http://go.microsoft.com/fwlink/?LinkId=398175).

## <a name="discovering-items-from-the-powershell-gallery"></a>Обнаружение элементов в коллекции PowerShell

Найти элементы в коллекции PowerShell можно при помощи элемента управления **Поиск** на сайте или просмотрев страницы "Модули" и "Скрипты". Найти элементы в коллекции PowerShell можно также при помощи командлетов [Find-Module](https://go.microsoft.com/fwlink/?LinkId=821658) и [Find-Script](https://go.microsoft.com/fwlink/?LinkId=822322) (в зависимости от типа элемента) с параметром `-Repository PSGallery`.

Для фильтрации результатов поиска в коллекции используются параметры [Find-Module](https://go.microsoft.com/fwlink/?LinkId=821658) и [Find-Script](https://go.microsoft.com/fwlink/?LinkId=822322).

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

Если вас интересуют только определенные ресурсы DSC в коллекции, выполните командлет [Find-DscResource](https://go.microsoft.com/fwlink/?LinkId=517196).
При выполнении [Find-DscResource](https://go.microsoft.com/fwlink/?LinkId=517196) возвращаются сведения о ресурсах DSC, содержащихся в коллекции. Поскольку ресурсы DSC всегда являются частью модуля, вам по-прежнему потребуется выполнить командлет [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663), чтобы установить их.

## <a name="learning-about-items-in-the-powershell-gallery"></a>Изучение элементов в коллекции PowerShell

Когда вы нашли элемент, который вас интересует, о нем можно узнать больше. Для этого можно изучить страницу конкретного элемента в коллекции. На ней представлены все метаданные, переданные вместе с элементом. Эти метаданные предоставляются автором элемента и не проверяются корпорацией Майкрософт. Владелец элемента тесно связан с учетной записью в коллекции, используемой для публикации элемента, поэтому ориентироваться на нее — более надежно, чем на информацию в поле "Автор".

Если вы нашли элемент, который по вашему мнению опубликован с нарушениями, щелкните **Сообщить о нарушении** на странице этого элемента.

При использовании командлетов [Find-Module](https://go.microsoft.com/fwlink/?LinkId=821658) или [Find-Script](https://go.microsoft.com/fwlink/?LinkId=822322) эти данные можно доступны в возвращенном объекте PSGetModuleInfo.
Например, при выполнении `Find-Module -Name PSReadLine -Repository PSGallery | Get-Member` возвращаются сведения о модуле PSReadLine, содержащемся в коллекции.

## <a name="downloading-items-from-the-powershell-gallery"></a>Скачивание элементов из коллекции PowerShell

При скачивании элементов из коллекции PowerShell рекомендуется использовать следующий процесс.

### <a name="inspect"></a>Изучение

Чтобы скачать элемент из коллекции для изучения, выполните командлет [Save-Module](https://go.microsoft.com/fwlink/?LinkId=821669) или [Save-Script](https://go.microsoft.com/fwlink/?LinkId=822334) в зависимости от типа элемента. Так вы сможете сохранить элемент локально без установки и проверить его содержимое. Не забудьте удалить элемент, сохраненный вручную.

Некоторые из этих элементов созданы корпорацией Майкрософт, а другие — сообществом PowerShell. Корпорация Майкрософт рекомендует ознакомиться с содержимым и кодом элементов в этой коллекции перед их установкой.

Если вы нашли элемент, который по вашему мнению опубликован с нарушениями, щелкните **Сообщить о нарушении** на странице этого элемента.

### <a name="install"></a>Установка

Чтобы установить элемент из коллекции для использования, выполните командлет [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663) или [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327) в зависимости от типа элемента.

Командлет [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663) устанавливает модуль в `$env:ProgramFiles\WindowsPowerShell\Modules` по умолчанию. Для выполнения этой операции необходима учетная запись администратора. При добавлении параметра `-Scope
CurrentUser` модуль будет установлен в каталог `$env:USERPROFILE\Documents\WindowsPowerShell\Modules`.

Командлет [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327) по умолчанию устанавливает скрипт в каталог `$env:ProgramFiles\WindowsPowerShell\Scripts`. Для выполнения этой операции необходима учетная запись администратора. При добавлении параметра `-Scope
CurrentUser` скрипт будет установлен в каталог `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts`.

По умолчанию командлеты [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663) and [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327) устанавливают последнюю версию элемента. Чтобы установить более раннюю версию элемента, добавьте параметр `-RequiredVersion`.

### <a name="deploy"></a>Развертывание

Чтобы развернуть элемент из коллекции PowerShell в службе автоматизации Azure, нажмите кнопку **Развернуть в службе автоматизации Azure** на странице подробностей об элементе. После этого вы будете перенаправлены на портал управления Azure, на который нужно войти с использованием учетных данных учетной записи Azure. Обратите внимание, что развертывание элементов с зависимостями приводит к развертыванию всех зависимостей в службе автоматизации Azure. Кнопку "Развернуть в службе автоматизации Azure" можно отключить, добавив тег **AzureAutomationNotSupported** в метаданные элемента.

Подробности о службе автоматизации Azure см. на [сайте службы автоматизации Azure](http://azure.microsoft.com/services/automation/).

## <a name="updating-items-from-the-powershell-gallery"></a>Обновление элементов из коллекции PowerShell

Чтобы обновить элементы, установленные из коллекции PowerShell, выполните командлет [Update-Module](https://go.microsoft.com/fwlink/?LinkID=398576) или [Update-Script](http://go.microsoft.com/fwlink/?LinkId=619787). При запуске без дополнительных параметров [Update-Module](https://go.microsoft.com/fwlink/?LinkID=398576) пытается обновить каждый модуль, установленный командлетом [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663).
Чтобы выборочно обновить модули, добавьте параметр `-Name`.

Аналогично при запуске без дополнительных параметров [Update-Script](http://go.microsoft.com/fwlink/?LinkId=619787) пытается обновить каждый скрипт, установленный командлетом [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327).
Чтобы выборочно обновить скрипты, добавьте параметр `-Name`.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>Перечисление элементов, установленных из коллекции PowerShell

Чтобы узнать, какие модули вы установили из коллекции PowerShell, выполните командлет [Get-InstalledModule](https://go.microsoft.com/fwlink/?LinkId=526863). Эта команда перечисляет все модули в системе, установленные непосредственно из коллекции PowerShell.

Аналогично, чтобы узнать, какие скрипты были установлены из коллекции PowerShell, выполните командлет [Get-InstalledScript](https://go.microsoft.com/fwlink/?LinkId=619790). Эта команда перечисляет все скрипты в системе, установленные непосредственно из коллекции PowerShell.

