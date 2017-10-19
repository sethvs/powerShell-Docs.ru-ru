---
ms.date: 2017-06-09
schema: 2.0.0
keywords: powershell
title: RequireLicenseAcceptance
ms.openlocfilehash: 260ccc1ee52d09a640e88203c5644f20f9723d6f
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="modules-requiring-license-acceptance"></a>Модули, для использования которых требуется принять условия лицензии

## <a name="synopsis"></a>КРАТКИЙ ОБЗОР
В юридических требованиях некоторых издателей модулей указано, что перед установкой модуля из коллекции PowerShell пользователи должны явным образом принять условия лицензионного соглашения. Если пользователь устанавливает, обновляет или сохраняет такой модуль с помощью PowerShellGet (непосредственно или как зависимость для другого элемента), он должен указать, что принимает такие условия. Иначе операция завершится ошибкой.

## <a name="publish-requirements-for-modules"></a>Требования к публикации модулей

Модули, для использования которых нужно принять условия лицензионного соглашения, должны соответствовать следующим требованиям:
    
- В разделе PSData манифеста модуля для параметра RequireLicenseAcceptance должно быть установлено значение $True.
- В корневом каталоге модуля должен содержаться файл license.txt.
- Манифест модуля должен содержать URI лицензии.
- Модуль должен быть опубликован в формате PowerShellGet 2.0 или более поздней версии.

## <a name="impact-on-installsaveupdate-module"></a>Влияние на командлеты Install/Save/Update-Module

- Командлеты установки, сохранения и обновления будут поддерживать новый параметр -AcceptLicense. Его поведение аналогично действиям пользователя после прочтения лицензионного соглашения.
- Если для параметра RequiredLicenseAcceptance установлено значение True, а параметр -AcceptLicense не указан, для пользователя будет отображаться файл license.txt и запрос &quot;Вы принимаете условия лицензионного соглашения? (Yes/No/YesToAll/NoToAll)&quot;.
  - Если условия лицензионного соглашения принимаются:
    - **Save-Module:** модуль будет скопирован в систему пользователя.
    - **Install-Module:** модуль будет скопирован в надлежащую папку в системе пользователя (в зависимости от области действия).
    - **Update-Module:** модуль будет обновлен.
  - Если условия лицензионного соглашения отклоняются: 
    - Операция будет отменена.
- Все командлеты проверяют метаданные (requireLicenseAcceptance и версию формата), которые свидетельствуют о том, что требуется принять условия лицензионного соглашения.
  - Если версия формата клиента ниже 2.0, операция завершится ошибкой. Поступит запрос на обновление клиента.
  - Если модуль опубликован с версией формата ниже 2.0, флаг requireLicenseAcceptance будет игнорироваться.

    
 ## <a name="module-dependencies"></a>Зависимости модулей
- Если при установке, сохранении или обновлении зависимого модуля (или модуля, от которого зависят другие функции) требуется принять условия лицензионного соглашения, примите их (процедура описана выше).
- Если версия модуля уже указана в локальном каталоге как установленная в системе, пропустите процедуру проверки лицензии.
- Если при установке, сохранении или обновлении зависимого модуля требуется принять условия лицензионного соглашения, но они не принимаются, операция завершится ошибкой. Будут выполняться стандартные процессы, сопровождающие ошибку установки, сохранения или обновления элемента.

 ## <a name="impact-on--force"></a>Влияние на параметр -Force

Указание -Force НЕ является достаточным для принятия условий лицензионного соглашения. Для разрешения на установку требуется указать -AcceptLicense. Если указан параметр -Force, RequiredLicenseAcceptance имеет значение True, а параметр -AcceptLicense НЕ указан, операция завершится ошибкой.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>Пример 1. Обновление манифеста модуля для запроса на принятие условий лицензионного соглашения
```PowerShell
PS C:\> Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance

PrivateData = @{

    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable
    
 } # End of PrivateData hashtable
```
Эта команда позволяет обновить файл манифеста и установить для флага RequireLicenseAcceptance значение true.
### <a name="example-2-install-module-requiring-license-acceptance"></a>Пример 2. Установка модуля, для использования которого требуется принять условия лицензионного соглашения
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 

```
Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>Пример 3. Установка модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
Модуль устанавливается без запросов на принятие условий лицензионного соглашения.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>Пример 4. Установка модуля, для использования которого требуется принять условия лицензионного соглашения при помощи -Force
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -Force
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>Пример 5. Установка модуля с зависимостями, для использования которого требуется принять условия лицензионного соглашения
Модуль ModuleWithDependency зависит от модуля ModuleRequireLicenseAcceptance. Пользователю предлагается принять условия лицензионного соглашения.
```PowerShell
PS C:\> Install-Module -Name ModuleWithDependency

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Пример 6. Установка модуля с зависимостями, для использования которого требуется принять условия лицензионного соглашения и указать -AcceptLicense
Модуль ModuleWithDependency зависит от модуля ModuleRequireLicenseAcceptance. Пользователю не предлагается принять условия лицензии, так как указан параметр -AcceptLicense.
```PowerShell
PS C:\>  Install-Module -Name ModuleWithDependency -AcceptLicense
```
### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>Пример 7. Установка модуля, для использования которого требуется принять условия лицензионного соглашения, в клиенте с версией ниже, чем PSGetFormatVersion 2.0
```PowerShell
PS C:\windows\system32> Install-Module -Name ModuleRequireLicenseAcceptance

WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.

```
### <a name="example-8-save-module-requiring-license-acceptance"></a>Пример 8. Сохранение модуля, для использования которого требуется принять условия лицензионного соглашения
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```
Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>Пример 9. Сохранение модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```
Модуль сохраняется без запроса на принятие условий лицензионного соглашения.

### <a name="example-10-update-module-requiring-license-acceptance"></a>Пример 10. Обновление модуля, для использования которого требуется принять условия лицензионного соглашения
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```
Эта команда предназначена для отображения лицензии в файле license.txt и запроса на принятие условий лицензионного соглашения.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>Пример 11. Обновление модуля, для использования которого требуется принять условия лицензионного соглашения, при помощи -AcceptLicense
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
Модуль обновляется без запроса на принятие условий лицензионного соглашения.

## <a name="more-details"></a>Дополнительные подробности
### <a name="require-license-acceptance-for-scriptsscriptscriptrequirelicenseacceptancemd"></a>[Запрос на принятие условий лицензии для скриптов](../script/script_RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[Поддержка запроса на принятие условий лицензионного соглашения в коллекции PowerShell](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
