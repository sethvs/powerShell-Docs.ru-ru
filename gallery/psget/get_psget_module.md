---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: коллекция,powershell,командлет,psget
title: Получение модуля PowerShellGet
ms.openlocfilehash: a392f795d8c065ff881bc6cc113e63a1f18bcb44
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
<a name="get-powershellget-module"></a>Получение модуля PowerShellGet
========================

### <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>Модуль PowerShellGet входит в комплект поставки в следующих выпусках:
- [Windows 10](https://www.microsoft.com/windows/get-windows-10) или более поздняя версия;
- [Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/windows-server-2016) или более поздняя версия;
- [Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) или более поздняя версия;
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases).

### <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>Получение модуля PowerShellGet для PowerShell версии 3.0 и 4.0
- [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

### <a name="get-the-latest-version-from-powershell-gallery"></a>Получение последней версии из коллекции PowerShell

- Перед обновлением PowerShellGet всегда устанавливайте последний поставщик Nuget. Для этого выполните следующую команду в сеансе PowerShell с повышенными привилегиями.
```powershell
Install-PackageProvider Nuget –Force
Exit
```

#### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>Для систем с PowerShell 5.0 (или более поздней версии) можно установить последнюю версию PowerShellGet
- Чтобы сделать это в Windows 10, Windows Server 2016, любой системе с установленным WMF 5.0 или 5.1 или любой системе с PowerShell 6, выполните следующие команды из сеанса PowerShell с повышенными привилегиями.
```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- Update-Module позволяет получить более новые версии.
```powershell
Update-Module -Name PowerShellGet
Exit
```

#### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a>Для систем под управлением PowerShell 3 или PowerShell 4, на которых установлено [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

- Используйте командлеты PowerShellGet ниже из сеанса PowerShell с повышенными привилегиями, чтобы сохранить модули в локальный каталог.

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- Убедитесь, что модули PowerShellGet и PackageManagment не загружены в других процессах.
- Удалите содержимое папок `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` и `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\`.
- Снова откройте консоль PS с повышенным уровнем разрешений, а затем выполните следующие команды.

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
```