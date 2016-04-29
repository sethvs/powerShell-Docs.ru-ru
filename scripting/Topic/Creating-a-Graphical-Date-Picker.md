---
title: Создание графического элемента управления "Выбор даты"
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
---
# Создание графического элемента управления "Выбор даты"
Используйте Windows PowerShell 3.0 и более поздние версии для создания формы с графическим элементом управления "Календарь", в котором пользователи могут выбрать день месяца.

## Создание графического элемента "Выбор даты"
Скопируйте и вставьте следующий код в интегрированную среду сценариев Windows PowerShell, а затем сохраните файл как сценарий Windows PowerShell (PS1-файл).

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

Сценарий начинается с загрузки двух классов .NET Framework: **System.Drawing** и **System.Windows.Forms**. Затем вы запускаете новый экземпляр класса .NET Framework **Windows.Forms.Form**, предоставляющий пустую форму или окно, в которые можно добавить элементы управления.

```
$form = New-Object Windows.Forms.Form
```

После создания экземпляра класса "Форма" назначьте значения для трех свойств этого класса.

-   **Текст.** Это будет заголовком окна.

-   **Размер.** Это размер формы в пикселях. Предыдущий сценарий создает форму шириной 243 пикселей и высотой 230 пикселей.

-   **StartingPosition.** Для этого дополнительного свойства задается значение **CenterScreen** в предыдущем сценарии. Если это свойство не добавлено, Windows выберет расположение после открытия формы. Если для **StartingPosition** задать значение **CenterScreen**, форма будет автоматически отображаться в центре экрана при загрузке.

```
$form.Text = "Select a Date" 
$form.Size = New-Object Drawing.Size @(243,230) 
$form.StartPosition = "CenterScreen"
```

Далее создайте и добавьте элемент управления "Календарь" в форму. В этом примере текущий день не выделен и не обведен. Пользователи могут выбрать в календаре не больше одного дня за раз.

```
$calendar = New-Object System.Windows.Forms.MonthCalendar 
$calendar.ShowTodayCircle = $False
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

Далее создайте кнопку **OК** для формы. Укажите размер и поведение кнопки **ОК**. В этом примере кнопка расположена на 165 пикселей ниже верхней границы формы и на 38 пикселей правее левой границы. Высота кнопки — 23 пикселя, а длина — 75 пикселей. Сценарий использует предопределенные типы Windows Forms для определения поведения кнопок.

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Аналогичным образом создайте кнопку **Отмена**. Кнопка **Отмена** расположена на 165 пикселей ниже верхней границы и на 113 пикселей правее левой границы окна.

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Задайте для свойства **Topmost** значение **$True**, чтобы принудительно открыть окно поверх других диалоговых окон.

```
$form.Topmost = $True
```

Добавьте следующую строку кода для отображения формы в Windows.

```
$result = $form.ShowDialog()
```

Наконец, код внутри блока **If** указывает Windows, что следует делать с формой после того, как пользователь выберет день из календаря и нажмет кнопку **ОК** или клавишу **ВВОД**. Windows PowerShell отображает выбранную дату для пользователей.

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## См. также
[Блог Hey Scripting Guy: Why don’t these PowerShell GUI examples work? (Почему эти примеры сценариев PowerShell GUI не работают)](http://go.microsoft.com/fwlink/?LinkId=506644)
[GitHub: Dave Wyatt's WinFormsExampleUpdates (WinFormsExampleUpdates от Дейва Вьятта)](https://github.com/dlwyatt/WinFormsExampleUpdates)
[Windows PowerShell Tip of the Week: Creating a Graphical Date Picker (Совет недели для Windows PowerShell: создание графического элемента управления "Выбор даты")](http://technet.microsoft.com/library/ff730942.aspx)



<!--HONumber=Apr16_HO1-->


