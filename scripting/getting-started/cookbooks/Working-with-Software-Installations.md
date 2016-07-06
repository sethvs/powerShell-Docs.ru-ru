---
title: "Работа с программами установки программного обеспечения"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: 9f60be9bebe9dfaa98f495c8e9a9c0d8c2fa5cc2

---

# Работа с программами установки программного обеспечения
Доступ к приложениям, использующим установщик Windows, можно получить в классе **Win32\_Product** WMI, но не все современные приложения используют установщик Windows. Так как установщик Windows предоставляет самый широкий ряд стандартных методов работы с устанавливаемыми приложениями, обратим внимание в первую очередь на эти приложения. Установщик Windows обычно не управляет приложениями, использующими другие процедуры установки. Конкретные техники работы с этими приложениями будут зависеть от программного обеспечения установщика и решений, принятых разработчиком приложения.

> [!NOTE]
> Приложения, которые устанавливаются путем копирования файлов приложения на компьютер, обычно не могут управляться методами, описанными здесь. Вы можете управлять этими приложениями, как файлами и папками, с помощью способов, приведенных в разделе "Работа с файлами и папками".

### Создание списков приложений установщика Windows
Чтобы создать список приложений, установленных с помощью установщика Windows в локальной или удаленной системе, используйте следующий простой запрос WMI:

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

Чтобы отобразить все свойства объекта Win32Product\_Product, используйте параметр Properties командлетов форматирования, например Format\-List, со значением \* (все).

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *
Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

Также можно использовать параметр **Get\-WmiObject Filter**, чтобы выбрать только Microsoft .NET Framework 2.0. Так как фильтр, использованный в этой команде, является фильтром WMI, он использует синтаксис языка запросов WMI (WQL), а не синтаксис Windows PowerShell. Вместо этого:

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

Обратите внимание, что в запросах WQL часто используются символы (например, пробелы или знаки равенства), которые имеют особое значение в Windows PowerShell. По этой причине целесообразно всегда заключать значение параметра фильтра в кавычки. Кроме того, можно использовать escape-символ Windows PowerShell — обратный апостроф (\`), хотя это может ухудшить удобочитаемость. Следующая команда эквивалентна предыдущей и возвращает те же результаты, но использует обратный апостроф в качестве escape-символа для специальных знаков вместо того, чтобы заключать в кавычки всю строку фильтра.

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

Чтобы создать список только интересующих вас свойств, используйте параметр Property командлетов форматирования.

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

Наконец, чтобы найти имена только установленных приложений, упростите выходные данные с помощью оператора **Format\-Wide**:

```
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

Несмотря на то что теперь нам известно несколько способов поиска приложений, использовавших установщик Windows, другие приложения не были рассмотрены. Так как большинство стандартных приложений регистрируют программу удаления в Windows, с ними можно работать локально, в реестре Windows.

### Создание списка всех удаленных приложений
Несмотря на то что не существует гарантированного способа найти все приложения в системе, можно найти все программы со списками, отображенными в диалоговом окне "Добавление или удаление программ". В окне "Добавление или удаление программ" выполняется поиск этих приложений в следующем разделе реестра:

**HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.

В этом разделе также можно найти приложения. Чтобы упростить просмотр раздела "Удаление", можно сопоставить диск Windows PowerShell с данным расположением реестра:

```
PS>    

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> Диск **HKLM**: сопоставляется с корнем **HKEY\_LOCAL\_MACHINE**, поэтому этот диск используется в пути к разделу Uninstall. Вместо **HKLM:** можно было указать путь к реестру с помощью **HKLM** или **HKEY\_LOCAL\_MACHINE**. Преимущество использования диска существующего реестра состоит в том, что теперь можно применять клавишу TAB для заполнения названий разделов, а не вводить их.

Теперь диск с именем "Удаление" можно использовать для быстрого и удобного поиска установок приложений. Количество установленных приложений можно найти, подсчитав количество разделов реестра в разделе "Uninstall" для диска Windows PowerShell:

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

С помощью разных методов, начиная с **Get\-ChildItem**, можно дальше выполнять поиск в списке приложений. Чтобы получить список приложений и сохранить их в переменную **$UninstallableApplications**, используйте следующую команду:

```
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> В данном случае длинное имя переменной используется для ясности. При фактическом использовании нет причин использовать длинные имена. Хотя имена переменных можно заполнять нажатием клавиши TAB, для скорости можно использовать имена из одного-двух символов. Длинные описательные имена полезны при разработке кода для повторного использования.

Чтобы отобразить значения записей реестра в подразделах реестра раздела "Удаление", используйте метод GetValue. Значение метода является записью реестра.

Например, чтобы найти отображаемые имена приложений в разделе "Удаление", используйте следующую команду:

```
PS> Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("DisplayName") }
```

Нет никакой гарантии, что эти значения уникальны. В следующем примере два установленных элемента отображаются как Windows Media Encoder 9 Series:

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### Установка приложений
Вы можете использовать класс **Win32Product\_Product** для удаленной или локальной установки пакетов установщика Windows.

> [!NOTE]
> Чтобы установить приложение в Windows Vista, Windows Server 2008 и более поздних версиях Windows, необходимо запустить Windows PowerShell с параметром "Запустить от имени администратора".

При удаленной установке используйте сетевой UNC-путь, чтобы указать путь к пакету MSI, так как подсистема WMI не распознает пути Windows PowerShell. Например, чтобы установить пакет NewPackage.msi, расположенный в общей сетевой папке \\\\AppServ\\dsp на удаленном компьютере PC01, введите следующую команду в командной строке Windows PowerShell:

```
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq "Win32_Product"}).Install(\\AppSrv\dsp\NewPackage.msi)
```

Приложения, которые не используют метод установщика Windows, могут включать специальные методы для автоматического развертывания конкретного приложения. Чтобы определить, существует ли метод автоматического развертывания, проверьте документацию приложения или обратитесь в службу поддержки поставщика приложения. В некоторых случаях даже в том случае, если поставщик приложения не разрабатывал способы автоматической установки в приложении, производитель программного обеспечения установщика мог включить некоторые методы автоматизации.

### Удаление приложений
Удаление пакета установщика Windows с помощью Windows PowerShell работает примерно так же, как и установка пакета. Далее представлен пример, в котором пакет для удаления выбирается на основе имени. В некоторых случаях его может быть проще отфильтровать с помощью **IdentifyingNumber**:

```
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

Удаление других приложений не так просто, даже если оно выполняется локально. Строки удаления командной строки для этих приложений можно найти путем извлечения свойства **UninstallString**. Этот способ работает для приложений установщика Windows и более старых программ, отображающихся в разделе "Удаление":

```
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

Выходные данные при необходимости можно отфильтровать по отображаемому имени:

```
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -like "Win*"} | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

Однако эти строки невозможно напрямую использовать из командной строки Windows PowerShell без внесения некоторых изменений.

### Обновление приложений установщика Windows
Чтобы обновить приложение, необходимо знать название приложения и путь к пакету обновлений приложения. Получив эти сведения, можно обновить приложение с помощью одной команды Windows PowerShell:

```
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```




<!--HONumber=Jun16_HO4-->


