---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Создание графического элемента управления \"Выбор даты\""
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 7be72be7e9732737f00b15b6b2b83adcca4393ae
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2017
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="b7753-103">Создание графического элемента управления "Выбор даты"</span><span class="sxs-lookup"><span data-stu-id="b7753-103">Creating a Graphical Date Picker</span></span>
<span data-ttu-id="b7753-104">Используйте Windows PowerShell 3.0 и более поздние версии для создания формы с графическим элементом управления "Календарь", в котором пользователи могут выбрать день месяца.</span><span class="sxs-lookup"><span data-stu-id="b7753-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="b7753-105">Создание графического элемента "Выбор даты"</span><span class="sxs-lookup"><span data-stu-id="b7753-105">Create a graphical date-picker control</span></span>
<span data-ttu-id="b7753-106">Скопируйте и вставьте следующий код в интегрированную среду сценариев Windows PowerShell, а затем сохраните файл как сценарий Windows PowerShell (PS1-файл).</span><span class="sxs-lookup"><span data-stu-id="b7753-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form 

$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"

$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar) 

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $True

$result = $form.ShowDialog() 

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

<span data-ttu-id="b7753-107">Сценарий начинается с загрузки двух классов .NET Framework: **System.Drawing** и **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="b7753-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="b7753-108">Затем вы запускаете новый экземпляр класса .NET Framework **Windows.Forms.Form**, предоставляющий пустую форму или окно, в которые можно добавить элементы управления.</span><span class="sxs-lookup"><span data-stu-id="b7753-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="b7753-109">После создания экземпляра класса "Форма" назначьте значения для трех свойств этого класса.</span><span class="sxs-lookup"><span data-stu-id="b7753-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="b7753-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="b7753-110">**Text.**</span></span> <span data-ttu-id="b7753-111">Это будет заголовком окна.</span><span class="sxs-lookup"><span data-stu-id="b7753-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="b7753-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="b7753-112">**Size.**</span></span> <span data-ttu-id="b7753-113">Это размер формы в пикселях.</span><span class="sxs-lookup"><span data-stu-id="b7753-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="b7753-114">Предыдущий сценарий создает форму шириной 243 пикселей и высотой 230 пикселей.</span><span class="sxs-lookup"><span data-stu-id="b7753-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

- <span data-ttu-id="b7753-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="b7753-115">**StartingPosition.**</span></span> <span data-ttu-id="b7753-116">Для этого дополнительного свойства задается значение **CenterScreen** в предыдущем сценарии.</span><span class="sxs-lookup"><span data-stu-id="b7753-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="b7753-117">Если это свойство не добавлено, Windows выберет расположение после открытия формы.</span><span class="sxs-lookup"><span data-stu-id="b7753-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="b7753-118">Если для **StartingPosition** задать значение **CenterScreen**, форма будет автоматически отображаться в центре экрана при загрузке.</span><span class="sxs-lookup"><span data-stu-id="b7753-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```
$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"
```

<span data-ttu-id="b7753-119">Далее создайте и добавьте элемент управления "Календарь" в форму.</span><span class="sxs-lookup"><span data-stu-id="b7753-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="b7753-120">В этом примере текущий день не выделен и не обведен.</span><span class="sxs-lookup"><span data-stu-id="b7753-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="b7753-121">Пользователи могут выбрать в календаре не больше одного дня за раз.</span><span class="sxs-lookup"><span data-stu-id="b7753-121">Users can select only one day on the calendar at one time.</span></span>

```
$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="b7753-122">Далее создайте кнопку **OК** для формы.</span><span class="sxs-lookup"><span data-stu-id="b7753-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="b7753-123">Укажите размер и поведение кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b7753-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="b7753-124">В этом примере кнопка расположена на 165 пикселей ниже верхней границы формы и на 38 пикселей правее левой границы.</span><span class="sxs-lookup"><span data-stu-id="b7753-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="b7753-125">Высота кнопки — 23 пикселя, а длина — 75 пикселей.</span><span class="sxs-lookup"><span data-stu-id="b7753-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="b7753-126">Сценарий использует предопределенные типы Windows Forms для определения поведения кнопок.</span><span class="sxs-lookup"><span data-stu-id="b7753-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="b7753-127">Аналогичным образом создайте кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="b7753-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="b7753-128">Кнопка **Отмена** расположена на 165 пикселей ниже верхней границы и на 113 пикселей правее левой границы окна.</span><span class="sxs-lookup"><span data-stu-id="b7753-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="b7753-129">Задайте для свойства **Topmost** значение **$True**, чтобы принудительно открыть окно поверх других диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="b7753-129">Set the **Topmost** property to **$True** to force the window to open atop other open windows and dialog boxes.</span></span>

```
$form.Topmost = $True
```

<span data-ttu-id="b7753-130">Добавьте следующую строку кода для отображения формы в Windows.</span><span class="sxs-lookup"><span data-stu-id="b7753-130">Add the following line of code to display the form in Windows.</span></span>

```
$result = $form.ShowDialog()
```

<span data-ttu-id="b7753-131">Наконец, код внутри блока **If** указывает Windows, что следует делать с формой после того, как пользователь выберет день из календаря и нажмет кнопку **ОК** или клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b7753-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="b7753-132">Windows PowerShell отображает выбранную дату для пользователей.</span><span class="sxs-lookup"><span data-stu-id="b7753-132">Windows PowerShell displays the selected date to users.</span></span>

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="b7753-133">См. также</span><span class="sxs-lookup"><span data-stu-id="b7753-133">See Also</span></span>
- [<span data-ttu-id="b7753-134">Блог Hey Scripting Guy: Why don’t these PowerShell GUI examples work? (Почему эти примеры скриптов PowerShell GUI не работают)</span><span class="sxs-lookup"><span data-stu-id="b7753-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="b7753-135">GitHub: Dave Wyatt's WinFormsExampleUpdates (WinFormsExampleUpdates от Дэйва Уайята)</span><span class="sxs-lookup"><span data-stu-id="b7753-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- <span data-ttu-id="b7753-136">[Windows PowerShell Tip of the Week: Creating a Graphical Date Picker](http://technet.microsoft.com/library/ff730942.aspx) (Совет недели для Windows PowerShell: создание графического элемента управления "Выбор даты")</span><span class="sxs-lookup"><span data-stu-id="b7753-136">[Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker](http://technet.microsoft.com/library/ff730942.aspx)</span></span>

