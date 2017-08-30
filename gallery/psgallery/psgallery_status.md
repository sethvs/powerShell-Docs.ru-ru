---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "коллекции,powershell,командлет,psgallery"
title: "psgallery_состояние"
ms.openlocfilehash: d192c706bdbe9aa693f791ef1c8108aeaaae385b
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2017
---
<a name="powershell-gallery-status"></a><span data-ttu-id="5cc52-103">Состояние коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cc52-103">PowerShell Gallery Status</span></span>
=========================
## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a><span data-ttu-id="5cc52-104">01.06.2017. Развертывание в службу автоматизации Azure сейчас недоступно</span><span class="sxs-lookup"><span data-stu-id="5cc52-104">06/01/2017 - Deploy to Azure Automation Currently Unavailable</span></span>

<span data-ttu-id="5cc52-105">__Сводка по влиянию.__ Сейчас развертывание элементов с зависимостями из коллекции PowerShell в службу автоматизации Azure недоступно.</span><span class="sxs-lookup"><span data-stu-id="5cc52-105">__Summary of Impact__: Deploying items with dependencies to Azure Automation from the PowerShell Gallery is currently unavailable.</span></span>  <span data-ttu-id="5cc52-106">Импорт элементов из коллекции PowerShell изнутри службы автоматизации Azure все еще доступен.</span><span class="sxs-lookup"><span data-stu-id="5cc52-106">Importing items from the PowerShell Gallery from inside Azure Automation is still available.</span></span>  
 
<span data-ttu-id="5cc52-107">__Основная причина.__ Элементы с зависимостями от других элементов, ранее развернутые в службу автоматизации Azure, не будут развертываться в эту службу.</span><span class="sxs-lookup"><span data-stu-id="5cc52-107">__Root Cause__: Items that have dependencies on others, and have been previously deployed to Azure Automation, will not be deployed to Azure Automation.</span></span> <span data-ttu-id="5cc52-108">Инженеры обнаружили проблему с тем, как создаются шаблоны ARM для элементов с зависимостями для функции развертывания в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5cc52-108">Engineers have identified an issue with how ARM templates are generated for items with dependencies for the Deploy to Azure Automation functionality.</span></span>

<span data-ttu-id="5cc52-109">__Решение.__ Инженеры работают над устранением проблемы.</span><span class="sxs-lookup"><span data-stu-id="5cc52-109">__Resolution__: Engineers are working to resolve issue.</span></span>  <span data-ttu-id="5cc52-110">Текущее решение для пользователей — импортировать элемент из коллекции PowerShell изнутри службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="5cc52-110">The current workaround for users is to import the item from the PowerShell Gallery from inside Azure Automation.</span></span> 

<span data-ttu-id="5cc52-111">__Дальнейшие действия.__ Инженеры вскоре выпустят исправление.</span><span class="sxs-lookup"><span data-stu-id="5cc52-111">__Next Steps__: Engineers will release the fix shortly.</span></span>  <span data-ttu-id="5cc52-112">Тем временем используйте рекомендуемое решение.</span><span class="sxs-lookup"><span data-stu-id="5cc52-112">In the meantime, please use the recommended workaround.</span></span> 


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a><span data-ttu-id="5cc52-113">11.04.2017 г. — пользователи не могут выполнить вход с помощью учетных записей Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="5cc52-113">04/11/2017 - Users unable to log in with Azure Active Directory (AAD) accounts</span></span>

<span data-ttu-id="5cc52-114">__Сводка по влиянию__. Некоторым пользователям не удалось выполнить вход в коллекцию PowerShell с помощью учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cc52-114">__Summary of Impact__: Some users were unable to log in to the PowerShell Gallery using Azure AD Accounts.</span></span> 
 
<span data-ttu-id="5cc52-115">__Причина__. Во время обновления было пропущено изменение параметра для безопасного взаимодействия с AAD.</span><span class="sxs-lookup"><span data-stu-id="5cc52-115">__Root Cause__: During an update to interact more securely with AAD, a setting change was missed.</span></span> <span data-ttu-id="5cc52-116">В процессе тестирования с целью обнаружения изменений определенные типы учетных записей AAD не использовались, что не повлияло на развертывание.</span><span class="sxs-lookup"><span data-stu-id="5cc52-116">The testing done to validate the change did not include certain types of AAD accounts, so the deployment proceeded.</span></span>

<span data-ttu-id="5cc52-117">__Решение__. Инженерам удалось определить упущенный параметр, и проблема была устранена.</span><span class="sxs-lookup"><span data-stu-id="5cc52-117">__Resolution__: Engineers identified the missing setting and corrected the problem.</span></span> 

<span data-ttu-id="5cc52-118">__Дальнейшие действия__. Планируется последующая доработка тестирования для расширения набора типов учетных записей AAD.</span><span class="sxs-lookup"><span data-stu-id="5cc52-118">__Next Steps__: We will be modifying our testing to include a broader set of AAD account types.</span></span>

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a><span data-ttu-id="5cc52-119">27.03.2017 — устранено. Не видны отдельные страницы модулей и скриптов</span><span class="sxs-lookup"><span data-stu-id="5cc52-119">03/27/2017 - RESOLVED: Unable to see individual module and script pages</span></span>

