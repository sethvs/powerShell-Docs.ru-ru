---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,конфигурация,установка
title: Ресурс Registry в DSC
ms.openlocfilehash: fcd24b1dd729dbb0abd697a4a628dce01fdd5422
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-registry-resource"></a><span data-ttu-id="7cfd4-103">Ресурс Registry в DSC</span><span class="sxs-lookup"><span data-stu-id="7cfd4-103">DSC Registry Resource</span></span>

> <span data-ttu-id="7cfd4-104">Область применения: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7cfd4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="7cfd4-105">Ресурс **Registry** в DSC Windows PowerShell предоставляет механизм управления разделами и значениями реестра на целевом узле.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7cfd4-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7cfd4-106">Syntax</span></span>

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a><span data-ttu-id="7cfd4-107">Свойства</span><span class="sxs-lookup"><span data-stu-id="7cfd4-107">Properties</span></span>
|  <span data-ttu-id="7cfd4-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="7cfd4-108">Property</span></span>  |  <span data-ttu-id="7cfd4-109">Описание</span><span class="sxs-lookup"><span data-stu-id="7cfd4-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="7cfd4-110">Клавиши</span><span class="sxs-lookup"><span data-stu-id="7cfd4-110">Key</span></span>| <span data-ttu-id="7cfd4-111">Указывает путь к разделу реестра, для которого требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="7cfd4-112">Этот путь должен включать куст.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-112">This path must include the hive.</span></span>|
| <span data-ttu-id="7cfd4-113">ValueName</span><span class="sxs-lookup"><span data-stu-id="7cfd4-113">ValueName</span></span>| <span data-ttu-id="7cfd4-114">Указывает имя значения реестра.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="7cfd4-115">Чтобы добавить или удалить раздел реестра, укажите это свойство как пустую строку, не указывая ValueType или ValueData.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="7cfd4-116">Чтобы изменить или удалить значение по умолчанию раздела реестра, укажите это свойство как пустую строку, указав ValueType или ValueData.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>|
| <span data-ttu-id="7cfd4-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="7cfd4-117">Ensure</span></span>| <span data-ttu-id="7cfd4-118">Указывает, существует ли ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="7cfd4-119">Для этого укажите для этого свойства значение Present.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="7cfd4-120">Чтобы они не существовали, укажите для этого свойства значение Absent.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="7cfd4-121">Значение по умолчанию — Present.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-121">The default value is "Present".</span></span>|
| <span data-ttu-id="7cfd4-122">Force</span><span class="sxs-lookup"><span data-stu-id="7cfd4-122">Force</span></span>| <span data-ttu-id="7cfd4-123">Если указанный раздел реестра присутствует, __Force__ перезаписывает его новым значением.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-123">If the specified registry key is present, __Force__ overwrites it with the new value.</span></span> <span data-ttu-id="7cfd4-124">При удалении раздела реестра с подразделами необходимо выбрать __$true__</span><span class="sxs-lookup"><span data-stu-id="7cfd4-124">If deleting a registry key with subkeys, this needs to be __$true__</span></span>|
| <span data-ttu-id="7cfd4-125">Hex</span><span class="sxs-lookup"><span data-stu-id="7cfd4-125">Hex</span></span>| <span data-ttu-id="7cfd4-126">Указывает, будут ли данные выражены в шестнадцатеричном формате.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="7cfd4-127">Если свойство задано, данные значения DWORD/QWORD будут представлены в шестнадцатеричном формате.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="7cfd4-128">Недопустимо для других типов.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-128">Not valid for other types.</span></span> <span data-ttu-id="7cfd4-129">Значение по умолчанию — __$false__.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-129">The default value is __$false__.</span></span>|
| <span data-ttu-id="7cfd4-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="7cfd4-130">DependsOn</span></span>| <span data-ttu-id="7cfd4-131">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7cfd4-132">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — __ResourceName__, а его тип — __ResourceType__, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-132">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="7cfd4-133">ValueData</span><span class="sxs-lookup"><span data-stu-id="7cfd4-133">ValueData</span></span>| <span data-ttu-id="7cfd4-134">Данные для значения реестра.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-134">The data for the registry value.</span></span>|
| <span data-ttu-id="7cfd4-135">ValueType</span><span class="sxs-lookup"><span data-stu-id="7cfd4-135">ValueType</span></span>| <span data-ttu-id="7cfd4-136">Указывает тип значения.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-136">Indicates the type of the value.</span></span> <span data-ttu-id="7cfd4-137">Поддерживаемые типы:</span><span class="sxs-lookup"><span data-stu-id="7cfd4-137">The supported types are:</span></span>
<ul><li><span data-ttu-id="7cfd4-138">строка (REG_SZ);</span><span class="sxs-lookup"><span data-stu-id="7cfd4-138">String (REG_SZ)</span></span></li>


<li><span data-ttu-id="7cfd4-139">двоичный файл (REG-BINARY);</span><span class="sxs-lookup"><span data-stu-id="7cfd4-139">Binary (REG-BINARY)</span></span></li>


<li><span data-ttu-id="7cfd4-140">Dword, 32-разрядный (REG_DWORD);</span><span class="sxs-lookup"><span data-stu-id="7cfd4-140">Dword 32-bit (REG_DWORD)</span></span></li>


<li><span data-ttu-id="7cfd4-141">Qword, 64-разрядный (REG_QWORD);</span><span class="sxs-lookup"><span data-stu-id="7cfd4-141">Qword 64-bit (REG_QWORD)</span></span></li>


<li><span data-ttu-id="7cfd4-142">несколько строк (REG_MULTI_SZ);</span><span class="sxs-lookup"><span data-stu-id="7cfd4-142">Multi-string (REG_MULTI_SZ)</span></span></li>


<li><span data-ttu-id="7cfd4-143">расширяемая строка (REG_EXPAND_SZ).</span><span class="sxs-lookup"><span data-stu-id="7cfd4-143">Expandable string (REG_EXPAND_SZ)</span></span></li></ul>

## <a name="example"></a><span data-ttu-id="7cfd4-144">Пример</span><span class="sxs-lookup"><span data-stu-id="7cfd4-144">Example</span></span>
<span data-ttu-id="7cfd4-145">В этом примере гарантируется, что ключ с именем ExampleKey присутствует в кусте **HKEY\_LOCAL\_MACHINE**.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-145">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>
```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

><span data-ttu-id="7cfd4-146">**Примечание.** Для изменения настройки реестра в кусте **HKEY\_CURRENT\_USER** требуется запустить конфигурацию с использованием учетных данных пользователя, а не системных.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-146">**Note:** Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span>
><span data-ttu-id="7cfd4-147">Вы можете использовать свойство **PsDscRunAsCredential**, чтобы указать учетные данные пользователя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7cfd4-147">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="7cfd4-148">Пример см. в статье [Запуск DSC с использованием учетных данных пользователя](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="7cfd4-148">For an example, see [Running DSC with user credentials](runAsUser.md)</span></span>