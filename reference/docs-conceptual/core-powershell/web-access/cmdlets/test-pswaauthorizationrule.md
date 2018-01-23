---
description: 
ms.topic: article
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "проверка pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: fb2937397616160c70b056e412e42fb8ff4c2f27
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="test-pswaauthorizationrule"></a><span data-ttu-id="ca479-103">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ca479-103">Test-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="ca479-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="ca479-104">SYNOPSIS</span></span>

<span data-ttu-id="ca479-105">Проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ca479-105">Verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>

## <a name="syntax"></a><span data-ttu-id="ca479-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="ca479-106">SYNTAX</span></span>

### <a name="computername"></a><span data-ttu-id="ca479-107">имя_компьютера</span><span class="sxs-lookup"><span data-stu-id="ca479-107">ComputerName</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a><span data-ttu-id="ca479-108">ConnectionUri</span><span class="sxs-lookup"><span data-stu-id="ca479-108">ConnectionUri</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="ca479-109">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="ca479-109">DESCRIPTION</span></span>

<span data-ttu-id="ca479-110">Командлет **Test-PswaAuthorizationRule** проверяет, существует ли правило для указанного пользователя, компьютера или конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ca479-110">The **Test-PswaAuthorizationRule** cmdlet verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>
<span data-ttu-id="ca479-111">Этот командлет также можно использовать для тестирования правил авторизации, чтобы гарантировать, что запрос на доступ конкретного пользователя, компьютера или конечной точки авторизован.</span><span class="sxs-lookup"><span data-stu-id="ca479-111">This cmdlet can also be used to test authorization rules, to validate that a particular user, computer or endpoint access request is authorized.</span></span>
<span data-ttu-id="ca479-112">По умолчанию этот командлет проверяет все правила в файле авторизации.</span><span class="sxs-lookup"><span data-stu-id="ca479-112">By default, this cmdlet evaluates all rules in the authorization file.</span></span>
<span data-ttu-id="ca479-113">Тем не менее можно указать набор правил для проверки.</span><span class="sxs-lookup"><span data-stu-id="ca479-113">However, you can specify a subset of rules to test.</span></span>

<span data-ttu-id="ca479-114">Этот командлет можно использовать для устранения неполадок проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ca479-114">You can use this cmdlet to help troubleshoot authentication failures.</span></span>

<span data-ttu-id="ca479-115">Параметры для этого командлета соответствуют полям на странице входа Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="ca479-115">The parameters for this cmdlet correspond to fields on the Windows PowerShell® Web Access sign-on page.</span></span>

## <a name="parameters"></a><span data-ttu-id="ca479-116">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="ca479-116">PARAMETERS</span></span>

### <a name="-computername-ltstringgt"></a><span data-ttu-id="ca479-117">-ComputerName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-117">-ComputerName &lt;String&gt;</span></span>

<span data-ttu-id="ca479-118">Задает имя проверяемого компьютера.</span><span class="sxs-lookup"><span data-stu-id="ca479-118">Specifies the name of the computer to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-119">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-119">Aliases</span></span>                              | <span data-ttu-id="ca479-120">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-120">none</span></span>                                 |
| <span data-ttu-id="ca479-121">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-121">Required?</span></span>                            | <span data-ttu-id="ca479-122">верно</span><span class="sxs-lookup"><span data-stu-id="ca479-122">true</span></span>                                 |
| <span data-ttu-id="ca479-123">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-123">Position?</span></span>                            | <span data-ttu-id="ca479-124">2</span><span class="sxs-lookup"><span data-stu-id="ca479-124">2</span></span>                                    |
| <span data-ttu-id="ca479-125">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-125">Default Value</span></span>                        | <span data-ttu-id="ca479-126">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-126">none</span></span>                                 |
| <span data-ttu-id="ca479-127">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-127">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-128">false</span><span class="sxs-lookup"><span data-stu-id="ca479-128">false</span></span>                                |
| <span data-ttu-id="ca479-129">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-129">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-130">false</span><span class="sxs-lookup"><span data-stu-id="ca479-130">false</span></span>                                |

### <a name="-configurationname-ltstringgt"></a><span data-ttu-id="ca479-131">-ConfigurationName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-131">-ConfigurationName &lt;String&gt;</span></span>

