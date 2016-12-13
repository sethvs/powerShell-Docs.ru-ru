---
title: "Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4662bfed62fce47be7d42a083ad5a7be801e6ff1
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager

Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a>Параметры
----------

*MetaConfiguration* \[out\]  
Выходные данные содержат встроенный экземпляр класса **MSFT_DSCMetaConfiguration**, который определяет параметры.

## <a name="return-value"></a>Возвращаемое значение
------------

Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.

## <a name="remarks"></a>Замечания

Это статический метод.

## <a name="requirements"></a>Требования
------------
>**MOF-файл:** DscCore.mof

>**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>См. также:


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 



