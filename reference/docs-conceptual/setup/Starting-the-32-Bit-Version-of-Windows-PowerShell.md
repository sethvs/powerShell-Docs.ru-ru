---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Запуск 32-разрядной версии Windows PowerShell"
ms.assetid: 12b31890-2609-4a76-8c24-0ebe78084f50
ms.openlocfilehash: d682ce45ebc92cda3a9008ab608bacf9ef8eba57
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/08/2018
---
# <a name="starting-the-32-bit-version-of-windows-powershell"></a><span data-ttu-id="97dd3-103">Запуск 32-разрядной версии Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="97dd3-103">Starting the 32-Bit Version of Windows PowerShell</span></span>
<span data-ttu-id="97dd3-104">При установке Windows PowerShell на 64-разрядном компьютере в дополнение к 64-разрядной версии устанавливается **Windows PowerShell (x86)** — 32-разрядная версия Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97dd3-104">When you install Windows PowerShell on a 64-bit computer, **Windows PowerShell (x86)**, a 32-bit version of Windows PowerShell is installed in addition to the 64-bit version.</span></span> <span data-ttu-id="97dd3-105">При открытии Windows PowerShell по умолчанию запускается 64-разрядная версия.</span><span class="sxs-lookup"><span data-stu-id="97dd3-105">When you run Windows PowerShell, the 64-bit version runs by default.</span></span>

<span data-ttu-id="97dd3-106">Однако в некоторых случаях нужно запустить **Windows PowerShell (x86)**, например при использовании модуля, которому требуется 32-разрядная версия, или при удаленном подключении к 32-разрядному компьютеру.</span><span class="sxs-lookup"><span data-stu-id="97dd3-106">However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32-bit version or when you are connecting remotely to a 32-bit computer.</span></span>

<span data-ttu-id="97dd3-107">Для запуска 32-разрядной версии Windows PowerShell воспользуйтесь любой из следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="97dd3-107">To start a 32-bit version of Windows PowerShell, use any of the following procedures.</span></span>

#### <a name="in-windows-server-2012-r2"></a><span data-ttu-id="97dd3-108">Windows Server® 2012 R2</span><span class="sxs-lookup"><span data-stu-id="97dd3-108">In Windows Server® 2012 R2</span></span>

- <span data-ttu-id="97dd3-109">На экране **Пуск** щелкните **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-109">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="97dd3-110">Щелкните плитку **Windows PowerShell x86**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-110">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="97dd3-111">Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-111">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-112">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-112">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-113">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="97dd3-113">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-server-2012"></a><span data-ttu-id="97dd3-114">Windows Server® 2012</span><span class="sxs-lookup"><span data-stu-id="97dd3-114">In Windows Server® 2012</span></span>

- <span data-ttu-id="97dd3-115">На экране **Пуск** введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-115">On the **Start** screen, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-116">Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-116">In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-117">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-117">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-118">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="97dd3-118">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-81"></a><span data-ttu-id="97dd3-119">Windows® 8.1</span><span class="sxs-lookup"><span data-stu-id="97dd3-119">In Windows® 8.1</span></span>

- <span data-ttu-id="97dd3-120">На экране **Пуск** щелкните **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-120">On the **Start** screen, type **Windows PowerShell (x86)**.</span></span> <span data-ttu-id="97dd3-121">Щелкните плитку **Windows PowerShell x86**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-121">Click the **Windows PowerShell x86** tile.</span></span>

- <span data-ttu-id="97dd3-122">Если вы используете [средства удаленного администрирования сервера](http://go.microsoft.com/fwlink/?LinkID=304145) для Windows 8.1, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="97dd3-122">If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="97dd3-123">Выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-123">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-124">На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-124">On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.</span></span>
   
- <span data-ttu-id="97dd3-125">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="97dd3-125">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

#### <a name="in-windows-8"></a><span data-ttu-id="97dd3-126">Windows® 8</span><span class="sxs-lookup"><span data-stu-id="97dd3-126">In Windows® 8</span></span>

- <span data-ttu-id="97dd3-127">На экране **Пуск** переместите курсор в правый верхний угол, щелкните **Параметры**, **Плитки**, а затем переместите ползунок **Показать средства администрирования** в значение "Да".</span><span class="sxs-lookup"><span data-stu-id="97dd3-127">On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes.</span></span> <span data-ttu-id="97dd3-128">Введите **PowerShell** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-128">Then, type **PowerShell** and click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-129">Если вы используете [средства удаленного администрирования сервера](http://www.microsoft.com/download/details.aspx?id=28972) для Windows 8, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера.</span><span class="sxs-lookup"><span data-stu-id="97dd3-129">If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu.</span></span> <span data-ttu-id="97dd3-130">Выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-130">Select **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-131">На экране **Пуск** или рабочем столе введите **PowerShell (x86)** и выберите **Windows PowerShell (x86)**.</span><span class="sxs-lookup"><span data-stu-id="97dd3-131">On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.</span></span>

- <span data-ttu-id="97dd3-132">В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span><span class="sxs-lookup"><span data-stu-id="97dd3-132">Via command line, enter: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`</span></span>

