---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "удаление pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: a8304b68a446de0be98aa732304c71302fb8389e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="remove-pswaauthorizationrule"></a><span data-ttu-id="bee50-103">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="bee50-103">Remove-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="bee50-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="bee50-104">SYNOPSIS</span></span>

<span data-ttu-id="bee50-105">Удаляет указанное правило авторизации из Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="bee50-105">Removes a specified authorization rule from Windows PowerShell® Web Access.</span></span>

## <a name="syntax"></a><span data-ttu-id="bee50-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="bee50-106">SYNTAX</span></span>

### <a name="id"></a><span data-ttu-id="bee50-107">Id</span><span class="sxs-lookup"><span data-stu-id="bee50-107">Id</span></span>
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a><span data-ttu-id="bee50-108">Правило</span><span class="sxs-lookup"><span data-stu-id="bee50-108">Rule</span></span>
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="bee50-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="bee50-109">DESCRIPTION</span></span>

<span data-ttu-id="bee50-110">Удаляет указанное правило авторизации из Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="bee50-110">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="parameters"></a><span data-ttu-id="bee50-111">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="bee50-111">PARAMETERS</span></span>

### <a name="-force"></a><span data-ttu-id="bee50-112">-Force</span><span class="sxs-lookup"><span data-stu-id="bee50-112">-Force</span></span>

<span data-ttu-id="bee50-113">Запуск командлета без запроса на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="bee50-113">Runs the cmdlet without prompting for confirmation.</span></span> <span data-ttu-id="bee50-114">По умолчанию командлет запрашивает подтверждение, прежде чем продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="bee50-114">By default the cmdlet asks for confirmation before proceeding.</span></span>

|||  
|-|-|
| <span data-ttu-id="bee50-115">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="bee50-115">Aliases</span></span>                              | <span data-ttu-id="bee50-116">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-116">none</span></span>                                 |
| <span data-ttu-id="bee50-117">Требуется?</span><span class="sxs-lookup"><span data-stu-id="bee50-117">Required?</span></span>                            | <span data-ttu-id="bee50-118">false</span><span class="sxs-lookup"><span data-stu-id="bee50-118">false</span></span>                                |
| <span data-ttu-id="bee50-119">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="bee50-119">Position?</span></span>                            | <span data-ttu-id="bee50-120">с именем</span><span class="sxs-lookup"><span data-stu-id="bee50-120">named</span></span>                                |
| <span data-ttu-id="bee50-121">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bee50-121">Default Value</span></span>                        | <span data-ttu-id="bee50-122">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-122">none</span></span>                                 |
| <span data-ttu-id="bee50-123">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="bee50-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="bee50-124">false</span><span class="sxs-lookup"><span data-stu-id="bee50-124">false</span></span>                                |
| <span data-ttu-id="bee50-125">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="bee50-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="bee50-126">false</span><span class="sxs-lookup"><span data-stu-id="bee50-126">false</span></span>                                |

### <a name="-id-ltint32gt"></a><span data-ttu-id="bee50-127">-Id &lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="bee50-127">-Id &lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="bee50-128">Указывает идентификаторы (ID) одного или нескольких удаляемых правил.</span><span class="sxs-lookup"><span data-stu-id="bee50-128">Specifies the identifiers (IDs) of one or more rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="bee50-129">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="bee50-129">Aliases</span></span>                              | <span data-ttu-id="bee50-130">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-130">none</span></span>                                 |
| <span data-ttu-id="bee50-131">Требуется?</span><span class="sxs-lookup"><span data-stu-id="bee50-131">Required?</span></span>                            | <span data-ttu-id="bee50-132">верно</span><span class="sxs-lookup"><span data-stu-id="bee50-132">true</span></span>                                 |
| <span data-ttu-id="bee50-133">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="bee50-133">Position?</span></span>                            | <span data-ttu-id="bee50-134">2</span><span class="sxs-lookup"><span data-stu-id="bee50-134">2</span></span>                                    |
| <span data-ttu-id="bee50-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bee50-135">Default Value</span></span>                        | <span data-ttu-id="bee50-136">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-136">none</span></span>                                 |
| <span data-ttu-id="bee50-137">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="bee50-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="bee50-138">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="bee50-138">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="bee50-139">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="bee50-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="bee50-140">false</span><span class="sxs-lookup"><span data-stu-id="bee50-140">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="bee50-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="bee50-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="bee50-142">Указывает правила, которые необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="bee50-142">Specifies the rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="bee50-143">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="bee50-143">Aliases</span></span>                              | <span data-ttu-id="bee50-144">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-144">none</span></span>                                 |
| <span data-ttu-id="bee50-145">Требуется?</span><span class="sxs-lookup"><span data-stu-id="bee50-145">Required?</span></span>                            | <span data-ttu-id="bee50-146">верно</span><span class="sxs-lookup"><span data-stu-id="bee50-146">true</span></span>                                 |
| <span data-ttu-id="bee50-147">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="bee50-147">Position?</span></span>                            | <span data-ttu-id="bee50-148">2</span><span class="sxs-lookup"><span data-stu-id="bee50-148">2</span></span>                                    |
| <span data-ttu-id="bee50-149">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bee50-149">Default Value</span></span>                        | <span data-ttu-id="bee50-150">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="bee50-150">none</span></span>                                 |
| <span data-ttu-id="bee50-151">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="bee50-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="bee50-152">True (ByValue)</span><span class="sxs-lookup"><span data-stu-id="bee50-152">True (ByValue)</span></span>                       |
| <span data-ttu-id="bee50-153">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="bee50-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="bee50-154">false</span><span class="sxs-lookup"><span data-stu-id="bee50-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="bee50-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="bee50-155">-Confirm</span></span>

