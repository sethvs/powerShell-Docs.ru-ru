# Разделение данных конфигурации и данных среды

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

Настройка требуемого состояния Windows PowerShell позволяет отделить данные конфигурации от логики конфигурации. Это можно рассматривать как отделение структурной конфигурации (например, конфигурации, которая требует установки IIS) от конфигурации среды (т. е. при существовании тестовой и рабочей среды имена узлов различаются, но к каждому из них применяется одна и та же конфигурация). Подобное разделение обеспечивает следующие преимущества.

* Возможность применения одних и тех же данных конфигурации для различных источников, узлов и конфигураций.
* Логика настройки без жестко прописанных в коде данных более удобна для повторного использования. В этом случае она работает как рекомендации по составлению сценариев для функций.
* Если некоторые данные необходимо изменить, изменения достаточно внести только в одном месте, сэкономив тем самым время и уменьшив вероятность ошибок.

## Базовые концепции и примеры

Для указания на среду как часть конфигурации в DSC используется параметр **ConfigurationData**, который представляет собой хэш-таблицу (или принимает PSD1-файл, содержащий хэш-таблицу). Хэш-таблица должна содержать по меньшей мере один ключ **AllNodes** со структурированными значениями. Например:

```powershell
$MyData = 
@{
    AllNodes = @();
    NonNodeData = ""   
}
```

Обратите внимание на ключ AllNodes, значение которого представляет собой массив. Кроме того, каждый элемент этого массива является хэш-таблицей, для которой ключом служит ключ NodeName:

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

Каждая запись хэш-таблицы в ключе AllNodes соответствует данным конфигурации для узла в конфигурации. Наряду с обязательным ключом NodeName в хэш-таблицу можно добавлять и другие ключи, например:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName = "VM-1";
            Role     = "WebServer"
        },

 
        @{
            NodeName = "VM-2";
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3";
            Role     = "WebServer"
        }
    );

    NonNodeData = ""   
}
```

В DSC есть три специальные переменные для использования в сценарии настройки:

* **$AllNodes**: ссылается на все узлы. Если применить фильтрацию с параметрами **.Where()** и **.ForEach()**, то для выбора узлов VM-1 и VM-3 в приведенном выше примере можно не прописывать их имена в коде, а написать следующее:

```powershell
configuration MyConfiguration
{
    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
    }
}
```

* **$Node**: отфильтровав набор узлов, можно сослаться на определенную запись с помощью переменной $Node. Например:

```powershell
configuration MyConfiguration
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite
    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = "Present"
        }
    }
}
```

Чтобы применить свойство ко всем узлам, используйте запись NodeName = “*”. Например, чтобы присвоить свойство LogPath каждому узлу, можно написать следующее:

```
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = "*"
            LogPath            = "C:\Logs"
        },

 
        @{
            NodeName = "VM-1";
            Role     = "WebServer"
            SiteContents = "C:\Site1"
            SiteName = "Website1"
        },

 
        @{
            NodeName = "VM-2";
            Role     = "SQLServer"
        },

 
        @{
            NodeName = "VM-3";
            Role     = "WebServer";
            SiteContents = "C:\Site2"
            SiteName = "Website3"
        }
    );
}
```

* **$ConfigurationData**: эта переменная используется в конфигурации для доступа к хэш-таблице данных конфигурации, передаваемой в виде параметра. Например:

```powershell
$MyData = 
@{
    AllNodes = 
    @(
        @{
            NodeName           = "*"
            LogPath            = "C:\Logs"
        },

 
        @{
            NodeName = "VM-1";
            Role     = "WebServer"
            SiteContents = "C:\Site1"
            SiteName = "Website1"
        },

 
        @{
            NodeName = "VM-2";
            Role     = "SQLServer"
        },
 

        @{
            NodeName = "VM-3";
            Role     = "WebServer";
            SiteContents = "C:\Site2"
            SiteName = "Website3"
        }
    );

    NonNodeData = 
    @{
        ConfigFileContents = (Get-Content C:\Template\Config.xml)
     }   
} 

configuration MyConfiguration
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name         = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure       = "Present"
        }

        File ConfigFile
        {
            DestinationPath = $Node.SiteContents + "\\config.xml"
            Contents = $ConfigurationData.NonNodeData.ConfigFileContents
        }
    }
}
```

Полный пример входит в [модуль xWebAdministration](https://powershellgallery.com/packages/xWebAdministration).
<!--HONumber=Feb16_HO4-->
