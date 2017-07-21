---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: d3a625d05eaf4e7448b4abf90499f6a94e2f7718
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a><span data-ttu-id="dab8c-102">Поддержка идентичных повторяющихся ресурсов в конфигурации</span><span class="sxs-lookup"><span data-stu-id="dab8c-102">Allowing for Identical Duplicate Resources in a Configuration</span></span>

<span data-ttu-id="dab8c-103">DSC не допускает и не обрабатывает конфликтующие определения ресурсов в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dab8c-103">DSC does not allow or handle conflicting resource definitions within a configuration.</span></span> <span data-ttu-id="dab8c-104">Вместо того чтобы попытаться разрешить конфликт, он просто завершается со сбоем.</span><span class="sxs-lookup"><span data-stu-id="dab8c-104">Instead of trying to resolve the conflict, it simply fails.</span></span> <span data-ttu-id="dab8c-105">По мере того, как конфигурации все больше используются повторно с помощью составных ресурсов и т. п., конфликты будут возникать все чаще.</span><span class="sxs-lookup"><span data-stu-id="dab8c-105">As configuration reuse becomes more utilized through composite resources, etc. conflicts will occur more often.</span></span> <span data-ttu-id="dab8c-106">Если конфликтующие определения ресурсов идентичны, DSC необходимо разрешить такую работу.</span><span class="sxs-lookup"><span data-stu-id="dab8c-106">When conflicting resource definitions are identical, DSC should be smart and allow this.</span></span> <span data-ttu-id="dab8c-107">В этом выпуске мы включаем поддержку нескольких экземпляров ресурсов с одинаковыми определениями:</span><span class="sxs-lookup"><span data-stu-id="dab8c-107">With this release, we support having multiple resource instances that have identical definitions:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="dab8c-108">Если бы в предыдущих выпусках имелся конфликт между экземплярами WindowsFeature FE_IIS и WindowsFeature Worker_IIS, пытающимися проверить установку роли "Веб-сервер", компиляция завершилась бы сбоем.</span><span class="sxs-lookup"><span data-stu-id="dab8c-108">In previous releases, the result would be a failed compilation due to a conflict between the WindowsFeature FE_IIS and WindowsFeature Worker_IIS instances trying to ensure the 'Web-Server' role is installed.</span></span> <span data-ttu-id="dab8c-109">Обратите внимание, что в этих двух конфигурациях *все* настраиваемые свойства идентичны.</span><span class="sxs-lookup"><span data-stu-id="dab8c-109">Notice that *all* of the properties that are being configured are identical in these two configurations.</span></span> <span data-ttu-id="dab8c-110">И именно благодаря идентичности *всех* свойств в этих двух ресурсах компиляция теперь выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="dab8c-110">Since *all* of the properties in these two resources are identical, this will result in a successful compilation now.</span></span> 

<span data-ttu-id="dab8c-111">Если же какие-либо свойства между двумя ресурсами не совпадают, они не считаются идентичными и компиляция завершается ошибкой:</span><span class="sxs-lookup"><span data-stu-id="dab8c-111">If any of the properties are different between the two resources, they will not be considered identical and compilation will fail:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="dab8c-112">Эта конфигурация, которая очень похожа на предыдущую, завершается с ошибкой, поскольку ресурсы WindowsFeature FE_IIS и WindowsFeature Worker_IIS больше не совпадают, а значит конфликтуют.</span><span class="sxs-lookup"><span data-stu-id="dab8c-112">This very similar configuration will fail because the WindowsFeature FE_IIS and the WindowsFeature Worker_IIS resources are no longer identical and therefore conflict.</span></span>

