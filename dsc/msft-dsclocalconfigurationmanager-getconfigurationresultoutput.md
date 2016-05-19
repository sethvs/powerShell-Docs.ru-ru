---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Получение выходных данных агента конфигурации, относящихся к определенному заданию'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_getconfigurationresultoutput'
MSHAttr: 'PreferredLib:/library'
title: 'Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager'
---

# Метод GetConfigurationResultOutput класса MSFT_DSCLocalConfigurationManager

Получает выходные данные агента конфигурации, относящиеся к определенному заданию.

Синтаксис
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

Параметры
----------

*jobId* \[in\]  
Идентификатор задания, для которого необходимо получить выходные данные.

*resumeOutputBookmark* \[in\]  
Указывает, что выходные данные должны быть продолжением от предыдущей закладки.

*output* \[out\]  
Выходные данные для указанного задания.

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


