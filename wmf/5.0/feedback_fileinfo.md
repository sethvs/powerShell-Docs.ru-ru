---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 6356902193fc6ec651b2f7e53f8885cb59f17542
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="updates-to-fileinfo-object"></a>Изменения объекта FileInfo
Сведения о версии файла могут вводить пользователя в заблуждение, особенно в случаях, когда файл был исправлен. Этот выпуск WMF 5.0 добавляет новые свойства **FileVersionRaw** и **ProductVersionRaw** сценария для объектов FileInfo. Ниже приведены свойства, отображаемые для powershell.exe (при условии, что $pid является идентификатором процесса PowerShell).

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117