---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Откат к предыдущей конфигурации.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_rollback'
MSHAttr: 'PreferredLib:/library'
title: 'Метод RollBack класса MSFT_DSCLocalConfigurationManager'
---

# Метод RollBack класса MSFT_DSCLocalConfigurationManager

Выполняет откат конфигурации к предыдущей версии.

Синтаксис
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

Параметры
----------

*configurationNumber* \[in\]  
Указывает запрошенную конфигурацию. 

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