<span data-ttu-id="5cc52-120">__Сводка по влиянию__. Прямые ссылки на отдельные страницы модулей и скриптов на сайте https://www.powershellgallery.com были недоступны.</span><span class="sxs-lookup"><span data-stu-id="5cc52-120">__Summary of Impact__: Direct links to individual module and script pages on https://www.powershellgallery.com were broken.</span></span> <span data-ttu-id="5cc52-121">Это было актуально для всех регионов.</span><span class="sxs-lookup"><span data-stu-id="5cc52-121">This was being reported across all the regions.</span></span> <span data-ttu-id="5cc52-122">Это не повлияло на командлеты PowerShellGet: Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Scirpt по-прежнему работали.</span><span class="sxs-lookup"><span data-stu-id="5cc52-122">This did not impact any of the PowerShellGet cmdlets ie., Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Scirpt continued to work.</span></span>

<span data-ttu-id="5cc52-123">__Причина__. Инженеры определили причину как проблему при включении кнопок социальных сетей (например, Facebook) на страницу.</span><span class="sxs-lookup"><span data-stu-id="5cc52-123">__Root Cause__: Engineers identified the cause as an issue bringing up social media buttons like Facebook onto the page.</span></span>  

<span data-ttu-id="5cc52-124">__Решение__. Инженеры исправили проблему, отключив сведения о числе подключений через Facebook.</span><span class="sxs-lookup"><span data-stu-id="5cc52-124">__Resolution__: Engineers fixed the problem by disabling the Facebook count information.</span></span>

<span data-ttu-id="5cc52-125">__Дальнейшие действия__. Мы открыли обращение о внутреннем отслеживании, чтобы исправить использование API Facebook.</span><span class="sxs-lookup"><span data-stu-id="5cc52-125">__Next Steps__: We opened an internal tracking issue to fix our usage of Facebook API.</span></span>

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a><span data-ttu-id="5cc52-126">15.12.2016 — не удается отправить сообщения электронной почты через веб-сайт PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="5cc52-126">12/15/2016 - Unable to send emails via PowerShellGallery website</span></span>

<span data-ttu-id="5cc52-127">__Сводка по влиянию__. Между 13.12.2016 и 15.12.2016 все сообщения, отправленные через функции "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", не были получены администраторами коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cc52-127">__Summary of Impact__: Between 12/13/2016 and 12/15/2016, any messages sent via Contact Owners, Manage Owners, Contact Support, or Report Abuse were not received by the PowerShell Gallery Administrators.</span></span>  
<span data-ttu-id="5cc52-128">__Первопричина__. Инженеры выявили, что причина состояла в проблеме проверки подлинности на SMTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="5cc52-128">__Root Cause__: Engineers identified the cause as an authentication issue with the SMTP server.</span></span>  
<span data-ttu-id="5cc52-129">__Решение__. Инженеры смогли устранить проблему проверки подлинности и восстановить подключение к SMTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="5cc52-129">__Resolution__: Engineers were able to resolve the authentication issue and restore connection to the SMTP server.</span></span>  
<span data-ttu-id="5cc52-130">__Дальнейшие действия__. Если вы использовали ссылки "Связаться с владельцами", "Управление владельцами", "Обратитесь в службу поддержки" или "Сообщение о нарушении", чтобы отправить почту по адресу cgadmin@microsoft.com в это время, и не получили ответа, повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="5cc52-130">__Next Steps__: If you used the Contact Owners, Manage Owners, Contact Support, or Report Abuse links to send mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="5cc52-131">Приносим извинения за причиненные неудобства.</span><span class="sxs-lookup"><span data-stu-id="5cc52-131">We apologize for the inconvenience.</span></span>  



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a><span data-ttu-id="5cc52-132">10.08.2016 — устранена ошибка: не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="5cc52-132">8/10/2016 - Resolved: Unable to send emails to cgadmin@microsoft.com</span></span>

<span data-ttu-id="5cc52-133">__Сводка по влиянию__. С 05.08.2016 по 10.08.2016 клиентам не удавалось отправлять электронные письма по адресу cgadmin@microsoft.com или использовать функцию "Обратная связь".</span><span class="sxs-lookup"><span data-stu-id="5cc52-133">__Summary of Impact__: Between 8/5/2016 and 8/10/2016, customers were unable to send emails to cgadmin@microsoft.com, or use the Contact Us feature.</span></span>  
<span data-ttu-id="5cc52-134">__Первопричина__. Инженеры выявили, что причина состояла в изменении конфигурации учетной записи электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5cc52-134">__Root Cause__: Engineers identified the cause as a configuration change of the email account.</span></span>  
<span data-ttu-id="5cc52-135">__Решение__. Инженеры устранили проблему в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5cc52-135">__Resolution__: Engineers worked to resolve the configuration issue.</span></span>  
<span data-ttu-id="5cc52-136">__Дальнейшие действия__. Если вы использовали ссылку "Обратная связь" или отправляли почту по адресу cgadmin@microsoft.com в это время и не получили ответа, повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="5cc52-136">__Next Steps__: If you used the Contact Us link or sent mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="5cc52-137">Благодарим за терпение.</span><span class="sxs-lookup"><span data-stu-id="5cc52-137">Thank you for your patience.</span></span>



