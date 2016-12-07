---
title: "Указание межузловых зависимостей"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: c99ef444027a82d3adeba6a060f60fba3a0fe530
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="specifying-cross-node-dependencies"></a>Указание межузловых зависимостей

> Область применения: Windows PowerShell 5.0

DSC предоставляет специальные ресурсы, **WaitForAll**, **WaitForAny** и **WaitForSome**, которые можно использовать в конфигурациях для указания зависимостей от конфигураций на других узлах. Поведение этих ресурсов описано ниже.

* **WaitForAll** — успешное выполнение, если указанный ресурс находится в нужном состоянии на всех целевых узлах, определенных в свойстве **NodeName**.
* **WaitForAny** — успешное выполнение, если указанный ресурс находится в нужном состоянии как минимум на одном из целевых узлов, определенных в свойстве **NodeName**.
* **WaitForSome** — указывает свойство **NodeCount** в дополнение к свойству **NodeName**. Ресурс выполняется успешно, если он находится в нужном состоянии на минимальном количестве узлов (определяется свойством **NodeCount**), заданных свойством **NodeName**. 

## <a name="using-waitforxxxx-resources"></a>Использование ресурсов WaitForXXXX

Для использования ресурсов **WaitForXXXX** создается блок этого типа ресурса, указывающий ресурсы и узлы DSC для ожидания. Затем используется свойство **DependsOn** в любых других блоках ресурсов в конфигурации для ожидания успешного выполнения условий, указанных в узле **WaitForXXXX**.

Например, в следующей конфигурации целевой узел ожидает завершения выполнения ресурса **xADDomain** на узле **MyDC** не более чем с 30 повторными попытками (с интервалом 15 секунд), прежде чем присоединиться к домену.

```PowerShell
Configuration JoinDomain

{
    Import-DscResource -Module xComputerManagement

    Node myDomainJoinedServer
    {

        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'MyPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

>**Примечание.** По умолчанию ресурсы WaitForXXX выполняют одну попытку, а затем выдают ошибку. Хотя это необязательно, обычно требуется указать интервал и число повторных попыток.

## <a name="see-also"></a>См. также
* [Конфигурации DSC](configurations.md)
* [Ресурсы DSC](resources.md)
* [Настройка локального диспетчера конфигураций](metaConfig.md)

