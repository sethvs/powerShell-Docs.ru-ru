---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурсы DSC"
ms.openlocfilehash: 62bf352b929d661e585e145e5aab0f44f13010a1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-resources"></a>Ресурсы DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC. В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).

Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.  Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.  

Описание ресурсов DSC см. в следующих разделах:

- [Встроенные ресурсы DSC](builtInResource.md)
- [Встроенные пользовательские ресурсы DSC](authoringResource.md)
- [Встроенные ресурсы DSC для Linux](lnxBuiltInResources.md)

