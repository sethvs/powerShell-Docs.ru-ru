---
description: 
ms.topic: article
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "удаление pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: 4d039e7e00f87bc7aebb89217251edbbb5c3f5be
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="remove-pswaauthorizationrule"></a><span data-ttu-id="2ef40-103">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2ef40-103">Remove-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="2ef40-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="2ef40-104">SYNOPSIS</span></span>

<span data-ttu-id="2ef40-105">Удаляет указанное правило авторизации из Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="2ef40-105">Removes a specified authorization rule from Windows PowerShell® Web Access.</span></span>

## <a name="syntax"></a><span data-ttu-id="2ef40-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="2ef40-106">SYNTAX</span></span>

### <a name="id"></a><span data-ttu-id="2ef40-107">Id</span><span class="sxs-lookup"><span data-stu-id="2ef40-107">Id</span></span>
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a><span data-ttu-id="2ef40-108">Правило</span><span class="sxs-lookup"><span data-stu-id="2ef40-108">Rule</span></span>
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="2ef40-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="2ef40-109">DESCRIPTION</span></span>

<span data-ttu-id="2ef40-110">Удаляет указанное правило авторизации из Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="2ef40-110">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="parameters"></a><span data-ttu-id="2ef40-111">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="2ef40-111">PARAMETERS</span></span>

### <a name="-force"></a><span data-ttu-id="2ef40-112">-Force</span><span class="sxs-lookup"><span data-stu-id="2ef40-112">-Force</span></span>

<span data-ttu-id="2ef40-113">Запуск командлета без запроса на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="2ef40-113">Runs the cmdlet without prompting for confirmation.</span></span> <span data-ttu-id="2ef40-114">По умолчанию командлет запрашивает подтверждение, прежде чем продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="2ef40-114">By default the cmdlet asks for confirmation before proceeding.</span></span>

|||  
|-|-|
| <span data-ttu-id="2ef40-115">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="2ef40-115">Aliases</span></span>                              | <span data-ttu-id="2ef40-116">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-116">none</span></span>                                 |
| <span data-ttu-id="2ef40-117">Требуется?</span><span class="sxs-lookup"><span data-stu-id="2ef40-117">Required?</span></span>                            | <span data-ttu-id="2ef40-118">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-118">false</span></span>                                |
| <span data-ttu-id="2ef40-119">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="2ef40-119">Position?</span></span>                            | <span data-ttu-id="2ef40-120">с именем</span><span class="sxs-lookup"><span data-stu-id="2ef40-120">named</span></span>                                |
| <span data-ttu-id="2ef40-121">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ef40-121">Default Value</span></span>                        | <span data-ttu-id="2ef40-122">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-122">none</span></span>                                 |
| <span data-ttu-id="2ef40-123">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="2ef40-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="2ef40-124">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-124">false</span></span>                                |
| <span data-ttu-id="2ef40-125">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="2ef40-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="2ef40-126">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-126">false</span></span>                                |

### <a name="-id-ltint32gt"></a><span data-ttu-id="2ef40-127">-Id &lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="2ef40-127">-Id &lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="2ef40-128">Указывает идентификаторы (ID) одного или нескольких удаляемых правил.</span><span class="sxs-lookup"><span data-stu-id="2ef40-128">Specifies the identifiers (IDs) of one or more rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="2ef40-129">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="2ef40-129">Aliases</span></span>                              | <span data-ttu-id="2ef40-130">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-130">none</span></span>                                 |
| <span data-ttu-id="2ef40-131">Требуется?</span><span class="sxs-lookup"><span data-stu-id="2ef40-131">Required?</span></span>                            | <span data-ttu-id="2ef40-132">верно</span><span class="sxs-lookup"><span data-stu-id="2ef40-132">true</span></span>                                 |
| <span data-ttu-id="2ef40-133">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="2ef40-133">Position?</span></span>                            | <span data-ttu-id="2ef40-134">2</span><span class="sxs-lookup"><span data-stu-id="2ef40-134">2</span></span>                                    |
| <span data-ttu-id="2ef40-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ef40-135">Default Value</span></span>                        | <span data-ttu-id="2ef40-136">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-136">none</span></span>                                 |
| <span data-ttu-id="2ef40-137">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="2ef40-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="2ef40-138">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="2ef40-138">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="2ef40-139">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="2ef40-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="2ef40-140">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-140">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="2ef40-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="2ef40-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="2ef40-142">Указывает правила, которые необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="2ef40-142">Specifies the rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="2ef40-143">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="2ef40-143">Aliases</span></span>                              | <span data-ttu-id="2ef40-144">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-144">none</span></span>                                 |
| <span data-ttu-id="2ef40-145">Требуется?</span><span class="sxs-lookup"><span data-stu-id="2ef40-145">Required?</span></span>                            | <span data-ttu-id="2ef40-146">верно</span><span class="sxs-lookup"><span data-stu-id="2ef40-146">true</span></span>                                 |
| <span data-ttu-id="2ef40-147">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="2ef40-147">Position?</span></span>                            | <span data-ttu-id="2ef40-148">2</span><span class="sxs-lookup"><span data-stu-id="2ef40-148">2</span></span>                                    |
| <span data-ttu-id="2ef40-149">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ef40-149">Default Value</span></span>                        | <span data-ttu-id="2ef40-150">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="2ef40-150">none</span></span>                                 |
| <span data-ttu-id="2ef40-151">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="2ef40-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="2ef40-152">True (ByValue)</span><span class="sxs-lookup"><span data-stu-id="2ef40-152">True (ByValue)</span></span>                       |
| <span data-ttu-id="2ef40-153">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="2ef40-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="2ef40-154">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="2ef40-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="2ef40-155">-Confirm</span></span>

