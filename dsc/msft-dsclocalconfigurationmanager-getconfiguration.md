---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Отправка документа конфигурации на управляемый узел и использование агента конфигурации для применения конфигурации с помощью метода Get.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_getconfiguration'
MSHAttr: 'PreferredLib:/library'
title: 'Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager'
---

# Метод GetConfiguration класса MSFT_DSCLocalConfigurationManager

Отправляет документ конфигурации на управляемый узел и использует метод **Get** агента конфигурации для применения конфигурации.

Синтаксис
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

Параметры
----------

*configurationData* \[in\]  
Указывает передаваемые данные конфигурации.

*configurations* \[out\]  
Выходные данные содержат встроенный экземпляр конфигураций.

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


