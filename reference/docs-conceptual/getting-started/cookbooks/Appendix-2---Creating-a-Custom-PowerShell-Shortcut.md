---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Приложение 2. Создание настраиваемого ярлыка PowerShell"
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: 31fdc388ae8859191f75c3c4120667cdbeff1669
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2017
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a><span data-ttu-id="acac1-103">Приложение 2. Создание настраиваемого ярлыка PowerShell</span><span class="sxs-lookup"><span data-stu-id="acac1-103">Appendix 2 - Creating a Custom PowerShell Shortcut</span></span>
<span data-ttu-id="acac1-104">Следующая процедура описывает создание ярлыка для Windows PowerShell, в котором уже заданы нужные параметры.</span><span class="sxs-lookup"><span data-stu-id="acac1-104">The following procedure describes how to create a shortcut to Windows PowerShell that has several convenient options customized.</span></span>

1.  <span data-ttu-id="acac1-105">Создайте ярлык, указывающий на Powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="acac1-105">Create a shortcut that points to Powershell.exe.</span></span>

2.  <span data-ttu-id="acac1-106">Щелкните его правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="acac1-106">Right-click the shortcut, and then click **Properties**.</span></span>

3.  <span data-ttu-id="acac1-107">Откройте вкладку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="acac1-107">Click the **Options** tab.</span></span>

4.  <span data-ttu-id="acac1-108">В разделе **Правка** установите флажок **Для выделения**.</span><span class="sxs-lookup"><span data-stu-id="acac1-108">In the **Edit Options** section, select the **QuickEdit** check box.</span></span>

    <span data-ttu-id="acac1-109">Этот параметр позволяет выбрать текст в окне консоли Windows PowerShell, перетащив курсор при нажатой левой кнопки мыши, а также скопировать текст в буфер обмена, нажав клавишу ВВОД или правую кнопку мыши.</span><span class="sxs-lookup"><span data-stu-id="acac1-109">This setting lets you select text in the Windows PowerShell console window by dragging the left mouse button, and it lets you copy text to the clipboard by pressing ENTER or by right-clicking the mouse.</span></span>

5.  <span data-ttu-id="acac1-110">В разделе **Правка** установите флажок **Быстрая вставка**.</span><span class="sxs-lookup"><span data-stu-id="acac1-110">In the **Edit Options** section, select the **Insert Mode** check box.</span></span> <span data-ttu-id="acac1-111">Этот параметр позволяет автоматически вставить текст из буфера обмена с помощью щелчка правой кнопкой мыши в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="acac1-111">This setting lets you right-click in the console window to automatically paste text from the clipboard.</span></span>

6.  <span data-ttu-id="acac1-112">В поле **Размер буфера** раздела **Запоминание команд** введите или выберите число от 1 до 999.</span><span class="sxs-lookup"><span data-stu-id="acac1-112">In the **Command History** section, type or select a number between 1 and 999 in the **Buffer Size** box.</span></span> <span data-ttu-id="acac1-113">Это задает число введенных команд, которые сохраняются в буфере консоли.</span><span class="sxs-lookup"><span data-stu-id="acac1-113">This sets the number of typed commands that will be kept in the console buffer.</span></span>

7.  <span data-ttu-id="acac1-114">В разделе **Запоминание команд** установите флажок **Отбрасывать повторения**, чтобы исключить повторяющиеся команды из буфера консоли.</span><span class="sxs-lookup"><span data-stu-id="acac1-114">In the **Command History** section, select the **Discard Old Duplicates** check box to eliminate repeated commands from the console buffer.</span></span>

8.  <span data-ttu-id="acac1-115">Откройте вкладку **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="acac1-115">Click the **Layout** tab.</span></span>

9. <span data-ttu-id="acac1-116">В поле **Высота** раздела **Screen Buffer** (Буфер экрана) введите число от 1 до 9999.</span><span class="sxs-lookup"><span data-stu-id="acac1-116">In the **Screen Buffer** section, type a number between 1 and 9999 in the **Height** box.</span></span> <span data-ttu-id="acac1-117">Высота обозначает число строк выходных данных, помещаемых в буфер.</span><span class="sxs-lookup"><span data-stu-id="acac1-117">The height represents the number of lines of output that are buffered.</span></span> <span data-ttu-id="acac1-118">Это максимальное число строк, сохраняемых для просмотра при прокрутке в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="acac1-118">This is the maximum number of lines retained for viewing when you scroll through the console window.</span></span> <span data-ttu-id="acac1-119">Если это число меньше высоты, отображаемой в разделе **Размер окна**, высота окна автоматически уменьшается до того же значения.</span><span class="sxs-lookup"><span data-stu-id="acac1-119">If this number is lower than the height shown in the **Window size** section, the window size height will automatically be reduced to the same value.</span></span>

10. <span data-ttu-id="acac1-120">В разделе **Размер окна** введите число от 1 до 9999 для ширины.</span><span class="sxs-lookup"><span data-stu-id="acac1-120">In the **Window Size** section, type a number between 1 and 9999 for the width.</span></span> <span data-ttu-id="acac1-121">Оно представляет число символов, отображаемых в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="acac1-121">This represents the number of characters that are displayed across the console window.</span></span> <span data-ttu-id="acac1-122">По умолчанию ширина равна 80, и именно на нее рассчитано форматирование выходных данных Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acac1-122">The default width is 80, and Windows PowerShell's output formatting is designed for this width.</span></span>

11. <span data-ttu-id="acac1-123">Если вы хотите, чтобы при открытии консоль располагалась в определенной точке на рабочем столе, снимите флажок **Автоматический выбор** в разделе **Положение окна**, а затем измените значения в полях **Слева** и **Сверху** раздела **Положение окна**.</span><span class="sxs-lookup"><span data-stu-id="acac1-123">If you want to place the console at a particular point on the desktop when it is opened, clear the **Let system position window** check box in the **Window position** section, and then change the values in the **Left** and **Top** boxes in the **Window position** section.</span></span>

12. <span data-ttu-id="acac1-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="acac1-124">Click **OK**.</span></span>

