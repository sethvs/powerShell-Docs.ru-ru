---
ms.date: 06/09/2017
schema: 2.0.0
keywords: powershell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 4a2dc39c2b6c380fb4ca94f9fd071ed9cdb35049
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="requiring-license-acceptance-for-scripts"></a>Запрос на принятие условий лицензии для скриптов

Для скриптов процедура принятия условий лицензионного соглашения не поддерживается. Но поддерживается вариант, при котором скрипт зависит от модуля, для использования которого требуется принять условия лицензионного соглашения.

Команды скрипта (Install-Script/Save-Script/Update-Script) поддерживают новый параметр -AcceptLicense. Его поведение аналогично действиям пользователя после прочтения лицензионного соглашения. Если параметр -AcceptLicense не указан, для пользователя будет отображаться файл license.txt зависимого модуля и запрос на принятие условий лицензионного соглашения.

## <a name="examples"></a>ПРИМЕРЫ

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>Пример 1. Установка скрипта с зависимостями, для использования которого требуется принять условия лицензионного соглашения
Скрипт ScriptRequireLicenseAcceptance зависит от модуля ModuleRequireLicenseAcceptance. Пользователю предлагается принять условия лицензионного соглашения.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Пример 2. Установка скрипта с зависимостями, для использования которого требуется принять условия лицензионного соглашения и указать -AcceptLicense
Скрипт ScriptRequireLicenseAcceptance зависит от модуля ModuleRequireLicenseAcceptance. Пользователю не предлагается принять условия лицензии, так как указан параметр -AcceptLicense.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>Дополнительные подробности
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[Поддержка запроса на принятие условий лицензионного соглашения для модулей](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[Поддержка запроса на принятие условий лицензионного соглашения в коллекции PowerShell](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)