---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
contributor: ryanpu
title: "Улучшения Just Enough Administration (JEA)"
ms.openlocfilehash: 2811b4deb3f4fca513791c7389ee5f9f877dbfe8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="9ddc6-103">Улучшения Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="9ddc6-103">Improvements to Just Enough Administration (JEA)</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="9ddc6-104">Ограниченное копирование файлов в конечные точки JEA и из них</span><span class="sxs-lookup"><span data-stu-id="9ddc6-104">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="9ddc6-105">Теперь вы можете удаленно копировать файлы в конечную точку JEA и из нее, не беспокоясь о том, что подключающийся пользователь сможет скопировать *любой* файл в вашей системе.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-105">You can now remotely copy files to/from a JEA endpoint and rest assured that the connecting user can't copy just *any* file on your system.</span></span>
<span data-ttu-id="9ddc6-106">Это возможно благодаря настройке подключения диска пользователя в PSSC-файле.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-106">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span>
<span data-ttu-id="9ddc6-107">Диск пользователя — это новый PSDrive, уникальный для каждого подключающегося пользователя; он сохраняется между сеансами.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-107">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span>
<span data-ttu-id="9ddc6-108">Когда для копирования файлов в сеанс JEA или из него используется Copy-Item, доступ разрешен только на диск пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-108">When Copy-Item is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span>
<span data-ttu-id="9ddc6-109">Копировать файлы на другой PSDrive будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-109">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="9ddc6-110">Чтобы настроить диск пользователя в файле конфигурации сеанса JEA, используйте следующие новые поля.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-110">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="9ddc6-111">Папка с резервной копией диска пользователя будет создана здесь: `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-111">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="9ddc6-112">Чтобы использовать диск пользователя и копировать файлы в конечную точку JEA с доступом к диску пользователя и из нее, используйте параметры `-ToSession` и `-FromSession` в Copy-Item.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-112">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on Copy-Item.</span></span>

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

<span data-ttu-id="9ddc6-113">Затем вы сможете записать пользовательские функции для обработки данных, хранящихся на диске пользователя, и предоставить их пользователям в файле возможностей ролей.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-113">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="9ddc6-114">Поддержка групповых учетных записей управляемой службы</span><span class="sxs-lookup"><span data-stu-id="9ddc6-114">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="9ddc6-115">В некоторых случаях для выполнения задачи пользователем в сеансе JEA может потребоваться доступ к ресурсам за пределами локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-115">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span>
<span data-ttu-id="9ddc6-116">Если в сеансе JEA настроено использование виртуальной учетной записи, любые попытки подключиться к таким ресурсам будут отображаться как полученные из удостоверения локального компьютера, а не из виртуальной учетной записи или от подключенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-116">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span>
<span data-ttu-id="9ddc6-117">В TP5 включена поддержка работы JEA в контексте [групповой учетной записи управляемой службы](https://technet.microsoft.com/ru-ru/library/jj128431(v=ws.11\).aspx), что упрощает доступ к сетевым ресурсам благодаря использованию удостоверения домена.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-117">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="9ddc6-118">Чтобы настроить работу сеанса JEA в учетной записи gMSA, используйте следующий новый ключ в PSSC-файле:</span><span class="sxs-lookup"><span data-stu-id="9ddc6-118">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> <span data-ttu-id="9ddc6-119">**Примечание**. Групповые учетные записи управляемой службы не допускают изоляцию или ограниченную область виртуальных учетных записей.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-119">**Note:** Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="9ddc6-120">Каждый подключающийся пользователь будет иметь такое удостоверение gMSA, у которого могут быть разрешения во всей организации.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-120">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span>
> <span data-ttu-id="9ddc6-121">Будьте внимательны при использовании gMSA. По возможности всегда рекомендуется использовать виртуальные учетные записи, действующие на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-121">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="9ddc6-122">Политики условного доступа</span><span class="sxs-lookup"><span data-stu-id="9ddc6-122">Conditional access policies</span></span>

<span data-ttu-id="9ddc6-123">JEA отлично подходит для ограничения действий управления при подключении к системе, но что, если вы также хотите ограничить *время* использования JEA?</span><span class="sxs-lookup"><span data-stu-id="9ddc6-123">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span>
<span data-ttu-id="9ddc6-124">Мы добавили варианты настройки в файлы конфигурации сеанса (PSSC), чтобы вы могли указать группы безопасности, к которым должен принадлежать пользователь для запуска сеанса JEA.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-124">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span>
<span data-ttu-id="9ddc6-125">Это может быть особенно полезным, если в вашей среде установлена система Just In Time (JIT) и вам нужно, чтобы пользователи повышали права перед доступом к привилегированной конечной точке JEA.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-125">This can be particularly helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="9ddc6-126">Новое поле *RequiredGroups* в PSSC-файле позволяет указать, может ли пользователь подключиться к JEA.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-126">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span>
<span data-ttu-id="9ddc6-127">Логика состоит в указании хэш-таблицы (при необходимости вложенной), которая использует ключи And и Or для создания правил.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-127">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="9ddc6-128">Ниже представлены примеры использования этого поля.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-128">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="9ddc6-129">Исправлено: виртуальные учетные записи теперь поддерживаются в Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="9ddc6-129">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>
<span data-ttu-id="9ddc6-130">Теперь в WMF 5.1 вы можете использовать виртуальные учетные записи в Windows Server 2008 R2, включив согласованные конфигурации и паритет функций в Windows Server 2008 R2 — 2016.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-130">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span>
<span data-ttu-id="9ddc6-131">Виртуальные учетные записи по-прежнему не поддерживаются при использовании JEA в Windows 7.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-131">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>

