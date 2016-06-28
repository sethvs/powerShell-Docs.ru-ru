---
title: "Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 919438862ca9786447b690d2db10e905da0a7c42
ms.openlocfilehash: 19d4790f22491e0bb11de1e315d1ee3b07929d55

---

# Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager

Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.

Синтаксис
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

Параметры
----------

*configurationData* \[in\]  
Указывает передаваемые данные конфигурации.

*configurations* \[out\]  
Выходные данные содержат встроенный экземпляр конфигураций.

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


