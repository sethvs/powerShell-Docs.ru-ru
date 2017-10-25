---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Разделение данных конфигурации и данных среды"
ms.openlocfilehash: df3cfea08419c37716b408fdbd6b43e78be2331c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="separating-configuration-and-environment-data"></a>Разделение данных конфигурации и данных среды

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Отделение данных, используемых в конфигурации DSC, от самой конфигурации с помощью данных конфигурации может быть полезным.
Это позволит использовать одну конфигурацию для нескольких сред.

Например, при разработке приложения можно использовать одну и ту же конфигурацию для среды разработки и для рабочей среды и указать данные для каждой среды с помощью данных конфигурации.

## <a name="what-is-configuration-data"></a>Что такое данные конфигурации?

Данные конфигурации — это данные, определяемые в хэш-таблице и передаваемые в конфигурацию DSC в процессе ее компиляции.

Подробное описание хэш-таблицы **ConfigurationData** см. в статье об [использовании данных конфигурации](configData.md).

## <a name="a-simple-example"></a>Простой пример

Чтобы увидеть, как это работает, рассмотрим очень простой пример. Мы создадим одну конфигурацию, в соответствии с которой на некоторых узлах будет находиться **IIS**, а на других узлах — **Hyper-V**: 

```powershell
Configuration MyDscConfiguration {
    
    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        WindowsFeature IISInstall {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
        
    }
    Node $AllNodes.Where{$_.Role -eq "VMHost"}.NodeName
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
        },

        @{
            NodeName    = 'VM-2'
            Role = 'VMHost'
        }
    )
}

MyDscConfiguration -ConfigurationData $MyData
```

В последней строке этого сценария выполняется компиляция конфигурации. Для этого в качестве значения параметра **ConfigurationData** передается `$MyData`.

В результате этого создаются два MOF-файла:

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
-a----        3/31/2017   5:09 PM           1968 VM-1.mof                                                                                                                
-a----        3/31/2017   5:09 PM           1970 VM-2.mof  
```
 
`$MyData` указывает два разных узла, каждый из которых имеет свои собственные `NodeName` и `Role`. В конфигурации динамически создаются блоки **Node** с помощью фильтрации коллекции узлов, полученной от `$MyData` (в частности, `$AllNodes`), по свойству `Role`.

## <a name="using-configuration-data-to-define-development-and-production-environments"></a>Использование данных конфигурации для определения среды разработки и рабочей среды

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
        },

        @{
            NodeName         = "Dev"
            Role             = "MSSQL", "Web"
            SiteContents     = "C:\Website\Dev\SiteContents\"
            SitePath         = "\\Dev\Website\"
        }
    )
}
```

### <a name="configuration-script-file"></a>Файл сценария конфигурации

Теперь в конфигурации, определенной в файле `.ps1`, отфильтруем узлы, определенные в файле `DevProdEnvData.psd1`, по их роли (`MSSQL`, `Dev` или и то и другое) и настроим их соответствующим образом. В среде разработки службы IIS и SQL Server установлены на одном узле, а в рабочей среде на двух различных узлах. Содержимое сайта также различно, как указано в свойствах `SiteContents`.

В конце сценария конфигурации мы вызываем конфигурацию (компилируем ее в документ MOF), передав `DevProdEnvData.psd1` в качестве параметра `$ConfigurationData`.

>**Примечание**. Эта конфигурация требует, чтобы модули `xSqlPs` и `xWebAdministration` были установлены на целевом узле.

Давайте определим конфигурацию в файле с именем `MyWebApp.ps1`:

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs
    Import-DscResource -Module xWebAdministration

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

   Node $AllNodes.Where{$_.Role -contains "Web"}.NodeName
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

При запуске этой конфигурации создаются три MOF-файла (по одному для каждой именованной записи в массиве **AllNodes**):

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof                                                                                                            
-a----        3/31/2017   5:47 PM           6994 Dev.mof                                                                                                                 
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a>Использование данных, отличных от данных узла

Можно добавить дополнительные ключи в хэш-таблицу **ConfigurationData** для данных, не относящихся к узлу.
Следующая конфигурация обеспечивает наличие двух веб-сайтов.
Данные для каждого веб-сайта определяются в массиве **AllNodes**.
Файл `Config.xml` используется для обоих веб-сайтов, поэтому мы определим его в дополнительном ключе с именем `NonNodeData`.
Обратите внимание, что можно создавать столько дополнительных ключей, сколько потребуется, и присваивать им любые имена.
`NonNodeData` не является зарезервированным словом — это просто выбранное нами имя для дополнительного ключа.

Доступ к дополнительным ключам можно получить с помощью специальной переменной **$ConfigurationData**.
В этом примере доступ к `ConfigFileContents` осуществляется с помощью строки
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 в блоке ресурса `File`.


```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = “*”
            LogPath            = “C:\Logs”
        },
 
        @{
            NodeName = “VM-1”
            SiteContents = “C:\Site1”
            SiteName = “Website1”
        },
 
        
        @{
            NodeName = “VM-2”;
            SiteContents = “C:\Site2”
            SiteName = “Website2”
        }
    );
 
    NonNodeData = 
    @{
        ConfigFileContents = (Get-Content C:\Template\Config.xml)
     }   
} 
 
configuration WebsiteConfig
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite
 
    node $AllNodes.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = “Present”
        }
 
        File ConfigFile
        {
            DestinationPath = $Node.SiteContents + “\\config.xml”
            Contents = $ConfigurationData.NonNodeData.ConfigFileContents
        }
    }
} 
```


## <a name="see-also"></a>См. также
- [Использование данных конфигурации](configData.md)
- [Параметры учетных данных в данных конфигурации](configDataCredentials.md)
- [Конфигурации DSC](configurations.md)

