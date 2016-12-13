---
title: "Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 701063dfa37fe4ba8b014cadadd10339b7fd1bf7
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager

Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a>Параметры
----------

*ConfigurationData* \[in\]  
Данные среды для конфигурации.

*force* \[in\]  
Значение **true** для принудительной остановки конфигурации.

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


 

 



