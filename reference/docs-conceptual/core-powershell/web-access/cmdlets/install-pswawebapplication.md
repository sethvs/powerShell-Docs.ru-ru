---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "установка pswawebapplication"
ms.technology: powershell
ms.openlocfilehash: a608a6272d3eae56ccf808b9d94525ca39df50cb
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="85a52-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="85a52-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="85a52-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="85a52-104">SYNOPSIS</span></span>

<span data-ttu-id="85a52-105">Настраивает веб-приложение Windows PowerShell® Web Access в IIS.</span><span class="sxs-lookup"><span data-stu-id="85a52-105">Configures the Windows PowerShell® Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="85a52-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="85a52-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="85a52-107">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="85a52-108">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="85a52-108">DESCRIPTION</span></span>

<span data-ttu-id="85a52-109">Командлет **Install-PswaWebApplication** настраивает веб-приложение Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="85a52-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="85a52-110">Этот командлет устанавливает веб-приложение, связывает его с веб-сайтом и при необходимости создает тестовый сертификат SSL с помощью параметра **useTestCertificate**.</span><span class="sxs-lookup"><span data-stu-id="85a52-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="85a52-111">Для обеспечения безопасности веб-администраторам не следует использовать тестовый сертификат для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="85a52-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="85a52-112">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="85a52-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="85a52-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="85a52-113">-UseTestCertificate</span></span>

<span data-ttu-id="85a52-114">Указывает, что создается тестовый сертификат.</span><span class="sxs-lookup"><span data-stu-id="85a52-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="85a52-115">Если этот параметр имеет значение true, то командлет создает тестовый сертификат и настраивает веб-приложение Windows PowerShell Web Access для использования сертификата для HTTPS-запросов.</span><span class="sxs-lookup"><span data-stu-id="85a52-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="85a52-116">Если этот параметр имеет значение false, то ни сертификат, ни привязка не создаются.</span><span class="sxs-lookup"><span data-stu-id="85a52-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="85a52-117">Задайте значение false, если для Windows PowerShell Web Access используется другой сертификат.</span><span class="sxs-lookup"><span data-stu-id="85a52-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||  
|-|-|
| <span data-ttu-id="85a52-118">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="85a52-118">Aliases</span></span>                              | <span data-ttu-id="85a52-119">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="85a52-119">none</span></span>                                 |
| <span data-ttu-id="85a52-120">Требуется?</span><span class="sxs-lookup"><span data-stu-id="85a52-120">Required?</span></span>                            | <span data-ttu-id="85a52-121">false</span><span class="sxs-lookup"><span data-stu-id="85a52-121">false</span></span>                                |
| <span data-ttu-id="85a52-122">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="85a52-122">Position?</span></span>                            | <span data-ttu-id="85a52-123">с именем</span><span class="sxs-lookup"><span data-stu-id="85a52-123">named</span></span>                                |
| <span data-ttu-id="85a52-124">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-124">Default Value</span></span>                        | <span data-ttu-id="85a52-125">верно</span><span class="sxs-lookup"><span data-stu-id="85a52-125">true</span></span>                                 |
| <span data-ttu-id="85a52-126">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="85a52-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="85a52-127">false</span><span class="sxs-lookup"><span data-stu-id="85a52-127">false</span></span>                                |
| <span data-ttu-id="85a52-128">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="85a52-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="85a52-129">false</span><span class="sxs-lookup"><span data-stu-id="85a52-129">false</span></span>                                |

### <a name="-webapplicationnameltstringgt"></a><span data-ttu-id="85a52-130">-WebApplicationName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="85a52-130">-WebApplicationName&lt;String&gt;</span></span>

<span data-ttu-id="85a52-131">Указывает имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="85a52-131">Specifies the name for your web application.</span></span> <span data-ttu-id="85a52-132">Отображается как последняя часть URL-адреса Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="85a52-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||  
|-|-|
| <span data-ttu-id="85a52-133">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="85a52-133">Aliases</span></span>                              | <span data-ttu-id="85a52-134">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="85a52-134">none</span></span>                                 |
| <span data-ttu-id="85a52-135">Требуется?</span><span class="sxs-lookup"><span data-stu-id="85a52-135">Required?</span></span>                            | <span data-ttu-id="85a52-136">false</span><span class="sxs-lookup"><span data-stu-id="85a52-136">false</span></span>                                |
| <span data-ttu-id="85a52-137">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="85a52-137">Position?</span></span>                            | <span data-ttu-id="85a52-138">1</span><span class="sxs-lookup"><span data-stu-id="85a52-138">1</span></span>                                    |
| <span data-ttu-id="85a52-139">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-139">Default Value</span></span>                        | <span data-ttu-id="85a52-140">pswa</span><span class="sxs-lookup"><span data-stu-id="85a52-140">pswa</span></span>                                 |
| <span data-ttu-id="85a52-141">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="85a52-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="85a52-142">false</span><span class="sxs-lookup"><span data-stu-id="85a52-142">false</span></span>                                |
| <span data-ttu-id="85a52-143">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="85a52-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="85a52-144">false</span><span class="sxs-lookup"><span data-stu-id="85a52-144">false</span></span>                                |

### <a name="-websitenameltstringgt"></a><span data-ttu-id="85a52-145">-WebSiteName&lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="85a52-145">-WebSiteName&lt;String&gt;</span></span>

