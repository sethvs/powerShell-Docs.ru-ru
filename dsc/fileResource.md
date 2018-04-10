---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс File в DSC
ms.openlocfilehash: 7964eabe5f4585600ae80f3e5ff7439c0d954769
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-file-resource"></a><span data-ttu-id="5fc0e-103">Ресурс File в DSC</span><span class="sxs-lookup"><span data-stu-id="5fc0e-103">DSC File Resource</span></span>

> <span data-ttu-id="5fc0e-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5fc0e-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="5fc0e-105">Ресурс File в DSC Windows PowerShell предоставляет механизм управления файлами и папками на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-105">The File resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and folders on the target node.</span></span>

><span data-ttu-id="5fc0e-106">**Примечание**. Если свойство **MatchSource** имеет значение **$false** (значение по умолчанию), копируемое содержимое будет кэшироваться при первом применении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-106">**Note:** If the **MatchSource** property is set to **$false** (which is the default value), the contents to be copied are cached the first time the configuration is applied.</span></span>
><span data-ttu-id="5fc0e-107">При последующем применении конфигурации файлы и папки в пути, указанном в параметре **SourcePath**, не будут проверяться на наличие обновлений.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-107">Subsequent applications of the configuration will not check for updated files and/or folders in the path specified by **SourcePath**.</span></span> <span data-ttu-id="5fc0e-108">Если вы хотите, чтобы файлы и папки в **SourcePath** проверялись на наличие обновлений при каждом применении конфигурации, установите для свойства **MatchSource** значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-108">If you want to check for updates to the files and/or folders in **SourcePath** every time the configuration is applied, set **MatchSource** to **$true**.</span></span>

