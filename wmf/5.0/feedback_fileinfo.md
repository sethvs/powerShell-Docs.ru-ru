---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 587f3f592f4aab53c95bbc6d37ea37d7f2364aec
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="updates-to-fileinfo-object"></a><span data-ttu-id="9cc3b-102">Изменения объекта FileInfo</span><span class="sxs-lookup"><span data-stu-id="9cc3b-102">Updates to FileInfo object</span></span>
<span data-ttu-id="9cc3b-103">Сведения о версии файла могут вводить пользователя в заблуждение, особенно в случаях, когда файл был исправлен.</span><span class="sxs-lookup"><span data-stu-id="9cc3b-103">File version information can be misleading, particularly in cases where the file was patched.</span></span> <span data-ttu-id="9cc3b-104">Этот выпуск WMF 5.0 добавляет новые свойства **FileVersionRaw** и **ProductVersionRaw** сценария для объектов FileInfo.</span><span class="sxs-lookup"><span data-stu-id="9cc3b-104">This release of WMF 5.0 adds new **FileVersionRaw** and **ProductVersionRaw** script properties to FileInfo objects.</span></span> <span data-ttu-id="9cc3b-105">Ниже приведены свойства, отображаемые для powershell.exe (при условии, что $pid является идентификатором процесса PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9cc3b-105">Here are the properties as displayed for powershell.exe (assuming $pid is the ID of the PowerShell process):</span></span>

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117

