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
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="4da23-103">Запрос на принятие условий лицензии для скриптов</span><span class="sxs-lookup"><span data-stu-id="4da23-103">Requiring License Acceptance for Scripts</span></span>

<span data-ttu-id="4da23-104">Для скриптов процедура принятия условий лицензионного соглашения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4da23-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="4da23-105">Но поддерживается вариант, при котором скрипт зависит от модуля, для использования которого требуется принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="4da23-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="4da23-106">Команды скрипта (Install-Script/Save-Script/Update-Script) поддерживают новый параметр -AcceptLicense. Его поведение аналогично действиям пользователя после прочтения лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="4da23-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="4da23-107">Если параметр -AcceptLicense не указан, для пользователя будет отображаться файл license.txt зависимого модуля и запрос на принятие условий лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="4da23-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="4da23-108">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="4da23-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="4da23-109">Пример 1. Установка скрипта с зависимостями, для использования которого требуется принять условия лицензионного соглашения</span><span class="sxs-lookup"><span data-stu-id="4da23-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>
<span data-ttu-id="4da23-110">Скрипт ScriptRequireLicenseAcceptance зависит от модуля ModuleRequireLicenseAcceptance.</span><span class="sxs-lookup"><span data-stu-id="4da23-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="4da23-111">Пользователю предлагается принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="4da23-111">User is prompted to Accept License.</span></span>
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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="4da23-112">Пример 2. Установка скрипта с зависимостями, для использования которого требуется принять условия лицензионного соглашения и указать -AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="4da23-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>
<span data-ttu-id="4da23-113">Скрипт ScriptRequireLicenseAcceptance зависит от модуля ModuleRequireLicenseAcceptance.</span><span class="sxs-lookup"><span data-stu-id="4da23-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="4da23-114">Пользователю не предлагается принять условия лицензии, так как указан параметр -AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="4da23-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="4da23-115">Дополнительные подробности</span><span class="sxs-lookup"><span data-stu-id="4da23-115">More details</span></span>
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[<span data-ttu-id="4da23-116">Поддержка запроса на принятие условий лицензионного соглашения для модулей</span><span class="sxs-lookup"><span data-stu-id="4da23-116">Require License Acceptance support for Modules</span></span>](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[<span data-ttu-id="4da23-117">Поддержка запроса на принятие условий лицензионного соглашения в коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="4da23-117">Require License Acceptance support on PowerShellGallery</span></span>](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[<span data-ttu-id="4da23-118">Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="4da23-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)