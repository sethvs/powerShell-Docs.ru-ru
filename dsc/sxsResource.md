---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Использование ресурсов с несколькими версиями
ms.openlocfilehash: 9e5b989be3f33fb9151f76cecb6d5f700b1e36c9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="using-resources-with-multiple-versions"></a><span data-ttu-id="66278-103">Использование ресурсов с несколькими версиями</span><span class="sxs-lookup"><span data-stu-id="66278-103">Using resources with multiple versions</span></span>

> <span data-ttu-id="66278-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="66278-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="66278-105">В PowerShell 5.0 ресурсы DSC могут иметь несколько версий, и эти версии можно устанавливать на компьютере параллельно.</span><span class="sxs-lookup"><span data-stu-id="66278-105">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="66278-106">Это реализуется благодаря наличию нескольких версий модуля ресурсов, которые содержатся в одной папке модуля.</span><span class="sxs-lookup"><span data-stu-id="66278-106">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>

## <a name="installing-multiple-resource-versions-side-by-side"></a><span data-ttu-id="66278-107">Параллельная установка нескольких версий ресурса</span><span class="sxs-lookup"><span data-stu-id="66278-107">Installing multiple resource versions side-by-side</span></span>

<span data-ttu-id="66278-108">Параметры **MinimumVersion**, **MaximumVersion** и **RequiredVersion** командлета [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) можно использовать, чтобы указать версию модуля для установки.</span><span class="sxs-lookup"><span data-stu-id="66278-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="66278-109">Вызов командлета **Install-Module** без указания версии устанавливает последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="66278-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="66278-110">Например, существует несколько версий модуля **xFailOverCluster**, каждая из которых содержит ресурс **xCluster**.</span><span class="sxs-lookup"><span data-stu-id="66278-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resouce.</span></span> <span data-ttu-id="66278-111">Результат вызова командлета **Install-Module** без указания номера версии будет следующим.</span><span class="sxs-lookup"><span data-stu-id="66278-111">The result of calling **Install-Module** without specifying the version number is as follows:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="66278-112">Если снова вызвать командлет **Install-Module** и указать для параметра **RequiredVersion** значение 1.1.0.0, результат будет следующим:</span><span class="sxs-lookup"><span data-stu-id="66278-112">Now, if you call **Install-Module** again, but specify a **RequiredVersion** of 1.1.0.0, it results in the following:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="66278-113">Указание версии ресурса в конфигурации</span><span class="sxs-lookup"><span data-stu-id="66278-113">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="66278-114">Если имеется несколько ресурсов, установленных на компьютере, необходимо указать версию нужного ресурса при его использовании в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="66278-114">If you have multiple resources installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="66278-115">Это делается путем указания параметра **ModuleVersion** ключевого слова **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="66278-115">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="66278-116">Если не указать версию модуля ресурсов для ресурса, имеющего несколько установленных версий, конфигурация породит ошибку.</span><span class="sxs-lookup"><span data-stu-id="66278-116">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="66278-117">В конфигурации ниже показано, как указать версию ресурса для вызова:</span><span class="sxs-lookup"><span data-stu-id="66278-117">The following configuration shows how to specify the version of the resource to call:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

><span data-ttu-id="66278-118">Примечание. Параметр ModuleVersion ключевого слова Import-DscResource недоступен в PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="66278-118">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="66278-119">В PowerShell 4.0 версию модуля можно задать, передав объект спецификации модуля в параметр ModuleName ключевого слова Import-DscResource.</span><span class="sxs-lookup"><span data-stu-id="66278-119">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="66278-120">Объект спецификации модуля представляет собой хэш-таблицу, содержащую ключи ModuleName и RequiredVersion.</span><span class="sxs-lookup"><span data-stu-id="66278-120">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="66278-121">Например:</span><span class="sxs-lookup"><span data-stu-id="66278-121">For example:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

<span data-ttu-id="66278-122">Этот способ также будет работать в PowerShell 5.0, однако рекомендуется использовать параметр **ModuleVersion**.</span><span class="sxs-lookup"><span data-stu-id="66278-122">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="66278-123">См. также:</span><span class="sxs-lookup"><span data-stu-id="66278-123">See also</span></span>
* [<span data-ttu-id="66278-124">Конфигурации DSC</span><span class="sxs-lookup"><span data-stu-id="66278-124">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="66278-125">Ресурсы DSC</span><span class="sxs-lookup"><span data-stu-id="66278-125">DSC Resources</span></span>](resources.md)