## <a name="syntax"></a><span data-ttu-id="5fc0e-109">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="5fc0e-109">Syntax</span></span>
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ]
    [ MatchSource = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="5fc0e-110">Свойства</span><span class="sxs-lookup"><span data-stu-id="5fc0e-110">Properties</span></span>

|  <span data-ttu-id="5fc0e-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="5fc0e-111">Property</span></span>  |  <span data-ttu-id="5fc0e-112">Описание</span><span class="sxs-lookup"><span data-stu-id="5fc0e-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="5fc0e-113">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="5fc0e-113">DestinationPath</span></span>| <span data-ttu-id="5fc0e-114">Указывает, в каком расположении нужно проверить состояние файла или каталога.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-114">Indicates the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="5fc0e-115">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="5fc0e-115">Attributes</span></span>| <span data-ttu-id="5fc0e-116">Указывает требуемое состояние атрибутов для целевого файла или папки.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-116">Specifies the desired state of the attributes for the targeted file or directory.</span></span>|
| <span data-ttu-id="5fc0e-117">Контрольная сумма</span><span class="sxs-lookup"><span data-stu-id="5fc0e-117">Checksum</span></span>| <span data-ttu-id="5fc0e-118">Указывает тип контрольной суммы для использования при проверке двух файлов на идентичность.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-118">Indicates the checksum type to use when determining whether two files are the same.</span></span> <span data-ttu-id="5fc0e-119">Если свойство __Checksum__ не задано, для сравнения используется только имя файла или каталога.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-119">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="5fc0e-120">Допустимые значения: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-120">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span></span>|
| <span data-ttu-id="5fc0e-121">Содержимое</span><span class="sxs-lookup"><span data-stu-id="5fc0e-121">Contents</span></span>| <span data-ttu-id="5fc0e-122">Указывает содержимое файла, например определенную строку.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-122">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="5fc0e-123">Учетные данные</span><span class="sxs-lookup"><span data-stu-id="5fc0e-123">Credential</span></span>| <span data-ttu-id="5fc0e-124">Указывает учетные данные, необходимые для доступа к ресурсам (например, к исходным файлам), если такой доступ является обязательным.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-124">Indicates the credentials that are required to access resources, such as source files, if such access is required.</span></span>|
| <span data-ttu-id="5fc0e-125">Ensure</span><span class="sxs-lookup"><span data-stu-id="5fc0e-125">Ensure</span></span>| <span data-ttu-id="5fc0e-126">Указывает, существует ли файл или каталог.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-126">Indicates if the file or directory exists.</span></span> <span data-ttu-id="5fc0e-127">Чтобы убедиться, что файл или каталог не существует, укажите для этого свойства значение Absent.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-127">Set this property to "Absent" to ensure that the file or directory does not exist.</span></span> <span data-ttu-id="5fc0e-128">Чтобы убедиться, что файл или каталог существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-128">Set it to "Present" to ensure that the file or directory does exist.</span></span> <span data-ttu-id="5fc0e-129">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-129">The default is "Present".</span></span>|
| <span data-ttu-id="5fc0e-130">Force</span><span class="sxs-lookup"><span data-stu-id="5fc0e-130">Force</span></span>| <span data-ttu-id="5fc0e-131">Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-131">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="5fc0e-132">Свойство Force позволяет переопределять такие ошибки.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-132">Using the Force property overrides such errors.</span></span> <span data-ttu-id="5fc0e-133">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-133">The default value is __$false__.</span></span>|
| <span data-ttu-id="5fc0e-134">Recurse</span><span class="sxs-lookup"><span data-stu-id="5fc0e-134">Recurse</span></span>| <span data-ttu-id="5fc0e-135">Указывает, используются ли вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-135">Indicates if subdirectories are included.</span></span> <span data-ttu-id="5fc0e-136">Если свойство имеет значение __$true__, вложенные папки включаются.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-136">Set this property to __$true__ to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="5fc0e-137">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-137">The default is __$false__.</span></span> <span data-ttu-id="5fc0e-138">**Примечание**. Это свойство можно использовать только в том случае, если свойство Type имеет значение Directory.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-138">**Note**: This property is only valid when the Type property is set to Directory.</span></span>|
| <span data-ttu-id="5fc0e-139">DependsOn</span><span class="sxs-lookup"><span data-stu-id="5fc0e-139">DependsOn</span></span> | <span data-ttu-id="5fc0e-140">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5fc0e-141">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-141">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="5fc0e-142">SourcePath</span><span class="sxs-lookup"><span data-stu-id="5fc0e-142">SourcePath</span></span>| <span data-ttu-id="5fc0e-143">Указывает, откуда нужно скопировать файл или папку.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-143">Indicates the path from which to copy the file or folder resource.</span></span>|
| <span data-ttu-id="5fc0e-144">Type</span><span class="sxs-lookup"><span data-stu-id="5fc0e-144">Type</span></span>| <span data-ttu-id="5fc0e-145">Указывает, является ли настраиваемый ресурс каталогом или файлом.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-145">Indicates if the resource being configured is a directory or a file.</span></span> <span data-ttu-id="5fc0e-146">Если выбрано значение Directory, то ресурс является каталогом,</span><span class="sxs-lookup"><span data-stu-id="5fc0e-146">Set this property to "Directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="5fc0e-147">а если значение File, то файлом.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-147">Set it to "File" to indicate that the resource is a file.</span></span> <span data-ttu-id="5fc0e-148">Значение по умолчанию — File.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-148">The default value is “File”.</span></span>|
| <span data-ttu-id="5fc0e-149">MatchSource</span><span class="sxs-lookup"><span data-stu-id="5fc0e-149">MatchSource</span></span>| <span data-ttu-id="5fc0e-150">Если используется значение по умолчанию __$false__, все файлы в источнике (например, файлы A, B и C) добавляются в папку назначения при первом применении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-150">If set to the default value of __$false__, then any files on the source (say, files A, B, and C) will be added to the destination the first time the configuration is applied.</span></span> <span data-ttu-id="5fc0e-151">Если в источник добавляется новый файл (D), он не будет добавлен в папку назначения даже при последующем повторном применении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-151">If a new file (D) is added to the source, it will not be added to the destination, even when the configuration is re-applied later.</span></span> <span data-ttu-id="5fc0e-152">Если используется значение __$true__, при каждом применении конфигурации в папку назначения будут добавляться все найденные новые файлы (в нашем примере это файл D).</span><span class="sxs-lookup"><span data-stu-id="5fc0e-152">If the value is __$true__, then each time the configuration is applied, new files subsequently found on the source (such as file D in this example) are added to the destination.</span></span> <span data-ttu-id="5fc0e-153">Значение по умолчанию — **$false**.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-153">The default value is **$false**.</span></span>|

## <a name="example"></a><span data-ttu-id="5fc0e-154">Пример</span><span class="sxs-lookup"><span data-stu-id="5fc0e-154">Example</span></span>

<span data-ttu-id="5fc0e-155">В представленном ниже примере показано, как использовать ресурс файла, чтобы проверить наличие каталога `C:\Users\Public\Documents\DSCDemo\DemoSource` (вместе со всеми подкаталогами) с исходного компьютера (например, опрашивающего сервера) на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-155">The following example shows how to use the File resource to ensure that a directory with the path `C:\Users\Public\Documents\DSCDemo\DemoSource` on a source computer (such as the “pull” server) is also present (along with all subdirectories) on the target node.</span></span> <span data-ttu-id="5fc0e-156">Кроме того, по завершении настройки в журнал записывается сообщение и указывается оператор, гарантирующий запуск операции проверки файла перед операцией записи в журнал.</span><span class="sxs-lookup"><span data-stu-id="5fc0e-156">It also writes a confirmatory message to the log when complete and includes a statement to ensure that the file-checking operation runs prior to the logging operation.</span></span>

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```