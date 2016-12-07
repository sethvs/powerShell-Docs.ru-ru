---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "рекомендации по ограничениям команд"
ms.technology: powershell
ms.openlocfilehash: 0b4396ee130d99c42f613c1b79193c236ad472e7
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
### <a name="considerations-when-limiting-commands"></a>Рекомендации по ограничениям команд
На этом этапе необходимо обратить внимание на один важный момент.
Все возможности, предоставляемые через JEA, находятся в областях, ограниченных правами администратора.
Пользователи без прав не должны иметь возможность изменять используемые сценарии через конечные точки JEA.

Кроме того, ни в коем случае нельзя предоставлять пользователям JEA возможность перезаписывать конфигурации JEA и сценарии из разрешенного списка во время сеансов JEA.
Будьте особенно внимательны, предоставляя доступ к таким командам, как `Copy-Item`.

