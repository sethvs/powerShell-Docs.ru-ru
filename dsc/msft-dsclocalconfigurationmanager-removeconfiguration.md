---
title: "Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 4f3d74949d98e3ab3f5136303e229c23ed903c5d
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager

Удаляет файлы конфигурации.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a>Параметры
----------

*Stage* \[in\]  
Указывает, какой документ конфигурации необходимо удалить. Допустимы следующие значения:

|Значение |Описание |
|:--- |:---|
|**1** | Документ **текущей** конфигурации (current.mof). |
|**2** | Документ **ожидающей** конфигурации (pending.mof).  |
|**4** | Документ **предыдущей** конфигурации (previous.mof). |

*Force* \[in\]  
Значение **true** для принудительного удаления конфигурации.

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


 

 



