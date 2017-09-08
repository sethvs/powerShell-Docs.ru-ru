---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "получение pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: 43997320ec7ab779b2061a0af88f97db0b7e93d6
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
#  <a name="get-pswaauthorizationrule"></a><span data-ttu-id="7c92d-103">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="7c92d-103">Get-PswaAuthorizationRule</span></span>

##  <a name="synopsis"></a><span data-ttu-id="7c92d-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="7c92d-104">SYNOPSIS</span></span>

<span data-ttu-id="7c92d-105">Возвращает набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="7c92d-105">Returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>

##  <a name="syntax"></a><span data-ttu-id="7c92d-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7c92d-106">Syntax</span></span>

###  <a name="id"></a><span data-ttu-id="7c92d-107">ID</span><span class="sxs-lookup"><span data-stu-id="7c92d-107">ID</span></span>
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

###  <a name="name"></a><span data-ttu-id="7c92d-108">Название</span><span class="sxs-lookup"><span data-stu-id="7c92d-108">Name</span></span>
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="7c92d-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="7c92d-109">DESCRIPTION</span></span>

<span data-ttu-id="7c92d-110">Командлет **Get-PswaAuthorizationRule** возвращает набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="7c92d-110">The **Get-PswaAuthorizationRule** cmdlet returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>
<span data-ttu-id="7c92d-111">Если не заданы параметры **Id** или **RuleName**, этот командлет перечисляет все правила.</span><span class="sxs-lookup"><span data-stu-id="7c92d-111">If neither the **Id** parameter nor the **RuleName** parameter is specified, then this cmdlet lists all rules.</span></span> <span data-ttu-id="7c92d-112">Параметр **Id** можно использовать для фильтрации результатов.</span><span class="sxs-lookup"><span data-stu-id="7c92d-112">The **Id** parameter can be used to filter the results.</span></span>

## <a name="parameters"></a><span data-ttu-id="7c92d-113">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="7c92d-113">PARAMETERS</span></span>

### <a name="-idltint32gt"></a><span data-ttu-id="7c92d-114">-Id&lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="7c92d-114">-Id&lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="7c92d-115">Указывает идентификаторы (ID) правил, которые должен получить этот командлет.</span><span class="sxs-lookup"><span data-stu-id="7c92d-115">Specifies the identifiers (IDs) of the rules that this cmdlet should get.</span></span> <span data-ttu-id="7c92d-116">Если идентификаторы не указаны, этот командлет возвращает все правила авторизации.</span><span class="sxs-lookup"><span data-stu-id="7c92d-116">If no IDs are specified, then this cmdlet returns all authorization rules.</span></span>

|||  
|-|-|
| <span data-ttu-id="7c92d-117">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="7c92d-117">Aliases</span></span>                              | <span data-ttu-id="7c92d-118">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="7c92d-118">none</span></span>                                 |
| <span data-ttu-id="7c92d-119">Требуется?</span><span class="sxs-lookup"><span data-stu-id="7c92d-119">Required?</span></span>                            | <span data-ttu-id="7c92d-120">false</span><span class="sxs-lookup"><span data-stu-id="7c92d-120">false</span></span>                                |
| <span data-ttu-id="7c92d-121">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="7c92d-121">Position?</span></span>                            | <span data-ttu-id="7c92d-122">2</span><span class="sxs-lookup"><span data-stu-id="7c92d-122">2</span></span>                                    |
| <span data-ttu-id="7c92d-123">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7c92d-123">Default Value</span></span>                        | <span data-ttu-id="7c92d-124">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="7c92d-124">none</span></span>                                 |
| <span data-ttu-id="7c92d-125">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="7c92d-125">Accept Pipeline Input?</span></span>               | <span data-ttu-id="7c92d-126">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="7c92d-126">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="7c92d-127">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="7c92d-127">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="7c92d-128">false</span><span class="sxs-lookup"><span data-stu-id="7c92d-128">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="7c92d-129">-RuleName&lt;строка\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="7c92d-129">-RuleName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="7c92d-130">Указывает имена правил авторизации для получения.</span><span class="sxs-lookup"><span data-stu-id="7c92d-130">Specifies the names of authorization rules to retrieve.</span></span> <span data-ttu-id="7c92d-131">Этот параметр возвращает все правила, имена которых точно соответствуют именам правил в строках этого массива.</span><span class="sxs-lookup"><span data-stu-id="7c92d-131">This parameter returns any rules that exactly match the rule names of the strings in this array.</span></span>

