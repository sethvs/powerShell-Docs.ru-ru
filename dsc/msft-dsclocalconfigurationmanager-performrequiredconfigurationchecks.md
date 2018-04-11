---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9cc4384088fcc39b09979b8ae4d023fc46307b13
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager

Запускает проверку согласованности с помощью планировщика заданий.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a>Параметры
----------

*Flags* \[in\] Битовая маска, определяющая тип выполняемой проверки согласованности. Допустимы следующие значения, которые можно объединить с помощью битовой операции **OR**:

|Значение |Описание |
|:--- |:---|
|**1** | Обычная проверка согласованности. |
|**2** | Продолжение проверки согласованности после перезагрузки. Это значение не следует использовать в сочетании с другими значениями. |
|**4** | Конфигурация должна извлекаться с запрашивающего сервера, указанного в метаконфигурации для узла. Это значение следует всегда использовать в сочетании с **1**, если указано значение **5**. |
|**8** | Состояние отправки на сервер отчетов. |

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