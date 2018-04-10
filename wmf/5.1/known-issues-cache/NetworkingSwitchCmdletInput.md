---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
contributor: vaibch
title: Сбой командлетов диспетчера сетевых коммутаторов
ms.openlocfilehash: 626809513e7a8f1aa2c47a48c74e69ca4077f598
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
<span data-ttu-id="d6456-103">Командлеты диспетчера сетевых коммутаторов можно использовать для управления сетевыми коммутаторами по WSMAN.</span><span class="sxs-lookup"><span data-stu-id="d6456-103">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span>
<span data-ttu-id="d6456-104">Несколько командлетов этого модуля могут принимать значения из конвейеров.</span><span class="sxs-lookup"><span data-stu-id="d6456-104">A few cmdlets of this module are capable of accepting values from pipelines.</span></span>
<span data-ttu-id="d6456-105">В WMF 5.1 Preview командлеты, которые принимают значение из конвейера, не могут быть выполнены, если значения не переданы через конвейеры.</span><span class="sxs-lookup"><span data-stu-id="d6456-105">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="d6456-106">Если параметр InputObject не используется, командлет должен по-прежнему работать без сбоев.</span><span class="sxs-lookup"><span data-stu-id="d6456-106">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="d6456-107">Список затронутых командлетов, например тех, которые могут принять значение для параметра InputObject из конвейера.</span><span class="sxs-lookup"><span data-stu-id="d6456-107">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span>
<span data-ttu-id="d6456-108">Если это значение не передано из конвейера, произойдет сбой выполнения командлета.</span><span class="sxs-lookup"><span data-stu-id="d6456-108">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="d6456-109">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="d6456-109">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="d6456-110">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="d6456-110">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="d6456-111">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="d6456-111">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="d6456-112">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="d6456-112">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="d6456-113">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="d6456-113">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="d6456-114">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="d6456-114">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="d6456-115">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="d6456-115">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="d6456-116">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="d6456-116">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="d6456-117">Remove-NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="d6456-117">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="d6456-118">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="d6456-118">Set-NetworkSwitchVlanProperty</span></span>

### <a name="resolution"></a><span data-ttu-id="d6456-119">Разрешение</span><span class="sxs-lookup"><span data-stu-id="d6456-119">Resolution</span></span>
<span data-ttu-id="d6456-120">Командлеты работают нормально, если значение параметра InputObject передается через конвейер.</span><span class="sxs-lookup"><span data-stu-id="d6456-120">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="d6456-121">Ниже приведены примеры, подходящие для командлетов выше.</span><span class="sxs-lookup"><span data-stu-id="d6456-121">A few examples that work for the above cmdlets are:</span></span>

- <span data-ttu-id="d6456-122">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="d6456-122">Disable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="d6456-123">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="d6456-123">Enable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="d6456-124">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="d6456-124">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- <span data-ttu-id="d6456-125">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="d6456-125">Set-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- <span data-ttu-id="d6456-126">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="d6456-126">Set-NetworkSwitchPortProperty</span></span>
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- <span data-ttu-id="d6456-127">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="d6456-127">Disable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="d6456-128">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="d6456-128">Enable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="d6456-129">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="d6456-129">Set-NetworkSwitchVlanProperty</span></span>
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```