|||  
|-|-|
| <span data-ttu-id="7c92d-132">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="7c92d-132">Aliases</span></span>                              | <span data-ttu-id="7c92d-133">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="7c92d-133">none</span></span>                                 |
| <span data-ttu-id="7c92d-134">Требуется?</span><span class="sxs-lookup"><span data-stu-id="7c92d-134">Required?</span></span>                            | <span data-ttu-id="7c92d-135">верно</span><span class="sxs-lookup"><span data-stu-id="7c92d-135">true</span></span>                                 |
| <span data-ttu-id="7c92d-136">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="7c92d-136">Position?</span></span>                            | <span data-ttu-id="7c92d-137">2</span><span class="sxs-lookup"><span data-stu-id="7c92d-137">2</span></span>                                    |
| <span data-ttu-id="7c92d-138">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7c92d-138">Default Value</span></span>                        | <span data-ttu-id="7c92d-139">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="7c92d-139">none</span></span>                                 |
| <span data-ttu-id="7c92d-140">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="7c92d-140">Accept Pipeline Input?</span></span>               | <span data-ttu-id="7c92d-141">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="7c92d-141">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="7c92d-142">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="7c92d-142">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="7c92d-143">false</span><span class="sxs-lookup"><span data-stu-id="7c92d-143">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="7c92d-144">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="7c92d-144">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="7c92d-145">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="7c92d-145">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="7c92d-146">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="7c92d-146">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="7c92d-147">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="7c92d-147">INPUTS</span></span>

###  <a name="int"></a><span data-ttu-id="7c92d-148">int\[\]</span><span class="sxs-lookup"><span data-stu-id="7c92d-148">int\[\]</span></span>

<span data-ttu-id="7c92d-149">Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="7c92d-149">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

###  <a name="string"></a><span data-ttu-id="7c92d-150">String\[\]</span><span class="sxs-lookup"><span data-stu-id="7c92d-150">String\[\]</span></span>

<span data-ttu-id="7c92d-151">Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="7c92d-151">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

##  <a name="outputs"></a><span data-ttu-id="7c92d-152">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="7c92d-152">OUTPUTS</span></span>

###  <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="7c92d-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="7c92d-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="7c92d-154">Этот командлет создает объект PswaAuthorizationRule в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="7c92d-154">This cmdlet produces a PswaAuthorizationRule object as output.</span></span>


## <a name="examples"></a><span data-ttu-id="7c92d-155">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="7c92d-155">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="7c92d-156">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="7c92d-156">EXAMPLE 1</span></span>

<span data-ttu-id="7c92d-157">Этот пример получает все правила.</span><span class="sxs-lookup"><span data-stu-id="7c92d-157">This example gets all of the rules.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a><span data-ttu-id="7c92d-158">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="7c92d-158">EXAMPLE 2</span></span>

<span data-ttu-id="7c92d-159">Этот пример получает правило с идентификатором *2*.</span><span class="sxs-lookup"><span data-stu-id="7c92d-159">This example gets a rule with an ID of *2*.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="7c92d-160">ПРИМЕР 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="7c92d-160">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="7c92d-161">В этом примере показано, как командлет принимает значение из конвейера.</span><span class="sxs-lookup"><span data-stu-id="7c92d-161">This example illustrates how the cmdlet accepts a value from pipeline.</span></span>
<span data-ttu-id="7c92d-162">В этот командлет передаются идентификатор и имя правила.</span><span class="sxs-lookup"><span data-stu-id="7c92d-162">A rule id and a rule name are passed in this cmdlet.</span></span>

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

##  <a name="related-topics"></a><span data-ttu-id="7c92d-163">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="7c92d-163">Related topics</span></span>

-  [<span data-ttu-id="7c92d-164">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="7c92d-164">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
-  [<span data-ttu-id="7c92d-165">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="7c92d-165">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
-  [<span data-ttu-id="7c92d-166">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="7c92d-166">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
-  [<span data-ttu-id="7c92d-167">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="7c92d-167">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
