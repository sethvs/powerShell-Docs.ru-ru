---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Разделение данных конфигурации и данных среды
ms.openlocfilehash: c89e26105611eae59a926be1432079913c40671f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="separating-configuration-and-environment-data"></a><span data-ttu-id="e165b-103">Разделение данных конфигурации и данных среды</span><span class="sxs-lookup"><span data-stu-id="e165b-103">Separating configuration and environment data</span></span>

><span data-ttu-id="e165b-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e165b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e165b-105">Отделение данных, используемых в конфигурации DSC, от самой конфигурации с помощью данных конфигурации может быть полезным.</span><span class="sxs-lookup"><span data-stu-id="e165b-105">It can be useful to separate the data used in a DSC configuration from the configuration itself by using configuration data.</span></span>
<span data-ttu-id="e165b-106">Это позволит использовать одну конфигурацию для нескольких сред.</span><span class="sxs-lookup"><span data-stu-id="e165b-106">By doing this, you can use a single configuration for multiple environments.</span></span>

<span data-ttu-id="e165b-107">Например, при разработке приложения можно использовать одну и ту же конфигурацию для среды разработки и для рабочей среды и указать данные для каждой среды с помощью данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e165b-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

## <a name="what-is-configuration-data"></a><span data-ttu-id="e165b-108">Что такое данные конфигурации?</span><span class="sxs-lookup"><span data-stu-id="e165b-108">What is configuration data?</span></span>

<span data-ttu-id="e165b-109">Данные конфигурации — это данные, определяемые в хэш-таблице и передаваемые в конфигурацию DSC в процессе ее компиляции.</span><span class="sxs-lookup"><span data-stu-id="e165b-109">Configuration data is data that is defined in a hashtable and passed to a DSC configuration when you compile that configuration.</span></span>

<span data-ttu-id="e165b-110">Подробное описание хэш-таблицы **ConfigurationData** см. в статье об [использовании данных конфигурации](configData.md).</span><span class="sxs-lookup"><span data-stu-id="e165b-110">For a detailed description of the **ConfigurationData** hashtable, see [Using configuration data](configData.md).</span></span>

## <a name="a-simple-example"></a><span data-ttu-id="e165b-111">Простой пример</span><span class="sxs-lookup"><span data-stu-id="e165b-111">A simple example</span></span>

<span data-ttu-id="e165b-112">Чтобы увидеть, как это работает, рассмотрим очень простой пример.</span><span class="sxs-lookup"><span data-stu-id="e165b-112">Let's look at a very simple example to see how this works.</span></span>
<span data-ttu-id="e165b-113">Мы создадим одну конфигурацию, в соответствии с которой на некоторых узлах будет находиться **IIS**, а на других узлах — **Hyper-V**:</span><span class="sxs-lookup"><span data-stu-id="e165b-113">We'll create a single configuration that ensures that **IIS** is present on some nodes, and that **Hyper-V** is present on others:</span></span>

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

<span data-ttu-id="e165b-114">В последней строке этого сценария выполняется компиляция конфигурации. Для этого в качестве значения параметра **ConfigurationData** передается `$MyData`.</span><span class="sxs-lookup"><span data-stu-id="e165b-114">The last line in this script compiles the configuration, passing `$MyData` as the value **ConfigurationData** parameter.</span></span>

<span data-ttu-id="e165b-115">В результате этого создаются два MOF-файла:</span><span class="sxs-lookup"><span data-stu-id="e165b-115">The result is that two MOF files are created:</span></span>

```
    Directory: C:\DscTests\MyDscConfiguration


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:09 PM           1968 VM-1.mof
-a----        3/31/2017   5:09 PM           1970 VM-2.mof
```

<span data-ttu-id="e165b-116">`$MyData` указывает два разных узла, каждый из которых имеет свои собственные `NodeName` и `Role`.</span><span class="sxs-lookup"><span data-stu-id="e165b-116">`$MyData` specifies two different nodes, each with its own `NodeName` and `Role`.</span></span> <span data-ttu-id="e165b-117">В конфигурации динамически создаются блоки **Node** с помощью фильтрации коллекции узлов, полученной от `$MyData` (в частности, `$AllNodes`), по свойству `Role`.</span><span class="sxs-lookup"><span data-stu-id="e165b-117">The configuration dynamically creates **Node** blocks by taking the collection of nodes it gets from `$MyData` (specifically, `$AllNodes`) and filters that collection against the `Role` property..</span></span>

