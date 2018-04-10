---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: a565f2befddc32f5088fa3e158f58d2dd78d41b4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-module-versioning-support-for-dsc-resources"></a>Поддержка параллельного управления версиями модулей для ресурсов DSC

Модули, содержащие ресурсы DSC, могут быть установлены параллельно, а конфигурации DSC могут использовать конкретную версию ресурса, установленного в системе.

Дополнительные сведения см. в разделе [Использование ресурсов с несколькими версиями](https://msdn.microsoft.com/powershell/dsc/sxsresource).

## <a name="known-issues"></a>Известные проблемы

Ниже перечислены известные с параллельной установкой в этом выпуске:

-   Использование двух различных версий ресурса DSC в одной конфигурации не поддерживается.