---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Запуск Windows PowerShell в более ранних версиях Windows"
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
ms.openlocfilehash: cb56fded1e67a4f4219d210dd95078314e855b1a
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="starting-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="b72e2-103">Запуск Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="b72e2-103">Starting Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="b72e2-104">В этом разделе объясняется, как запустить Windows PowerShell и интегрированную среду скриптов Windows PowerShell (ISE) в Windows® 7, Windows Server® 2008 R2 и Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b72e2-104">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="b72e2-105">Кроме того, здесь поясняется, как включить дополнительный компонент Windows PowerShell ISE в Windows PowerShell 2.0 в ОС Windows Server® 2008 R2 и Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="b72e2-105">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="b72e2-106">Чтобы установить Windows PowerShell 4.0 на поддерживаемых системах, скачайте и установите [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span><span class="sxs-lookup"><span data-stu-id="b72e2-106">To install Windows PowerShell 4.0 on supported systems, download and install [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881).</span></span> <span data-ttu-id="b72e2-107">Дополнительные сведения см. в статье [Установка Windows PowerShell](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="b72e2-107">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

<span data-ttu-id="b72e2-108">Чтобы установить Windows PowerShell 3.0 на поддерживаемых системах, скачайте и установите [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span><span class="sxs-lookup"><span data-stu-id="b72e2-108">To install Windows PowerShell 3.0 on supported systems, download and install [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290).</span></span> <span data-ttu-id="b72e2-109">Дополнительные сведения см. в статье [Установка Windows PowerShell](Installing-Windows-PowerShell.md).</span><span class="sxs-lookup"><span data-stu-id="b72e2-109">For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="b72e2-110">Запуск Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="b72e2-110">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>
<span data-ttu-id="b72e2-111">Используйте любой из следующих методов для запуска установленной версии Windows PowerShell 3.0 или Windows PowerShell 4.0, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="b72e2-111">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b72e2-112">Из меню "Пуск"</span><span class="sxs-lookup"><span data-stu-id="b72e2-112">From the Start Menu</span></span>

-   <span data-ttu-id="b72e2-113">Нажмите кнопку **Пуск**, введите **PowerShell** и выберите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-113">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>

-   <span data-ttu-id="b72e2-114">В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-114">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b72e2-115">В командной строке</span><span class="sxs-lookup"><span data-stu-id="b72e2-115">At the Command Prompt</span></span>

-   <span data-ttu-id="b72e2-116">В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:</span><span class="sxs-lookup"><span data-stu-id="b72e2-116">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell
    ```

    <span data-ttu-id="b72e2-117">Можно также использовать параметры программы PowerShell.exe для настройки сеанса.</span><span class="sxs-lookup"><span data-stu-id="b72e2-117">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="b72e2-118">Дополнительные сведения см. в статье [Справка по командной строке PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="b72e2-118">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b72e2-119">С правами администратора ("Запуск от имени администратора")</span><span class="sxs-lookup"><span data-stu-id="b72e2-119">With Administrative privileges ("Run as administrator")</span></span>

1.  <span data-ttu-id="b72e2-120">Нажмите кнопку **Пуск**, введите **PowerShell**, щелкните правой кнопкой мыши **Windows PowerShell** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-120">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b72e2-121">Запуск интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="b72e2-121">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="b72e2-122">Используйте один из следующих методов для запуска интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b72e2-122">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="b72e2-123">Из меню "Пуск"</span><span class="sxs-lookup"><span data-stu-id="b72e2-123">From the Start Menu</span></span>

-   <span data-ttu-id="b72e2-124">Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев** и выберите **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-124">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>

-   <span data-ttu-id="b72e2-125">В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-125">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="b72e2-126">В командной строке</span><span class="sxs-lookup"><span data-stu-id="b72e2-126">At the Command Prompt</span></span>

-   <span data-ttu-id="b72e2-127">В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:</span><span class="sxs-lookup"><span data-stu-id="b72e2-127">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

    ```
    PowerShell_ISE
    ```

    <span data-ttu-id="b72e2-128">или</span><span class="sxs-lookup"><span data-stu-id="b72e2-128">or</span></span>

    ```
    ISE
    ```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="b72e2-129">С правами администратора ("Запуск от имени администратора")</span><span class="sxs-lookup"><span data-stu-id="b72e2-129">With Administrative privileges ("Run as administrator")</span></span>

1.  <span data-ttu-id="b72e2-130">Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев**, щелкните правой кнопкой мыши **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-130">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="b72e2-131">Включение интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="b72e2-131">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>
<span data-ttu-id="b72e2-132">При использовании Windows PowerShell 4.0 и Windows PowerShell 3.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена во всех версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="b72e2-132">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="b72e2-133">Если она еще не включена, Windows Management Framework 4.0 или Windows Management Framework 3.0 включает ее.</span><span class="sxs-lookup"><span data-stu-id="b72e2-133">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="b72e2-134">При использовании Windows PowerShell 2.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена в Windows 7.</span><span class="sxs-lookup"><span data-stu-id="b72e2-134">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="b72e2-135">В Windows Server 2008 R2 и Windows Server 2008 эта функция является дополнительной.</span><span class="sxs-lookup"><span data-stu-id="b72e2-135">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="b72e2-136">Чтобы включить интегрированную среду сценариев Windows PowerShell для Windows PowerShell 2.0 в Windows Server 2008 R2 или Windows Server 2008, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b72e2-136">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="b72e2-137">Включение интегрированной среды сценариев Windows PowerShell Windows PowerShell (ISE)</span><span class="sxs-lookup"><span data-stu-id="b72e2-137">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1.  <span data-ttu-id="b72e2-138">Запустите диспетчер сервера.</span><span class="sxs-lookup"><span data-stu-id="b72e2-138">Start Server Manager.</span></span>

2.  <span data-ttu-id="b72e2-139">Щелкните **Компоненты** и выберите **Добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="b72e2-139">Click **Features** and then click **Add Features**.</span></span>

3.  <span data-ttu-id="b72e2-140">В меню "Выберите компоненты" щелкните интегрированную среду сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b72e2-140">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

