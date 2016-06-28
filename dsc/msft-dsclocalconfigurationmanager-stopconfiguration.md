---
title: "Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: c915ebd021ed20209bc491505d45cff2ac89f21d
ms.openlocfilehash: 9721486cca6f94d6b156c6ee1992eced6652c123

---

# Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager

Останавливает выполняемое изменение конфигурации.

Синтаксис
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

Параметры
----------

*force* \[in\]  
Значение **true** для принудительной остановки конфигурации.

## Возвращаемое значение
------------

Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.

## Замечания

Это статический метод.

## Требования
------------
>**MOF-файл:** DscCore.mof

>**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration


## См. также:


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 






<!--HONumber=Jun16_HO4-->


