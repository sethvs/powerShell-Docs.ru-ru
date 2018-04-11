---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Создание настраиваемого поля ввода
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 681a75a28a8fb03eb4442d5e20b32b25a337d540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="bbbea-103">Создание настраиваемого поля ввода</span><span class="sxs-lookup"><span data-stu-id="bbbea-103">Creating a Custom Input Box</span></span>

<span data-ttu-id="bbbea-104">Создание сценария настраиваемого графического поля ввода с помощью функций создания форм Microsoft .NET Framework в Windows PowerShell 3.0 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="bbbea-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="bbbea-105">Создание настраиваемого графического поля ввода</span><span class="sxs-lookup"><span data-stu-id="bbbea-105">Create a custom, graphical input box</span></span>

<span data-ttu-id="bbbea-106">Скопируйте и вставьте следующий код в интегрированную среду сценариев Windows PowerShell, а затем сохраните файл как сценарий Windows PowerShell (PS1-файл).</span><span class="sxs-lookup"><span data-stu-id="bbbea-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)

$form.Topmost = $true

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

<span data-ttu-id="bbbea-107">Сценарий начинается с загрузки двух классов .NET Framework: **System.Drawing** и **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="bbbea-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="bbbea-108">Затем вы запускаете новый экземпляр класса .NET Framework **System.Windows.Forms.Form**, предоставляющий пустую форму или окно, в которые можно добавить элементы управления.</span><span class="sxs-lookup"><span data-stu-id="bbbea-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="bbbea-109">После создания экземпляра класса "Форма" назначьте значения для трех свойств этого класса.</span><span class="sxs-lookup"><span data-stu-id="bbbea-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="bbbea-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="bbbea-110">**Text.**</span></span> <span data-ttu-id="bbbea-111">Это будет заголовком окна.</span><span class="sxs-lookup"><span data-stu-id="bbbea-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="bbbea-112">**Size.**</span><span class="sxs-lookup"><span data-stu-id="bbbea-112">**Size.**</span></span> <span data-ttu-id="bbbea-113">Это размер формы в пикселях.</span><span class="sxs-lookup"><span data-stu-id="bbbea-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="bbbea-114">Предыдущий сценарий создает форму шириной 300 пикселей и высотой 200 пикселей.</span><span class="sxs-lookup"><span data-stu-id="bbbea-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="bbbea-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="bbbea-115">**StartingPosition.**</span></span> <span data-ttu-id="bbbea-116">Для этого дополнительного свойства задается значение **CenterScreen** в предыдущем сценарии.</span><span class="sxs-lookup"><span data-stu-id="bbbea-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="bbbea-117">Если это свойство не добавлено, Windows выберет расположение после открытия формы.</span><span class="sxs-lookup"><span data-stu-id="bbbea-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="bbbea-118">Если для **StartingPosition** задать значение **CenterScreen**, форма будет автоматически отображаться в центре экрана при загрузке.</span><span class="sxs-lookup"><span data-stu-id="bbbea-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="bbbea-119">Далее создайте кнопку **OК** для формы.</span><span class="sxs-lookup"><span data-stu-id="bbbea-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="bbbea-120">Укажите размер и поведение кнопки **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bbbea-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="bbbea-121">В этом примере кнопка расположена на 120 пикселей ниже верхней границы формы и на 75 пикселей правее левой границы.</span><span class="sxs-lookup"><span data-stu-id="bbbea-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="bbbea-122">Высота кнопки — 23 пикселя, а длина — 75 пикселей.</span><span class="sxs-lookup"><span data-stu-id="bbbea-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="bbbea-123">Сценарий использует предопределенные типы Windows Forms для определения поведения кнопок.</span><span class="sxs-lookup"><span data-stu-id="bbbea-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="bbbea-124">Аналогичным образом создайте кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="bbbea-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="bbbea-125">Кнопка **Отмена** расположена на 120 пикселей ниже верхней границы и на 150 пикселей правее левой границы окна.</span><span class="sxs-lookup"><span data-stu-id="bbbea-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="bbbea-126">Далее введите текст метки в окне, который должны получить пользователи.</span><span class="sxs-lookup"><span data-stu-id="bbbea-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

<span data-ttu-id="bbbea-127">Добавьте элемент управления (в данном случае текстовое поле), который позволит пользователям указать сведения, описанные в тексте метки.</span><span class="sxs-lookup"><span data-stu-id="bbbea-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="bbbea-128">Помимо текстового поля существует много других элементов управления, которые можно применить. Их описание см. в статье [Пространство имен System.Windows.Forms](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="bbbea-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

<span data-ttu-id="bbbea-129">Задайте для свойства **Topmost** значение **$true**, чтобы принудительно открыть окно поверх других диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="bbbea-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="bbbea-130">Затем добавьте следующую строку кода, чтобы активировать форму и установить фокус на текстовое поле, которое вы создали.</span><span class="sxs-lookup"><span data-stu-id="bbbea-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```powershell
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="bbbea-131">Добавьте следующую строку кода для отображения формы в Windows.</span><span class="sxs-lookup"><span data-stu-id="bbbea-131">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="bbbea-132">Наконец, код внутри блока **If** указывает Windows, что следует делать с формой после того, как пользователь задаст текст в поле и нажмет кнопку **ОК** или клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="bbbea-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="bbbea-133">См. также</span><span class="sxs-lookup"><span data-stu-id="bbbea-133">See Also</span></span>

- [<span data-ttu-id="bbbea-134">Блог Hey Scripting Guy: Why don’t these PowerShell GUI examples work? (Почему эти примеры скриптов PowerShell GUI не работают)</span><span class="sxs-lookup"><span data-stu-id="bbbea-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="bbbea-135">GitHub: Dave Wyatt's WinFormsExampleUpdates (WinFormsExampleUpdates от Дэйва Уайята)</span><span class="sxs-lookup"><span data-stu-id="bbbea-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- <span data-ttu-id="bbbea-136">[Windows PowerShell Tip of the Week: Creating a Custom Input Box](http://technet.microsoft.com/library/ff730941.aspx) (Совет недели для Windows PowerShell: создание настраиваемого поля ввода)</span><span class="sxs-lookup"><span data-stu-id="bbbea-136">[Windows PowerShell Tip of the Week:  Creating a Custom Input Box](http://technet.microsoft.com/library/ff730941.aspx)</span></span>