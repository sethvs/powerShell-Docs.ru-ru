---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: psget_устранение_проблем_с_командлетами
ms.openlocfilehash: bc49dc78b8205d1194ddfe4bdca98b3e681860bd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
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