---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "проверка pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: 900547301c815ba6fe3a9507f975503fec864e4e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="test-pswaauthorizationrule"></a><span data-ttu-id="6585c-103">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="6585c-103">Test-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="6585c-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="6585c-104">SYNOPSIS</span></span>

<span data-ttu-id="6585c-105">Проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="6585c-105">Verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>

## <a name="syntax"></a><span data-ttu-id="6585c-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="6585c-106">SYNTAX</span></span>

### <a name="computername"></a><span data-ttu-id="6585c-107">имя_компьютера</span><span class="sxs-lookup"><span data-stu-id="6585c-107">ComputerName</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a><span data-ttu-id="6585c-108">ConnectionUri</span><span class="sxs-lookup"><span data-stu-id="6585c-108">ConnectionUri</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="6585c-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="6585c-109">DESCRIPTION</span></span>

<span data-ttu-id="6585c-110">Командлет **Test-PswaAuthorizationRule** проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="6585c-110">The **Test-PswaAuthorizationRule** cmdlet verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>
<span data-ttu-id="6585c-111">Этот командлет также можно использовать для тестирования правил авторизации, чтобы гарантировать, что запрос на доступ конкретного пользователя, компьютера или конечной точки авторизован.</span><span class="sxs-lookup"><span data-stu-id="6585c-111">This cmdlet can also be used to test authorization rules, to validate that a particular user, computer or endpoint access request is authorized.</span></span>
<span data-ttu-id="6585c-112">По умолчанию этот командлет проверяет все правила в файле авторизации.</span><span class="sxs-lookup"><span data-stu-id="6585c-112">By default, this cmdlet evaluates all rules in the authorization file.</span></span>
<span data-ttu-id="6585c-113">Тем не менее можно указать набор правил для проверки.</span><span class="sxs-lookup"><span data-stu-id="6585c-113">However, you can specify a subset of rules to test.</span></span>

<span data-ttu-id="6585c-114">Этот командлет можно использовать для устранения неполадок проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6585c-114">You can use this cmdlet to help troubleshoot authentication failures.</span></span>

<span data-ttu-id="6585c-115">Параметры для этого командлета соответствуют полям на странице входа Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="6585c-115">The parameters for this cmdlet correspond to fields on the Windows PowerShell® Web Access sign-on page.</span></span>

## <a name="parameters"></a><span data-ttu-id="6585c-116">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="6585c-116">PARAMETERS</span></span>

### <a name="-computername-ltstringgt"></a><span data-ttu-id="6585c-117">-ComputerName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-117">-ComputerName &lt;String&gt;</span></span>

<span data-ttu-id="6585c-118">Задает имя проверяемого компьютера.</span><span class="sxs-lookup"><span data-stu-id="6585c-118">Specifies the name of the computer to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-119">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-119">Aliases</span></span>                              | <span data-ttu-id="6585c-120">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-120">none</span></span>                                 |
| <span data-ttu-id="6585c-121">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-121">Required?</span></span>                            | <span data-ttu-id="6585c-122">верно</span><span class="sxs-lookup"><span data-stu-id="6585c-122">true</span></span>                                 |
| <span data-ttu-id="6585c-123">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-123">Position?</span></span>                            | <span data-ttu-id="6585c-124">2</span><span class="sxs-lookup"><span data-stu-id="6585c-124">2</span></span>                                    |
| <span data-ttu-id="6585c-125">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-125">Default Value</span></span>                        | <span data-ttu-id="6585c-126">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-126">none</span></span>                                 |
| <span data-ttu-id="6585c-127">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-127">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-128">false</span><span class="sxs-lookup"><span data-stu-id="6585c-128">false</span></span>                                |
| <span data-ttu-id="6585c-129">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-129">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-130">false</span><span class="sxs-lookup"><span data-stu-id="6585c-130">false</span></span>                                |

### <a name="-configurationname-ltstringgt"></a><span data-ttu-id="6585c-131">-ConfigurationName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-131">-ConfigurationName &lt;String&gt;</span></span>

