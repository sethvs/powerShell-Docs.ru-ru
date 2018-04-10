---
description: ''
ms.topic: article
ms.prod: powershell
keywords: powershell,командлет
ms.date: 12/12/2016
title: удаление pswawebapplication
ms.technology: powershell
ms.openlocfilehash: 139c8358a24e54dec630f8c78737728330ba4aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="e339a-103">Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="e339a-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="e339a-104">КРАТКИЙ ОБЗОР</span><span class="sxs-lookup"><span data-stu-id="e339a-104">SYNOPSIS</span></span>

<span data-ttu-id="e339a-105">Удаляет веб-приложение Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="e339a-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="e339a-106">СИНТАКСИС</span><span class="sxs-lookup"><span data-stu-id="e339a-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="e339a-107">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="e339a-108">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="e339a-108">DESCRIPTION</span></span>

<span data-ttu-id="e339a-109">Командлет **Uninstall-PswaWebApplication** удаляет веб-приложение Windows PowerShell и веб-сайт с сервера IIS.</span><span class="sxs-lookup"><span data-stu-id="e339a-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="e339a-110">Командлет не удаляет службы IIS или другие установленные компоненты, так как они требуются для работы Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e339a-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="e339a-111">ПАРАМЕТРЫ</span><span class="sxs-lookup"><span data-stu-id="e339a-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="e339a-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="e339a-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="e339a-113">Указывает, что тестовые сертификаты, созданные командлетом **Install\_PswaWebApplication** (с параметром **UseTestCertificate**), удаляются.</span><span class="sxs-lookup"><span data-stu-id="e339a-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="e339a-114">Удаляется только тестовый сертификат с тем же именем, что и созданный командлетом **Install-PswaWebApplication**.</span><span class="sxs-lookup"><span data-stu-id="e339a-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||
|-|-|
| <span data-ttu-id="e339a-115">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="e339a-115">Aliases</span></span>                              | <span data-ttu-id="e339a-116">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="e339a-116">none</span></span>                                 |
| <span data-ttu-id="e339a-117">Требуется?</span><span class="sxs-lookup"><span data-stu-id="e339a-117">Required?</span></span>                            | <span data-ttu-id="e339a-118">false</span><span class="sxs-lookup"><span data-stu-id="e339a-118">false</span></span>                                |
| <span data-ttu-id="e339a-119">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="e339a-119">Position?</span></span>                            | <span data-ttu-id="e339a-120">с именем</span><span class="sxs-lookup"><span data-stu-id="e339a-120">named</span></span>                                |
| <span data-ttu-id="e339a-121">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-121">Default Value</span></span>                        | <span data-ttu-id="e339a-122">верно</span><span class="sxs-lookup"><span data-stu-id="e339a-122">true</span></span>                                 |
| <span data-ttu-id="e339a-123">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="e339a-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e339a-124">false</span><span class="sxs-lookup"><span data-stu-id="e339a-124">false</span></span>                                |
| <span data-ttu-id="e339a-125">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="e339a-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e339a-126">false</span><span class="sxs-lookup"><span data-stu-id="e339a-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="e339a-127">-WebApplicationName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="e339a-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="e339a-128">Указывает имя удаляемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e339a-128">Specifies the name of the web application to uninstall.</span></span>

|||
|-|-|
| <span data-ttu-id="e339a-129">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="e339a-129">Aliases</span></span>                              | <span data-ttu-id="e339a-130">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="e339a-130">none</span></span>                                 |
| <span data-ttu-id="e339a-131">Требуется?</span><span class="sxs-lookup"><span data-stu-id="e339a-131">Required?</span></span>                            | <span data-ttu-id="e339a-132">false</span><span class="sxs-lookup"><span data-stu-id="e339a-132">false</span></span>                                |
| <span data-ttu-id="e339a-133">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="e339a-133">Position?</span></span>                            | <span data-ttu-id="e339a-134">1</span><span class="sxs-lookup"><span data-stu-id="e339a-134">1</span></span>                                    |
| <span data-ttu-id="e339a-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-135">Default Value</span></span>                        | <span data-ttu-id="e339a-136">pswa</span><span class="sxs-lookup"><span data-stu-id="e339a-136">pswa</span></span>                                 |
| <span data-ttu-id="e339a-137">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="e339a-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e339a-138">false</span><span class="sxs-lookup"><span data-stu-id="e339a-138">false</span></span>                                |
| <span data-ttu-id="e339a-139">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="e339a-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e339a-140">false</span><span class="sxs-lookup"><span data-stu-id="e339a-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="e339a-141">-WebSiteName &lt;строка&gt;</span><span class="sxs-lookup"><span data-stu-id="e339a-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="e339a-142">Задает имя веб-сайта, на котором установлено веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e339a-142">Specifies the name of the web site where the web application is installed.</span></span>

|||
|-|-|
| <span data-ttu-id="e339a-143">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="e339a-143">Aliases</span></span>                              | <span data-ttu-id="e339a-144">отсутствуют</span><span class="sxs-lookup"><span data-stu-id="e339a-144">none</span></span>                                 |
| <span data-ttu-id="e339a-145">Требуется?</span><span class="sxs-lookup"><span data-stu-id="e339a-145">Required?</span></span>                            | <span data-ttu-id="e339a-146">false</span><span class="sxs-lookup"><span data-stu-id="e339a-146">false</span></span>                                |
| <span data-ttu-id="e339a-147">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="e339a-147">Position?</span></span>                            | <span data-ttu-id="e339a-148">с именем</span><span class="sxs-lookup"><span data-stu-id="e339a-148">named</span></span>                                |
| <span data-ttu-id="e339a-149">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-149">Default Value</span></span>                        | <span data-ttu-id="e339a-150">Веб-сайт по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-150">Default Web Site</span></span>                     |
| <span data-ttu-id="e339a-151">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="e339a-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e339a-152">false</span><span class="sxs-lookup"><span data-stu-id="e339a-152">false</span></span>                                |
| <span data-ttu-id="e339a-153">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="e339a-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e339a-154">false</span><span class="sxs-lookup"><span data-stu-id="e339a-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="e339a-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="e339a-155">-Confirm</span></span>