## <a name="7132016---download-items-failed"></a><span data-ttu-id="5cc52-138">13.07.2016 — сбой скачивания элементов</span><span class="sxs-lookup"><span data-stu-id="5cc52-138">7/13/2016 - Download Items Failed</span></span>

<span data-ttu-id="5cc52-139">__Сводка по влиянию__. С 11.07.2016 по 13.07.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cc52-139">__Summary of Impact__: Between 7/11/2016 and 7/13/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="5cc52-140">Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.</span><span class="sxs-lookup"><span data-stu-id="5cc52-140">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
PS C:\> Install-Module xStorage 
PackageManagement\Install-Package : Package 'xStorage' failed to be installed because: 
End of Central Directory record could not be found. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1375 char:21 + ... 
$null = PackageManagement\Install-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + CategoryInfo : InvalidResult: 
(xStorage:String) [Install-Package], Exception + FullyQualifiedErrorId : Package '{0}' 
failed to be installed because: {1},Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage 
```

<span data-ttu-id="5cc52-141">__Предварительная первопричина__. Инженеры выявили проблему в сети доставки содержимого Azure (CDN), развернутой для коллекции PowerShell 11.07.2016.</span><span class="sxs-lookup"><span data-stu-id="5cc52-141">__Preliminary root cause__: Engineers identified an issue with Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 7/11/2016.</span></span>  
<span data-ttu-id="5cc52-142">__Устранение рисков__. Инженеры отключили Azure CDN в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cc52-142">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>  
<span data-ttu-id="5cc52-143">__Дальнейшие действия__. Мы находимся в процессе поиска первопричины и разрабатываем решение, чтобы предотвратить появление проблемы в будущем.</span><span class="sxs-lookup"><span data-stu-id="5cc52-143">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>


## <a name="5192016---download-items-failed"></a><span data-ttu-id="5cc52-144">19.05.2016 — сбой скачивания элементов</span><span class="sxs-lookup"><span data-stu-id="5cc52-144">5/19/2016 - Download Items Failed</span></span>
<span data-ttu-id="5cc52-145">__Сводка по влиянию__. С 17.05.2016 по 19.05.2016 у ряда клиентов возникали проблемы со скачиванием элементов из коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cc52-145">__Summary of Impact__: Between 5/17/2016 and 5/19/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="5cc52-146">Скорее всего, проблема проявлялась в виде следующего сообщения об ошибке, возвращаемого из Install-Module/Install-Script и Save-Module/Save-Script.</span><span class="sxs-lookup"><span data-stu-id="5cc52-146">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
VERBOSE: Hash for package 'AzureRM.OperationalInsights' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='AzureRM.OperationalInsights', version='1.0.8',
destination='C:\Users\jbritt\AppData\Local\Temp\2\1741355729'
WARNING: Package 'AzureRM.OperationalInsights' failed to be installed because: 
End of Central Directory record could not be found. 
WARNING: Dependent Package 'AzureRM.OperationalInsights' failed to install. 
WARNING: Package 'AzureRM' failed to install. 
VERBOSE: Module 'AzureRM.Network' was saved successfully. 
VERBOSE: Saving the dependency module 'AzureRM.NotificationHubs' with version '1.0.8' for the 
module 'AzureRM'. 
VERBOSE: Module 'AzureRM.NotificationHubs' was saved successfully. 
PackageManagement\Save-Package : Unable to save the module 'AzureRM'. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1187 char:21 + 
$null = PackageManagement\Save-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + 
CategoryInfo : InvalidOperation: (Microsoft.Power...ets.SavePackage:SavePackage) 
[Save-Package], Exception + FullyQualifiedErrorId : ProviderFailToDownloadFile,
Microsoft.PowerShell.PackageManagement.Cmdlets.SavePackage 
```

<span data-ttu-id="5cc52-147">__Предварительная первопричина__. Инженеры обнаружили сбой в базовом поставщике сети доставки содержимого Azure (CDN), развернутой для коллекции PowerShell 17.05.2016.</span><span class="sxs-lookup"><span data-stu-id="5cc52-147">__Preliminary root cause__: Engineers identified an outage in the underlying provider of Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 5/17/2016.</span></span>  
<span data-ttu-id="5cc52-148">__Устранение рисков__. Инженеры отключили Azure CDN в коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cc52-148">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>  
<span data-ttu-id="5cc52-149">__Дальнейшие действия__. Мы находимся в процессе поиска первопричины и разрабатываем решение, чтобы предотвратить появление проблемы в будущем.</span><span class="sxs-lookup"><span data-stu-id="5cc52-149">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>

