---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Запуск Windows PowerShell
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="starting-windows-powershell"></a><span data-ttu-id="d0b48-103">Запуск Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0b48-103">Starting Windows PowerShell</span></span>
<span data-ttu-id="d0b48-104">PowerShell — это библиотека DLL обработчика скриптов, которая внедрена в несколько узлов.</span><span class="sxs-lookup"><span data-stu-id="d0b48-104">PowerShell is a scripting engine dll which is embedded into multiple hosts.</span></span>  <span data-ttu-id="d0b48-105">Самый распространенный запускаемый узел — интерактивная командная строка (PowerShell.exe) и интерактивная среда скриптов (PowerShell_ISE.exe).</span><span class="sxs-lookup"><span data-stu-id="d0b48-105">The most common host you will start are the interactive command line PowerShell.exe and the Interactive Scripting Environment PowerShell_ISE.exe.</span></span>

<span data-ttu-id="d0b48-106">Информацию о запуске Windows PowerShell® в Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 и Windows 8 см. в статье [Общие задачи управления и навигации](http://technet.microsoft.com/library/hh831491.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0b48-106">To start Windows PowerShell® on Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012, and Windows 8, see [Common Management Tasks and Navigation](http://technet.microsoft.com/library/hh831491.aspx).</span></span>

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a><span data-ttu-id="d0b48-107">Запуск Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="d0b48-107">How to Start Windows PowerShell on Earlier Versions of Windows</span></span>

<span data-ttu-id="d0b48-108">В этом разделе объясняется, как запустить Windows PowerShell и интегрированную среду скриптов Windows PowerShell (ISE) в Windows® 7, Windows Server® 2008 R2 и Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="d0b48-108">This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server® 2008.</span></span> <span data-ttu-id="d0b48-109">Кроме того, здесь поясняется, как включить дополнительный компонент Windows PowerShell ISE в Windows PowerShell 2.0 в ОС Windows Server® 2008 R2 и Windows Server® 2008.</span><span class="sxs-lookup"><span data-stu-id="d0b48-109">It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server® 2008.</span></span>

<span data-ttu-id="d0b48-110">Используйте любой из следующих методов для запуска установленной версии Windows PowerShell 3.0 или Windows PowerShell 4.0, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="d0b48-110">Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="d0b48-111">Из меню "Пуск"</span><span class="sxs-lookup"><span data-stu-id="d0b48-111">From the Start Menu</span></span>

- <span data-ttu-id="d0b48-112">Нажмите кнопку **Пуск**, введите **PowerShell** и выберите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-112">Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.</span></span>
- <span data-ttu-id="d0b48-113">В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-113">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="d0b48-114">В командной строке</span><span class="sxs-lookup"><span data-stu-id="d0b48-114">At the Command Prompt</span></span>

<span data-ttu-id="d0b48-115">В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:</span><span class="sxs-lookup"><span data-stu-id="d0b48-115">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell
```

<span data-ttu-id="d0b48-116">Можно также использовать параметры программы PowerShell.exe для настройки сеанса.</span><span class="sxs-lookup"><span data-stu-id="d0b48-116">You can also use the parameters of the PowerShell.exe program to customize the session.</span></span> <span data-ttu-id="d0b48-117">Дополнительные сведения см. в статье [Справка по командной строке PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span><span class="sxs-lookup"><span data-stu-id="d0b48-117">For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).</span></span>

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="d0b48-118">С правами администратора ("Запуск от имени администратора")</span><span class="sxs-lookup"><span data-stu-id="d0b48-118">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="d0b48-119">Нажмите кнопку **Пуск**, введите **PowerShell**, щелкните правой кнопкой мыши **Windows PowerShell** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-119">Click **Start**, type **PowerShell**, right-click **Windows PowerShell**, and then click **Run as administrator**.</span></span>

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="d0b48-120">Запуск интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="d0b48-120">How to Start Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="d0b48-121">Используйте один из следующих методов для запуска интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0b48-121">Use any of the following methods to start Windows PowerShell ISE.</span></span>

#### <a name="from-the-start-menu"></a><span data-ttu-id="d0b48-122">Из меню "Пуск"</span><span class="sxs-lookup"><span data-stu-id="d0b48-122">From the Start Menu</span></span>

- <span data-ttu-id="d0b48-123">Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев** и выберите **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-123">Click **Start**, type **ISE**, and then click **Windows PowerShell ISE**.</span></span>
- <span data-ttu-id="d0b48-124">В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Интегрированная среда сценариев Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-124">From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell ISE**.</span></span>

#### <a name="at-the-command-prompt"></a><span data-ttu-id="d0b48-125">В командной строке</span><span class="sxs-lookup"><span data-stu-id="d0b48-125">At the Command Prompt</span></span>

<span data-ttu-id="d0b48-126">В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:</span><span class="sxs-lookup"><span data-stu-id="d0b48-126">In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:</span></span>

```
PowerShell_ISE
```

<span data-ttu-id="d0b48-127">или</span><span class="sxs-lookup"><span data-stu-id="d0b48-127">or</span></span>

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a><span data-ttu-id="d0b48-128">С правами администратора ("Запуск от имени администратора")</span><span class="sxs-lookup"><span data-stu-id="d0b48-128">With Administrative privileges ("Run as administrator")</span></span>

<span data-ttu-id="d0b48-129">Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев**, щелкните правой кнопкой мыши **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-129">Click **Start**, type **ISE**, right-click **Windows PowerShell ISE**, and then click **Run as administrator**.</span></span>

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a><span data-ttu-id="d0b48-130">Включение интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows</span><span class="sxs-lookup"><span data-stu-id="d0b48-130">How to Enable Windows PowerShell ISE on Earlier Releases of Windows</span></span>

<span data-ttu-id="d0b48-131">При использовании Windows PowerShell 4.0 и Windows PowerShell 3.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена во всех версиях Windows.</span><span class="sxs-lookup"><span data-stu-id="d0b48-131">In Windows PowerShell 4.0 and Windows PowerShell 3.0, Windows PowerShell ISE is enabled by default on all versions of Windows.</span></span> <span data-ttu-id="d0b48-132">Если она еще не включена, Windows Management Framework 4.0 или Windows Management Framework 3.0 включает ее.</span><span class="sxs-lookup"><span data-stu-id="d0b48-132">If it is not already enabled, Windows Management Framework 4.0 or Windows Management Framework 3.0 enables it.</span></span>

<span data-ttu-id="d0b48-133">При использовании Windows PowerShell 2.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена в Windows 7.</span><span class="sxs-lookup"><span data-stu-id="d0b48-133">In Windows PowerShell 2.0, Windows PowerShell ISE is enabled by default on Windows 7.</span></span> <span data-ttu-id="d0b48-134">В Windows Server 2008 R2 и Windows Server 2008 эта функция является дополнительной.</span><span class="sxs-lookup"><span data-stu-id="d0b48-134">However, on Windows Server 2008 R2 and Windows Server 2008, it is an optional feature.</span></span>

<span data-ttu-id="d0b48-135">Чтобы включить интегрированную среду сценариев Windows PowerShell для Windows PowerShell 2.0 в Windows Server 2008 R2 или Windows Server 2008, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d0b48-135">To enable Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server 2008 R2 or Windows Server 2008, use the following procedure.</span></span>

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a><span data-ttu-id="d0b48-136">Включение интегрированной среды сценариев Windows PowerShell Windows PowerShell (ISE)</span><span class="sxs-lookup"><span data-stu-id="d0b48-136">To enable Windows PowerShell Integrated Scripting Environment (ISE)</span></span>

1. <span data-ttu-id="d0b48-137">Запустите диспетчер сервера.</span><span class="sxs-lookup"><span data-stu-id="d0b48-137">Start Server Manager.</span></span>
2. <span data-ttu-id="d0b48-138">Щелкните **Компоненты** и выберите **Добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-138">Click **Features** and then click **Add Features**.</span></span>
3. <span data-ttu-id="d0b48-139">В меню "Выберите компоненты" щелкните интегрированную среду сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0b48-139">In Select Features, click Windows PowerShell Integrated Scripting Environment (ISE).</span></span>

## <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="d0b48-140">Запуск 32-разрядной версии Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0b48-140">Starting the 32-Bit Version of Windows PowerShell</span></span>

<span data-ttu-id="d0b48-141">При установке Windows PowerShell на 64-разрядном компьютере в дополнение к 64-разрядной версии устанавливается **Windows PowerShell (x86)** — 32-разрядная версия Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0b48-141">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="d0b48-142">При открытии Windows PowerShell по умолчанию запускается 64-разрядная версия.</span><span class="sxs-lookup"><span data-stu-id="d0b48-142">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="d0b48-143">Однако в некоторых случаях нужно запустить **Windows PowerShell (x86)**, например при использовании модуля, которому требуется 32-разрядная версия, или при удаленном подключении к 32-разрядному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="d0b48-143">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="d0b48-144">Для запуска 32-разрядной версии Windows PowerShell воспользуйтесь любой из следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="d0b48-144">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="d0b48-145">Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d0b48-145">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="d0b48-146">На экране **Пуск** щелкните **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-146">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="d0b48-147">Щелкните плитку **Windows PowerShell x86**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-147">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="d0b48-148">Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-148">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-149">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-149">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-150">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="d0b48-150">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="d0b48-151">Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="d0b48-151">In Windows Server® 2012</span></span>

- <span data-ttu-id="d0b48-152">На экране **Пуск** введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-152">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-153">Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-153">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-154">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-154">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-155">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="d0b48-155">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="d0b48-156">Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="d0b48-156">In Windows® 8.1</span></span>

- <span data-ttu-id="d0b48-157">На экране **Пуск** щелкните **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-157">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="d0b48-158">Щелкните плитку **Windows PowerShell x86**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-158">Click the **Windows PowerShell x86** tile.</span></span>
- <span data-ttu-id="d0b48-159">Если вы используете [средства удаленного администрирования сервера](http://go.microsoft.com/fwlink/?LinkID=304145) для Windows 8.1, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="d0b48-159">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span>
  <span data-ttu-id="d0b48-160">Выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-160">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-161">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-161">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-162">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="d0b48-162">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="d0b48-163">Windows® 8</span><span class="sxs-lookup"><span data-stu-id="d0b48-163">In Windows® 8</span></span>

- <span data-ttu-id="d0b48-164">На экране **Пуск** переместите курсор в правый верхний угол, щелкните **Параметры**, **Плитки**, а затем переместите ползунок **Показать средства администрирования** в значение "Да".</span><span class="sxs-lookup"><span data-stu-id="d0b48-164">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="d0b48-165">Введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-165">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-166">Если вы используете [средства удаленного администрирования сервера](http://www.microsoft.com/download/details.aspx?id=28972) для Windows 8, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="d0b48-166">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="d0b48-167">Выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-167">Select **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-168">На экране **Пуск** или рабочем столе введите **PowerShell (x86)** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="d0b48-168">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>
- <span data-ttu-id="d0b48-169">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="d0b48-169">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>