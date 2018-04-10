---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: установка pswawebapplication
ms.technology: powershell
ms.openlocfilehash: c7f7768a41b6784d8c29afa1fccf0b855160b777
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="d30e6-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="d30e6-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="d30e6-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="d30e6-104">SYNOPSIS</span></span>

<span data-ttu-id="d30e6-105">Настраивает веб-приложение Windows PowerShell® Web Access в IIS.</span><span class="sxs-lookup"><span data-stu-id="d30e6-105">Configures the Windows PowerShell® Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="d30e6-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="d30e6-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="d30e6-107">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="d30e6-108">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="d30e6-108">DESCRIPTION</span></span>

<span data-ttu-id="d30e6-109">Командлет **Install-PswaWebApplication** настраивает веб-приложение Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d30e6-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="d30e6-110">Этот командлет устанавливает веб-приложение, связывает его с веб-сайтом и при необходимости создает тестовый сертификат SSL с помощью параметра **useTestCertificate**.</span><span class="sxs-lookup"><span data-stu-id="d30e6-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="d30e6-111">Для обеспечения безопасности веб-администраторам не следует использовать тестовый сертификат для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="d30e6-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="d30e6-112">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="d30e6-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="d30e6-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="d30e6-113">-UseTestCertificate</span></span>

<span data-ttu-id="d30e6-114">Указывает, что создается тестовый сертификат.</span><span class="sxs-lookup"><span data-stu-id="d30e6-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="d30e6-115">Если этот параметр имеет значение true, то командлет создает тестовый сертификат и настраивает веб-приложение Windows PowerShell Web Access для использования сертификата для HTTPS-запросов.</span><span class="sxs-lookup"><span data-stu-id="d30e6-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="d30e6-116">Если этот параметр имеет значение false, то ни сертификат, ни привязка не создаются.</span><span class="sxs-lookup"><span data-stu-id="d30e6-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="d30e6-117">Задайте значение false, если для Windows PowerShell Web Access используется другой сертификат.</span><span class="sxs-lookup"><span data-stu-id="d30e6-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="d30e6-118">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="d30e6-118">Aliases</span></span>                              | <span data-ttu-id="d30e6-119">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="d30e6-119">none</span></span>                                 |
| <span data-ttu-id="d30e6-120">Требуется?</span><span class="sxs-lookup"><span data-stu-id="d30e6-120">Required?</span></span>                            | <span data-ttu-id="d30e6-121">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-121">false</span></span>                                |
| <span data-ttu-id="d30e6-122">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="d30e6-122">Position?</span></span>                            | <span data-ttu-id="d30e6-123">с именем</span><span class="sxs-lookup"><span data-stu-id="d30e6-123">named</span></span>                                |
| <span data-ttu-id="d30e6-124">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-124">Default Value</span></span>                        | <span data-ttu-id="d30e6-125">верно</span><span class="sxs-lookup"><span data-stu-id="d30e6-125">true</span></span>                                 |
| <span data-ttu-id="d30e6-126">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="d30e6-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="d30e6-127">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-127">false</span></span>                                |
| <span data-ttu-id="d30e6-128">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="d30e6-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="d30e6-129">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-129">false</span></span>                                |

### <a name="-webapplicationnameltstringgt"></a><span data-ttu-id="d30e6-130">-WebApplicationName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="d30e6-130">-WebApplicationName&lt;String&gt;</span></span>

<span data-ttu-id="d30e6-131">Указывает имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d30e6-131">Specifies the name for your web application.</span></span> <span data-ttu-id="d30e6-132">Отображается как последняя часть URL-адреса Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d30e6-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="d30e6-133">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="d30e6-133">Aliases</span></span>                              | <span data-ttu-id="d30e6-134">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="d30e6-134">none</span></span>                                 |
| <span data-ttu-id="d30e6-135">Требуется?</span><span class="sxs-lookup"><span data-stu-id="d30e6-135">Required?</span></span>                            | <span data-ttu-id="d30e6-136">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-136">false</span></span>                                |
| <span data-ttu-id="d30e6-137">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="d30e6-137">Position?</span></span>                            | <span data-ttu-id="d30e6-138">1</span><span class="sxs-lookup"><span data-stu-id="d30e6-138">1</span></span>                                    |
| <span data-ttu-id="d30e6-139">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-139">Default Value</span></span>                        | <span data-ttu-id="d30e6-140">pswa</span><span class="sxs-lookup"><span data-stu-id="d30e6-140">pswa</span></span>                                 |
| <span data-ttu-id="d30e6-141">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="d30e6-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="d30e6-142">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-142">false</span></span>                                |
| <span data-ttu-id="d30e6-143">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="d30e6-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="d30e6-144">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-144">false</span></span>                                |

