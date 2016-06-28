---
title: "Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: c915ebd021ed20209bc491505d45cff2ac89f21d
ms.openlocfilehash: 8f13964dfbbe1cd827c58232a35d1cbacddeed1b

---

# Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager

Получает выходные данные агента конфигурации, относящиеся к определенному заданию.

Синтаксис
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

Параметры
----------

*jobId* \[in\]  
Идентификатор задания, для которого необходимо получить выходные данные.

*resumeOutputBookmark* \[in\]  
Указывает, что выходные данные должны быть продолжением от предыдущей закладки.

*output* \[out\]  
Выходные данные для указанного задания.

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


