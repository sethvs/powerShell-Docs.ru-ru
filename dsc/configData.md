---
title: "Разделение данных конфигурации и данных среды"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 72555a36819c9717fafdd3daede8fa2f02c692b2
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="separating-configuration-and-environment-data"></a>Разделение данных конфигурации и данных среды

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

С помощью встроенного параметра DSC **ConfigurationData** можно определить данные, которые будут использоваться в конфигурации. Это позволяет создать единую конфигурацию, которую можно использовать для нескольких узлов или для различных сред. Например, при разработке приложения можно использовать одну и ту же конфигурацию для среды разработки и для рабочей среды и указать данные для каждой среды с помощью данных конфигурации.

Чтобы увидеть, как это работает, рассмотрим очень простой пример. Мы создадим одну конфигурацию, в соответствии с которой на некоторых узлах будет находиться **IIS**, а на других узлах — **Hyper-V**: 

```powershell
Configuration MyDscConfiguration {
    
    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        WindowsFeature IISInstall {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
        
    }
    Node $AllNodes.Where($_.Role -eq "VMHost").NodeName
    {
        WindowsFeature HyperVInstall {
            Ensure = 'Present'
            Name   = 'Hyper-V'
        }
    }
}

$MyData = 
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            Role = 'WebServer'
        }

        @{
            NodeName    = 'VM-2'
            FeatureName = 'VMHost'
        }
    )
}

MyDscConfiguration -ConfigurationData $MyData
```

В последней строке этого сценария конфигурация компилируется в документы MOF. Для этого в качестве значения параметра **ConfigurationData** передается `$MyData`. `$MyData` указывает два разных узла, каждый из которых имеет свои собственные `NodeName` и `Role`. В конфигурации динамически создаются блоки **Node** с помощью фильтрации коллекции узлов, полученной от `$MyData` (в частности, `$AllNodes`), по свойству `Role`.

Теперь рассмотрим, как это работает, более подробно.

## <a name="the-configurationdata-parameter"></a>Параметр ConfigurationData

Конфигурация DSC принимает параметр **ConfigurationData**. Этот параметр указывается при компиляции конфигурации. Сведения о компиляции конфигураций см. в разделе [Конфигурации DSC](configurations.md).

Параметр **ConfigurationData** представляет собой хэш-таблицу, в которой должен быть по меньшей мере один ключ с именем **AllNodes**. В ней также могут быть другие ключи:

```powershell
$MyData = 
@{
    AllNodes = @()
    NonNodeData = ""   
}
```

Значение ключа **AllNodes** представляет собой массив. Каждый элемент этого массива также является хэш-таблицей, в которой должен быть по меньшей мере один ключ с именем **AllNodes**:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
        },

 
        @{
            NodeName = "VM-2"
        },

 
        @{
            NodeName = "VM-3"
        }
    );

    NonNodeData = ""   
}
```

В каждую хэш-таблицу можно добавить и другие ключи:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1"
            Role     = "WebServer"
        },

 
        @{
            NodeName = "VM-2"
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3"
            Role     = "WebServer"
        }
    );

    NonNodeData = ""   
}
```