<span data-ttu-id="85a52-146">Задает имя веб-сайта веб-сервера (IIS) для установки этого веб-приложения Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="85a52-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||  
|-|-|
| <span data-ttu-id="85a52-147">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="85a52-147">Aliases</span></span>                              | <span data-ttu-id="85a52-148">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="85a52-148">none</span></span>                                 |
| <span data-ttu-id="85a52-149">Требуется?</span><span class="sxs-lookup"><span data-stu-id="85a52-149">Required?</span></span>                            | <span data-ttu-id="85a52-150">false</span><span class="sxs-lookup"><span data-stu-id="85a52-150">false</span></span>                                |
| <span data-ttu-id="85a52-151">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="85a52-151">Position?</span></span>                            | <span data-ttu-id="85a52-152">с именем</span><span class="sxs-lookup"><span data-stu-id="85a52-152">named</span></span>                                |
| <span data-ttu-id="85a52-153">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-153">Default Value</span></span>                        | <span data-ttu-id="85a52-154">Веб-сайт по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-154">Default Web Site</span></span>                     |
| <span data-ttu-id="85a52-155">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="85a52-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="85a52-156">false</span><span class="sxs-lookup"><span data-stu-id="85a52-156">false</span></span>                                |
| <span data-ttu-id="85a52-157">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="85a52-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="85a52-158">false</span><span class="sxs-lookup"><span data-stu-id="85a52-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="85a52-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="85a52-159">-Confirm</span></span>

<span data-ttu-id="85a52-160">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="85a52-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="85a52-161">Требуется?</span><span class="sxs-lookup"><span data-stu-id="85a52-161">Required?</span></span>                            | <span data-ttu-id="85a52-162">false</span><span class="sxs-lookup"><span data-stu-id="85a52-162">false</span></span>                                |
| <span data-ttu-id="85a52-163">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="85a52-163">Position?</span></span>                            | <span data-ttu-id="85a52-164">с именем</span><span class="sxs-lookup"><span data-stu-id="85a52-164">named</span></span>                                |
| <span data-ttu-id="85a52-165">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-165">Default Value</span></span>                        | <span data-ttu-id="85a52-166">false</span><span class="sxs-lookup"><span data-stu-id="85a52-166">false</span></span>                                |
| <span data-ttu-id="85a52-167">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="85a52-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="85a52-168">false</span><span class="sxs-lookup"><span data-stu-id="85a52-168">false</span></span>                                |
| <span data-ttu-id="85a52-169">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="85a52-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="85a52-170">false</span><span class="sxs-lookup"><span data-stu-id="85a52-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="85a52-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="85a52-171">-WhatIf</span></span>

<span data-ttu-id="85a52-172">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="85a52-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="85a52-173">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="85a52-173">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="85a52-174">Требуется?</span><span class="sxs-lookup"><span data-stu-id="85a52-174">Required?</span></span>                            | <span data-ttu-id="85a52-175">false</span><span class="sxs-lookup"><span data-stu-id="85a52-175">false</span></span>                                |
| <span data-ttu-id="85a52-176">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="85a52-176">Position?</span></span>                            | <span data-ttu-id="85a52-177">с именем</span><span class="sxs-lookup"><span data-stu-id="85a52-177">named</span></span>                                |
| <span data-ttu-id="85a52-178">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="85a52-178">Default Value</span></span>                        | <span data-ttu-id="85a52-179">false</span><span class="sxs-lookup"><span data-stu-id="85a52-179">false</span></span>                                |
| <span data-ttu-id="85a52-180">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="85a52-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="85a52-181">false</span><span class="sxs-lookup"><span data-stu-id="85a52-181">false</span></span>                                |
| <span data-ttu-id="85a52-182">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="85a52-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="85a52-183">false</span><span class="sxs-lookup"><span data-stu-id="85a52-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="85a52-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="85a52-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="85a52-185">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="85a52-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="85a52-186">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="85a52-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="85a52-187">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="85a52-187">INPUTS</span></span>

<span data-ttu-id="85a52-188">Этот командлет не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="85a52-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="85a52-189">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="85a52-189">OUTPUTS</span></span>

<span data-ttu-id="85a52-190">Этот командлет не создает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="85a52-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="85a52-191">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="85a52-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="85a52-192">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="85a52-192">EXAMPLE 1</span></span>

<span data-ttu-id="85a52-193">В этом примере выполняется установка веб-приложения PSWA с использованием значений по умолчанию для параметров **WebApplicationName** (*pswa*) и **WebSiteName** (*веб-сайт по умолчанию*).</span><span class="sxs-lookup"><span data-stu-id="85a52-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="85a52-194">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="85a52-194">EXAMPLE 2</span></span>

<span data-ttu-id="85a52-195">В этом примере выполняется установка веб-приложения PSWA с тестовым сертификатом и со значениями по умолчанию для параметров **WebApplicationName** и **WebSiteName**.</span><span class="sxs-lookup"><span data-stu-id="85a52-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="85a52-196">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="85a52-196">Related topics</span></span>

- [<span data-ttu-id="85a52-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="85a52-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="85a52-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="85a52-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="85a52-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="85a52-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="85a52-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="85a52-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
