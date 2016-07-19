---
title: "Конфигурации DSC"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 59bf4cff540dabeeb77038ea84177f7c6bac2b4b
ms.openlocfilehash: e5412a3168a18d1dbd117ed8b3eb6dd42a8d8f70

---

# Конфигурации DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Конфигурации DSC — это сценарии PowerShell, определяющие особый тип функции. Для определения конфигурации используйте ключевое слово PowerShell __Configuration__.

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
```

Сохраните сценарий как PS1-файл.

## Синтаксис конфигурации

Сценарий конфигурации состоит из следующих элементов:

- Блок **Configuration**. Это основной блок сценария. Для его определения необходимо использовать ключевое слово **Configuration** и указать имя. В этом случае имя конфигурации — MyDscConfiguration.
- Один блок **Node** или несколько. Определяют настраиваемые вами узлы (компьютеры или виртуальные машины). В представленной выше конфигурации присутствует один блок **Node**, соответствующий компьютеру с именем TEST-PC1.
- Один блок ресурсов или несколько. В этих блоках конфигурация определяет свойства настраиваемых ресурсов. В данном случае используются два блока ресурсов, каждый из которых вызывает ресурс WindowsFeature.

В блоке **Configuration** можно делать все то же самое, что и в функции PoweShell. Например, в предыдущем примере вместо того, чтобы прописывать имя целевого компьютера конфигурации в коде, можно добавить в имя узла соответствующий параметр:

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
```

В данном примере вы указываете имя узла, передавая его как параметр $ComputerName при [компиляции конфигурации](# Compiling the configuration). По умолчанию используется имя localhost.

## Компиляция конфигурации
Прежде чем активировать конфигурацию, необходимо скомпилировать ее в MOF-документ. Для этого нужно вызвать конфигурацию так же, как функцию PowerShell.
>__Примечание__. Для вызова конфигурация функция должна находиться в глобальной области видимости (как и любая другая функция PowerShell). Для этого нужно либо использовать вызов сценария с точкой, либо выполнить сценарий конфигурации, нажав клавишу F5 или кнопку __Выполнить сценарий__ в интегрированной среде сценариев. Чтобы использовать вызов сценария с точкой, выполните команду `. .\myConfig.ps1`, где `myConfig.ps1` — это имя файла сценария, который содержит конфигурацию.

При вызове конфигурации она выполняет следующие действия:

- разрешает все переменные; 
- создает папку в текущем каталоге с тем же именем, что и у конфигурации;
- создает файл с именем _имя_узла_.mof в новой папке, где _имя_узла_ — это имя целевого узла конфигурации. Если узлов несколько, MOF-файл создается для каждого из них.

>__Примечание__. MOF-файл содержит все сведения о конфигурации целевого узла. Поэтому его необходимо хранить в безопасном месте. Дополнительные сведения см. в статье [Защита MOF-файла](secureMOF.md).

При компиляции первой приведенной конфигурации создается следующая структура папок:

```powershell
PS C:\users\default\Documents\DSC Configurations> . .\MyDscConfiguration.ps1
PS C:\users\default\Documents\DSC Configurations> MyDscConfiguration
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 TEST-PC1.mof
```  

Если конфигурация принимает какой-либо параметр, как во втором примере, его необходимо указывать во время компиляции. Вот как это выглядит:

```powershell
PS C:\users\default\Documents\DSC Configurations> . .\MyDscConfiguration.ps1
PS C:\users\default\Documents\DSC Configurations> MyDscConfiguration -ComputerName 'MyTestNode'
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```      

## Использование ключевого слова DependsOn
Одно из полезных ключевых слов DSC — это __DependsOn__. Как правило (хоть и не всегда), DSC применяет ресурсы в порядке их появления в конфигурации. Ключевое слово __DependsOn__ определяет, какие ресурсы зависят от других ресурсов, а LCM следит за тем, чтобы они применялись в правильном порядке независимо от того, в каком порядке определены экземпляры ресурсов. Например, в конфигурации может быть указано, что экземпляр ресурса __User__ зависит от наличия ресурса __Group__:

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}
```

## Использование новых ресурсов в конфигурации
Выполняя предыдущие примеры, вы могли заметить предупреждение о том, что используемый ресурс не импортирован.
Сейчас DSC поставляется с модулем PSDesiredStateConfiguration, в который входят 12 ресурсов. Другие ресурсы во внешних модулях необходимо добавлять в `$env:PSModulePath` в том порядке, в котором LCM должен будет их распознать. Определить, какие ресурсы установлены в системе и доступны для использования LCM, позволяет новый командлет [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx). После добавления в `$env:PSModulePath` и правильного распознавания командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) эти модули нужно будет загрузить в конфигурацию. __Import-DscResource__ — это динамическое ключевое слово, распознаваемое только в блоке __Configuration__ (т. е. оно не является командлетом). __Import-DscResource__ поддерживает два параметра:
* Параметр __ModuleName__ — рекомендуемый способ применения __Import-DscResource__. Он принимает имя модуля, содержащего ресурсы для импорта (а также массив строк с именами модулей). 
* Параметр __Name__ — имя импортируемого ресурса. Это не то понятное имя, которое возвращается командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), а имя класса, используемое при определении схемы ресурса (возвращается как параметр __ResourceType__ командлетом [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)). 

## См. также
* [Общие сведения о службе настройки требуемого состояния Windows PowerShell](overview.md)
* [Ресурсы DSC](resources.md)
* [Настройка локального диспетчера конфигураций](metaConfig.md)




<!--HONumber=Jul16_HO1-->


