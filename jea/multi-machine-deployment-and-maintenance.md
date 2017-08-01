---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "обслуживание и развертывание на нескольких компьютерах"
ms.technology: powershell
ms.openlocfilehash: 8117d0d12c062b460cb7117b54c138c8db5a1d0c
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
# <a name="multi-machine-deployment-and-maintenance"></a><span data-ttu-id="5e01e-103">Обслуживание и развертывание на нескольких компьютерах</span><span class="sxs-lookup"><span data-stu-id="5e01e-103">Multi-machine Deployment and Maintenance</span></span>
<span data-ttu-id="5e01e-104">К этому моменту вы уже неоднократно развертывали JEA в локальных системах.</span><span class="sxs-lookup"><span data-stu-id="5e01e-104">At this point, you have deployed JEA to local systems several times.</span></span>
<span data-ttu-id="5e01e-105">Так как ваша рабочая среда может включать не один компьютер, а несколько, нужно выполнить критически важные шаги в процессе развертывания и повторить их на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="5e01e-105">Because your production environment probably consists of more than one machine, it's important to walk through the critical steps in the deployment process that must be repeated on each machine.</span></span>

## <a name="high-level-steps"></a><span data-ttu-id="5e01e-106">Шаги на высоком уровне.</span><span class="sxs-lookup"><span data-stu-id="5e01e-106">High Level Steps:</span></span>
1.  <span data-ttu-id="5e01e-107">Скопируйте модули (с возможностями ролей) в каждый узел.</span><span class="sxs-lookup"><span data-stu-id="5e01e-107">Copy your modules (with Role Capabilities) to each node.</span></span>
2.  <span data-ttu-id="5e01e-108">Скопируйте файлы конфигурации сеансов на каждый узел.</span><span class="sxs-lookup"><span data-stu-id="5e01e-108">Copy your session configuration files to each node.</span></span>
3.  <span data-ttu-id="5e01e-109">Выполните `Register-PSSessionConfiguration` с конфигурацией сеанса.</span><span class="sxs-lookup"><span data-stu-id="5e01e-109">Run `Register-PSSessionConfiguration` with your session configuration.</span></span>
4.  <span data-ttu-id="5e01e-110">Сохраните копию конфигурации сеанса и наборы инструментов в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="5e01e-110">Keep a copy of your session configuration and toolkits in a secure location.</span></span>
<span data-ttu-id="5e01e-111">Внося изменения, хорошо иметь исходный эталонный образец.</span><span class="sxs-lookup"><span data-stu-id="5e01e-111">As you make modifications, it's good to have a "single source of truth."</span></span>

## <a name="example-script"></a><span data-ttu-id="5e01e-112">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="5e01e-112">Example Script</span></span>
<span data-ttu-id="5e01e-113">Рассмотрим пример сценария развертывания.</span><span class="sxs-lookup"><span data-stu-id="5e01e-113">Here's an example script for deployment.</span></span>
<span data-ttu-id="5e01e-114">Чтобы использовать его в среде, необходимо вставить имена и пути реальных общих папок и модулей.</span><span class="sxs-lookup"><span data-stu-id="5e01e-114">To use it in your environment, you'll have to use the names/paths of real file shares and modules.</span></span>
```PowerShell
# First, copy the session configuration and modules (containing role capability files) onto a file share you have access to.
Copy-Item -Path 'C:\Demo\Demo.pssc' -Destination '\\FileShare\JEA\Demo.pssc'
Copy-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\SomeModule\' -Recurse -Destination '\\FileShare\JEA\SomeModule'

# Next, author a setup script (C:\JEA\Deploy.ps1) to run on each individual node
    # Contents of C:\JEA\Deploy.ps1
    New-Item -ItemType Directory -Path C:\JEADeploy
    Copy-Item -Path '\\FileShare\JEA\Demo.pssc' -Destination 'C:\JEADeploy\'
    Copy-Item -Path '\\FileShare\JEA\SomeModule' -Recurse -Destination 'C:\Program Files\WindowsPowerShell\Modules' # Remember, Role Capability Files are found in modules
    if (Get-PSSessionConfiguration -Name JEADemo -ErrorAction SilentlyContinue)
    {
        Unregister-PSSessionConfiguration -Name JEADemo -ErrorAction Stop
    }

    Register-PSSessionConfiguration -Name JEADemo -Path 'C:\JEADeploy\Demo.pssc'
    Remove-Item -Path 'C:\JEADeploy' # Don't forget to clean up!

# Now, invoke the script on all of the target machines.
# Note: this requires PowerShell Remoting be enabled on each machine. Enabling PowerShell remoting is a requirement to use JEA as well.
# You may need to provide the "-Credential" parameter if your current user account does not have admin permissions on these machines.
Invoke-Command –ComputerName 'Node1', 'Node2', 'Node3', 'NodeN' -FilePath 'C:\JEA\Deploy.ps1'

# Finally, delete the session configuration and role capability files from the file share.
Remove-Item -Path '\\FileShare\JEA\Demo.pssc'
Remove-Item -Path '\\FileShare\JEA\SomeModule' -Recurse
```
## <a name="modifying-capabilities"></a><span data-ttu-id="5e01e-115">Изменение возможностей</span><span class="sxs-lookup"><span data-stu-id="5e01e-115">Modifying Capabilities</span></span>
<span data-ttu-id="5e01e-116">При работе с несколькими компьютерами важно вносить изменения согласованно.</span><span class="sxs-lookup"><span data-stu-id="5e01e-116">When dealing with many machines, it's important that modifications are rolled out in a consistent manner.</span></span>
<span data-ttu-id="5e01e-117">Когда у JEA появится ресурс DSC, это позволит обеспечить синхронизацию среды.</span><span class="sxs-lookup"><span data-stu-id="5e01e-117">Once JEA has a DSC Resource, this will help ensure your environment is in sync.</span></span>
<span data-ttu-id="5e01e-118">Пока же настоятельно рекомендуем сохранять мастер-копии конфигураций сеансов и обращаться к ним при каждом изменении.</span><span class="sxs-lookup"><span data-stu-id="5e01e-118">Until that time, we highly recommend you keep a master copy of your session configurations and re-deploy each time you make a modification.</span></span>

## <a name="removing-capabilities"></a><span data-ttu-id="5e01e-119">Удаление возможностей</span><span class="sxs-lookup"><span data-stu-id="5e01e-119">Removing Capabilities</span></span>
<span data-ttu-id="5e01e-120">Чтобы удалить конфигурацию JEA из системы, выполните на каждом компьютере следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5e01e-120">To remove your JEA configuration from your systems, use the following command on each machine:</span></span>
```PowerShell
Unregister-PSSessionConfiguration -Name JEADemo
```

