---
description: 
manager: carolz
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет,коллекция"
ms.date: 2016-10-14
contributor: manikb
title: "psget_заполнениезависимостеймодуля"
ms.technology: powershell
ms.openlocfilehash: 3d89dddf2fc31a9fdb1a57f21baaf757990989c7
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a>Логика для подготовки зависимостей модуля во время операции публикации
1.  Модули, перечисленные в списке RequiredModules, считаются зависимостями.
2.  Модули, перечисленные в списке NestedModules, база модуля которых не находится под указанной базой модуля, считаются зависимостями.

3.  Указанные выше зависимости должны быть доступны в том же целевом репозитории, иначе операция публикации приведет к ошибке.
    Например, если SnippetPx недоступен в репозитории, возникнет следующая ошибка.
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  Некоторые зависимости модуля могут управляться извне; в этом случае они должны добавляться в запись ExternalModuleDependencies раздела PSData манифеста модуля.
    Ниже приводится часть вышеупомянутого сообщения об ошибке
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

*Во время установки модуля подготовленный выше список зависимостей используется для установки зависимостей.*

*Убедитесь, что зависимости вашего модуля доступны в разделе $env:PSModulePath в системе во время публикации.*

