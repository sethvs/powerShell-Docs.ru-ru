---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Задание параметров локального диспетчера конфигураций, которые используются для управления агентом конфигурации.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_sendmetaconfigurationapply'
MSHAttr: 'PreferredLib:/library'
title: 'Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager'
---

# Метод SendMetaConfigurationApply класса MSFT_DSCLocalConfigurationManager

Задает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.

Синтаксис
------

```mof
uint32 SendMetaConfigurationApply(
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


