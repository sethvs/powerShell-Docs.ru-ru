---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Выполнение метода Get непосредственно в поставщике.'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_resourceget'
MSHAttr: 'PreferredLib:/library'
title: 'Метод ResourceGet класса MSFT_DSCLocalConfigurationManager'
---

# Метод ResourceGet класса MSFT_DSCLocalConfigurationManager

Напрямую вызывает метод **Get** ресурса DSC.

Синтаксис
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

Параметры
----------

*ResourceType* \[in\]  
Имя вызываемого ресурса.

*ModuleName* \[in\]  
Имя модуля, содержащего вызываемый ресурс.

*resourceProperty* \[in\]  
Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно. Используйте
командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.

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


