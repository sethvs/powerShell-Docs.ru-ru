---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Остановка выполняющейся конфигурации.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_stopconfiguration'
MSHAttr: 'PreferredLib:/library'
title: 'Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager'
---

# Метод StopConfiguration класса MSFT_DSCLocalConfigurationManager

Останавливает выполняемое изменение конфигурации.

Синтаксис
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

Параметры
----------

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