<span data-ttu-id="bee50-156">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="bee50-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="bee50-157">Требуется?</span><span class="sxs-lookup"><span data-stu-id="bee50-157">Required?</span></span>                            | <span data-ttu-id="bee50-158">false</span><span class="sxs-lookup"><span data-stu-id="bee50-158">false</span></span>                                |
| <span data-ttu-id="bee50-159">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="bee50-159">Position?</span></span>                            | <span data-ttu-id="bee50-160">с именем</span><span class="sxs-lookup"><span data-stu-id="bee50-160">named</span></span>                                |
| <span data-ttu-id="bee50-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bee50-161">Default Value</span></span>                        | <span data-ttu-id="bee50-162">false</span><span class="sxs-lookup"><span data-stu-id="bee50-162">false</span></span>                                |
| <span data-ttu-id="bee50-163">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="bee50-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="bee50-164">false</span><span class="sxs-lookup"><span data-stu-id="bee50-164">false</span></span>                                |
| <span data-ttu-id="bee50-165">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="bee50-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="bee50-166">false</span><span class="sxs-lookup"><span data-stu-id="bee50-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="bee50-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="bee50-167">-WhatIf</span></span>

<span data-ttu-id="bee50-168">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="bee50-168">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="bee50-169">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="bee50-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="bee50-170">Требуется?</span><span class="sxs-lookup"><span data-stu-id="bee50-170">Required?</span></span>                            | <span data-ttu-id="bee50-171">false</span><span class="sxs-lookup"><span data-stu-id="bee50-171">false</span></span>                                |
| <span data-ttu-id="bee50-172">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="bee50-172">Position?</span></span>                            | <span data-ttu-id="bee50-173">с именем</span><span class="sxs-lookup"><span data-stu-id="bee50-173">named</span></span>                                |
| <span data-ttu-id="bee50-174">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bee50-174">Default Value</span></span>                        | <span data-ttu-id="bee50-175">false</span><span class="sxs-lookup"><span data-stu-id="bee50-175">false</span></span>                                |
| <span data-ttu-id="bee50-176">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="bee50-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="bee50-177">false</span><span class="sxs-lookup"><span data-stu-id="bee50-177">false</span></span>                                |
| <span data-ttu-id="bee50-178">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="bee50-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="bee50-179">false</span><span class="sxs-lookup"><span data-stu-id="bee50-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="bee50-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="bee50-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="bee50-181">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="bee50-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="bee50-182">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="bee50-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="bee50-183">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="bee50-183">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="bee50-184">int\[\]</span><span class="sxs-lookup"><span data-stu-id="bee50-184">int\[\]</span></span>

<span data-ttu-id="bee50-185">Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="bee50-185">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

### <a name="pswaauthorizationrule"></a><span data-ttu-id="bee50-186">PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="bee50-186">PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="bee50-187">Этот командлет принимает массив целых чисел или массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="bee50-187">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

## <a name="outputs"></a><span data-ttu-id="bee50-188">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="bee50-188">OUTPUTS</span></span>

<span data-ttu-id="bee50-189">Этот командлет не создает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="bee50-189">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="bee50-190">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="bee50-190">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="bee50-191">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="bee50-191">EXAMPLE 1</span></span>

<span data-ttu-id="bee50-192">Этот пример удаляет правило авторизации с идентификатором *2*.</span><span class="sxs-lookup"><span data-stu-id="bee50-192">This example removes the authorization rule with an ID of *2*.</span></span>

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a><span data-ttu-id="bee50-193">ПРИМЕР 2 {#example-2 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="bee50-193">EXAMPLE 2 {#example-2 .subHeading}</span></span>

<span data-ttu-id="bee50-194">Этот пример удаляет все правила авторизации, а также требует подтверждения пользователя.</span><span class="sxs-lookup"><span data-stu-id="bee50-194">This example removes all authorization rules and also requires confirmation by the user.</span></span>

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a><span data-ttu-id="bee50-195">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="bee50-195">Related topics</span></span>

- [<span data-ttu-id="bee50-196">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="bee50-196">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="bee50-197">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="bee50-197">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="bee50-198">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="bee50-198">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="bee50-199">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="bee50-199">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