## <a name="using-configuration-data-to-define-development-and-production-environments"></a><span data-ttu-id="e165b-118">Использование данных конфигурации для определения среды разработки и рабочей среды</span><span class="sxs-lookup"><span data-stu-id="e165b-118">Using configuration data to define development and production environments</span></span>

<span data-ttu-id="e165b-119">Рассмотрим полный пример использования одной и той же конфигурации для настройки среды разработки и рабочей среды веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="e165b-119">Let's look at a complete example that uses a single configuration to set up both development and production environments of a website.</span></span> <span data-ttu-id="e165b-120">В среде разработки службы IIS и SQL Server устанавливаются на одних и тех же узлах.</span><span class="sxs-lookup"><span data-stu-id="e165b-120">In the development environment, both IIS and SQL Server are installed on a single nodes.</span></span> <span data-ttu-id="e165b-121">В рабочей среде службы IIS и SQL Server устанавливаются на отдельных узлах.</span><span class="sxs-lookup"><span data-stu-id="e165b-121">In the production environment, IIS and SQL Server are installed on separate nodes.</span></span> <span data-ttu-id="e165b-122">Для указания данных конфигурации для двух различных сред мы будем использовать PSD1-файл данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e165b-122">We'll use a configuration data .psd1 file to specify the data for the two different environments.</span></span>

 ### <a name="configuration-data-file"></a><span data-ttu-id="e165b-123">Файл данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="e165b-123">Configuration data file</span></span>

<span data-ttu-id="e165b-124">Данные среды разработки и рабочей среды определяются в файле `DevProdEnvData.psd1` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e165b-124">We'll define the development and production environment data in a file namd `DevProdEnvData.psd1` as follows:</span></span>

```powershell
@{

    AllNodes = @(

        @{
            NodeName        = "*"
            SQLServerName   = "MySQLServer"
            SqlSource       = "C:\Software\Sql"
            DotNetSrc       = "C:\Software\sxs"
        WebSiteName     = "New website"
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

### <a name="configuration-script-file"></a><span data-ttu-id="e165b-125">Файл сценария конфигурации</span><span class="sxs-lookup"><span data-stu-id="e165b-125">Configuration script file</span></span>

<span data-ttu-id="e165b-126">Теперь в конфигурации, определенной в файле `.ps1`, отфильтруем узлы, определенные в файле `DevProdEnvData.psd1`, по их роли (`MSSQL`, `Dev` или и то и другое) и настроим их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e165b-126">Now, in the configuration, which is defined in a `.ps1` file, we filter the nodes we defined in `DevProdEnvData.psd1` by their role (`MSSQL`, `Dev`, or both), and configure them accordingly.</span></span>
<span data-ttu-id="e165b-127">В среде разработки службы IIS и SQL Server установлены на одном узле, а в рабочей среде на двух различных узлах.</span><span class="sxs-lookup"><span data-stu-id="e165b-127">The development environment has both the SQL Server and IIS on one node, while the production environment has them on two different nodes.</span></span>
<span data-ttu-id="e165b-128">Содержимое сайта также различно, как указано в свойствах `SiteContents`.</span><span class="sxs-lookup"><span data-stu-id="e165b-128">The site contents is also different, as specified by the `SiteContents` properties.</span></span>

<span data-ttu-id="e165b-129">В конце сценария конфигурации мы вызываем конфигурацию (компилируем ее в документ MOF), передав `DevProdEnvData.psd1` в качестве параметра `$ConfigurationData`.</span><span class="sxs-lookup"><span data-stu-id="e165b-129">At the end of the configuration script, we call the configuration (compile it into a MOF document), passing `DevProdEnvData.psd1` as the `$ConfigurationData` parameter.</span></span>

><span data-ttu-id="e165b-130">**Примечание**. Эта конфигурация требует, чтобы модули `xSqlPs` и `xWebAdministration` были установлены на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="e165b-130">**Note:** This configuration requires the modules `xSqlPs` and `xWebAdministration` to be installed on the target node.</span></span>

<span data-ttu-id="e165b-131">Давайте определим конфигурацию в файле с именем `MyWebApp.ps1`:</span><span class="sxs-lookup"><span data-stu-id="e165b-131">Let's define the configuration in a file named `MyWebApp.ps1`:</span></span>

```powershell
Configuration MyWebApp
{
    Import-DscResource -Module PSDesiredStateConfiguration
    Import-DscResource -Module xSqlPs
    Import-DscResource -Module xWebAdministration

    Node $AllNodes.Where{$_.Role -contains "MSSQL"}.NodeName
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
            Name            = $Node.WebSiteName
            State           = 'Started'
            PhysicalPath    = $Node.SitePath
            DependsOn       = '[File]WebContent'
        }

    }

}

