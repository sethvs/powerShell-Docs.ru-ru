---
title: "Метод ResourceGet класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 1666b85402f17230090f7290c8cb400dd9fbf0a6
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод ResourceGet класса MSFT_DSCLocalConfigurationManager

Напрямую вызывает метод **Get** ресурса DSC.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a>Параметры
----------

*ResourceType* \[in\]  
Имя вызываемого ресурса.

*ModuleName* \[in\]  
Имя модуля, содержащего вызываемый ресурс.

*resourceProperty* \[in\]  
Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно. Используйте командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.

*configurations* \[out\]  
Выходные данные содержат встроенный экземпляр конфигураций.

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


 

 