<span data-ttu-id="6585c-132">Указывает имя конфигурации сеанса Windows PowerShell (также известной как конечная точка или пространство выполнения) для проверки.</span><span class="sxs-lookup"><span data-stu-id="6585c-132">Specifies the name of the Windows PowerShell session configuration, also known as endpoint or runspace, to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-133">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-133">Aliases</span></span>                              | <span data-ttu-id="6585c-134">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-134">none</span></span>                                 |
| <span data-ttu-id="6585c-135">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-135">Required?</span></span>                            | <span data-ttu-id="6585c-136">false</span><span class="sxs-lookup"><span data-stu-id="6585c-136">false</span></span>                                |
| <span data-ttu-id="6585c-137">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-137">Position?</span></span>                            | <span data-ttu-id="6585c-138">3</span><span class="sxs-lookup"><span data-stu-id="6585c-138">3</span></span>                                    |
| <span data-ttu-id="6585c-139">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-139">Default Value</span></span>                        | <span data-ttu-id="6585c-140">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-140">none</span></span>                                 |
| <span data-ttu-id="6585c-141">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-142">false</span><span class="sxs-lookup"><span data-stu-id="6585c-142">false</span></span>                                |
| <span data-ttu-id="6585c-143">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-144">false</span><span class="sxs-lookup"><span data-stu-id="6585c-144">false</span></span>                                |

### <a name="-connectionuri-lturigt"></a><span data-ttu-id="6585c-145">-ConnectionUri &lt;Uri&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-145">-ConnectionUri &lt;Uri&gt;</span></span>

<span data-ttu-id="6585c-146">Указывает URI подключения для проверки.</span><span class="sxs-lookup"><span data-stu-id="6585c-146">Specifies the connection URI to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-147">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-147">Aliases</span></span>                              | <span data-ttu-id="6585c-148">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-148">none</span></span>                                 |
| <span data-ttu-id="6585c-149">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-149">Required?</span></span>                            | <span data-ttu-id="6585c-150">верно</span><span class="sxs-lookup"><span data-stu-id="6585c-150">true</span></span>                                 |
| <span data-ttu-id="6585c-151">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-151">Position?</span></span>                            | <span data-ttu-id="6585c-152">2</span><span class="sxs-lookup"><span data-stu-id="6585c-152">2</span></span>                                    |
| <span data-ttu-id="6585c-153">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-153">Default Value</span></span>                        | <span data-ttu-id="6585c-154">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-154">none</span></span>                                 |
| <span data-ttu-id="6585c-155">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-156">false</span><span class="sxs-lookup"><span data-stu-id="6585c-156">false</span></span>                                |
| <span data-ttu-id="6585c-157">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-158">false</span><span class="sxs-lookup"><span data-stu-id="6585c-158">false</span></span>                                |

### <a name="-credential-ltpscredentialgt"></a><span data-ttu-id="6585c-159">-Credential &lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-159">-Credential &lt;PSCredential&gt;</span></span>

<span data-ttu-id="6585c-160">Указывает объект **PSCredential** для учетной записи пользователя, который предполагается использовать для проверки правил авторизации Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="6585c-160">Specifies a **PSCredential** object for a user account that you want to use to test Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="6585c-161">Если этот параметр не добавлен, командлет будет использовать учетную запись текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6585c-161">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="6585c-162">Чтобы получить объект **PSCredential**, который требуется для удаленной проверки правил авторизации, запустите командлет [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936).</span><span class="sxs-lookup"><span data-stu-id="6585c-162">To get a **PSCredential** object, which is required to test authorization rules remotely, run the [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-163">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-163">Aliases</span></span>                              | <span data-ttu-id="6585c-164">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-164">none</span></span>                                 |
| <span data-ttu-id="6585c-165">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-165">Required?</span></span>                            | <span data-ttu-id="6585c-166">false</span><span class="sxs-lookup"><span data-stu-id="6585c-166">false</span></span>                                |
| <span data-ttu-id="6585c-167">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-167">Position?</span></span>                            | <span data-ttu-id="6585c-168">с именем</span><span class="sxs-lookup"><span data-stu-id="6585c-168">named</span></span>                                |
| <span data-ttu-id="6585c-169">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-169">Default Value</span></span>                        | <span data-ttu-id="6585c-170">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-170">none</span></span>                                 |
| <span data-ttu-id="6585c-171">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-171">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-172">false</span><span class="sxs-lookup"><span data-stu-id="6585c-172">false</span></span>                                |
| <span data-ttu-id="6585c-173">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-173">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-174">false</span><span class="sxs-lookup"><span data-stu-id="6585c-174">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="6585c-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="6585c-176">Задает набор правил для проверки.</span><span class="sxs-lookup"><span data-stu-id="6585c-176">Specifies a subset of rules to test.</span></span> <span data-ttu-id="6585c-177">Если этот параметр не указан, командлет проверяет соответствие всем правилам авторизации.</span><span class="sxs-lookup"><span data-stu-id="6585c-177">If this parameter is not specified, then this cmdlet tests against all authorization rules.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-178">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-178">Aliases</span></span>                              | <span data-ttu-id="6585c-179">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-179">none</span></span>                                 |
| <span data-ttu-id="6585c-180">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-180">Required?</span></span>                            | <span data-ttu-id="6585c-181">false</span><span class="sxs-lookup"><span data-stu-id="6585c-181">false</span></span>                                |
| <span data-ttu-id="6585c-182">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-182">Position?</span></span>                            | <span data-ttu-id="6585c-183">с именем</span><span class="sxs-lookup"><span data-stu-id="6585c-183">named</span></span>                                |
| <span data-ttu-id="6585c-184">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-184">Default Value</span></span>                        | <span data-ttu-id="6585c-185">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-185">none</span></span>                                 |
| <span data-ttu-id="6585c-186">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-186">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-187">True (ByValue)</span><span class="sxs-lookup"><span data-stu-id="6585c-187">True (ByValue)</span></span>                       |
| <span data-ttu-id="6585c-188">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-188">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-189">false</span><span class="sxs-lookup"><span data-stu-id="6585c-189">false</span></span>                                |

