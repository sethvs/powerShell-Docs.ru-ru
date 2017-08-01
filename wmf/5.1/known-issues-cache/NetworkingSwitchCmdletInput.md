---
title: "Сбой командлетов диспетчера сетевых коммутаторов"
contributor: vaibch
ms.openlocfilehash: e32e31762b665a7e2c6f6938fe494cb6127d4264
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
ms.translationtype: HT
ms.contentlocale: ru-RU
---
<span data-ttu-id="6eb38-102">Командлеты диспетчера сетевых коммутаторов можно использовать для управления сетевыми коммутаторами по WSMAN.</span><span class="sxs-lookup"><span data-stu-id="6eb38-102">The Network Switch Manager cmdlets can be used to manage network switches over WSMAN.</span></span> <span data-ttu-id="6eb38-103">Несколько командлетов этого модуля могут принимать значения из конвейеров.</span><span class="sxs-lookup"><span data-stu-id="6eb38-103">A few cmdlets of this module are capable of accepting values from pipelines.</span></span> <span data-ttu-id="6eb38-104">В WMF 5.1 Preview командлеты, которые принимают значение из конвейера, не могут быть выполнены, если значения не переданы через конвейеры.</span><span class="sxs-lookup"><span data-stu-id="6eb38-104">In WMF 5.1 Preview, the cmdlets that can accept value from pipeline fail to execute when the values are not passed through pipelines.</span></span>

<span data-ttu-id="6eb38-105">Если параметр InputObject не используется, командлет должен по-прежнему работать без сбоев.</span><span class="sxs-lookup"><span data-stu-id="6eb38-105">If "InputObject" parameter is not used, the cmdlet should continue to execute without failures.</span></span>

<span data-ttu-id="6eb38-106">Список затронутых командлетов, например тех, которые могут принять значение для параметра InputObject из конвейера.</span><span class="sxs-lookup"><span data-stu-id="6eb38-106">Here is the list of affected cmdlets i.e. these cmdlets can accept value for "InputObject" parameter from pipeline.</span></span> <span data-ttu-id="6eb38-107">Если это значение не передано из конвейера, произойдет сбой выполнения командлета.</span><span class="sxs-lookup"><span data-stu-id="6eb38-107">If this value is not passed from pipeline the execution of cmdlet will fail.</span></span>

- <span data-ttu-id="6eb38-108">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="6eb38-108">Disable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="6eb38-109">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="6eb38-109">Enable-NetworkSwitchEthernetPort</span></span>
- <span data-ttu-id="6eb38-110">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="6eb38-110">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="6eb38-111">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="6eb38-111">Set-NetworkSwitchEthernetPortIPAddress</span></span>
- <span data-ttu-id="6eb38-112">Set-NetworkSwitchPortMode</span><span class="sxs-lookup"><span data-stu-id="6eb38-112">Set-NetworkSwitchPortMode</span></span>
- <span data-ttu-id="6eb38-113">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="6eb38-113">Set-NetworkSwitchPortProperty</span></span>
- <span data-ttu-id="6eb38-114">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="6eb38-114">Disable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="6eb38-115">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="6eb38-115">Enable-NetworkSwitchFeature</span></span>
- <span data-ttu-id="6eb38-116">Remove-NetworkSwitchVlan</span><span class="sxs-lookup"><span data-stu-id="6eb38-116">Remove-NetworkSwitchVlan</span></span>
- <span data-ttu-id="6eb38-117">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="6eb38-117">Set-NetworkSwitchVlanProperty</span></span>

### <a name="resolution"></a><span data-ttu-id="6eb38-118">Разрешение</span><span class="sxs-lookup"><span data-stu-id="6eb38-118">Resolution</span></span>
<span data-ttu-id="6eb38-119">Командлеты работают нормально, если значение параметра InputObject передается через конвейер.</span><span class="sxs-lookup"><span data-stu-id="6eb38-119">The cmdlets work fine when the value of InputObject parameter are passed into it through pipeline.</span></span> <span data-ttu-id="6eb38-120">Ниже приведены примеры, подходящие для командлетов выше.</span><span class="sxs-lookup"><span data-stu-id="6eb38-120">A few examples that work for the above cmdlets are:</span></span>

- <span data-ttu-id="6eb38-121">Disable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="6eb38-121">Disable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Disable-NetworkSwitchEthernetPort -CimSession $cimSession
```
- <span data-ttu-id="6eb38-122">Enable-NetworkSwitchEthernetPort</span><span class="sxs-lookup"><span data-stu-id="6eb38-122">Enable-NetworkSwitchEthernetPort</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Enable-NetworkSwitchEthernetPort -CimSession $cimSession
```

- <span data-ttu-id="6eb38-123">Remove-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="6eb38-123">Remove-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Remove-NetworkSwitchEthernetPortIPAddress -CimSession $cimSession
```

- <span data-ttu-id="6eb38-124">Set-NetworkSwitchEthernetPortIPAddress</span><span class="sxs-lookup"><span data-stu-id="6eb38-124">Set-NetworkSwitchEthernetPortIPAddress</span></span>
```powershell
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$ipAddress = "192.168.10.1"
$subnetAddress = "255.255.255.0"
$port | Set-NetworkSwitchEthernetPortIPAddress -IpAddress $ipAddress -SubnetAddress $subnetAddress -CimSession $cimSession
```

- <span data-ttu-id="6eb38-125">Set-NetworkSwitchPortProperty</span><span class="sxs-lookup"><span data-stu-id="6eb38-125">Set-NetworkSwitchPortProperty</span></span>
```powershell
$portProperties = @{Caption = "New Caption"}
$port = Get-CimInstance -Namespace root/interop -ClassName CIM_EthernetPort -CimSession $cimSession | Select-Object -First 1
$port | Set-NetworkSwitchPortProperty -Property $portProperties -CimSession $cimSession
```

- <span data-ttu-id="6eb38-126">Disable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="6eb38-126">Disable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Disable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="6eb38-127">Enable-NetworkSwitchFeature</span><span class="sxs-lookup"><span data-stu-id="6eb38-127">Enable-NetworkSwitchFeature</span></span>
```powershell
$feature = Get-CimInstance -Namespace root/interop -ClassName MSFT_Feature -CimSession $cimSession | Select-Object -First 1
$feature | Enable-NetworkSwitchFeature -CimSession $cimSession
```

- <span data-ttu-id="6eb38-128">Set-NetworkSwitchVlanProperty</span><span class="sxs-lookup"><span data-stu-id="6eb38-128">Set-NetworkSwitchVlanProperty</span></span>
```powershell
$properties = @{Caption = "New Caption"}
$vlan = Get-CimInstance -ClassName CIM_NetworkVlan -Namespace root/interop -CimSession $cimSession | Select-Object -First 1
$vlan | Set-NetworkSwitchVlanProperty -Property $properties -CimSession $cimSession
```
