---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: d40e5475c4132d6377c9a4559262a41b4842180a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="class-based-dsc-resources"></a>Ресурсы DSC, основанные на классах

## <a name="defining-dsc-resources-with-classes"></a>Определение ресурсов DSC с помощью классов

Основываясь на полученных отзывах, мы упростили создание и использование ресурсов DSC на основе классов. Ресурс DSC на основе класса и поставщик ресурсов DSC командлета имеют следующие отличия.

* MOF-файл для схемы не требуется.
* Вложенная папка **DSCResource** в папке модуля не требуется.
* Файл модуля PowerShell может содержать несколько классов ресурсов DSC.

Дополнительные сведения см. в разделе [Написание пользовательских ресурсов DSC с использованием классов PowerShell](https://msdn.microsoft.com/powershell/dsc/authoringresource).