<span data-ttu-id="ca479-132">Указывает имя конфигурации сеанса Windows PowerShell (также известной как конечная точка или пространство выполнения) для проверки.</span><span class="sxs-lookup"><span data-stu-id="ca479-132">Specifies the name of the Windows PowerShell session configuration, also known as endpoint or runspace, to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-133">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-133">Aliases</span></span>                              | <span data-ttu-id="ca479-134">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-134">none</span></span>                                 |
| <span data-ttu-id="ca479-135">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-135">Required?</span></span>                            | <span data-ttu-id="ca479-136">false</span><span class="sxs-lookup"><span data-stu-id="ca479-136">false</span></span>                                |
| <span data-ttu-id="ca479-137">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-137">Position?</span></span>                            | <span data-ttu-id="ca479-138">3</span><span class="sxs-lookup"><span data-stu-id="ca479-138">3</span></span>                                    |
| <span data-ttu-id="ca479-139">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-139">Default Value</span></span>                        | <span data-ttu-id="ca479-140">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-140">none</span></span>                                 |
| <span data-ttu-id="ca479-141">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-142">false</span><span class="sxs-lookup"><span data-stu-id="ca479-142">false</span></span>                                |
| <span data-ttu-id="ca479-143">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-144">false</span><span class="sxs-lookup"><span data-stu-id="ca479-144">false</span></span>                                |

### <a name="-connectionuri-lturigt"></a><span data-ttu-id="ca479-145">-ConnectionUri &lt;Uri&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-145">-ConnectionUri &lt;Uri&gt;</span></span>

<span data-ttu-id="ca479-146">Указывает URI подключения для проверки.</span><span class="sxs-lookup"><span data-stu-id="ca479-146">Specifies the connection URI to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-147">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-147">Aliases</span></span>                              | <span data-ttu-id="ca479-148">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-148">none</span></span>                                 |
| <span data-ttu-id="ca479-149">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-149">Required?</span></span>                            | <span data-ttu-id="ca479-150">верно</span><span class="sxs-lookup"><span data-stu-id="ca479-150">true</span></span>                                 |
| <span data-ttu-id="ca479-151">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-151">Position?</span></span>                            | <span data-ttu-id="ca479-152">2</span><span class="sxs-lookup"><span data-stu-id="ca479-152">2</span></span>                                    |
| <span data-ttu-id="ca479-153">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-153">Default Value</span></span>                        | <span data-ttu-id="ca479-154">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-154">none</span></span>                                 |
| <span data-ttu-id="ca479-155">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-156">false</span><span class="sxs-lookup"><span data-stu-id="ca479-156">false</span></span>                                |
| <span data-ttu-id="ca479-157">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-158">false</span><span class="sxs-lookup"><span data-stu-id="ca479-158">false</span></span>                                |

### <a name="-credential-ltpscredentialgt"></a><span data-ttu-id="ca479-159">-Credential &lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-159">-Credential &lt;PSCredential&gt;</span></span>

