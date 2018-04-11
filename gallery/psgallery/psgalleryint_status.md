---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: psgalleryint_состояние
ms.openlocfilehash: 4f7d300bb07fcbdb100c2fb029f8f66ab260fe7a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
<a name="powershell-gallery-status"></a><span data-ttu-id="b3208-103">Состояние коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3208-103">PowerShell Gallery Status</span></span>
=========================

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a><span data-ttu-id="b3208-104">27.03.2017 — устранено. Не видны отдельные страницы модулей и скриптов</span><span class="sxs-lookup"><span data-stu-id="b3208-104">03/27/2017 - RESOLVED: Unable to see individual module and script pages</span></span>

<span data-ttu-id="b3208-105">__Сводка по влиянию__. Прямые ссылки на отдельные страницы модулей и скриптов на https://www.powershellgallery.com недействительны.</span><span class="sxs-lookup"><span data-stu-id="b3208-105">__Summary of Impact__: Direct links to individual module and script pages on https://www.powershellgallery.com were broken.</span></span> <span data-ttu-id="b3208-106">Это было актуально для всех регионов.</span><span class="sxs-lookup"><span data-stu-id="b3208-106">This was being reported across all the regions.</span></span> <span data-ttu-id="b3208-107">Это не повлияло на командлеты PowerShellGet: Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Script по-прежнему работали.</span><span class="sxs-lookup"><span data-stu-id="b3208-107">This did not impact any of the PowerShellGet cmdlets ie., Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Script continued to work.</span></span>

<span data-ttu-id="b3208-108">__Причина__. Инженеры определили причину как проблему при включении кнопок социальных сетей (например, Facebook) на страницу.</span><span class="sxs-lookup"><span data-stu-id="b3208-108">__Root Cause__: Engineers identified the cause as an issue bringing up social media buttons like Facebook onto the page.</span></span>

<span data-ttu-id="b3208-109">__Решение__. Инженеры исправили проблему, отключив сведения о числе подключений через Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3208-109">__Resolution__: Engineers fixed the problem by disabling the Facebook count information.</span></span>

<span data-ttu-id="b3208-110">__Дальнейшие действия__. Мы открыли обращение о внутреннем отслеживании, чтобы исправить использование API Facebook.</span><span class="sxs-lookup"><span data-stu-id="b3208-110">__Next Steps__: We opened an internal tracking issue to fix our usage of Facebook API.</span></span>

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a><span data-ttu-id="b3208-111">15.12.2016 — не удается отправить сообщения электронной почты через веб-сайт PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="b3208-111">12/15/2016 - Unable to send emails via PowerShellGallery website</span></span>

<span data-ttu-id="b3208-112">__Сводка по влиянию__. Между 13.12.2016 и 15.12.2016 все сообщения, отправленные через функции "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", не были получены администраторами коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3208-112">__Summary of Impact__: Between 12/13/2016 and 12/15/2016, any messages sent via Contact Owners, Manage Owners, Contact Support, or Report Abuse were not received by the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="b3208-113">__Первопричина__. Инженеры выявили, что причина состояла в проблеме проверки подлинности на SMTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="b3208-113">__Root Cause__: Engineers identified the cause as an authentication issue with the SMTP server.</span></span>
<span data-ttu-id="b3208-114">__Решение__. Инженеры смогли устранить проблему проверки подлинности и восстановить подключение к SMTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="b3208-114">__Resolution__: Engineers were able to resolve the authentication issue and restore connection to the SMTP server.</span></span>
<span data-ttu-id="b3208-115">__Дальнейшие действия__. Если вы использовали ссылки "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", чтобы отправить почту по адресу cgadmin@microsoft.com в это время, и не получили ответа, повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="b3208-115">__Next Steps__: If you used the Contact Owners, Manage Owners, Contact Support, or Report Abuse links to send mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="b3208-116">Приносим извинения за причиненные неудобства.</span><span class="sxs-lookup"><span data-stu-id="b3208-116">We apologize for the inconvenience.</span></span>


## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a><span data-ttu-id="b3208-117">10.08.2016 — устранена ошибка: не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="b3208-117">8/10/2016 - Resolved: Unable to send emails to cgadmin@microsoft.com</span></span>
<span data-ttu-id="b3208-118">__Сводка по влиянию__. С 05.08.2016 по 10.08.2016 клиентам не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com или использовать функцию "Обратная связь".</span><span class="sxs-lookup"><span data-stu-id="b3208-118">__Summary of Impact__: Between 8/5/2016 and 8/10/2016, customers were unable to send emails to cgadmin@microsoft.com, or use the Contact Us feature.</span></span>
<span data-ttu-id="b3208-119">__Первопричина__. Инженеры выявили, что причина состояла в изменении конфигурации учетной записи электронной почты.</span><span class="sxs-lookup"><span data-stu-id="b3208-119">__Root Cause__: Engineers identified the cause as a configuration change of the email account.</span></span>
<span data-ttu-id="b3208-120">__Решение__. Инженеры устранили проблему в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b3208-120">__Resolution__: Engineers worked to resolve the configuration issue.</span></span>
<span data-ttu-id="b3208-121">__Дальнейшие действия__. Если вы использовали ссылку "Обратная связь" или отправляли почту по адресу cgadmin@microsoft.com в это время и не получили ответа, повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="b3208-121">__Next Steps__: If you used the Contact Us link or sent mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="b3208-122">Благодарим за терпение.</span><span class="sxs-lookup"><span data-stu-id="b3208-122">Thank you for your patience.</span></span>