<span data-ttu-id="2ef40-156">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="2ef40-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="2ef40-157">Требуется?</span><span class="sxs-lookup"><span data-stu-id="2ef40-157">Required?</span></span>                            | <span data-ttu-id="2ef40-158">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-158">false</span></span>                                |
| <span data-ttu-id="2ef40-159">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="2ef40-159">Position?</span></span>                            | <span data-ttu-id="2ef40-160">с именем</span><span class="sxs-lookup"><span data-stu-id="2ef40-160">named</span></span>                                |
| <span data-ttu-id="2ef40-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ef40-161">Default Value</span></span>                        | <span data-ttu-id="2ef40-162">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-162">false</span></span>                                |
| <span data-ttu-id="2ef40-163">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="2ef40-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="2ef40-164">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-164">false</span></span>                                |
| <span data-ttu-id="2ef40-165">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="2ef40-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="2ef40-166">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="2ef40-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="2ef40-167">-WhatIf</span></span>

<span data-ttu-id="2ef40-168">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="2ef40-168">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="2ef40-169">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="2ef40-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="2ef40-170">Требуется?</span><span class="sxs-lookup"><span data-stu-id="2ef40-170">Required?</span></span>                            | <span data-ttu-id="2ef40-171">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-171">false</span></span>                                |
| <span data-ttu-id="2ef40-172">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="2ef40-172">Position?</span></span>                            | <span data-ttu-id="2ef40-173">с именем</span><span class="sxs-lookup"><span data-stu-id="2ef40-173">named</span></span>                                |
| <span data-ttu-id="2ef40-174">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2ef40-174">Default Value</span></span>                        | <span data-ttu-id="2ef40-175">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-175">false</span></span>                                |
| <span data-ttu-id="2ef40-176">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="2ef40-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="2ef40-177">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-177">false</span></span>                                |
| <span data-ttu-id="2ef40-178">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="2ef40-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="2ef40-179">false</span><span class="sxs-lookup"><span data-stu-id="2ef40-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="2ef40-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="2ef40-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="2ef40-181">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="2ef40-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="2ef40-182">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="2ef40-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="2ef40-183">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="2ef40-183">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="2ef40-184">int\[\]</span><span class="sxs-lookup"><span data-stu-id="2ef40-184">int\[\]</span></span>

<span data-ttu-id="2ef40-185">Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="2ef40-185">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

### <a name="pswaauthorizationrule"></a><span data-ttu-id="2ef40-186">PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="2ef40-186">PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="2ef40-187">Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="2ef40-187">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

## <a name="outputs"></a><span data-ttu-id="2ef40-188">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="2ef40-188">OUTPUTS</span></span>

<span data-ttu-id="2ef40-189">Этот командлет не создает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2ef40-189">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="2ef40-190">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="2ef40-190">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="2ef40-191">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="2ef40-191">EXAMPLE 1</span></span>

<span data-ttu-id="2ef40-192">Этот пример удаляет правило авторизации с идентификатором *2*.</span><span class="sxs-lookup"><span data-stu-id="2ef40-192">This example removes the authorization rule with an ID of *2*.</span></span>

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a><span data-ttu-id="2ef40-193">ПРИМЕР 2 {#example-2 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="2ef40-193">EXAMPLE 2 {#example-2 .subHeading}</span></span>

<span data-ttu-id="2ef40-194">Этот пример удаляет все правила авторизации, а также требует подтверждения пользователя.</span><span class="sxs-lookup"><span data-stu-id="2ef40-194">This example removes all authorization rules and also requires confirmation by the user.</span></span>

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a><span data-ttu-id="2ef40-195">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="2ef40-195">Related topics</span></span>

- [<span data-ttu-id="2ef40-196">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2ef40-196">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="2ef40-197">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2ef40-197">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="2ef40-198">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="2ef40-198">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="2ef40-199">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="2ef40-199">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