<span data-ttu-id="ca479-160">Указывает объект **PSCredential** для учетной записи пользователя, который предполагается использовать для проверки правил авторизации Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="ca479-160">Specifies a **PSCredential** object for a user account that you want to use to test Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="ca479-161">Если этот параметр не добавлен, командлет будет использовать учетную запись текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="ca479-161">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="ca479-162">Чтобы получить объект **PSCredential**, который требуется для удаленной проверки правил авторизации, запустите командлет [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936).</span><span class="sxs-lookup"><span data-stu-id="ca479-162">To get a **PSCredential** object, which is required to test authorization rules remotely, run the [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-163">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-163">Aliases</span></span>                              | <span data-ttu-id="ca479-164">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-164">none</span></span>                                 |
| <span data-ttu-id="ca479-165">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-165">Required?</span></span>                            | <span data-ttu-id="ca479-166">false</span><span class="sxs-lookup"><span data-stu-id="ca479-166">false</span></span>                                |
| <span data-ttu-id="ca479-167">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-167">Position?</span></span>                            | <span data-ttu-id="ca479-168">с именем</span><span class="sxs-lookup"><span data-stu-id="ca479-168">named</span></span>                                |
| <span data-ttu-id="ca479-169">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-169">Default Value</span></span>                        | <span data-ttu-id="ca479-170">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-170">none</span></span>                                 |
| <span data-ttu-id="ca479-171">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-171">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-172">false</span><span class="sxs-lookup"><span data-stu-id="ca479-172">false</span></span>                                |
| <span data-ttu-id="ca479-173">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-173">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-174">false</span><span class="sxs-lookup"><span data-stu-id="ca479-174">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="ca479-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="ca479-176">Задает набор правил для проверки.</span><span class="sxs-lookup"><span data-stu-id="ca479-176">Specifies a subset of rules to test.</span></span> <span data-ttu-id="ca479-177">Если этот параметр не указан, командлет проверяет соответствие всем правилам авторизации.</span><span class="sxs-lookup"><span data-stu-id="ca479-177">If this parameter is not specified, then this cmdlet tests against all authorization rules.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-178">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-178">Aliases</span></span>                              | <span data-ttu-id="ca479-179">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-179">none</span></span>                                 |
| <span data-ttu-id="ca479-180">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-180">Required?</span></span>                            | <span data-ttu-id="ca479-181">false</span><span class="sxs-lookup"><span data-stu-id="ca479-181">false</span></span>                                |
| <span data-ttu-id="ca479-182">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-182">Position?</span></span>                            | <span data-ttu-id="ca479-183">с именем</span><span class="sxs-lookup"><span data-stu-id="ca479-183">named</span></span>                                |
| <span data-ttu-id="ca479-184">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-184">Default Value</span></span>                        | <span data-ttu-id="ca479-185">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-185">none</span></span>                                 |
| <span data-ttu-id="ca479-186">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-186">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-187">True (ByValue)</span><span class="sxs-lookup"><span data-stu-id="ca479-187">True (ByValue)</span></span>                       |
| <span data-ttu-id="ca479-188">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-188">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-189">false</span><span class="sxs-lookup"><span data-stu-id="ca479-189">false</span></span>                                |

### <a name="-username-ltstringgt"></a><span data-ttu-id="ca479-190">-UserName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-190">-UserName &lt;String&gt;</span></span>

<span data-ttu-id="ca479-191">Задает имя проверяемого пользователя.</span><span class="sxs-lookup"><span data-stu-id="ca479-191">Specifies the name of the user to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="ca479-192">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ca479-192">Aliases</span></span>                              | <span data-ttu-id="ca479-193">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-193">none</span></span>                                 |
| <span data-ttu-id="ca479-194">Требуется?</span><span class="sxs-lookup"><span data-stu-id="ca479-194">Required?</span></span>                            | <span data-ttu-id="ca479-195">верно</span><span class="sxs-lookup"><span data-stu-id="ca479-195">true</span></span>                                 |
| <span data-ttu-id="ca479-196">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="ca479-196">Position?</span></span>                            | <span data-ttu-id="ca479-197">1</span><span class="sxs-lookup"><span data-stu-id="ca479-197">1</span></span>                                    |
| <span data-ttu-id="ca479-198">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ca479-198">Default Value</span></span>                        | <span data-ttu-id="ca479-199">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="ca479-199">none</span></span>                                 |
| <span data-ttu-id="ca479-200">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="ca479-200">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ca479-201">false</span><span class="sxs-lookup"><span data-stu-id="ca479-201">false</span></span>                                |
| <span data-ttu-id="ca479-202">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="ca479-202">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ca479-203">false</span><span class="sxs-lookup"><span data-stu-id="ca479-203">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="ca479-204">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="ca479-204">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="ca479-205">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="ca479-205">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="ca479-206">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="ca479-206">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="ca479-207">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="ca479-207">INPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="ca479-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="ca479-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="ca479-209">Этот командлет принимает в качестве входных данных массив объектов PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="ca479-209">This cmdlet accepts an array of PswaAuthorizationRule objects as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="ca479-210">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="ca479-210">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="ca479-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="ca479-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="ca479-212">Этот командлет создает массив объектов PswaAuthorizationRule в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ca479-212">This cmdlet produces an array of PswaAuthorizationRule objects as output.</span></span>

## <a name="examples"></a><span data-ttu-id="ca479-213">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="ca479-213">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="ca479-214">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="ca479-214">EXAMPLE 1</span></span>

<span data-ttu-id="ca479-215">В этом примере проверяются все правила авторизации, чтобы отобразить все правила, позволяющие пользователю *contoso\\mhanson* подключаться к компьютеру *srv2* и использовать конфигурацию сеанса Windows PowerShell с именем *test*.</span><span class="sxs-lookup"><span data-stu-id="ca479-215">This example tests all authorization rules in order to display all the rules that allow the user *contoso\\mhanson* to connect to the computer *srv2* and use a Windows PowerShell session configuration named *test*.</span></span>

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a><span data-ttu-id="ca479-216">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="ca479-216">EXAMPLE 2</span></span>

<span data-ttu-id="ca479-217">В этом примере проверяются все правила авторизации, чтобы узнать, какие правила авторизации применяются к пользователю *contoso\\mhanson*.</span><span class="sxs-lookup"><span data-stu-id="ca479-217">This example tests all authorization rules to check which authorization rules apply to the user *contoso\\mhanson*.</span></span>

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a><span data-ttu-id="ca479-218">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="ca479-218">Related topics</span></span>

- [<span data-ttu-id="ca479-219">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ca479-219">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="ca479-220">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ca479-220">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="ca479-221">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="ca479-221">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="ca479-222">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ca479-222">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
