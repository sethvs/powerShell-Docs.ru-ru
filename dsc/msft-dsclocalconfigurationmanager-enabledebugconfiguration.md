---
title: "Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: f74e9941180c00a1aae1bd1d7b48fa4de0c8790d
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager

Включает отладку ресурсов DSC.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a>Параметры
----------

*BreakAll* \[in\]  
Устанавливает точку останова в каждой строке в сценарии ресурса.

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
 

 



