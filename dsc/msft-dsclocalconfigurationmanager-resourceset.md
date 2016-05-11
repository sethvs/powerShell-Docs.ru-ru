---
DCS.appliesToProduct: 'WindowsServer\_Dev'
Description: 'Выполнение метода Set непосредственно в поставщике'
MS-HAID: 'cimwin32a.MSFT_DSCLocalConfigurationManager\_resourceset'
MSHAttr: 'PreferredLib:/library'
title: 'Метод ResourceSet класса MSFT_DSCLocalConfigurationManager'
---

# Метод ResourceSet класса MSFT_DSCLocalConfigurationManager

Напрямую вызывает метод **Set** ресурса DSC.

Синтаксис
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
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

*RebootRequired* \[out\]  
В выходных данных это свойство имеет значение **true**, если целевой узел необходимо перезагрузить.

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


