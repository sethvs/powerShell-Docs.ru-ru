---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "Командлеты для работы с каталогами"
ms.openlocfilehash: 88ca8a3366f7b1d83ba2596d7ae1230427797cf4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="catalog-cmdlets"></a><span data-ttu-id="c7811-103">Командлеты для работы с каталогами</span><span class="sxs-lookup"><span data-stu-id="c7811-103">Catalog Cmdlets</span></span>  

<span data-ttu-id="c7811-104">Мы добавили два новых командлета для создания и проверки файлов каталога Windows в модуль [Microsoft.Powershell.Security](https://technet.microsoft.com/en-us/library/hh847877.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7811-104">We have added two new cmdlets in [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) module to generate and validate windows catalog files.</span></span>  

## <a name="new-filecatalog"></a><span data-ttu-id="c7811-105">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="c7811-105">New-FileCatalog</span></span> 
--------------------------------

<span data-ttu-id="c7811-106">`New-FileCatalog` создает файл каталога Windows для набора файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="c7811-106">`New-FileCatalog` creates a windows catalog file for set of folders and files.</span></span> <span data-ttu-id="c7811-107">Файл каталога содержит хэши для всех файлов, находящихся по указанным путям.</span><span class="sxs-lookup"><span data-stu-id="c7811-107">A catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="c7811-108">Пользователь может распространять набор папок вместе с соответствующим файлом каталога, представляющим этих папки.</span><span class="sxs-lookup"><span data-stu-id="c7811-108">Users can distribute the set of folders along with corresponding the catalog file that represents those folders.</span></span> <span data-ttu-id="c7811-109">Файл каталога может использоваться получателем содержимого, чтобы проверить, были ли внесены изменения в папки после создания каталога.</span><span class="sxs-lookup"><span data-stu-id="c7811-109">A catalog file can be used by the recipient of content to validate whether any changes were made to the folders after the catalog was created.</span></span>    

```PowerShell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="c7811-110">Поддерживается создание каталогов версий 1 и 2.</span><span class="sxs-lookup"><span data-stu-id="c7811-110">We support creating catalog version 1 and 2.</span></span> <span data-ttu-id="c7811-111">В версии 1 для создания хэшей файлов используется алгоритм хэширования SHA1, в версии 2 — SHA256.</span><span class="sxs-lookup"><span data-stu-id="c7811-111">Version 1 uses SHA1 hashing algorithm to create file hashes and version 2 uses SHA256.</span></span> <span data-ttu-id="c7811-112">Каталог версии 2 не поддерживается в *Windows Server 2008 R2* и *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="c7811-112">Catalog version 2 is not supported on *Windows Server 2008 R2* and *Windows 7*.</span></span> <span data-ttu-id="c7811-113">На платформах *Windows 8* и *Windows Server 2012* и более поздней версии рекомендуется использовать каталог версии 2.</span><span class="sxs-lookup"><span data-stu-id="c7811-113">It is recommended to use catalog version 2 if using platforms *Windows 8*, *Windows Server 2012* and above.</span></span>  

<span data-ttu-id="c7811-114">Для использования этой команды в существующем модуле укажите для переменных CatalogFilePath и Path значения, соответствующие расположению манифеста модуля.</span><span class="sxs-lookup"><span data-stu-id="c7811-114">To use this command on an existing module, specify the CatalogFilePath and Path variables to match the location of the module manifest.</span></span> <span data-ttu-id="c7811-115">В следующем примере манифест модуля располагается в папке "C:\Program Files\Windows PowerShell\Modules\Pester".</span><span class="sxs-lookup"><span data-stu-id="c7811-115">In the example below, the module manifest is in C:\Program Files\Windows PowerShell\Modules\Pester.</span></span> 

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="c7811-116">Следующая команда создает файл каталога.</span><span class="sxs-lookup"><span data-stu-id="c7811-116">This creates the catalog file.</span></span> 

![](../images/CatalogFile1.jpg)  

![](../images/CatalogFile2.jpg) 

<span data-ttu-id="c7811-117">Для проверки целостности файла каталога (Pester.cat в примере выше) его нужно подписать командлетом [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7811-117">To verify the integrity of a catalog file (Pester.cat in above exmaple) it should be signed using the [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>   


## <a name="test-filecatalog"></a><span data-ttu-id="c7811-118">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="c7811-118">Test-FileCatalog</span></span> 
--------------------------------

<span data-ttu-id="c7811-119">`Test-FileCatalog` проверяет каталог, представляющий набор папок.</span><span class="sxs-lookup"><span data-stu-id="c7811-119">`Test-FileCatalog` validates the catalog representing a set of folders.</span></span> 

```PowerShell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="c7811-120">Этот командлет сравнивает хэши всех файлов и их относительные пути, найденные в файле каталога, с сохраненными на жестком диске.</span><span class="sxs-lookup"><span data-stu-id="c7811-120">This cmdlet compares the hashes of all files and their relative paths found in the catalog file with ones saved to disk.</span></span> <span data-ttu-id="c7811-121">При обнаружении любого несоответствия между хэшами файлов и путями он возвращает состояние `ValidationFailed`.</span><span class="sxs-lookup"><span data-stu-id="c7811-121">If it detects any mismatch between file hashes and paths it returns a status of `ValidationFailed`.</span></span> <span data-ttu-id="c7811-122">Все эти данные можно получить при помощи флага `Detailed`.</span><span class="sxs-lookup"><span data-stu-id="c7811-122">Users can retrieve all this information using the `Detailed` switch.</span></span> <span data-ttu-id="c7811-123">Состояние подписанности каталога отображается в поле `Signature`. Подпись также можно определить, вызвав командлет [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) и указав файл каталога.</span><span class="sxs-lookup"><span data-stu-id="c7811-123">The signing status of the catalog is displayed as the `Signature` field, which is same as calling the [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet on the catalog file.</span></span> <span data-ttu-id="c7811-124">Также можно исключить любые файлы из проверки, указав их в параметре `FilesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="c7811-124">Users can also skip any file during validation by using the `FilesToSkip` parameter.</span></span> 

