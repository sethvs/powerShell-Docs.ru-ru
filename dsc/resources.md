---
title: "Ресурсы DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 0a27a40b995393c41f0496a5f7fa3f56fbd865dd
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-resources"></a>Ресурсы DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC. В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).

Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.  Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.  

Описание ресурсов DSC см. в следующих разделах:

- [Встроенные ресурсы DSC](builtInResource.md)
- [Встроенные пользовательские ресурсы DSC](authoringResource.md)
- [Встроенные ресурсы DSC для Linux](lnxBuiltInResources.md)