### <a name="-username-ltstringgt"></a><span data-ttu-id="6585c-190">-UserName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-190">-UserName &lt;String&gt;</span></span>

<span data-ttu-id="6585c-191">Задает имя проверяемого пользователя.</span><span class="sxs-lookup"><span data-stu-id="6585c-191">Specifies the name of the user to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="6585c-192">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="6585c-192">Aliases</span></span>                              | <span data-ttu-id="6585c-193">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-193">none</span></span>                                 |
| <span data-ttu-id="6585c-194">Требуется?</span><span class="sxs-lookup"><span data-stu-id="6585c-194">Required?</span></span>                            | <span data-ttu-id="6585c-195">верно</span><span class="sxs-lookup"><span data-stu-id="6585c-195">true</span></span>                                 |
| <span data-ttu-id="6585c-196">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="6585c-196">Position?</span></span>                            | <span data-ttu-id="6585c-197">1</span><span class="sxs-lookup"><span data-stu-id="6585c-197">1</span></span>                                    |
| <span data-ttu-id="6585c-198">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6585c-198">Default Value</span></span>                        | <span data-ttu-id="6585c-199">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="6585c-199">none</span></span>                                 |
| <span data-ttu-id="6585c-200">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="6585c-200">Accept Pipeline Input?</span></span>               | <span data-ttu-id="6585c-201">false</span><span class="sxs-lookup"><span data-stu-id="6585c-201">false</span></span>                                |
| <span data-ttu-id="6585c-202">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="6585c-202">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="6585c-203">false</span><span class="sxs-lookup"><span data-stu-id="6585c-203">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="6585c-204">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="6585c-204">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="6585c-205">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="6585c-205">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="6585c-206">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="6585c-206">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="6585c-207">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="6585c-207">INPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="6585c-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="6585c-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="6585c-209">Этот командлет принимает в качестве входных данных массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="6585c-209">This cmdlet accepts an array of PswaAuthorizationRule objects as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="6585c-210">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="6585c-210">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="6585c-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="6585c-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="6585c-212">Этот командлет создает массив объектов PswaAuthorizationRule в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6585c-212">This cmdlet produces an array of PswaAuthorizationRule objects as output.</span></span>

## <a name="examples"></a><span data-ttu-id="6585c-213">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="6585c-213">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="6585c-214">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="6585c-214">EXAMPLE 1</span></span>

<span data-ttu-id="6585c-215">В этом примере проверяются все правила авторизации, чтобы отобразить все правила, позволяющие пользователю *contoso\\mhanson* подключаться к компьютеру *srv2* и использовать конфигурацию сеанса Windows PowerShell с именем *test*.</span><span class="sxs-lookup"><span data-stu-id="6585c-215">This example tests all authorization rules in order to display all the rules that allow the user *contoso\\mhanson* to connect to the computer *srv2* and use a Windows PowerShell session configuration named *test*.</span></span>

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a><span data-ttu-id="6585c-216">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="6585c-216">EXAMPLE 2</span></span>

<span data-ttu-id="6585c-217">В этом примере проверяются все правила авторизации, чтобы узнать, какие правила авторизации применяются к пользователю *contoso\\mhanson*.</span><span class="sxs-lookup"><span data-stu-id="6585c-217">This example tests all authorization rules to check which authorization rules apply to the user *contoso\\mhanson*.</span></span>

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a><span data-ttu-id="6585c-218">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="6585c-218">Related topics</span></span>

- [<span data-ttu-id="6585c-219">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="6585c-219">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="6585c-220">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="6585c-220">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="6585c-221">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="6585c-221">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="6585c-222">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="6585c-222">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