Чтобы применить свойство ко всем узлам, можно создать элемент массива **AllNodes**, значение параметра **NodeName** для которого будет равно `*`. Например, чтобы присвоить каждому узлу свойство `LogPath`, можно написать следующее:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName     = "*"
            LogPath      = "C:\Logs"
        },

 
        @{
            NodeName     = "VM-1"
            Role         = "WebServer"
            SiteContents = "C:\Site1"
            SiteName     = "Website1"
        },

 
        @{
            NodeName     = "VM-2"
            Role         = "SQLServer"
        },

 
        @{
            NodeName     = "VM-3"
            Role         = "WebServer"
            SiteContents = "C:\Site2"
            SiteName     = "Website3"
        }
    );
}
```

Это аналогично добавлению свойства с именем `LogPath` и значением `"C:\Logs"` в каждый из других блоков (`VM-1`, `VM-2` и `VM-3`).

## <a name="defining-the-configurationdata-hashtable"></a>Определение хэш-таблицы ConfigurationData

Хэш-таблицу **ConfigurationData** можно определить в виде переменной в файле сценария конфигурации (как в наших предыдущих примерах) или в отдельном PSD1-файле. Чтобы определить хэш-таблицу **ConfigurationData** в PSD1-файле, создайте файл, который будет содержать только хэш-таблицу, представляющую данные конфигурации.

Например, можно создать файл с именем `MyData.psd1` и со следующим содержимым:

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        }

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

Чтобы использовать данные конфигурации, которая определена в PSD1-файле, передайте путь и имя этого файла в качестве значения параметра **ConfigurationData** при компиляции конфигурации:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Использование переменных ConfigurationData в конфигурации

DSC предоставляет три специальные переменные, которые могут использоваться в сценарии конфигурации: **$AllNodes**, **$Node** и **$ConfigurationData**.

- **$AllNodes** относится ко всей коллекции узлов, определенных в **ConfigurationData**. Коллекцию **AllNodes** можно отфильтровать с помощью **.Where()** и **.ForEach()**.
- После фильтрации коллекции с помощью **.Where()** или **.ForEach()** элемент **Node** будет указывать на конкретную запись в **AllNodes**.
- **ConfigurationData** ссылается на всю хэш-таблицу, которая передается в качестве параметра при компиляции конфигурации.

## <a name="devops-example"></a>Пример DevOps

Рассмотрим полный пример использования одной и той же конфигурации для настройки среды разработки и рабочей среды веб-сайта. В среде разработки службы IIS и SQL Server устанавливаются на одних и тех же узлах. В рабочей среде службы IIS и SQL Server устанавливаются на отдельных узлах. Для указания данных конфигурации для двух различных сред мы будем использовать PSD1-файл данных конфигурации.

### <a name="configuration-data-file"></a>Файл данных конфигурации

Данные среды разработки и рабочей среды определяются в файле `DevProdEnvData.psd1` следующим образом:

```powershell
@{

    AllNodes = @(

        @{
            NodeName        = "*"
            SQLServerName   = "MySQLServer"
            SqlSource       = "C:\Software\Sql"
            DotNetSrc       = "C:\Software\sxs"
        },

        @{
            NodeName        = "Prod-SQL"
            Role            = "MSSQL"
        },

        @{
            NodeName        = "Prod-IIS"
            Role            = "Web"
            SiteContents    = "C:\Website\Prod\SiteContents\"
            SitePath        = "\\Prod-IIS\Website\"
        }

        @{
            NodeName         = "Dev"
            Role             = "MSSQL", "Web"
            SiteContents     = "C:\Website\Dev\SiteContents\"
            SitePath         = "\\Dev\Website\"

        }

    )

}

    )

}
```

### <a name="configuration-file"></a>Файл конфигурации

Теперь отфильтруем узлы, определенные в `DevProdEnvData.psd1`, по их роли (`MSSQL`, `Dev` или и то и другое) и настроим их соответствующим образом. В среде разработки службы IIS и SQL Server установлены на одном узле, а в рабочей среде на двух различных узлах. Содержимое сайта также различно, как указано в свойствах `SiteContents`.

В конце сценария конфигурации мы вызываем конфигурацию (компилируем ее в документ MOF), передав `DevProdEnvData.psd1` в качестве параметра `$ConfigurationData`.

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs

    Node $AllNodes.Where{$_.Role -contains "MSSQL"}.Nodename
   {
        # Install prerequisites
        WindowsFeature installdotNet35
        {            
            Ensure      = "Present"
            Name        = "Net-Framework-Core"
            Source      = "c:\software\sxs"
        }

        # Install SQL Server
        xSqlServerInstall InstallSqlServer
        {
            InstanceName = $Node.SQLServerName
            SourcePath   = $Node.SqlSource
            Features     = "SQLEngine,SSMS"
            DependsOn    = "[WindowsFeature]installdotNet35"

        }
   }

   Node $AllNodes.Where($_.Role -contains "Web")
   {
        # Install the IIS role
        WindowsFeature IIS
        {
            Ensure       = 'Present'
            Name         = 'Web-Server'
        }

        # Install the ASP .NET 4.5 role
        WindowsFeature AspNet45
        {
            Ensure       = 'Present'
            Name         = 'Web-Asp-Net45'

        }

        # Stop the default website
        xWebsite DefaultSite 
        {
            Ensure       = 'Present'
            Name         = 'Default Web Site'
            State        = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn    = '[WindowsFeature]IIS'

        }

        # Copy the website content
        File WebContent

        {
            Ensure          = 'Present'
            SourcePath      = $Node.SiteContents
            DestinationPath = $Node.SitePath
            Recurse         = $true
            Type            = 'Directory'
            DependsOn       = '[WindowsFeature]AspNet45'

        }       


        # Create the new Website

        xWebsite NewWebsite

        {

            Ensure          = 'Present'
            Name            = $WebSiteName
            State           = 'Started'
            PhysicalPath    = $Node.SitePath
            DependsOn       = '[File]WebContent'
        }

    }

}

MyWebApp -ConfigurationData DevProdEnvData.psd1
```

## <a name="see-also"></a>См. также
- [Параметры учетных данных в данных конфигурации](configDataCredentials.md)
- [Конфигурации DSC](configurations.md)