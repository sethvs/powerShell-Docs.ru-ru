---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод RemoveConfiguration класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: fed45836293adedbce18f01cfe53cdfa1a474975
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
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


 

 



