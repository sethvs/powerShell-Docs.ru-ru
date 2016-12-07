---
title: "Встроенные ресурсы настройки требуемого состояния для Linux"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 6b001c12885022006003ef3ffe91b7aede07bd17
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Встроенные ресурсы настройки требуемого состояния для Linux

Ресурсы — это строительные блоки, которые можно использовать для написания сценария настройки требуемого состояния (DSC) PowerShell. DSC для Linux поставляется с набором встроенных возможностей для настройки ресурсов, таких как файлы и папки, пакеты, переменные среды, службы и процессы.

## <a name="built-in-resources"></a>Встроенные ресурсы 

Список ресурсов и ссылки на статьи, в которых они рассматриваются подробно.

* Ресурс [nxArchive](lnxArchiveResource.md) — предоставляет механизм распаковки файлов архива в формате TAR или ZIP в заданную папку.
* Ресурс [nxEnvironment](lnxEnvironmentResource.md) — управляет переменными среды на целевых узлах. 
* Ресурс [nxFile](lnxFileResource.md) — управляет файлами и каталогами Linux. 
* Ресурс [nxFileLine](lnxFileLineResource.md) — управляет отдельными строками в файле Linux. 
* Ресурс [nxGroup](lnxGroupResource.md) — управляет локальными группами Linux. 
* Ресурс [nxPackage](lnxPackageResource.md) — управляет пакетами на узлах Linux.
* Ресурс [nxScript](lnxScriptResource.md) — запускает сценарии на целевых узлах.
* Ресурс [nxService](lnxServiceResource.md) — управляет службами Linux (управляющими программами или "демонами").
* Ресурс [nxSshAuthorizedKeys](lnxSshAuthorizedKeysResource.md) — управляет открытыми SSH-ключами для пользователей Linux. 
* Ресурс [nxUser](lnxUserResource.md) — управляет локальными пользователями Linux. 
  
