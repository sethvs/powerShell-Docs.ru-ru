---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "коллекция,powershell,командлет,psget"
title: "psget_устранение_проблем_с_командлетами"
ms.openlocfilehash: ccb39f44e8d11f1e2a912da0c4f18b700e836c91
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Как разрешить проблему "ПРЕДУПРЕЖДЕНИЕ. Не удалось скачать пакет "имя вашего пакета""?




Нам известно, что на некоторых компьютерах командлеты Install-Module и Update-Module могут завершаться ошибкой.
По результатам нашего расследования это связано с сетевым подключением.
Недавно мы обновили поставщик NuGet, чтобы он смог надежно скачивать пакеты.
Выполните описанные ниже инструкции, чтобы установить последнюю сборку поставщика NuGet, а затем установите или обновите свой модуль.
Для примера возьмем модуль Azure.

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```

