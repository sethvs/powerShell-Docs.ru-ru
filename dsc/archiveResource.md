---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Archive в DSC
ms.openlocfilehash: 1accd48f3862ee09b88d2792f9b7e5a7324bcf17
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-archive-resource"></a><span data-ttu-id="97fab-103">Ресурс Archive в DSC</span><span class="sxs-lookup"><span data-stu-id="97fab-103">DSC Archive Resource</span></span>

> <span data-ttu-id="97fab-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="97fab-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="97fab-105">Ресурс Archive в DSC Windows PowerShell предоставляет механизм распаковки файлов архивов (ZIP) в указанную папку.</span><span class="sxs-lookup"><span data-stu-id="97fab-105">The Archive resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.zip) files at a specific path.</span></span>

## <a name="syntax"></a><span data-ttu-id="97fab-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="97fab-106">Syntax</span></span>
```MOF
Archive [string] #ResourceName
{
    Destination = [string]
    Path = [string]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Validate = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="97fab-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="97fab-107">Properties</span></span>

|  <span data-ttu-id="97fab-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="97fab-108">Property</span></span>  |  <span data-ttu-id="97fab-109">Описание</span><span class="sxs-lookup"><span data-stu-id="97fab-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="97fab-110">Destination</span><span class="sxs-lookup"><span data-stu-id="97fab-110">Destination</span></span>| <span data-ttu-id="97fab-111">Указывает, куда будет извлечено содержимое архива.</span><span class="sxs-lookup"><span data-stu-id="97fab-111">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="97fab-112">путь</span><span class="sxs-lookup"><span data-stu-id="97fab-112">Path</span></span>| <span data-ttu-id="97fab-113">Указывает исходный путь для файла архива.</span><span class="sxs-lookup"><span data-stu-id="97fab-113">Specifies the source path of the archive file.</span></span>|
| <span data-ttu-id="97fab-114">__Контрольная сумма__</span><span class="sxs-lookup"><span data-stu-id="97fab-114">__Checksum__</span></span>| <span data-ttu-id="97fab-115">Определяет тип проверки пары файлов на идентичность.</span><span class="sxs-lookup"><span data-stu-id="97fab-115">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="97fab-116">Если свойство __Checksum__ не задано, для сравнения используется только имя файла или каталога.</span><span class="sxs-lookup"><span data-stu-id="97fab-116">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="97fab-117">Допустимые значения: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="97fab-117">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate, none (default).</span></span> <span data-ttu-id="97fab-118">Если свойство __Checksum__ указано без свойства __Validate__, возникает ошибка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97fab-118">If you specify __Checksum__ without __Validate__, the configuration will fail.</span></span>|
| <span data-ttu-id="97fab-119">Ensure</span><span class="sxs-lookup"><span data-stu-id="97fab-119">Ensure</span></span>| <span data-ttu-id="97fab-120">Указывает необходимость проверки того, существует ли содержимое архива в __папке назначения__.</span><span class="sxs-lookup"><span data-stu-id="97fab-120">Determines whether to check if the content of the archive exists at the __Destination__.</span></span> <span data-ttu-id="97fab-121">Чтобы убедиться, что содержимое существует, укажите для этого свойства значение __Present__.</span><span class="sxs-lookup"><span data-stu-id="97fab-121">Set this property to __Present__ to ensure the contents exist.</span></span> <span data-ttu-id="97fab-122">Чтобы убедиться, что содержимого не существует, укажите для этого свойства значение __Absent__.</span><span class="sxs-lookup"><span data-stu-id="97fab-122">Set it to __Absent__ to ensure they do not exist.</span></span> <span data-ttu-id="97fab-123">Значение по умолчанию — __Present__.</span><span class="sxs-lookup"><span data-stu-id="97fab-123">The default value is __Present__.</span></span>|
| <span data-ttu-id="97fab-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="97fab-124">DependsOn</span></span> | <span data-ttu-id="97fab-125">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="97fab-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="97fab-126">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="97fab-126">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="97fab-127">Проверить</span><span class="sxs-lookup"><span data-stu-id="97fab-127">Validate</span></span>| <span data-ttu-id="97fab-128">Проверяет соответствие архива и подписи, используя свойство Checksum.</span><span class="sxs-lookup"><span data-stu-id="97fab-128">Uses the Checksum property to determine if the archive matches the signature.</span></span> <span data-ttu-id="97fab-129">Если свойство Checksum указано без свойства Validate, возникает ошибка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97fab-129">If you specify Checksum without Validate, the configuration will fail.</span></span> <span data-ttu-id="97fab-130">Если свойство Validate указано без свойства Checksum, по умолчанию используется контрольная сумма SHA-256.</span><span class="sxs-lookup"><span data-stu-id="97fab-130">If you specify Validate without Checksum, a SHA-256 checksum is used by default.</span></span>|
| <span data-ttu-id="97fab-131">Force</span><span class="sxs-lookup"><span data-stu-id="97fab-131">Force</span></span>| <span data-ttu-id="97fab-132">Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку.</span><span class="sxs-lookup"><span data-stu-id="97fab-132">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="97fab-133">Свойство Force позволяет переопределять такие ошибки.</span><span class="sxs-lookup"><span data-stu-id="97fab-133">Using the Force property overrides such errors.</span></span> <span data-ttu-id="97fab-134">По умолчанию используется значение False.</span><span class="sxs-lookup"><span data-stu-id="97fab-134">The default value is False.</span></span>|

## <a name="example"></a><span data-ttu-id="97fab-135">Пример</span><span class="sxs-lookup"><span data-stu-id="97fab-135">Example</span></span>

<span data-ttu-id="97fab-136">В следующем примере показано, как использовать ресурс Archive, чтобы убедиться, что содержимое архивного файла с именем Test.zip существует и извлекается в указанную папку.</span><span class="sxs-lookup"><span data-stu-id="97fab-136">The following example shows how to use the Archive resource to ensure that the contents of an archive file called Test.zip exist and are extracted at a given destination.</span></span>

```
Archive ArchiveExample {
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Path = "C:\Users\Public\Documents\Test.zip"
    Destination = "C:\Users\Public\Documents\ExtractionPath"
}
```