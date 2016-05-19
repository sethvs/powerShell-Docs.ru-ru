---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Получение параметров локального диспетчера конфигураций, которые используются для управления агентом конфигурации.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_getmetaconfiguration'
MSHAttr: 'PreferredLib:/library'
title: 'Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager'
---

# Метод GetMetaConfiguration класса MSFT_DSCLocalConfigurationManager

Получает параметры локального диспетчера конфигураций, которые используются для управления агентом конфигурации.

Синтаксис
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

Параметры
----------

*MetaConfiguration* \[out\]  
Выходные данные содержат встроенный экземпляр класса **MSFT_DSCMetaConfiguration**, который определяет параметры.

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


