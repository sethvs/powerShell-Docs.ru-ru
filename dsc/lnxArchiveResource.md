---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxArchive в DSC для Linux
ms.openlocfilehash: 142f0317914f1bd3a0523d706b19662f3f64c8b6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxarchive-resource"></a><span data-ttu-id="318ad-103">Ресурс nxArchive в DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="318ad-103">DSC for Linux nxArchive Resource</span></span>

<span data-ttu-id="318ad-104">Ресурс **nxArchive** в DSC PowerShell предоставляет механизм распаковки файлов архивов (TAR, ZIP) в указанную папку на узле с Linux.</span><span class="sxs-lookup"><span data-stu-id="318ad-104">The **nxArchive** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to unpack archive (.tar, .zip) files at a specific path on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="318ad-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="318ad-105">Syntax</span></span>

```
nxArchive <string> #ResourceName
{
    SourcePath = <string>
    DestinationPath = <string>
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Force = <bool> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present }  ]
}
```

## <a name="properties"></a><span data-ttu-id="318ad-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="318ad-106">Properties</span></span>

|  <span data-ttu-id="318ad-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="318ad-107">Property</span></span> |  <span data-ttu-id="318ad-108">Описание</span><span class="sxs-lookup"><span data-stu-id="318ad-108">Description</span></span> |
|---|---|
| <span data-ttu-id="318ad-109">SourcePath</span><span class="sxs-lookup"><span data-stu-id="318ad-109">SourcePath</span></span>| <span data-ttu-id="318ad-110">Указывает исходный путь для файла архива.</span><span class="sxs-lookup"><span data-stu-id="318ad-110">Specifies the source path of the archive file.</span></span> <span data-ttu-id="318ad-111">Это должен быть файл в формате TAR, ZIP или TAR.GZ.</span><span class="sxs-lookup"><span data-stu-id="318ad-111">This should be a .tar, .zip, or .tar.gz file.</span></span> |
| <span data-ttu-id="318ad-112">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="318ad-112">DestinationPath</span></span>| <span data-ttu-id="318ad-113">Указывает, куда будет извлечено содержимое архива.</span><span class="sxs-lookup"><span data-stu-id="318ad-113">Specifies the location where you want to ensure the archive contents are extracted.</span></span>|
| <span data-ttu-id="318ad-114">Контрольная сумма</span><span class="sxs-lookup"><span data-stu-id="318ad-114">Checksum</span></span>| <span data-ttu-id="318ad-115">Указывает тип для использования при определении факта обновления исходного архива.</span><span class="sxs-lookup"><span data-stu-id="318ad-115">Defines the type to use when determining whether the source archive has been updated.</span></span> <span data-ttu-id="318ad-116">Значения: ctime, mtime или md5.</span><span class="sxs-lookup"><span data-stu-id="318ad-116">Values are: "ctime", "mtime", or "md5".</span></span> <span data-ttu-id="318ad-117">Значение по умолчанию — md5.</span><span class="sxs-lookup"><span data-stu-id="318ad-117">The default value is "md5".</span></span>|
| <span data-ttu-id="318ad-118">Force</span><span class="sxs-lookup"><span data-stu-id="318ad-118">Force</span></span>| <span data-ttu-id="318ad-119">Определенные операции с файлами (например, перезапись файла или удаление непустого каталога) вызывают ошибку.</span><span class="sxs-lookup"><span data-stu-id="318ad-119">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="318ad-120">Свойство **Force** позволяет переопределять такие ошибки.</span><span class="sxs-lookup"><span data-stu-id="318ad-120">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="318ad-121">Значение по умолчанию — **$false**.</span><span class="sxs-lookup"><span data-stu-id="318ad-121">The default value is **$false**.</span></span>|
| <span data-ttu-id="318ad-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="318ad-122">DependsOn</span></span> | <span data-ttu-id="318ad-123">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="318ad-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="318ad-124">Например, если **идентификатор** первого запускаемого блока сценария для конфигурации ресурса — **ResourceName**, а его тип — **ResourceType**, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="318ad-124">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="318ad-125">Ensure</span><span class="sxs-lookup"><span data-stu-id="318ad-125">Ensure</span></span>| <span data-ttu-id="318ad-126">Указывает необходимость проверки того, существует ли содержимое архива в **папке назначения**.</span><span class="sxs-lookup"><span data-stu-id="318ad-126">Determines whether to check if the content of the archive exists at the **Destination**.</span></span> <span data-ttu-id="318ad-127">Чтобы убедиться, что содержимое существует, укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="318ad-127">Set this property to "Present" to ensure the contents exist.</span></span> <span data-ttu-id="318ad-128">Чтобы убедиться, что содержимое не существует, укажите для этого свойства значение Absent.</span><span class="sxs-lookup"><span data-stu-id="318ad-128">Set it to "Absent" to ensure they do not exist.</span></span> <span data-ttu-id="318ad-129">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="318ad-129">The default value is "Present".</span></span>|

## <a name="example"></a><span data-ttu-id="318ad-130">Пример</span><span class="sxs-lookup"><span data-stu-id="318ad-130">Example</span></span>

<span data-ttu-id="318ad-131">В следующем примере показано, как использовать ресурс **nxArchive**, чтобы убедиться, что содержимое архивного файла с именем `website.tar` существует и извлекается в указанную папку.</span><span class="sxs-lookup"><span data-stu-id="318ad-131">The following example shows how to use the **nxArchive** resource to ensure that the contents of an archive file called `website.tar` exist and are extracted at a given destination.</span></span>

```
Import-DSCResource -Module nx

nxFile SyncArchiveFromWeb
{
   Ensure = "Present"
   SourcePath = “http://release.contoso.com/releases/website.tar”
   DestinationPath = "/usr/release/staging/website.tar"
   Type = "File"
   Checksum = “mtime”
}

nxArchive SyncWebDir
{
   SourcePath = “/usr/release/staging/website.tar”
   DestinationPath = “/usr/local/apache2/htdocs/”
   Force = $false
   DependsOn = "[nxFile]SyncArchiveFromWeb"
}
```