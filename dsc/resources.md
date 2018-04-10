---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурсы DSC
ms.openlocfilehash: e393c8fe2e1ba8d68ba9aa1b656d1e5ebfad30e8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-resources"></a>Ресурсы DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC. В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).

Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.  Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.

Описание ресурсов DSC см. в следующих разделах:

- [Встроенные ресурсы DSC](builtInResource.md)
- [Встроенные пользовательские ресурсы DSC](authoringResource.md)
- [Встроенные ресурсы DSC для Linux](lnxBuiltInResources.md)