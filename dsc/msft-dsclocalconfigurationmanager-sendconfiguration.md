---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Отправка документа конфигурации на управляемый узел и сохранение в состоянии ожидания.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_sendconfiguration'
MSHAttr: 'PreferredLib:/library'
title: 'Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager'
---

# Метод SendConfiguration класса MSFT_DSCLocalConfigurationManager

Отправляет документ конфигурации на управляемый узел и сохраняет его как ожидающее изменение.

Синтаксис
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

Параметры
----------

*ConfigurationData* \[in\]  
Данные среды для конфигурации.

*force* \[in\]  
Значение **true** для принудительной остановки конфигурации.

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


