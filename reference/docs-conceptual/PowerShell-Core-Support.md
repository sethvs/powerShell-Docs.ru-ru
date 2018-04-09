# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="30c4f-101">Жизненный цикл поддержки PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="30c4f-101">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="30c4f-102">PowerShell Core — это отдельный набор средств и компонентов, поставляемых, устанавливаемых и настраиваемых отдельно от Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30c4f-102">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="30c4f-103">Поэтому на PowerShell Core не распространяются лицензионные соглашения Windows 7, 8.1, 10 или Windows Server.</span><span class="sxs-lookup"><span data-stu-id="30c4f-103">Therefore, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="30c4f-104">Однако PowerShell Core поддерживается в рамках традиционных соглашений о поддержке корпорации Майкрософт, включая [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement] и [Microsoft Software Assurance][assurance].</span><span class="sxs-lookup"><span data-stu-id="30c4f-104">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="30c4f-105">Вы также можете оплатить [техническую поддержку][] по PowerShell Core, направив в службу поддержки запрос о своей проблеме.</span><span class="sxs-lookup"><span data-stu-id="30c4f-105">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

<span data-ttu-id="30c4f-106">Мы также предлагаем [поддержку сообщества][] на GitHub, где вы можете зарегистрировать вопрос, ошибку или запрос функции.</span><span class="sxs-lookup"><span data-stu-id="30c4f-106">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="30c4f-107">Кроме того, вы можете обратиться за помощью к другим членам сообщества на сайтах [Microsoft Community][] или Microsoft [PowerShell Tech Community][].</span><span class="sxs-lookup"><span data-stu-id="30c4f-107">Alternatively, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="30c4f-108">Мы не можем гарантировать, что там вы оперативно получите решение своей проблемы.</span><span class="sxs-lookup"><span data-stu-id="30c4f-108">We offer no guarantee there that your issue will be addressed or resolved in a timely manner.</span></span>
<span data-ttu-id="30c4f-109">Если ваша проблема требует немедленного вмешательства, следует использовать традиционные платные варианты поддержки.</span><span class="sxs-lookup"><span data-stu-id="30c4f-109">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="30c4f-110">Жизненный цикл PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="30c4f-110">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="30c4f-111">В PowerShell Core внедряется [политика современного жизненного цикла Майкрософт][modern].</span><span class="sxs-lookup"><span data-stu-id="30c4f-111">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="30c4f-112">Этот жизненный цикл поддержки предназначен для предоставления клиентам актуальных версий.</span><span class="sxs-lookup"><span data-stu-id="30c4f-112">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="30c4f-113">Ветвь версии 6.x продукта PowerShell Core будет обновляться примерно каждые шесть месяцев (то есть 6.0, 6.1, 6.2 и т. д.)</span><span class="sxs-lookup"><span data-stu-id="30c4f-113">The version 6.x branch of PowerShell Core will be updated approximately once every six months (e.g. 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30c4f-114">Чтобы продолжить получать поддержку, вам нужно обновить продукт в течение шести месяцев после выпуска версии с новым дополнительным номером.</span><span class="sxs-lookup"><span data-stu-id="30c4f-114">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="30c4f-115">Например, если PowerShell Core 6.1 выпущена 1 июля 2018 года, для сохранения поддержки вам следует обновиться до PowerShell Core 6.1 к 1 января 2019 года.</span><span class="sxs-lookup"><span data-stu-id="30c4f-115">For example, if PowerShell Core 6.1 is released on July 1st, 2018, you would be expected to update to PowerShell Core 6.1 by January 1st, 2019 to maintain support.</span></span>

![Жизненный цикл ветви PowerShell Core][lifecycle-chart]

<span data-ttu-id="30c4f-117">Политика современного жизненного цикла также требует, чтобы корпорация Майкрософт предоставляла клиентам уведомление за 12 месяцев до прекращения поддержки продукта (т. е. PowerShell Core).</span><span class="sxs-lookup"><span data-stu-id="30c4f-117">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (i.e. PowerShell Core).</span></span>

<span data-ttu-id="30c4f-118">В конечном счете, мы планируем реализовать для PowerShell Core подход "долгосрочного обслуживания", чтобы нам требовалось лишь проводить обслуживание и выпускать обновления для системы безопасности, чтобы обеспечить поддержку определенной ветви или версии 6.x.</span><span class="sxs-lookup"><span data-stu-id="30c4f-118">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach where we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="30c4f-119">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="30c4f-119">Supported platforms</span></span>

<span data-ttu-id="30c4f-120">PowerShell Core официально поддерживается на следующих платформах:</span><span class="sxs-lookup"><span data-stu-id="30c4f-120">PowerShell Core is officially supported on the following platforms:</span></span>

* <span data-ttu-id="30c4f-121">Windows 7, 8.1 и 10</span><span class="sxs-lookup"><span data-stu-id="30c4f-121">Windows 7, 8.1, and 10</span></span>
* <span data-ttu-id="30c4f-122">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="30c4f-122">Windows Server 2008 R2, 2012 R2, 2016</span></span>
* <span data-ttu-id="30c4f-123">[Windows Server Semi-Annual Channel][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="30c4f-123">[Windows Server Semi-Annual Channel][semi-annual]</span></span>
* <span data-ttu-id="30c4f-124">Ubuntu 14.04, 16.04 и 17.04</span><span class="sxs-lookup"><span data-stu-id="30c4f-124">Ubuntu 14.04, 16.04, and 17.04</span></span>
* <span data-ttu-id="30c4f-125">Debian 8.7+ и 9</span><span class="sxs-lookup"><span data-stu-id="30c4f-125">Debian 8.7+, and 9</span></span>
* <span data-ttu-id="30c4f-126">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="30c4f-126">CentOS 7</span></span>
* <span data-ttu-id="30c4f-127">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="30c4f-127">Red Hat Enterprise Linux 7</span></span>
* <span data-ttu-id="30c4f-128">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="30c4f-128">OpenSUSE 42.2</span></span>
* <span data-ttu-id="30c4f-129">Fedora 25, 26</span><span class="sxs-lookup"><span data-stu-id="30c4f-129">Fedora 25, 26</span></span>
* <span data-ttu-id="30c4f-130">macOS 10.12+</span><span class="sxs-lookup"><span data-stu-id="30c4f-130">macOS 10.12+</span></span>

<span data-ttu-id="30c4f-131">Наше сообщество также предоставило пакеты для следующих платформ, однако они не поддерживаются официально:</span><span class="sxs-lookup"><span data-stu-id="30c4f-131">Our community has also contributed packages for the following platforms, but they are not officially suppported:</span></span>

* <span data-ttu-id="30c4f-132">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="30c4f-132">Arch Linux</span></span>
* <span data-ttu-id="30c4f-133">Kali Linux</span><span class="sxs-lookup"><span data-stu-id="30c4f-133">Kali Linux</span></span>
* <span data-ttu-id="30c4f-134">AppImage (работает на нескольких платформах Linux)</span><span class="sxs-lookup"><span data-stu-id="30c4f-134">AppImage (works on multiple Linux platforms)</span></span>

## <a name="notes-on-licensing"></a><span data-ttu-id="30c4f-135">Замечания по лицензированию</span><span class="sxs-lookup"><span data-stu-id="30c4f-135">Notes on licensing</span></span>

<span data-ttu-id="30c4f-136">PowerShell Core выпускается по [лицензии MIT][].</span><span class="sxs-lookup"><span data-stu-id="30c4f-136">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="30c4f-137">Согласно этой лицензии и в отсутствие соглашения о платной подписке пользователи ограничены лишь [поддержку сообщества][].</span><span class="sxs-lookup"><span data-stu-id="30c4f-137">Under this license, and in the absence of a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="30c4f-138">В рамках поддержки сообщества корпорация Майкрософт не предоставляет никаких гарантий оперативного реагирования или выпуска исправлений.</span><span class="sxs-lookup"><span data-stu-id="30c4f-138">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="30c4f-139">Модуль Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="30c4f-139">Windows PowerShell Module</span></span>

<span data-ttu-id="30c4f-140">Поддержка для PowerShell Core не распространяется на другие модули продукта, если только они не поддерживают PowerShell Core явным образом.</span><span class="sxs-lookup"><span data-stu-id="30c4f-140">Support for PowerShell Core does not extend to other product modules unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="30c4f-141">Например, использование модуля `ActiveDirectory`, который поставляется в составе Windows Server, является неподдерживаемым сценарием.</span><span class="sxs-lookup"><span data-stu-id="30c4f-141">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="30c4f-142">Однако в некоторых случаях модули, которые не поддерживают PowerShell Core явным образом, могут быть совместимы.</span><span class="sxs-lookup"><span data-stu-id="30c4f-142">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="30c4f-143">Установив модуль [`WindowsPSModulePath`][] можно добавить `PSModulePath` Windows PowerShell в `PSModulePath` PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="30c4f-143">By installing the [`WindowsPSModulePath`][] module, you can append the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="30c4f-144">Сначала установите модуль `WindowsPSModulePath` из коллекции PowerShell:</span><span class="sxs-lookup"><span data-stu-id="30c4f-144">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin 
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="30c4f-145">После установки модуля запустите командлет `Add-WindowsPSModulePath`, чтобы добавить `PSModulePath` Windows PowerShell в PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="30c4f-145">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[поддержку сообщества]: https://github.com/powershell/powershell/issues
[community support]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[техническую поддержку]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[лицензии MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath"]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
