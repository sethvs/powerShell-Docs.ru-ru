---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Использование данных конфигурации
ms.openlocfilehash: 19544494a547a06d87701b38585844cb11d03e33
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-configuration-data-in-dsc"></a><span data-ttu-id="6ae8f-103">Использование данных конфигурации в DSC</span><span class="sxs-lookup"><span data-stu-id="6ae8f-103">Using configuration data in DSC</span></span>

><span data-ttu-id="6ae8f-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6ae8f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6ae8f-105">С помощью встроенного параметра DSC **ConfigurationData** можно определить данные, которые будут использоваться в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-105">By using the built-in DSC **ConfigurationData** parameter, you can define data that can be used within a configuration.</span></span>
<span data-ttu-id="6ae8f-106">Это позволяет создать единую конфигурацию, которую можно использовать для нескольких узлов или для различных сред.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-106">This allows you to create a single configuration that can be used for multiple nodes or for different environments.</span></span>
<span data-ttu-id="6ae8f-107">Например, при разработке приложения можно использовать одну и ту же конфигурацию для среды разработки и для рабочей среды и указать данные для каждой среды с помощью данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-107">For example, if you are developing an application, you can use one configuration for both development and production environments, and use configuration data to specify data for each environment.</span></span>

<span data-ttu-id="6ae8f-108">В этом разделе описывается структура хэш-таблицы **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-108">This topic describes the structure of the **ConfigurationData** hashtable.</span></span>
<span data-ttu-id="6ae8f-109">Примеры использования данных конфигурации см. в статье [Разделение данных конфигурации и данных среды](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="6ae8f-109">For examples of how to use configuration data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="the-configurationdata-common-parameter"></a><span data-ttu-id="6ae8f-110">Общий параметр ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="6ae8f-110">The ConfigurationData common parameter</span></span>

<span data-ttu-id="6ae8f-111">Конфигурация DSC принимает общий параметр **ConfigurationData**. Этот параметр указывается при компиляции конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-111">A DSC configuration takes a common parameter, **ConfigurationData**, that you specify when you compile the configuration.</span></span>
<span data-ttu-id="6ae8f-112">Сведения о компиляции конфигураций см. в разделе [Конфигурации DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="6ae8f-112">For information about compiling configurations, see [DSC configurations](configurations.md).</span></span>

<span data-ttu-id="6ae8f-113">Параметр **ConfigurationData** представляет собой хэш-таблицу, в которой должен быть по меньшей мере один ключ с именем **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-113">The **ConfigurationData** parameter is a hasthtable that must have at least one key named **AllNodes**.</span></span>
<span data-ttu-id="6ae8f-114">В ней также может быть один или несколько других ключей.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-114">It can also have one or more other keys.</span></span>

><span data-ttu-id="6ae8f-115">**Примечание.** В примерах в этом разделе используется один дополнительный ключ (кроме названного ключа **AllNodes**) с именем `NonNodeData`, но вы можете включить любое число дополнительных ключей и указать для них любые имена.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-115">**Note:** The examples in this topic use a single additional key (other than the named **AllNodes** key) named `NonNodeData`, but you can include any number of additional keys, and name them whatever you want.</span></span>

```powershell
$MyData =
@{
    AllNodes = @()
    NonNodeData = ""
}
```

<span data-ttu-id="6ae8f-116">Значение ключа **AllNodes** представляет собой массив.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-116">The value of the **AllNodes** key is an array.</span></span> <span data-ttu-id="6ae8f-117">Каждый элемент этого массива также является хэш-таблицей, в которой должен быть по меньшей мере один ключ с именем **AllNodes**:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-117">Each element of this array is also a hash table that must have at least one key named **NodeName**:</span></span>

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

<span data-ttu-id="6ae8f-118">В каждую хэш-таблицу можно добавить и другие ключи:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-118">You can add other keys to each hash table as well:</span></span>

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

<span data-ttu-id="6ae8f-119">Чтобы применить свойство ко всем узлам, можно создать элемент массива **AllNodes**, значение параметра **NodeName** для которого будет равно `*`.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-119">To apply a property to all nodes, you can create a member of the **AllNodes** array that has a **NodeName** of `*`.</span></span>
<span data-ttu-id="6ae8f-120">Например, чтобы присвоить каждому узлу свойство `LogPath`, можно написать следующее:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-120">For example, to give every node a `LogPath` property, you could do this:</span></span>

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

<span data-ttu-id="6ae8f-121">Это аналогично добавлению свойства с именем `LogPath` и значением `"C:\Logs"` в каждый из других блоков (`VM-1`, `VM-2` и `VM-3`).</span><span class="sxs-lookup"><span data-stu-id="6ae8f-121">This is the equivalent of adding a property with a name of `LogPath` with a value of `"C:\Logs"` to each of the other blocks (`VM-1`, `VM-2`, and `VM-3`).</span></span>

## <a name="defining-the-configurationdata-hashtable"></a><span data-ttu-id="6ae8f-122">Определение хэш-таблицы ConfigurationData</span><span class="sxs-lookup"><span data-stu-id="6ae8f-122">Defining the ConfigurationData hashtable</span></span>

<span data-ttu-id="6ae8f-123">Хэш-таблицу **ConfigurationData** можно определить в виде переменной в файле сценария конфигурации (как в наших предыдущих примерах) или в отдельном файле типа `.psd1`.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-123">You can define **ConfigurationData** either as a variable within the same script file as a configuration (as in our previous examples) or in a separate `.psd1` file.</span></span>
<span data-ttu-id="6ae8f-124">Чтобы определить хэш-таблицу **ConfigurationData** в файле типа `.psd1`, создайте файл, который будет содержать только хэш-таблицу, представляющую данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-124">To define **ConfigurationData** in a `.psd1` file, create a file that contains only the hashtable that represents the configuration data.</span></span>

<span data-ttu-id="6ae8f-125">Например, можно создать файл с именем `MyData.psd1` и со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-125">For example, you could create a file named `MyData.psd1` with the following contents:</span></span>

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

## <a name="compiling-a-configuration-with-configuration-data"></a><span data-ttu-id="6ae8f-126">Компиляция конфигурации с помощью данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="6ae8f-126">Compiling a configuration with configuration data</span></span>

<span data-ttu-id="6ae8f-127">Чтобы компилировать конфигурацию с заданными данными, их нужно передать как значение параметра **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-127">To compile a configuration for which you have defined configuration data, you pass the configuration data as the value of the **ConfigurationData** parameter.</span></span>

<span data-ttu-id="6ae8f-128">При этом создается MOF-файл для каждой записи в массиве **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-128">This will create a MOF file for each entry in the **AllNodes** array.</span></span>
<span data-ttu-id="6ae8f-129">Каждый MOF-файл будет назван с использованием свойства `NodeName` соответствующей записи массива.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-129">Each MOF file will be named with the `NodeName` property of the corresponding array entry.</span></span>

<span data-ttu-id="6ae8f-130">Например, если вы определяете данные конфигурации, как в файле `MyData.psd1` выше, при компиляции конфигурации будут созданы файлы `VM-1.mof` и `VM-2.mof`.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-130">For example, if you define configuration data as in the `MyData.psd1` file above, compiling a configuration would create both `VM-1.mof` and `VM-2.mof` files.</span></span>

### <a name="compiling-a-configuration-with-configuration-data-using-a-variable"></a><span data-ttu-id="6ae8f-131">Компиляция конфигурации с помощью данных конфигурации с использованием переменной</span><span class="sxs-lookup"><span data-stu-id="6ae8f-131">Compiling a configuration with configuration data using a variable</span></span>

<span data-ttu-id="6ae8f-132">Чтобы использовать данные конфигурации, определенные в качестве переменной, в том же файле `.ps1`, что и конфигурация, передайте имя переменной в качестве значения параметра **ConfigurationData** при компиляции конфигурации:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-132">To use configuration data that is defined as a variable in the same `.ps1` file as the configuration, you pass the variable name as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData $MyData
```

### <a name="compiling-a-configuration-with-configuration-data-using-a-data-file"></a><span data-ttu-id="6ae8f-133">Компиляция конфигурации с помощью данных конфигурации с использованием файла данных</span><span class="sxs-lookup"><span data-stu-id="6ae8f-133">Compiling a configuration with configuration data using a data file</span></span>

<span data-ttu-id="6ae8f-134">Чтобы использовать данные конфигурации, которая определена в PSD1-файле, передайте путь и имя этого файла в качестве значения параметра **ConfigurationData** при компиляции конфигурации:</span><span class="sxs-lookup"><span data-stu-id="6ae8f-134">To use configuration data that is defined in a .psd1 file, you pass the path and name of that file as the value of the **ConfigurationData** parameter when compiling the configuration:</span></span>

```powershell
MyDscConfiguration -ConfigurationData .\MyData.psd1
```

## <a name="using-configurationdata-variables-in-a-configuration"></a><span data-ttu-id="6ae8f-135">Использование переменных ConfigurationData в конфигурации</span><span class="sxs-lookup"><span data-stu-id="6ae8f-135">Using ConfigurationData variables in a configuration</span></span>

<span data-ttu-id="6ae8f-136">DSC предоставляет три специальные переменные, которые могут использоваться в сценарии конфигурации: **$AllNodes**, **$Node** и **$ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-136">DSC provides three special variables that can be used in a configuration script: **$AllNodes**, **$Node**, and **$ConfigurationData**.</span></span>

- <span data-ttu-id="6ae8f-137">**$AllNodes** относится ко всей коллекции узлов, определенных в **ConfigurationData**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-137">**$AllNodes** refers to the entire collection of nodes defined in **ConfigurationData**.</span></span> <span data-ttu-id="6ae8f-138">Коллекцию **AllNodes** можно отфильтровать с помощью **.Where()** и **.ForEach()**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-138">You can filter the **AllNodes** collection by using **.Where()** and **.ForEach()**.</span></span>
- <span data-ttu-id="6ae8f-139">После фильтрации коллекции с помощью **.Where()** или **.ForEach()** элемент **Node** будет указывать на конкретную запись в **AllNodes**.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-139">**Node** refers to a particular entry in the **AllNodes** collection after it is filtered by using **.Where()** or **.ForEach()**.</span></span>
- <span data-ttu-id="6ae8f-140">**ConfigurationData** ссылается на всю хэш-таблицу, которая передается в качестве параметра при компиляции конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-140">**ConfigurationData** refers to the entire hash table that is passed as the parameter when compiling a configuration.</span></span>

## <a name="using-non-node-data"></a><span data-ttu-id="6ae8f-141">Использование данных, отличных от данных узла</span><span class="sxs-lookup"><span data-stu-id="6ae8f-141">Using non-node data</span></span>

<span data-ttu-id="6ae8f-142">Как видно из предыдущих примеров, хэш-таблица **ConfigurationData** кроме требуемого ключа **AllNodes** может содержать один или несколько ключей.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-142">As we've seen in previous examples, the **ConfigurationData** hashtable can have one or more keys in addition to the required **AllNodes** key.</span></span>
<span data-ttu-id="6ae8f-143">В примерах в этом разделе мы использовали только один дополнительный узел, назвав его `NonNodeData`.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-143">In the examples in this topic, we have used only a single additional node, and named it `NonNodeData`.</span></span>
<span data-ttu-id="6ae8f-144">Но вы можете определить любое число дополнительных ключей и назвать их как угодно.</span><span class="sxs-lookup"><span data-stu-id="6ae8f-144">However, you can define any number of additional keys, and name them anything you want.</span></span>

<span data-ttu-id="6ae8f-145">Пример использования данных, отличных от данных узла, см. в статье [Разделение данных конфигурации и данных среды](separatingEnvData.md).</span><span class="sxs-lookup"><span data-stu-id="6ae8f-145">For an example of using non-node data, see [Separating configuration and environment data](separatingEnvData.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6ae8f-146">См. также</span><span class="sxs-lookup"><span data-stu-id="6ae8f-146">See Also</span></span>
- [<span data-ttu-id="6ae8f-147">Параметры учетных данных в данных конфигурации</span><span class="sxs-lookup"><span data-stu-id="6ae8f-147">Credentials Options in Configuration Data</span></span>](configDataCredentials.md)
- [<span data-ttu-id="6ae8f-148">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="6ae8f-148">DSC Configurations</span></span>](configurations.md)