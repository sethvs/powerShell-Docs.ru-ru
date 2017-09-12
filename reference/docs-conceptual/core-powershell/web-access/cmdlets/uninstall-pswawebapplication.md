---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "удаление pswawebapplication"
ms.technology: powershell
ms.openlocfilehash: 5fe608b3bfbb90f842f16c1f5a8c51879589cf6d
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="4046e-103">Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="4046e-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="4046e-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="4046e-104">SYNOPSIS</span></span>

<span data-ttu-id="4046e-105">Удаляет веб-приложение Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="4046e-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="4046e-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="4046e-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="4046e-107">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="4046e-108">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="4046e-108">DESCRIPTION</span></span>

<span data-ttu-id="4046e-109">Командлет **Uninstall-PswaWebApplication** удаляет веб-приложение Windows PowerShell и веб-сайт с сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="4046e-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="4046e-110">Командлет не удаляет службы IIS или другие установленные компоненты, так как они требуются для работы Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4046e-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="4046e-111">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="4046e-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="4046e-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="4046e-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="4046e-113">Указывает, что тестовые сертификаты, созданные командлетом **Install\_PswaWebApplication** (с параметром **UseTestCertificate**), удаляются.</span><span class="sxs-lookup"><span data-stu-id="4046e-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="4046e-114">Удаляется только тестовый сертификат с тем же именем, что и созданный командлетом **Install-PswaWebApplication**.</span><span class="sxs-lookup"><span data-stu-id="4046e-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||  
|-|-|
| <span data-ttu-id="4046e-115">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4046e-115">Aliases</span></span>                              | <span data-ttu-id="4046e-116">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="4046e-116">none</span></span>                                 |
| <span data-ttu-id="4046e-117">Требуется?</span><span class="sxs-lookup"><span data-stu-id="4046e-117">Required?</span></span>                            | <span data-ttu-id="4046e-118">false</span><span class="sxs-lookup"><span data-stu-id="4046e-118">false</span></span>                                |
| <span data-ttu-id="4046e-119">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="4046e-119">Position?</span></span>                            | <span data-ttu-id="4046e-120">с именем</span><span class="sxs-lookup"><span data-stu-id="4046e-120">named</span></span>                                |
| <span data-ttu-id="4046e-121">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-121">Default Value</span></span>                        | <span data-ttu-id="4046e-122">верно</span><span class="sxs-lookup"><span data-stu-id="4046e-122">true</span></span>                                 |
| <span data-ttu-id="4046e-123">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4046e-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4046e-124">false</span><span class="sxs-lookup"><span data-stu-id="4046e-124">false</span></span>                                |
| <span data-ttu-id="4046e-125">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4046e-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4046e-126">false</span><span class="sxs-lookup"><span data-stu-id="4046e-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="4046e-127">-WebApplicationName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="4046e-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="4046e-128">Указывает имя удаляемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4046e-128">Specifies the name of the web application to uninstall.</span></span>

|||  
|-|-|
| <span data-ttu-id="4046e-129">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4046e-129">Aliases</span></span>                              | <span data-ttu-id="4046e-130">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="4046e-130">none</span></span>                                 |
| <span data-ttu-id="4046e-131">Требуется?</span><span class="sxs-lookup"><span data-stu-id="4046e-131">Required?</span></span>                            | <span data-ttu-id="4046e-132">false</span><span class="sxs-lookup"><span data-stu-id="4046e-132">false</span></span>                                |
| <span data-ttu-id="4046e-133">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="4046e-133">Position?</span></span>                            | <span data-ttu-id="4046e-134">1</span><span class="sxs-lookup"><span data-stu-id="4046e-134">1</span></span>                                    |
| <span data-ttu-id="4046e-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-135">Default Value</span></span>                        | <span data-ttu-id="4046e-136">pswa</span><span class="sxs-lookup"><span data-stu-id="4046e-136">pswa</span></span>                                 |
| <span data-ttu-id="4046e-137">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4046e-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4046e-138">false</span><span class="sxs-lookup"><span data-stu-id="4046e-138">false</span></span>                                |
| <span data-ttu-id="4046e-139">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4046e-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4046e-140">false</span><span class="sxs-lookup"><span data-stu-id="4046e-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="4046e-141">-WebSiteName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="4046e-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="4046e-142">Задает имя веб-сайта, на котором установлено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4046e-142">Specifies the name of the web site where the web application is installed.</span></span>