<span data-ttu-id="e339a-156">Запрос на подтверждение перед выполнением командлета.</span><span class="sxs-lookup"><span data-stu-id="e339a-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="e339a-157">Требуется?</span><span class="sxs-lookup"><span data-stu-id="e339a-157">Required?</span></span>                            | <span data-ttu-id="e339a-158">false</span><span class="sxs-lookup"><span data-stu-id="e339a-158">false</span></span>                                |
| <span data-ttu-id="e339a-159">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="e339a-159">Position?</span></span>                            | <span data-ttu-id="e339a-160">с именем</span><span class="sxs-lookup"><span data-stu-id="e339a-160">named</span></span>                                |
| <span data-ttu-id="e339a-161">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-161">Default Value</span></span>                        | <span data-ttu-id="e339a-162">false</span><span class="sxs-lookup"><span data-stu-id="e339a-162">false</span></span>                                |
| <span data-ttu-id="e339a-163">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="e339a-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e339a-164">false</span><span class="sxs-lookup"><span data-stu-id="e339a-164">false</span></span>                                |
| <span data-ttu-id="e339a-165">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="e339a-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e339a-166">false</span><span class="sxs-lookup"><span data-stu-id="e339a-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="e339a-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="e339a-167">-WhatIf</span></span>

<span data-ttu-id="e339a-168">Показывает, что произойдет при запуске командлета.</span><span class="sxs-lookup"><span data-stu-id="e339a-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="e339a-169">Командлет не запущен.</span><span class="sxs-lookup"><span data-stu-id="e339a-169">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="e339a-170">Требуется?</span><span class="sxs-lookup"><span data-stu-id="e339a-170">Required?</span></span>                            | <span data-ttu-id="e339a-171">false</span><span class="sxs-lookup"><span data-stu-id="e339a-171">false</span></span>                                |
| <span data-ttu-id="e339a-172">Указать положение?</span><span class="sxs-lookup"><span data-stu-id="e339a-172">Position?</span></span>                            | <span data-ttu-id="e339a-173">с именем</span><span class="sxs-lookup"><span data-stu-id="e339a-173">named</span></span>                                |
| <span data-ttu-id="e339a-174">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e339a-174">Default Value</span></span>                        | <span data-ttu-id="e339a-175">false</span><span class="sxs-lookup"><span data-stu-id="e339a-175">false</span></span>                                |
| <span data-ttu-id="e339a-176">Принимать входные данные конвейера?</span><span class="sxs-lookup"><span data-stu-id="e339a-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e339a-177">false</span><span class="sxs-lookup"><span data-stu-id="e339a-177">false</span></span>                                |
| <span data-ttu-id="e339a-178">Принимать подстановочные знаки?</span><span class="sxs-lookup"><span data-stu-id="e339a-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e339a-179">false</span><span class="sxs-lookup"><span data-stu-id="e339a-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="e339a-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="e339a-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="e339a-181">Данный командлет поддерживает общие параметры -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="e339a-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="e339a-182">Дополнительные сведения см. в разделе [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="e339a-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="e339a-183">ВХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="e339a-183">INPUTS</span></span>

<span data-ttu-id="e339a-184">Этот командлет не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="e339a-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="e339a-185">ВЫХОДНЫЕ ДАННЫЕ</span><span class="sxs-lookup"><span data-stu-id="e339a-185">OUTPUTS</span></span>

<span data-ttu-id="e339a-186">Этот командлет не возвращает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="e339a-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="e339a-187">ПРИМЕРЫ</span><span class="sxs-lookup"><span data-stu-id="e339a-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="e339a-188">ПРИМЕР 1</span><span class="sxs-lookup"><span data-stu-id="e339a-188">EXAMPLE 1</span></span>

<span data-ttu-id="e339a-189">Эта команда удаляет веб-приложение Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e339a-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="e339a-190">С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e339a-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="e339a-191">ПРИМЕР 2</span><span class="sxs-lookup"><span data-stu-id="e339a-191">EXAMPLE 2</span></span>

<span data-ttu-id="e339a-192">Эта команда удаляет веб-приложение Windows PowerShell, а также тестовый сертификат, связанный с приложением.</span><span class="sxs-lookup"><span data-stu-id="e339a-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="e339a-193">С помощью этого командлета можно удалить веб-приложение Windows PowerShell, если оно установлено с использованием значений по умолчанию, включая создание сертификата.</span><span class="sxs-lookup"><span data-stu-id="e339a-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="e339a-194">ПРИМЕР 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="e339a-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="e339a-195">Эта команда удаляет веб-приложение Windows PowerShell, если во время установки были указаны настраиваемый веб-сайт и приложение.</span><span class="sxs-lookup"><span data-stu-id="e339a-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="e339a-196">Эта команда удаляет веб-сайт с именем *MySite* и приложение с именем *TestApplication* и указывает, что тестовые сертификаты, связанные с приложением, также удаляются.</span><span class="sxs-lookup"><span data-stu-id="e339a-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="e339a-197">Связанные темы</span><span class="sxs-lookup"><span data-stu-id="e339a-197">Related topics</span></span>

- [<span data-ttu-id="e339a-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e339a-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="e339a-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e339a-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="e339a-200">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="e339a-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="e339a-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e339a-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="e339a-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e339a-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)