---
title: "Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 6f9c6a8851732574ac72bc4f3a3db1a73fbbecf2
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод ApplyConfiguration класса MSFT_DSCLocalConfigurationManager

Использует агент конфигурации для применения конфигурации, которая находится в состоянии ожидания. 

Если нет ожидающих конфигураций, этот метод повторно применяет текущую конфигурацию.


## <a name="syntax"></a>Синтаксис
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a>Параметры
----------

*force* \[in\]  
Если параметр имеет значение **true**, текущая конфигурация применяется повторно даже при наличии конфигурации в состоянии ожидания.

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

 

 



