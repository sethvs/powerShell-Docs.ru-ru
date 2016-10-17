---
title: "Соглашение об именовании для частичной конфигурации"
author: jaimeo
contributor: berheabrha
translationtype: Human Translation
ms.sourcegitcommit: dfa487a11528e26faf5b0e8637b75983abe0b1c8
ms.openlocfilehash: 368c26766961e760fd2de8c99057121bea076158

---

##Соглашение об именовании для частичной конфигурации
В предыдущих выпусках соглашение об именовании для частичной конфигурации гласило, что имя MOF-файла на опрашивающих сервере или в службе должно соответствовать имени частичной конфигурации, указанному в параметрах локального диспетчера конфигурации, которое, в свою очередь, должно соответствовать имени конфигурации, внедренному в MOF-файл. См. моментальные снимки ниже.- •   Параметры локальной конфигурации, определяющие частичную конфигурацию, которую разрешено получать узлу.

![Пример метаконфигурации](../../images/MetaConfigPartialOne.png)

•   Пример определения частичной конфигурации 

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

•   Имя конфигурации, включенное в созданный MOF-файл.

![Пример созданного MOF-файла](../../images/PartialGeneratedMof.png)

•   Имя файла в репозитории конфигураций 

![Имя файла в репозитории конфигураций](../../images/PartialInConfigRepository.png)

Служба автоматизации Azure создавала MOF-файлы с именами ``<ConfigurationName>.<NodeName>.mof``. Поэтому следующая конфигурация будет скомпилирована в файл PartialOne.Localhost.mof.  
Это делало невозможным запрос частичной конфигурации из службы автоматизации Azure.

```Powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test 
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

В WMF 5.1 частичная конфигурация на опрашивающем сервере или в службе может иметь имя ``<ConfigurationName>.<NodeName>.mof``. Кроме того, если компьютер запрашивает одну конфигурацию с опрашивающего сервера или службы, то документ конфигурации в репозитории конфигураций опрашивающего сервера может иметь любое имя. Такая гибкость именования позволяет управлять частичной конфигурацией узла как при помощи как локальной опрашивающей службы, так и принадлежащей к службе автоматизации Azure. Например, можно иметь "базовую" частичную конфигурацию, которая отправляется локально, и другую частичную конфигурацию, которая запрашивается из службы автоматизации Azure.

В следующей метаконфигурации узел находится как под локальным управлением, так и под управлением службы автоматизации Azure.

```Powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30;
            RefreshMode = "PULL";            
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation Service.
        PartialConfiguration PartialCOnfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"   
        }
    
        # This partial configuration is managed locally.
        PartialConfiguration OnPremConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   slcm -Path .\RegistrationMetaConfig -Verbose
 ```





<!--HONumber=Aug16_HO3-->


