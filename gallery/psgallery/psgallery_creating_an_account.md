---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: коллекции,powershell,командлет,psgallery
title: Создание учетной записи коллекции PowerShell
ms.openlocfilehash: c9c263a1926957cbdf059e062326b1903c117f46
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
## <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="f2ca3-103">Создание учетной записи коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2ca3-103">Creating a PowerShell Gallery Account</span></span>

<span data-ttu-id="f2ca3-104">Перед публикацией чего-либо в коллекции PowerShell необходимо создать учетную запись коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-104">A PowerShell Gallery account must be established before publishing anything to the PowerShell Gallery.</span></span>
<span data-ttu-id="f2ca3-105">Учетные записи коллекции PowerShell должны быть связаны с учетной записью с поддержкой электронной почты Azure Active Directory или учетной записью электронной почты Майкрософт (с доменом outlook.com, hotmail.com и т. д.).</span><span class="sxs-lookup"><span data-stu-id="f2ca3-105">The PowerShell Gallery accounts must be linked to an Azure Active Directory email-enabled account, or a Microsoft email account (with a domain of outlook.com, hotmail.com, etc.)</span></span>

<span data-ttu-id="f2ca3-106">Чтобы создать учетную запись коллекции PowerShell, перейдите на веб-сайт по адресу https://PowerShellGallery.com и выберите пункт "Зарегистрировать" (см. на рисунке ниже).</span><span class="sxs-lookup"><span data-stu-id="f2ca3-106">To create a PowerShell Gallery account, go to https://PowerShellGallery.com and click on "Register" (see the image below).</span></span>

![Регистрация новой учетной записи](./images/CreatingAccount-Register.png)

<span data-ttu-id="f2ca3-108">На следующей странице, чтобы использовать эту учетную запись Azure Active Directory, щелкните "Рабочая или учебная учетная запись" и выполните вход с помощью своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-108">In the next page, to use an Azure Active Directory account, select "Work or School Account", and log in with your account.</span></span>
<span data-ttu-id="f2ca3-109">Чтобы использовать учетную запись Майкрософт, такую как в домене Hotmail.com или Outlook.com, выберите "Личная учетная запись" и войдите.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-109">To use a Microsoft account - such as one in a Hotmail.com or Outlook.com domain - choose "Personal Account", and log in.</span></span>

<span data-ttu-id="f2ca3-110">После входа вам будет предложено создать имя пользователя для коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-110">Once you have logged in, you will be prompted to create a username for the PowerShell Gallery.</span></span>
<span data-ttu-id="f2ca3-111">Ознакомьтесь с предоставленными условиями использования и политикой конфиденциальности, введите имя пользователя и щелкните "Зарегистрировать".</span><span class="sxs-lookup"><span data-stu-id="f2ca3-111">Review the Terms of Use and Privacy Policy that are linked in, enter a username, and then click Register.</span></span>

<span data-ttu-id="f2ca3-112">Примечание. Имя учетной записи нельзя изменить после ее создания.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-112">Note: This account name cannot be changed once it is created.</span></span>
<span data-ttu-id="f2ca3-113">Дополнительные сведения см. в статье [Управление владельцами элементов](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners).</span><span class="sxs-lookup"><span data-stu-id="f2ca3-113">See [Managing Item Owners](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) for additional details related to this.</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="f2ca3-114">Рекомендации для учетных записей коллекции PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2ca3-114">Recommended Practices for PowerShell Gallery Accounts</span></span>

<span data-ttu-id="f2ca3-115">Важно, чтобы учетная запись электронной почты, используемая с вашей учетной записью PowerShell Gallery, постоянно отслеживалась.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-115">It is important that the email account used with your PowerShell Gallery account be actively monitored.</span></span>
<span data-ttu-id="f2ca3-116">Связь с владельцами элементов коллекции PowerShell осуществляется через электронную почту с использованием адреса, связанного с вашей учетной записью коллекции PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-116">All communiction with owners of PowerShell Gallery items is through the email using the address associated with your PowerShell Gallery account.</span></span>
<span data-ttu-id="f2ca3-117">Если мы не сможем связаться с владельцем элемента, группе эксплуатации может потребоваться удалить элемент при определенных обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-117">If we are unable to contact an item owner, the Operations team may be required to delete an item under some circumstances.</span></span>

<span data-ttu-id="f2ca3-118">Организации, которые публикуются в коллекции PowerShell, часто создают для этого уникальные учетные записи на Outlook.com или другом домене учетных записей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-118">Organizations that publish to the PowerShell Gallery often create a unique account for that purpose in Outlook.com, or another Microsoft account domain.</span></span>
<span data-ttu-id="f2ca3-119">Во многих случаях эта учетная запись не отслеживается регулярно.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-119">In many cases that account is not regularly monitored.</span></span>
<span data-ttu-id="f2ca3-120">В этом случае мы рекомендуем использовать пересылку Outlook для отправки электронной почты на другую учетную запись, как правило, из организации, которая будет отслеживаться владельцем элемента.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-120">A best practice in that case is to use Outlook Forwarding to send email to another account, typically one within the organization, that will be monitored by the item owner(s).</span></span>

<span data-ttu-id="f2ca3-121">При наличии нескольких владельцев, связанных с элементом, все сообщения, которые поступают из коллекции PowerShell, будут отправляться всем владельцам.</span><span class="sxs-lookup"><span data-stu-id="f2ca3-121">If there are multiple owners associated with an item, all communications that come from the PowerShell Gallery will go to all owners.</span></span>
<span data-ttu-id="f2ca3-122">Дополнительные сведения о добавлении владельцев элементу см. в статье [Управление владельцами элементов](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners).</span><span class="sxs-lookup"><span data-stu-id="f2ca3-122">See [Managing Item Owners](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) for additional details on adding owners to an item.</span></span>