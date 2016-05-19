---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Включение отладочной конфигурации DSC'
MS-HAID: 'cimwin32a.msft\_dsclocalconfigurationmanager\_enabledebugconfiguration'
MSHAttr: 'PreferredLib:/library'
title: 'Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager'
---

# Метод EnableDebugConfiguration класса MSFT_DSCLocalConfigurationManager

Включает отладку ресурсов DSC.

Синтаксис
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

Параметры
----------

*BreakAll* \[in\]  
Устанавливает точку останова в каждой строке в сценарии ресурса.

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


