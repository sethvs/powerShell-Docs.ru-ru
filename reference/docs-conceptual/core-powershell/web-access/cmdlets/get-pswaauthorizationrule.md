---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: получение pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 74c044c329d8b6a305b86c9056a7041fb5fd046b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="get-pswaauthorizationrule"></a><span data-ttu-id="8f8c2-103">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8f8c2-103">Get-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="8f8c2-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="8f8c2-104">SYNOPSIS</span></span>

<span data-ttu-id="8f8c2-105">Возвращает набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-105">Returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>

## <a name="syntax"></a><span data-ttu-id="8f8c2-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="8f8c2-106">Syntax</span></span>

### <a name="id"></a><span data-ttu-id="8f8c2-107">ID</span><span class="sxs-lookup"><span data-stu-id="8f8c2-107">ID</span></span>
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a><span data-ttu-id="8f8c2-108">Name</span><span class="sxs-lookup"><span data-stu-id="8f8c2-108">Name</span></span>
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="8f8c2-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="8f8c2-109">DESCRIPTION</span></span>

<span data-ttu-id="8f8c2-110">Командлет **Get-PswaAuthorizationRule** возвращает набор правил авторизации Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-110">The **Get-PswaAuthorizationRule** cmdlet returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>
<span data-ttu-id="8f8c2-111">Если не заданы параметры **Id** или **RuleName**, этот командлет перечисляет все правила.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-111">If neither the **Id** parameter nor the **RuleName** parameter is specified, then this cmdlet lists all rules.</span></span> <span data-ttu-id="8f8c2-112">Параметр **Id** можно использовать для фильтрации результатов.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-112">The **Id** parameter can be used to filter the results.</span></span>

## <a name="parameters"></a><span data-ttu-id="8f8c2-113">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="8f8c2-113">PARAMETERS</span></span>

### <a name="-idltint32gt"></a><span data-ttu-id="8f8c2-114">-Id&lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="8f8c2-114">-Id&lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="8f8c2-115">Указывает идентификаторы (ID) правил, которые должен получить этот командлет.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-115">Specifies the identifiers (IDs) of the rules that this cmdlet should get.</span></span> <span data-ttu-id="8f8c2-116">Если идентификаторы не указаны, этот командлет возвращает все правила авторизации.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-116">If no IDs are specified, then this cmdlet returns all authorization rules.</span></span>

|||
|-|-|
| <span data-ttu-id="8f8c2-117">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="8f8c2-117">Aliases</span></span>                              | <span data-ttu-id="8f8c2-118">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="8f8c2-118">none</span></span>                                 |
| <span data-ttu-id="8f8c2-119">Требуется?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-119">Required?</span></span>                            | <span data-ttu-id="8f8c2-120">false</span><span class="sxs-lookup"><span data-stu-id="8f8c2-120">false</span></span>                                |
| <span data-ttu-id="8f8c2-121">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-121">Position?</span></span>                            | <span data-ttu-id="8f8c2-122">2</span><span class="sxs-lookup"><span data-stu-id="8f8c2-122">2</span></span>                                    |
| <span data-ttu-id="8f8c2-123">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8f8c2-123">Default Value</span></span>                        | <span data-ttu-id="8f8c2-124">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="8f8c2-124">none</span></span>                                 |
| <span data-ttu-id="8f8c2-125">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-125">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8f8c2-126">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="8f8c2-126">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="8f8c2-127">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-127">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8f8c2-128">false</span><span class="sxs-lookup"><span data-stu-id="8f8c2-128">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="8f8c2-129">-RuleName&lt;строка\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="8f8c2-129">-RuleName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="8f8c2-130">Указывает имена правил авторизации для получения.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-130">Specifies the names of authorization rules to retrieve.</span></span> <span data-ttu-id="8f8c2-131">Этот параметр возвращает все правила, имена которых точно соответствуют именам правил в строках этого массива.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-131">This parameter returns any rules that exactly match the rule names of the strings in this array.</span></span>

|||
|-|-|
| <span data-ttu-id="8f8c2-132">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="8f8c2-132">Aliases</span></span>                              | <span data-ttu-id="8f8c2-133">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="8f8c2-133">none</span></span>                                 |
| <span data-ttu-id="8f8c2-134">Требуется?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-134">Required?</span></span>                            | <span data-ttu-id="8f8c2-135">верно</span><span class="sxs-lookup"><span data-stu-id="8f8c2-135">true</span></span>                                 |
| <span data-ttu-id="8f8c2-136">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-136">Position?</span></span>                            | <span data-ttu-id="8f8c2-137">2</span><span class="sxs-lookup"><span data-stu-id="8f8c2-137">2</span></span>                                    |
| <span data-ttu-id="8f8c2-138">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8f8c2-138">Default Value</span></span>                        | <span data-ttu-id="8f8c2-139">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="8f8c2-139">none</span></span>                                 |
| <span data-ttu-id="8f8c2-140">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-140">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8f8c2-141">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="8f8c2-141">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="8f8c2-142">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="8f8c2-142">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8f8c2-143">false</span><span class="sxs-lookup"><span data-stu-id="8f8c2-143">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="8f8c2-144">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="8f8c2-144">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="8f8c2-145">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-145">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="8f8c2-146">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="8f8c2-146">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="8f8c2-147">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="8f8c2-147">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="8f8c2-148">int\[\]</span><span class="sxs-lookup"><span data-stu-id="8f8c2-148">int\[\]</span></span>

<span data-ttu-id="8f8c2-149">Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-149">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

### <a name="string"></a><span data-ttu-id="8f8c2-150">String\[\]</span><span class="sxs-lookup"><span data-stu-id="8f8c2-150">String\[\]</span></span>

<span data-ttu-id="8f8c2-151">Этот командлет принимает массив целых чисел или массив строковых значений в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-151">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="8f8c2-152">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="8f8c2-152">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="8f8c2-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="8f8c2-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="8f8c2-154">Этот командлет создает объект PswaAuthorizationRule в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-154">This cmdlet produces a PswaAuthorizationRule object as output.</span></span>


## <a name="examples"></a><span data-ttu-id="8f8c2-155">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="8f8c2-155">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="8f8c2-156">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="8f8c2-156">EXAMPLE 1</span></span>

<span data-ttu-id="8f8c2-157">Этот пример получает все правила.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-157">This example gets all of the rules.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a><span data-ttu-id="8f8c2-158">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="8f8c2-158">EXAMPLE 2</span></span>

<span data-ttu-id="8f8c2-159">Этот пример получает правило с идентификатором *2*.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-159">This example gets a rule with an ID of *2*.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="8f8c2-160">ПРИМЕР 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="8f8c2-160">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="8f8c2-161">В этом примере показано, как командлет принимает значение из конвейера.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-161">This example illustrates how the cmdlet accepts a value from pipeline.</span></span>
<span data-ttu-id="8f8c2-162">В этот командлет передаются идентификатор и имя правила.</span><span class="sxs-lookup"><span data-stu-id="8f8c2-162">A rule id and a rule name are passed in this cmdlet.</span></span>

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a><span data-ttu-id="8f8c2-163">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="8f8c2-163">Related topics</span></span>

- [<span data-ttu-id="8f8c2-164">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8f8c2-164">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="8f8c2-165">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8f8c2-165">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="8f8c2-166">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8f8c2-166">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
- [<span data-ttu-id="8f8c2-167">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="8f8c2-167">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)