### <a name="-websitenameltstringgt"></a><span data-ttu-id="d30e6-145">-WebSiteName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="d30e6-145">-WebSiteName&lt;String&gt;</span></span>

<span data-ttu-id="d30e6-146">Задает имя веб-сайта веб-сервера (IIS) для установки этого веб-приложения Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="d30e6-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="d30e6-147">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="d30e6-147">Aliases</span></span>                              | <span data-ttu-id="d30e6-148">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="d30e6-148">none</span></span>                                 |
| <span data-ttu-id="d30e6-149">Требуется?</span><span class="sxs-lookup"><span data-stu-id="d30e6-149">Required?</span></span>                            | <span data-ttu-id="d30e6-150">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-150">false</span></span>                                |
| <span data-ttu-id="d30e6-151">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="d30e6-151">Position?</span></span>                            | <span data-ttu-id="d30e6-152">с именем</span><span class="sxs-lookup"><span data-stu-id="d30e6-152">named</span></span>                                |
| <span data-ttu-id="d30e6-153">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-153">Default Value</span></span>                        | <span data-ttu-id="d30e6-154">Веб-сайт по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-154">Default Web Site</span></span>                     |
| <span data-ttu-id="d30e6-155">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="d30e6-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="d30e6-156">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-156">false</span></span>                                |
| <span data-ttu-id="d30e6-157">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="d30e6-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="d30e6-158">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="d30e6-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="d30e6-159">-Confirm</span></span>

<span data-ttu-id="d30e6-160">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="d30e6-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="d30e6-161">Требуется?</span><span class="sxs-lookup"><span data-stu-id="d30e6-161">Required?</span></span>                            | <span data-ttu-id="d30e6-162">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-162">false</span></span>                                |
| <span data-ttu-id="d30e6-163">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="d30e6-163">Position?</span></span>                            | <span data-ttu-id="d30e6-164">с именем</span><span class="sxs-lookup"><span data-stu-id="d30e6-164">named</span></span>                                |
| <span data-ttu-id="d30e6-165">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-165">Default Value</span></span>                        | <span data-ttu-id="d30e6-166">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-166">false</span></span>                                |
| <span data-ttu-id="d30e6-167">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="d30e6-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="d30e6-168">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-168">false</span></span>                                |
| <span data-ttu-id="d30e6-169">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="d30e6-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="d30e6-170">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="d30e6-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="d30e6-171">-WhatIf</span></span>

<span data-ttu-id="d30e6-172">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="d30e6-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="d30e6-173">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="d30e6-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="d30e6-174">Требуется?</span><span class="sxs-lookup"><span data-stu-id="d30e6-174">Required?</span></span>                            | <span data-ttu-id="d30e6-175">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-175">false</span></span>                                |
| <span data-ttu-id="d30e6-176">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="d30e6-176">Position?</span></span>                            | <span data-ttu-id="d30e6-177">с именем</span><span class="sxs-lookup"><span data-stu-id="d30e6-177">named</span></span>                                |
| <span data-ttu-id="d30e6-178">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d30e6-178">Default Value</span></span>                        | <span data-ttu-id="d30e6-179">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-179">false</span></span>                                |
| <span data-ttu-id="d30e6-180">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="d30e6-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="d30e6-181">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-181">false</span></span>                                |
| <span data-ttu-id="d30e6-182">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="d30e6-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="d30e6-183">false</span><span class="sxs-lookup"><span data-stu-id="d30e6-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="d30e6-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="d30e6-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="d30e6-185">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="d30e6-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="d30e6-186">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="d30e6-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="d30e6-187">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="d30e6-187">INPUTS</span></span>

<span data-ttu-id="d30e6-188">Этот командлет не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="d30e6-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="d30e6-189">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="d30e6-189">OUTPUTS</span></span>

<span data-ttu-id="d30e6-190">Этот командлет не создает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="d30e6-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="d30e6-191">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="d30e6-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="d30e6-192">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="d30e6-192">EXAMPLE 1</span></span>

<span data-ttu-id="d30e6-193">В этом примере выполняется установка веб-приложения PSWA с использованием значений по умолчанию для параметров **WebApplicationName** (*pswa*) и **WebSiteName** (*веб-сайт по умолчанию*).</span><span class="sxs-lookup"><span data-stu-id="d30e6-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="d30e6-194">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="d30e6-194">EXAMPLE 2</span></span>

<span data-ttu-id="d30e6-195">В этом примере выполняется установка веб-приложения PSWA с тестовым сертификатом и со значениями по умолчанию для параметров **WebApplicationName** и **WebSiteName**.</span><span class="sxs-lookup"><span data-stu-id="d30e6-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="d30e6-196">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="d30e6-196">Related topics</span></span>

- [<span data-ttu-id="d30e6-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d30e6-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="d30e6-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d30e6-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="d30e6-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d30e6-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="d30e6-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="d30e6-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)