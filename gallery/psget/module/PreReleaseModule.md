---
ms.date: 2017-09-26
contributor: keithb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: PrereleaseModule
ms.openlocfilehash: d2c629d0e0ec0d4a4adafe5994a37d3985d13a06
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="prerelease-module-versions"></a>Предварительные версии модулей
Начиная с версии 1.6.0, PowerShellGet и коллекция PowerShell поддерживают маркировку версий с номерами выше 1.0.0 как предварительных. До этого номера предварительных версий должны были обязательно начинаться с 0. Такая возможность добавлена, чтобы улучшить поддержку соглашения о версиях [SemVer 1.0.0](http://semver.org/spec/v1.0.0.html) и при этом сохранить обратную совместимость с PowerShell версий 3 и выше, а также с текущими версиями PowerShellGet. Этот раздел описывает особенности присвоения версий модулям. Аналогичные возможности для сценариев см. в разделе [Предварительные версии сценариев](../script/PrereleaseScript.md). Благодаря этой возможности издатель может присвоить своему модулю или сценарию предварительную версию 2.5.0-alpha, а затем выпустить готовую к использованию версию 2.5.0, которая заменит предварительную. 

На высоком уровне возможности для предварительных версий модулей включают следующее.

* Добавление строки предварительной версии в раздел PSData манифеста модуля определяет версию модуля как предварительную. При публикации модуля в коллекции PowerShell эти данные извлекаются из манифеста и используются для определения элементов с предварительными версиями.
* Для получения предварительных версий необходимо добавить флаг -AllowPrerelease к следующим командам PowerShellGet: Find-Module, Install-Module, Update-Module и Save-Module. Если этот флаг не поставлен, предварительные версии не отображаются.  
* Версии модулей, отображаемые Find-Module и Get-InstalledModule, а также в коллекции PowerShell, будут отображаться как одна строка с добавлением строки предварительной версии, например: 2.5.0-alpha. 

Ниже приведено подробное описание этих возможностей. 

Данные изменения совместимы с PowerShell 3.0, 4.0 и 5 и не влияют на поддержку версий модулей, встроенную в PowerShell. 

## <a name="identifying-a-module-version-as-a-prerelease"></a>Определение версии модуля как предварительной 

Для использования предварительных версий в PowerShellGet необходимо заполнить два поля в манифесте модуля.

* Версия в поле ModuleVersion манифеста модуля должна состоять из трех частей и соответствовать текущей системе версий PowerShell. Формат версии должен быть вида A.B.C, где A, B и C — целые числа. 
* Строка предварительной версии задается в подразделе PSData раздела PrivateData в манифесте модуля. Ниже приведены подробные требования к строке предварительной версии. 

Пример раздела манифеста модуля, определяющего версию модуля как предварительную
```powershell
@{
    ModuleVersion = '2.5.0'
    #---
    PrivateData = @{
        PSData = @{
            Prerelease = 'alpha'
        }
    }
}
```

Подробные требования к строке предварительной версии. 

* Строку предварительной версии можно указать, только если версия в поле ModuleVersion состоит из трех сегментов в виде <основная_версия>.<дополнительная_версия>.<сборка>. Это соответствует соглашению о версиях SemVer 1.0.0.
* Разделителем между номером сборки и строкой предварительной версии является дефис. Дефис может включен в строку предварительной версии только как первый символ.
* Строка предварительной версии может содержать только буквенно-цифровые символы ASCII [0-9A-Za-z-]. Рекомендуем начинать эту строку с буквы, так как в таком случае проще отличать предварительные версии при просмотре списка элементов. 
* В настоящий момент поддерживается только SemVer версии 1.0.0. Строка предварительной версии __не должна__ содержать ни точек, ни символов + [.+], которые допустимы в SemVer 2.0. 
* Пример поддерживаемых строк предварительной версии: -alpha, -alpha1, -BETA, -update20171020

__Влияние предварительных версий на порядок сортировки и установочные папки__

При использовании предварительных версий изменяется порядок сортировки, что имеет значение при публикации сценариев в коллекции PowerShell и при установке модулей с помощью команд PowerShellGet. Если строка предварительной версии задана для двух модулей, то сортировка производится по части строки, следующей после дефиса. Таким образом версия 2.5.0-alpha меньше, чем 2.5.0-beta, а последняя меньше, чем 2.5.0-gamma. Если два модуля обладают одинаковым значением ModuleVersion и только у одного из них есть строка предварительной версии, то готовым к использованию модулем будет считаться модуль без этой строки и при сортировке он будет указываться, как имеющий более высокую версию по отношению к предварительной (включающей строку предварительной версии). Например: при сравнении версий 2.5.0 и 2.5.0-beta, будет считаться, что версия 2.5.0 имеет больший номер. 

По умолчанию при публикации в коллекции PowerShell новый модуль обязательно должен иметь более высокую версию, чем все модули, опубликованные ранее. 

## <a name="finding-and-acquiring-prerelease-items-using-powershellget-commands"></a>Поиск и получение предварительных версий при помощи команд PowerShellGet

Для работы с предварительными версиями при помощи PowerShellGet-команд Find-Module, Install-Module, Update-Module и Save-Module необходимо добавлять флаг -AllowPrerelease. Если задан флаг -AllowPrerelease, то в результат выполнения команды будут включены предварительные версии элементов при их наличии.
Если флаг -AllowPrerelease не задан, то предварительные версии не отображаются. 

Единственным исключением является команда Get-InstalledModule и в некоторых случаях команда Uninstall-Module. 

* Команда Get-InstalledModule всегда автоматически показывает информацию о предварительных версиях в строке версии для модулей. 
* Если __номер версии не указан__, то по умолчанию команда Uninstall-Module удалит самую последнюю версию модуля. Такое поведение команды осталось неизменным. Если в параметре -RequiredVersion указана предварительная версия, то необходимо будет также указать флаг -AllowPrerelease. 

## <a name="examples"></a>Примеры
```powershell
# Assume the PowerShell Gallery has TestPackage module versions 1.8.0 and 1.9.0-alpha. If -AllowPrerelease is not specified, only version 1.8.0 will be returned.
C:\windows\system32> find-module TestPackage 

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.8.0          TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-alpha    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

# To install a prerelease, always specify -AllowPrerelease. Specifying a prerelease version string is not sufficient. 

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha
PackageManagement\Find-Package : No match was found for the specified search criteria and module name 'TestPackage'.
Try Get-PSRepository to see all available registered module repositories.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.6.0\PSModule.psm1:1455 char:3
+         PackageManagement\Find-Package @PSBoundParameters | Microsoft ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Microsoft.Power...ets.FindPackage:FindPackage) [Find-Package], Exceptio
   n
    + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.FindPackage

# The previous command failed because -AllowPrerelease was not specified.
# Adding -AllowPrerelease will result in success.

C:\windows\system32> Install-module TestPackage -RequiredVersion 1.9.0-alpha -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

Не поддерживается одновременная установка модулей, версии которых отличаются только значением предварительной версии. При использовании PowerShellGet разные версии одного модуля могут быть установлены одновременно. Каждая из них помещается в папку с именем, использующим значение ModuleVersion. ModuleVersion используется для имени папки без добавления строки предварительной версии. Если пользователь установит модуль MyModule версии 2.5.0-alpha, этот модуль будет помещен в папку MyModule\2.5.0. Если пользователь затем установит версию 2.5.0-beta, то она __перезапишет__ содержимое папки MyModule\2.5.0. Одним из преимуществ такого подхода является то, что нет необходимости удалять предварительную версию после установки версии, готовой к использованию. Пример ниже иллюстрирует работу этого правила.


``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-alpha     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> find-module TestPackage -AllowPrerelease

Version        Name                                Repository           Description
-------        ----                                ----------           -----------
1.9.0-beta     TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Update-Module TestPackage -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

```

Если не задан флаг -RequiredVersion, то команда Uninstall-Module удалит самую последнюю версию модуля. Если в параметре -RequiredVersion указана предварительная версия, то необходимо обязательно добавить к команде флаг -AllowPrerelease. 

``` powershell
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.9.0-beta      TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta
Uninstall-Module : The '-AllowPrerelease' parameter must be specified when using the Prerelease string in
MinimumVersion, MaximumVersion, or RequiredVersion.
At line:1 char:1
+ Unnstall-Module TestPackage -RequiredVersion 1.9.0-beta
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Uninstall-Module], ArgumentException
    + FullyQualifiedErrorId : AllowPrereleaseRequiredToUsePrereleaseStringInVersion,Uninnstall-Module



C:\windows\system32> Uninstall-Module TestPackage -RequiredVersion 1.9.0-beta -AllowPrerelease
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
2.0.0-alpha1    TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...

C:\windows\system32> Uninstall-Module TestPackage
C:\windows\system32> Get-InstalledModule TestPackage -AllVersions

Version         Name                                Repository           Description
-------         ----                                ----------           -----------
1.8.0           TestPackage                         PSGallery            Package used to validate changes to the PowerShe...
1.1.3.2         TestPackage                         PSGallery            Package used to validate changes to the PowerShe...


```



## <a name="more-details"></a>Дополнительные подробности
### <a name="prerelease-script-versionsscriptprereleasescriptmd"></a>[Предварительные версии сценариев](../script/PrereleaseScript.md)
### <a name="find-modulepsgetfind-modulemd"></a>[Find-Module](./psget_find-module.md)
### <a name="install-modulepsgetinstall-modulemd"></a>[Install-Module](./psget_install-module.md)
### <a name="save-modulepsgetsave-modulemd"></a>[Save-Module](./psget_save-module.md)
### <a name="update-modulepsgetupdate-modulemd"></a>[Update-Module](./psget_update-module.md)
### <a name="get-installedmodulepsgetget-installedmodulemd"></a>[Get-InstalledModule](./psget_get-installedmodule.md)
### <a name="uninstall-modulepsgetuninstall-modulemd"></a>[Uninstall-Module](./psget_uninstall-module.md)
