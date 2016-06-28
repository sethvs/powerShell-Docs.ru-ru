---
title: "Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 919438862ca9786447b690d2db10e905da0a7c42
ms.openlocfilehash: 4662bfed62fce47be7d42a083ad5a7be801e6ff1

---


# Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager

Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.

Синтаксис
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

Параметры
----------

*MetaConfiguration* \[out\]  
Выходные данные содержат встроенный экземпляр класса **MSFT_DSCMetaConfiguration**, который определяет параметры.

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


