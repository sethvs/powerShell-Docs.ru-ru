---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class" class="xliff"></a>
# Метод SendConfigurationApplyAsync класса MSFT_DSCLocalConfigurationManager

Асинхронно отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.

<a id="syntax" class="xliff"></a>
Синтаксис
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a id="parameters" class="xliff"></a>
Параметры
----------

*ConfigurationData* \[in\]  
Данные среды для конфигурации.

*force* \[in\]  
Значение **true** для принудительной остановки конфигурации.

*jobId* \[in\]  
Идентификатор задания, для которого отправляется конфигурация.

<a id="return-value" class="xliff"></a>
## Возвращаемое значение
------------

Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.

<a id="remarks" class="xliff"></a>
## Замечания

Это статический метод.

<a id="requirements" class="xliff"></a>
## Требования
------------
>**MOF-файл:** DscCore.mof

>**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration


<a id="see-also" class="xliff"></a>
## См. также:


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)


 

 



