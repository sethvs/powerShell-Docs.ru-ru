---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Ресурс User в DSC"
ms.openlocfilehash: c1b8487d9adc899950d185036ada3a2fa3747417
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
#<a name="dsc-user-resource"></a><span data-ttu-id="6f322-103">Ресурс User в DSC</span><span class="sxs-lookup"><span data-stu-id="6f322-103">DSC User Resource#</span></span>

 
><span data-ttu-id="6f322-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6f322-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="6f322-105">Ресурс __User__ в DSC Windows PowerShell предоставляет механизм управления локальными учетными записями на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="6f322-105">The __User__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>


##<a name="syntax"></a><span data-ttu-id="6f322-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6f322-106">Syntax##</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="6f322-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="6f322-107">Properties</span></span>
|  <span data-ttu-id="6f322-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="6f322-108">Property</span></span>  |  <span data-ttu-id="6f322-109">Описание</span><span class="sxs-lookup"><span data-stu-id="6f322-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="6f322-110">UserName</span><span class="sxs-lookup"><span data-stu-id="6f322-110">UserName</span></span>| <span data-ttu-id="6f322-111">Указывает имя учетной записи, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="6f322-111">Indicates the account name for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="6f322-112">Описание</span><span class="sxs-lookup"><span data-stu-id="6f322-112">Description</span></span>| <span data-ttu-id="6f322-113">Указывает описание учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6f322-113">Indicates the description you want to use for the user account.</span></span>| 
| <span data-ttu-id="6f322-114">Отключен</span><span class="sxs-lookup"><span data-stu-id="6f322-114">Disabled</span></span>| <span data-ttu-id="6f322-115">Указывает, включена ли учетная запись.</span><span class="sxs-lookup"><span data-stu-id="6f322-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="6f322-116">Присвойте этому свойству значение __$true__, чтобы отключить учетную запись, и __$false__, чтобы включить ее.</span><span class="sxs-lookup"><span data-stu-id="6f322-116">Set this property to __$true__ to ensure that this account is disabled, and set it to __$false__ to ensure that it is enabled.</span></span>| 
| <span data-ttu-id="6f322-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="6f322-117">Ensure</span></span>| <span data-ttu-id="6f322-118">Указывает, существует ли учетная запись.</span><span class="sxs-lookup"><span data-stu-id="6f322-118">Indicates if the account exists.</span></span> <span data-ttu-id="6f322-119">Присвойте этому свойству значение Present, если учетная запись существует, и Absent, если не существует.</span><span class="sxs-lookup"><span data-stu-id="6f322-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>| 
| <span data-ttu-id="6f322-120">FullName</span><span class="sxs-lookup"><span data-stu-id="6f322-120">FullName</span></span>| <span data-ttu-id="6f322-121">Представляет строку с полным именем для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="6f322-121">Represents a string with the full name you want to use for the user account.</span></span>| 
| <span data-ttu-id="6f322-122">Пароль</span><span class="sxs-lookup"><span data-stu-id="6f322-122">Password</span></span>| <span data-ttu-id="6f322-123">Указывает пароль для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6f322-123">Indicates the password you want to use for this account.</span></span> | 
| <span data-ttu-id="6f322-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="6f322-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="6f322-125">Указывает, может ли пользователь изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="6f322-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="6f322-126">Присвойте этому свойству значение __$true__, чтобы пользователь не мог изменить пароль, и __$false__, чтобы мог.</span><span class="sxs-lookup"><span data-stu-id="6f322-126">Set this property to __$true__ to ensure that the user cannot change the password, and set it to __$false__ to allow the user to change the password.</span></span> <span data-ttu-id="6f322-127">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="6f322-127">The default value is __$false__.</span></span>| 
| <span data-ttu-id="6f322-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="6f322-128">PasswordChangeRequired</span></span>| <span data-ttu-id="6f322-129">Указывает, требуется ли смена пароля при следующем входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="6f322-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="6f322-130">Присвойте этому свойству значение __$true__, если пользователь должен изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="6f322-130">Set this property to __$true__ if the user must change the password.</span></span> <span data-ttu-id="6f322-131">По умолчанию используется значение __$true__.</span><span class="sxs-lookup"><span data-stu-id="6f322-131">The default value is __$true__.</span></span>| 
| <span data-ttu-id="6f322-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="6f322-132">PasswordNeverExpires</span></span>| <span data-ttu-id="6f322-133">Указывает, может ли истечь срок действия пароля.</span><span class="sxs-lookup"><span data-stu-id="6f322-133">Indicates if the password will expire.</span></span> <span data-ttu-id="6f322-134">Присвойте этому свойству значение __$true__, чтобы срок действия пароля никогда не истекал, и __$false__ в противном случае.</span><span class="sxs-lookup"><span data-stu-id="6f322-134">To ensure that the password for this account will never expire, set this property to __$true__, and set it to __$false__ if the password will expire.</span></span> <span data-ttu-id="6f322-135">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="6f322-135">The default value is __$false__.</span></span>| 
| <span data-ttu-id="6f322-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="6f322-136">DependsOn</span></span> | <span data-ttu-id="6f322-137">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="6f322-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6f322-138">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="6f322-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="6f322-139">Пример</span><span class="sxs-lookup"><span data-stu-id="6f322-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```

