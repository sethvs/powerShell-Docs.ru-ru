---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Использование данных конфигурации"
ms.openlocfilehash: 60c6c2d5694a03275e1a08522bdcf4b1bc5bb068
ms.sourcegitcommit: 60f06a06c2fce63024f3f4cbd7657b1dfe7fcb1a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2018
---
# <a name="using-configuration-data-in-dsc"></a>Использование данных конфигурации в DSC

>Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0

С помощью встроенного параметра DSC **ConfigurationData** можно определить данные, которые будут использоваться в конфигурации. Это позволяет создать единую конфигурацию, которую можно использовать для нескольких узлов или для различных сред. Например, при разработке приложения можно использовать одну и ту же конфигурацию для среды разработки и для рабочей среды и указать данные для каждой среды с помощью данных конфигурации.

В этом разделе описывается структура хэш-таблицы **ConfigurationData**. Примеры использования данных конфигурации см. в статье [Разделение данных конфигурации и данных среды](separatingEnvData.md).

## <a name="the-configurationdata-common-parameter"></a>Общий параметр ConfigurationData

Конфигурация DSC принимает общий параметр **ConfigurationData**. Этот параметр указывается при компиляции конфигурации. Сведения о компиляции конфигураций см. в разделе [Конфигурации DSC](configurations.md).

Параметр **ConfigurationData** представляет собой хэш-таблицу, в которой должен быть по меньшей мере один ключ с именем **AllNodes**. В ней также может быть один или несколько других ключей.

>**Примечание.** В примерах в этом разделе используется один дополнительный ключ (кроме названного ключа **AllNodes**) с именем `NonNodeData`, но вы можете включить любое число дополнительных ключей и указать для них любые имена.

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

Хэш-таблицу **ConfigurationData** можно определить в виде переменной в файле сценария конфигурации (как в наших предыдущих примерах) или в отдельном файле типа `.psd1`. Чтобы определить хэш-таблицу **ConfigurationData** в файле типа `.psd1`, создайте файл, который будет содержать только хэш-таблицу, представляющую данные конфигурации.

Например, можно создать файл с именем `MyData.psd1` и со следующим содержимым:

```powershell
@{
    AllNodes =
    @(
        @{
            NodeName    = 'VM-1'
            FeatureName = 'Web-Server'
        },

        @{
            NodeName    = 'VM-2'
            FeatureName = 'Hyper-V'
        }
    )
}
```

## <a name="compiling-a-configuration-with-configuration-data"></a>Компиляция конфигурации с помощью данных конфигурации

Чтобы компилировать конфигурацию с заданными данными, их нужно передать как значение параметра **ConfigurationData**.

При этом создается MOF-файл для каждой записи в массиве **AllNodes**.
Каждый MOF-файл будет назван с использованием свойства `NodeName` соответствующей записи массива.

Например, если вы определяете данные конфигурации, как в файле `MyData.psd1` выше, при компиляции конфигурации будут созданы файлы `VM-1.mof` и `VM-2.mof`.

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a>Компиляция конфигурации с помощью данных конфигурации с использованием переменной

Чтобы использовать данные конфигурации, определенные в качестве переменной, в том же файле `.ps1`, что и конфигурация, передайте имя переменной в качестве значения параметра **ConfigurationData** при компиляции конфигурации:

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a>Компиляция конфигурации с помощью данных конфигурации с использованием файла данных

Чтобы использовать данные конфигурации, которая определена в PSD1-файле, передайте путь и имя этого файла в качестве значения параметра **ConfigurationData** при компиляции конфигурации:

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a>Использование переменных ConfigurationData в конфигурации

DSC предоставляет три специальные переменные, которые могут использоваться в сценарии конфигурации: **$AllNodes**, **$Node** и **$ConfigurationData**.

- **$AllNodes** относится ко всей коллекции узлов, определенных в **ConfigurationData**. Коллекцию **AllNodes** можно отфильтровать с помощью **.Where()** и **.ForEach()**.
- После фильтрации коллекции с помощью **.Where()** или **.ForEach()** элемент **Node** будет указывать на конкретную запись в **AllNodes**.
- **ConfigurationData** ссылается на всю хэш-таблицу, которая передается в качестве параметра при компиляции конфигурации.

## <a name="using-non-node-data"></a>Использование данных, отличных от данных узла

Как видно из предыдущих примеров, хэш-таблица **ConfigurationData** кроме требуемого ключа **AllNodes** может содержать один или несколько ключей.
В примерах в этом разделе мы использовали только один дополнительный узел, назвав его `NonNodeData`. Но вы можете определить любое число дополнительных ключей и назвать их как угодно.

Пример использования данных, отличных от данных узла, см. в статье [Разделение данных конфигурации и данных среды](separatingEnvData.md).

## <a name="see-also"></a>См. также
- [Параметры учетных данных в данных конфигурации](configDataCredentials.md)
- [Конфигурации DSC](configurations.md)