MyWebApp -ConfigurationData DevProdEnvData.psd1
```

<span data-ttu-id="e165b-132">При запуске этой конфигурации создаются три MOF-файла (по одному для каждой именованной записи в массиве **AllNodes**):</span><span class="sxs-lookup"><span data-stu-id="e165b-132">When you run this configuration, three MOF files are created (one for each named entry in the **AllNodes** array):</span></span>

```
    Directory: C:\DscTests\MyWebApp


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/31/2017   5:47 PM           2944 Prod-SQL.mof
-a----        3/31/2017   5:47 PM           6994 Dev.mof
-a----        3/31/2017   5:47 PM           5338 Prod-IIS.mof
```

## <a name="using-non-node-data"></a><span data-ttu-id="e165b-133">Использование данных, отличных от данных узла</span><span class="sxs-lookup"><span data-stu-id="e165b-133">Using non-node data</span></span>

<span data-ttu-id="e165b-134">Можно добавить дополнительные ключи в хэш-таблицу **ConfigurationData** для данных, не относящихся к узлу.</span><span class="sxs-lookup"><span data-stu-id="e165b-134">You can add additional keys to the **ConfigurationData** hashtable for data that is not specific to a node.</span></span>
<span data-ttu-id="e165b-135">Следующая конфигурация обеспечивает наличие двух веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="e165b-135">The following configuration ensures the presence of two websites.</span></span>
<span data-ttu-id="e165b-136">Данные для каждого веб-сайта определяются в массиве **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="e165b-136">Data for each website are defined in the **AllNodes** array.</span></span>
<span data-ttu-id="e165b-137">Файл `Config.xml` используется для обоих веб-сайтов, поэтому мы определим его в дополнительном ключе с именем `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="e165b-137">The file `Config.xml` is used for both websites, so we define it in an additional key with the name `NonNodeData`.</span></span>
<span data-ttu-id="e165b-138">Обратите внимание, что можно создавать столько дополнительных ключей, сколько потребуется, и присваивать им любые имена.</span><span class="sxs-lookup"><span data-stu-id="e165b-138">Note that you can have as many additional keys as you want, and you can name them anything you want.</span></span>
<span data-ttu-id="e165b-139">`NonNodeData` не является зарезервированным словом — это просто выбранное нами имя для дополнительного ключа.</span><span class="sxs-lookup"><span data-stu-id="e165b-139">`NonNodeData` is not a reserved word, it is just what we decided to name the additional key.</span></span>

<span data-ttu-id="e165b-140">Доступ к дополнительным ключам можно получить с помощью специальной переменной **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="e165b-140">You access additional keys by using the special variable **$ConfigurationData**.</span></span>
<span data-ttu-id="e165b-141">В этом примере доступ к `ConfigFileContents` осуществляется с помощью строки</span><span class="sxs-lookup"><span data-stu-id="e165b-141">In this example, `ConfigFileContents` is accessed with the line:</span></span>
```powershell
 Contents = $ConfigurationData.NonNodeData.ConfigFileContents
 ```
 <span data-ttu-id="e165b-142">в блоке ресурса `File`.</span><span class="sxs-lookup"><span data-stu-id="e165b-142">in the `File` resource block.</span></span>


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


## <a name="see-also"></a><span data-ttu-id="e165b-143">См. также</span><span class="sxs-lookup"><span data-stu-id="e165b-143">See Also</span></span>
- [<span data-ttu-id="e165b-144">Использование данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="e165b-144">Using configuration data</span></span>](configData.md)
- [<span data-ttu-id="e165b-145">Параметры учетных данных в данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="e165b-145">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="e165b-146">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="e165b-146">DSC Configurations</span></span>](configurations.md)