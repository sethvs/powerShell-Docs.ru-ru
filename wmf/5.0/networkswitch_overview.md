---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 80852bf750700d549de24e150ffd89ac55b7bf88
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="29fde-102">Управление сетевыми коммутаторами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="29fde-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="29fde-103">Теперь командлет **Get-NetworkSwitchEthernetPort** возвращает вместе с экземплярами следующие дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="29fde-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="29fde-104">IPAddress — сопоставленный с портом IP-адрес</span><span class="sxs-lookup"><span data-stu-id="29fde-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="29fde-105">PortMode — режим порта: доступ, маршрут или магистраль</span><span class="sxs-lookup"><span data-stu-id="29fde-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="29fde-106">AccessVLAN — идентификатор виртуальной локальной сети, связанной с этим портом в режиме доступа</span><span class="sxs-lookup"><span data-stu-id="29fde-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="29fde-107">TrunkedVLANList — список идентификаторов виртуальных локальных сетей, связанных с этим портом в режиме магистрали</span><span class="sxs-lookup"><span data-stu-id="29fde-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="29fde-108">Основы управления сетевыми коммутаторами с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="29fde-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="29fde-109">Командлеты сетевых коммутаторов, представленные в WMF 5.0, позволяют применять конфигурацию коммутатора, виртуальной локальной сети и портов базового сетевого коммутатора уровня 2 к сетевым коммутаторам, прошедшим сертификацию для Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="29fde-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="29fde-110">Корпорация Майкрософт по-прежнему придерживается концепции уровня [абстракции центра обработки данных](http://technet.microsoft.com/en-us/cloud/dal.aspx) (DAL) и стремится продемонстрировать ту пользу, которую она может принести нашим клиентам и партнерам.</span><span class="sxs-lookup"><span data-stu-id="29fde-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/en-us/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="29fde-111">Эти командлеты позволяют осуществлять следующее.</span><span class="sxs-lookup"><span data-stu-id="29fde-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="29fde-112">Глобальная конфигурация коммутаторов, например следующее.</span><span class="sxs-lookup"><span data-stu-id="29fde-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="29fde-113">Задание имени узла</span><span class="sxs-lookup"><span data-stu-id="29fde-113">Set host name</span></span>
    - <span data-ttu-id="29fde-114">Задание баннера параметров</span><span class="sxs-lookup"><span data-stu-id="29fde-114">Set switch banner</span></span>
    - <span data-ttu-id="29fde-115">Сохранение конфигурации</span><span class="sxs-lookup"><span data-stu-id="29fde-115">Persist configuration</span></span>
    - <span data-ttu-id="29fde-116">Включение и отключение функции</span><span class="sxs-lookup"><span data-stu-id="29fde-116">Enable or disable feature</span></span>

- <span data-ttu-id="29fde-117">Конфигурация виртуальной локальной сети:</span><span class="sxs-lookup"><span data-stu-id="29fde-117">VLAN configuration:</span></span>
    - <span data-ttu-id="29fde-118">Создание или удаление виртуальной ЛС</span><span class="sxs-lookup"><span data-stu-id="29fde-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="29fde-119">Включение или отключение виртуальной ЛС</span><span class="sxs-lookup"><span data-stu-id="29fde-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="29fde-120">Перечисление виртуальной ЛС</span><span class="sxs-lookup"><span data-stu-id="29fde-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="29fde-121">Указание понятного имени для виртуальной ЛС</span><span class="sxs-lookup"><span data-stu-id="29fde-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="29fde-122">Конфигурация портов уровня 2:</span><span class="sxs-lookup"><span data-stu-id="29fde-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="29fde-123">Перечисление портов</span><span class="sxs-lookup"><span data-stu-id="29fde-123">Enumerate ports</span></span>
    - <span data-ttu-id="29fde-124">Включение или отключение портов</span><span class="sxs-lookup"><span data-stu-id="29fde-124">Enable or disable ports</span></span>
    - <span data-ttu-id="29fde-125">Задание свойств и режимов портов</span><span class="sxs-lookup"><span data-stu-id="29fde-125">Set port modes and properties</span></span>
    - <span data-ttu-id="29fde-126">Добавление или сопоставление виртуальной ЛС с режимом магистрали или доступа для порта</span><span class="sxs-lookup"><span data-stu-id="29fde-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="29fde-127">Ознакомьтесь со всеми командлетами NetworkSwitch.</span><span class="sxs-lookup"><span data-stu-id="29fde-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

<span data-ttu-id="29fde-128">Дополнительные сведения можно найти в записи блога Джеффри Сновера (Jeffrey Snover), посвященной выпуску WMF 5.0 Preview: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span><span class="sxs-lookup"><span data-stu-id="29fde-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>