|||  
|-|-|
| <span data-ttu-id="4046e-143">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="4046e-143">Aliases</span></span>                              | <span data-ttu-id="4046e-144">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="4046e-144">none</span></span>                                 |
| <span data-ttu-id="4046e-145">Требуется?</span><span class="sxs-lookup"><span data-stu-id="4046e-145">Required?</span></span>                            | <span data-ttu-id="4046e-146">false</span><span class="sxs-lookup"><span data-stu-id="4046e-146">false</span></span>                                |
| <span data-ttu-id="4046e-147">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="4046e-147">Position?</span></span>                            | <span data-ttu-id="4046e-148">с именем</span><span class="sxs-lookup"><span data-stu-id="4046e-148">named</span></span>                                |
| <span data-ttu-id="4046e-149">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-149">Default Value</span></span>                        | <span data-ttu-id="4046e-150">Веб-сайт по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-150">Default Web Site</span></span>                     |
| <span data-ttu-id="4046e-151">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4046e-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4046e-152">false</span><span class="sxs-lookup"><span data-stu-id="4046e-152">false</span></span>                                |
| <span data-ttu-id="4046e-153">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4046e-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4046e-154">false</span><span class="sxs-lookup"><span data-stu-id="4046e-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="4046e-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="4046e-155">-Confirm</span></span>

<span data-ttu-id="4046e-156">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="4046e-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="4046e-157">Требуется?</span><span class="sxs-lookup"><span data-stu-id="4046e-157">Required?</span></span>                            | <span data-ttu-id="4046e-158">false</span><span class="sxs-lookup"><span data-stu-id="4046e-158">false</span></span>                                |
| <span data-ttu-id="4046e-159">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="4046e-159">Position?</span></span>                            | <span data-ttu-id="4046e-160">с именем</span><span class="sxs-lookup"><span data-stu-id="4046e-160">named</span></span>                                |
| <span data-ttu-id="4046e-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-161">Default Value</span></span>                        | <span data-ttu-id="4046e-162">false</span><span class="sxs-lookup"><span data-stu-id="4046e-162">false</span></span>                                |
| <span data-ttu-id="4046e-163">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4046e-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4046e-164">false</span><span class="sxs-lookup"><span data-stu-id="4046e-164">false</span></span>                                |
| <span data-ttu-id="4046e-165">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4046e-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4046e-166">false</span><span class="sxs-lookup"><span data-stu-id="4046e-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="4046e-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="4046e-167">-WhatIf</span></span>

<span data-ttu-id="4046e-168">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="4046e-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="4046e-169">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="4046e-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="4046e-170">Требуется?</span><span class="sxs-lookup"><span data-stu-id="4046e-170">Required?</span></span>                            | <span data-ttu-id="4046e-171">false</span><span class="sxs-lookup"><span data-stu-id="4046e-171">false</span></span>                                |
| <span data-ttu-id="4046e-172">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="4046e-172">Position?</span></span>                            | <span data-ttu-id="4046e-173">с именем</span><span class="sxs-lookup"><span data-stu-id="4046e-173">named</span></span>                                |
| <span data-ttu-id="4046e-174">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4046e-174">Default Value</span></span>                        | <span data-ttu-id="4046e-175">false</span><span class="sxs-lookup"><span data-stu-id="4046e-175">false</span></span>                                |
| <span data-ttu-id="4046e-176">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="4046e-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4046e-177">false</span><span class="sxs-lookup"><span data-stu-id="4046e-177">false</span></span>                                |
| <span data-ttu-id="4046e-178">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="4046e-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4046e-179">false</span><span class="sxs-lookup"><span data-stu-id="4046e-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="4046e-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="4046e-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="4046e-181">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="4046e-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="4046e-182">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="4046e-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="4046e-183">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="4046e-183">INPUTS</span></span>

<span data-ttu-id="4046e-184">Этот командлет не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="4046e-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="4046e-185">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="4046e-185">OUTPUTS</span></span>

<span data-ttu-id="4046e-186">Этот командлет не возвращает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="4046e-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="4046e-187">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="4046e-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="4046e-188">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="4046e-188">EXAMPLE 1</span></span>

<span data-ttu-id="4046e-189">Эта команда удаляет веб-приложение Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4046e-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="4046e-190">С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4046e-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="4046e-191">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="4046e-191">EXAMPLE 2</span></span>

<span data-ttu-id="4046e-192">Эта команда удаляет веб-приложение Windows PowerShell, а также тестовый сертификат, связанный с приложением.</span><span class="sxs-lookup"><span data-stu-id="4046e-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="4046e-193">С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию, включая создание сертификата.</span><span class="sxs-lookup"><span data-stu-id="4046e-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="4046e-194">ПРИМЕР 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="4046e-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="4046e-195">Эта команда удаляет веб-приложение Windows PowerShell, если во время установки были указаны настраиваемый веб-сайт и приложение.</span><span class="sxs-lookup"><span data-stu-id="4046e-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="4046e-196">Эта команда удаляет веб-сайт с именем *MySite* и приложение с именем *TestApplication* и указывает, что тестовые сертификаты, связанные с приложением, также удаляются.</span><span class="sxs-lookup"><span data-stu-id="4046e-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="4046e-197">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="4046e-197">Related topics</span></span>

- [<span data-ttu-id="4046e-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4046e-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="4046e-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4046e-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="4046e-200">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="4046e-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="4046e-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4046e-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="4046e-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4046e-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
