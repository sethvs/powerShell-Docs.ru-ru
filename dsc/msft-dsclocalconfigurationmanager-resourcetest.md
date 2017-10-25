---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод ResourceTest класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: 73d7d543505a3768a0660084345d3858e055514f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a>Метод ResourceTest класса MSFT_DSCLocalConfigurationManager

Напрямую вызывает метод **Test** ресурса DSC.

<a name="syntax"></a>Синтаксис
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a>Параметры
----------

*ResourceType* \[in\]  
Имя вызываемого ресурса.

*ModuleName* \[in\]  
Имя модуля, содержащего вызываемый ресурс.

*resourceProperty* \[in\]  
Указывает имя свойства ресурса и его значение в хэш-таблице как ключ и значение соответственно. Используйте командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) для обнаружения свойств ресурсов и их типов.

*InDesiredState* \[out\]  
В выходных данных это свойство имеет значение **true**, если целевой узел находится в нужном состоянии.

## <a name="return-value"></a>Возвращаемое значение
------------

Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.

## <a name="remarks"></a>Замечания

Это статический метод.

## <a name="requirements"></a>Требования
------------
>**MOF-файл:** DscCore.mof

>**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>См. также:


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 



