---
title: "Ресурсы DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 6477ae8575c83fc24150f9502515ff5b82bc8198
ms.openlocfilehash: 0a27a40b995393c41f0496a5f7fa3f56fbd865dd

---

# Ресурсы DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Ресурсы службы настройки требуемого состояния (DSC) предоставляют шаблоны для настройки DSC. В ресурсе представлены свойства, которые можно настроить (схема), и функции сценариев PowerShell, которые вызывает локальный диспетчер конфигураций (LCM).

Ресурс может моделировать что-либо универсальное, например файл, или конкретное, например настройку сервера IIS.  Группы похожих ресурсов объединяются в DSC-модуль, в котором все необходимые файлы упорядочиваются в переносимую структуру и включаются метаданные для идентификации целевого предназначения ресурсов.  

Описание ресурсов DSC см. в следующих разделах:

- [Встроенные ресурсы DSC](builtInResource.md)
- [Создание пользовательских ресурсов DSC](authoringResource.md)
- [Встроенные ресурсы DSC для Linux](lnxBuiltInResources.md)




<!--HONumber=Jun16_HO4-->


