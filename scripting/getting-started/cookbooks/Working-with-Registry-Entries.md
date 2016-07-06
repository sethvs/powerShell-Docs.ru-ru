---
title: "Работа с записями реестра"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: d7fb731bc2527e324271bc75f00112a67a1147e3

---

# Работа с записями реестра
Так как записи реестра являются свойствами разделов и их невозможно открыть напрямую, при работе с ними необходимо использовать немного другой подход.

### Создание списков записей реестра
Существует несколько способов просмотра реестра. Самый простой — получить имена свойств, связанные с разделом. Например, чтобы увидеть имена записей в разделе реестра **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, используйте **Get\-Item**. Разделы реестра содержат свойство с универсальным именем Property, которое является списком записей реестра в разделе. Следующая команда выбирает свойство Property и расширяет элементы так, чтобы они отображались в списке:

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

Чтобы просмотреть записи реестра в более удобочитаемой форме, используйте **Get\-ItemProperty**:

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

Все свойства Windows PowerShell\-раздела имеют префиксы PS, например **PSPath**, **PSParentPath**, **PSChildName** и **PSProvider**.

Для ссылки на текущее расположение можно использовать нотацию "**.**". **Set\-Location** можно использовать для первоначального изменения значения на контейнер реестра **CurrentVersion**:

```
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Кроме того, можно использовать встроенный диск HKLM PSDrive с **Set\-Location**:

```
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Затем можно использовать нотацию "**.**" для текущего расположения, чтобы перечислить свойства без указания полного пути:

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

Расширение пути работает так же, как и в файловой системе, поэтому в этом расположении можно получить перечисление **ItemProperty** для **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** с помощью **Get\-ItemProperty \-Path ..\\Help**.

### Получение одной записи реестра
Если необходимо получить конкретную запись в разделе реестра, можно использовать один из нескольких возможных подходов. В этом примере выполняется поиск значения **DevicePath** в **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.

Используйте вместе с **Get\-ItemProperty** параметр **Path**, чтобы указать имя раздела, и параметр **Name**, чтобы указать имя записи **DevicePath**.

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

Эта команда возвращает стандартные свойства Windows PowerShell, а также свойство **DevicePath**.

> [!NOTE]
> Хотя **Get\-ItemProperty** содержит параметры **Filter**, **Include** и **Exclude**, их невозможно использовать для фильтрации по имени свойства. Эти параметры относятся в разделам реестра (путям элементов), а не к записям реестра (свойствам элементов).

Другой вариант — использовать средство командной строки Reg.exe. Для получения справки по reg.exe введите **reg.exe \/?** в командной строке. Чтобы найти запись DevicePath, используйте reg.exe, как показано в следующей команде:

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

Также можно использовать объект **WshShell COM**, чтобы найти некоторые записи реестра, хотя этот метод не работает с большими двоичными данными или именами записей реестра, включающими такие символы, как "\\". Добавьте имя свойства с разделителем "\\" в путь элемента:

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### Создание новых записей реестра
Чтобы добавить новую запись реестра с именем "PowerShellPath" в раздел **CurrentVersion**, используйте **New\-ItemProperty** с путем к разделу, именем записи и значением записи. В этом примере использовано значение переменной Windows PowerShell **$PSHome**, в которой хранится путь к каталогу установки для Windows PowerShell.

Вы можете добавить новую запись в раздел с помощью следующей команды, и команда также вернет сведения о новой записи:

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

Значение **PropertyType** должно быть именем элемента перечисления **Microsoft.Win32.RegistryValueKind** из следующей таблицы:

|Значение PropertyType|Значение|
|----------------------|-----------|
|Двоичные данные|Двоичные данные|
|DWord|Число, которое является допустимым UInt32|
|ExpandString|Строка, которая может содержать динамически раскрывающиеся переменные среды|
|MultiString|Многострочная строка|
|Строка|Любое строковое значение|
|QWord|8 байтов двоичных данных|

> [!NOTE]
> Запись реестра можно добавить в несколько расположений, указав массив значений для параметра **Path**:

```
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

Кроме того, можно перезаписать существующее значение записи реестра, добавив параметр **Force** в любую команду **New\-ItemProperty**.

### Переименование записей реестра
Чтобы переименовать запись **PowerShellPath** в "PSHome", используйте **Rename\-ItemProperty**:

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

Чтобы отобразить переименованное значение, добавьте параметр **PassThru** в команду.

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### Удаление записей реестра
Чтобы удалить записи реестра PSHome и PowerShellPath, используйте **Remove\-ItemProperty**:

```
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```




<!--HONumber=Jun16_HO4-->


