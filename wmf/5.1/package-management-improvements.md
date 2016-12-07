---
title: "Усовершенствования в управлении пакетами в WMF 5.1 (предварительная версия)"
ms.date: 2016-07-15
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: jaimeo
contributor: jianyunt, quoctruong
manager: dongill
ms.prod: powershell
ms.technology: WMF
ms.openlocfilehash: fd1fb6dd12b0a9ddcf69d159d83595955af62bc5
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="improvements-to-package-management-in-wmf-51-preview"></a>Усовершенствования в управлении пакетами в WMF 5.1 (предварительная версия) #

## <a name="improvements-in-packagemanagement"></a>Усовершенствования в управлении пакетами ##
Ниже перечислены исправления, внесенные в WMF 5.1. 

### <a name="version-alias"></a>Псевдоним версии

**Ситуация**. Если в системе установлены версии 1.0 и 2.0 пакета P1 и вы хотите удалить версию 1.0, вы выполняете команду `Uninstall-Package -Name P1 -Version 1.0`. При этом вы ожидаете, что после выполнения командлета будет удалена версия 1.0. Но в результате удаляется версия 2.0.  
    
Это происходит потому, что параметр `-Version` является псевдонимом параметра `-MinimumVersion`. Когда модуль PackageManagement ищет подходящий пакет с минимальной версией 1.0, он возвращает последнюю версию. Такое поведение является нормальным в большинстве случаев, так как обычно требуется найти именно последнюю версию. Но в случае с `Uninstall-Package` ситуация иная.
    
**Решение**. Полностью удалить псевдоним `-Version` в PackageManagement (так называемом OneGet) и PowerShellGet. 

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a>Несколько запросов на начальную загрузку поставщика NuGet

**Ситуация**. При первом выполнении командлета `Find-Module`, `Install-Module` или других командлетов PackageManagement на компьютере модуль PackageManagement пытается выполнить начальную загрузку поставщика NuGet. Связано это с тем, что поставщик PowershellGet также использует поставщик NuGet для скачивания модулей PowerShell. Затем модуль PackageManagement запрашивает у пользователя разрешение на установку поставщика NuGet. После того как пользователь разрешает начальную загрузку, устанавливается последняя версия поставщика NuGet. 
    
Но если на компьютере установлена старая версия поставщика NuGet, она иногда может загружаться первой в сеанс PowerShell (и в PackageManagement возникает состояние гонки). Но модуль PowerShellGet требует, чтобы работала последняя версия поставщика NuGet, поэтому он еще раз запрашивает начальную загрузку поставщика NuGet у модуля PackageManagement. Это приводит к выводу нескольких запросов на начальную загрузку поставщика NuGet.

**Решение**. В WMF 5.1 модуль PackageManagement теперь загружает последнюю версию поставщика NuGet во избежание вывода нескольких запросов на начальную загрузку поставщика NuGet.

Также имеется обходной путь: вы можете вручную удалить старую версию поставщика NuGet (NuGet-Anycpu.exe), если она существует, из папок $env:ProgramFiles\PackageManagement\ProviderAssemblies и $env:LOCALAPPDATA\PackageManagement\ProviderAssemblies


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a>Поддержка PackageManagement на компьютерах с доступом только к интрасети

**Ситуация**. В средах предприятий у пользователей может быть доступ только к интрасети, но не к Интернету. Модуль PackageManagement не поддерживал такую ситуацию в WMF 5.0.

**Ситуация**. В WMF 5.0 модуль PackageManagement не поддерживался на компьютерах с доступом только к интрасети (но не к Интернету).

**Решение**. Чтобы обеспечить использование PackageManagement на компьютерах в интрасети, в WMF 5.1 можно выполнить указанные ниже действия.

1. Скачайте поставщик NuGet с другого компьютера, имеющего подключение к Интернету, выполнив команду `Install-PackageProvider -Name NuGet`.

2. Поставщик NuGet находится в `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` или `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.

3. Скопируйте двоичные файлы в папку или сетевую папку, к которой есть доступ у компьютера в интрасети, и установите поставщик NuGet, выполнив команду `Install-PackageProvider -Name NuGet -Source <Path to folder>`.


### <a name="event-logging-improvements"></a>Усовершенствования, касающиеся ведения журнала событий

При установке пакетов состояние компьютера меняется. В WMF 5.1 модуль PackageManagement записывает события в журнал событий Windows для действий `Install-Package`, `Uninstall-Package` и `Save-Package`. Журнал событий совпадает с журналом событий для PowerShell, т. е. `Microsoft-Windows-PowerShell, Operational`.

### <a name="support-for-basic-authentication"></a>Поддержка обычной проверки подлинности

В WMF 5.1 модуль PackageManagement поддерживает поиск и установку пакетов из репозитория, требующего обычной проверки подлинности. Можно указать учетные данные в командлетах `Find-Package` и `Install-Package`. Например:

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
### <a name="support-for-using-packagemanagement-behind-a-proxy"></a>Поддержка использования PackageManagement через прокси-сервер

В WMF 5.1 модуль PackageManagement принимает новые параметры прокси-сервера, `-ProxyCredential` и `-Proxy`. В этих параметрах можно указать URL-адрес и учетные данные прокси-сервера для командлетов PackageManagement. По умолчанию используются системные настройки прокси-сервера. Например:

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```

