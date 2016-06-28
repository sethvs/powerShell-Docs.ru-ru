---
title: "Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: c915ebd021ed20209bc491505d45cff2ac89f21d
ms.openlocfilehash: 701063dfa37fe4ba8b014cadadd10339b7fd1bf7

---


# Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager

Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.

Синтаксис
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

Параметры
----------

*ConfigurationData* \[in\]  
Данные среды для конфигурации.

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


