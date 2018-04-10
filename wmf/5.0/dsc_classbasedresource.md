---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 4def20aa95f66ab23c9eee575150bc3db02541d8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="class-based-dsc-resources"></a>Ресурсы DSC, основанные на классах

## <a name="defining-dsc-resources-with-classes"></a>Определение ресурсов DSC с помощью классов

Основываясь на полученных отзывах, мы упростили создание и использование ресурсов DSC на основе классов.
Ресурс DSC на основе класса и поставщик ресурсов DSC командлета имеют следующие отличия.

* MOF-файл для схемы не требуется.
* Вложенная папка **DSCResource** в папке модуля не требуется.
* Файл модуля PowerShell может содержать несколько классов ресурсов DSC.

Дополнительные сведения см. в разделе [Написание пользовательских ресурсов DSC с использованием классов PowerShell](https://msdn.microsoft.com/powershell/dsc/authoringresource).