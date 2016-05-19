---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Запускает проверку согласованности.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_performrequiredconfigurationchecks'
MSHAttr: 'PreferredLib:/library'
title: 'Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager'
---

# Метод PerformRequiredConfigurationChecks класса MSFT_DSCLocalConfigurationManager

Запускает проверку согласованности с помощью планировщика заданий.

Синтаксис
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

Параметры
----------

*Flags* \[in\]  
Битовая маска, определяющая тип выполняемой проверки согласованности. Допустимы следующие значения, которые можно объединить с помощью битовой операции **OR**:

|Значение |Описание |
|:--- |:---|
|**1** | Обычная проверка согласованности. |
|**2** | Продолжение проверки согласованности после перезагрузки. Это значение не следует использовать в сочетании с другими значениями. |
|**4** | Конфигурация должна извлекаться с запрашивающего сервера, указанного в метаконфигурации для узла. Это значение следует всегда использовать в сочетании с **1**, если указано значение **5**. |
|**8** | Состояние отправки на сервер отчетов. |

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


 

 





<!--HONumber=Apr16_HO2-->


