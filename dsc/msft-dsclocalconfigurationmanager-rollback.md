---
title: "Метод RollBack класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: c915ebd021ed20209bc491505d45cff2ac89f21d
ms.openlocfilehash: 771a9c7b50aba26f89dbf6b24eb3df67bafeac0a

---


# Метод RollBack класса MSFT_DSCLocalConfigurationManager

Выполняет откат конфигурации к предыдущей версии.

Синтаксис
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

Параметры
----------

*configurationNumber* \[in\]  
Указывает запрошенную конфигурацию. 

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


