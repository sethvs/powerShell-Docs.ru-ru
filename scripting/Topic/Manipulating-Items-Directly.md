---
title: Прямое управление элементами
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
---
# Прямое управление элементами
Элементы, которые отображаются на дисках Windows PowerShell, например файлы и папки на дисках файловой системы и разделы реестра на дисках реестра Windows PowerShell, называются в Windows PowerShell *элементами*. Командлеты для работы с ними содержат существительное **Item** в именах.

В выходных данных команды **Get-Command -Noun Item** показано, что существует девять элементов Windows PowerShell.

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

### Создание новых элементов (New-Item)
Чтобы создать новый элемент в файловой системе, используйте командлет **New-Item**. Включите параметр **Path** с путем к элементу и параметр **ItemType** сo значением file или directory.

Например, чтобы создать каталог с именем New.Directory в каталоге C:\Temp, введите:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Чтобы создать файл, измените значение параметра **ItemType** на file. Например, чтобы создать файл с именем file1.txt в каталоге New.Directory, введите:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Тот же метод можно использовать для создания нового раздела реестра. На самом деле, раздел реестра создать проще, так как единственный тип элементов в реестре Windows — это раздел. (Записи реестра — это *свойства* элементов.) Например, чтобы создать раздел с именем _Test в подразделе CurrentVersion, введите:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

При вводе пути реестра не забудьте добавить двоеточие (**:**) в имена дисков Windows PowerShell — HKLM: и HKCU:. Без двоеточия Windows PowerShell не распознает имена дисков в пути.

### Причины, по которым значения реестра не являются элементами
При использовании командлета **Get-ChildItem** для поиска элементов в разделе реестра вы не увидите фактических записей реестра или их значений.

Например, раздел реестра **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run** обычно содержит записи реестра, представляющие приложения, которые выполняются при запуске системы.

Однако при использовании **Get-ChildItem** для поиска дочерних элементов в разделе отобразится только подраздел или раздел **OptionalComponents**:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

Хотя удобнее использовать записи реестра как элементы, невозможно указать путь к записи реестра способом, гарантирующим его уникальность. Нотация пути не различает подраздел реестра с именем **Run** и запись реестра **(Default)** в подразделе **Run**. Кроме того, так как имена записей реестра могут содержать обратную косую черту (**\**), если записи реестра были элементами, то нотацию пути невозможно использовать для различения записи реестра с именем **Windows\CurrentVersion\Run** от подраздела, расположенного в этом пути.

### Переименование существующих элементов (Rename-Item)
Чтобы изменить имя файла или папки, используйте командлет **Rename-Item**. Следующая команда изменяет имя файла **file1.txt** на **fileOne.txt**.

```
PS> Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

Командлет **Rename-Item** может изменить имя файла или папки, но не может переместить элемент. Произойдет сбой следующей команды, так как она попытается переместить файл из каталога New.Directory во временный каталог.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### Перемещение элементов (Move-Item)
Чтобы переместить файл или папку, используйте командлет **Move-Item**.

Например, следующая команда перемещает каталог New.Directory из каталога C:\temp в корень диска C:. Чтобы убедиться, что элемент перемещен, включите параметр **PassThru** командлета **Move-Item**. Без **Passthru** командлет **Move-Item** не отображает результаты.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### Копирование элементов (Copy-Item)
Если вы знакомы с операциями копирования в других оболочках, поведение командлета **Copy-Item** в Windows PowerShell может показаться нестандартным. При копировании элемента из одного расположения в другое командлет Copy-Item не копирует его содержимое по умолчанию.

Например, при копировании каталога **New.Directory** с диска C: в каталог C:\temp команда выполняется, но файлы в каталоге New.Directory не копируются.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Если отобразить содержимое **C:\temp\New.Directory**, оно не будет содержать файлы:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Почему командлет **Copy-Item** не копирует содержимое в новое расположение?

Командлет **Copy-Item** предполагалось использовать как универсальный; он не предназначен для простого копирования файлов и папок. Кроме того, даже при копировании файлов и папок может потребоваться копировать только контейнер без элементов внутри него.

Чтобы скопировать все содержимое папки, включите параметр **Recurse** командлета **Copy-Item** в команду. Если вы уже скопировали каталог без содержимого, добавьте параметр **Force**, который позволит перезаписать пустую папку.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

### Удаление элементов (Remove-Item)
Чтобы удалить файлы и папки, используйте командлет **Remove-Item**. Командлеты Windows PowerShell, например **Remove-Item**, которые могут вносить значительные и необратимые изменения, часто будут запрашивать подтверждение при вводе команд. Например, при попытке удалить папку **New.Directory** вам предлагается подтвердить команду, так как папка содержит файлы:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Так как ответ **Да** является ответом по умолчанию, чтобы удалить папку вместе файлами, нажмите клавишу **ВВОД**. Чтобы удалить папку без подтверждения, используйте параметр **-Recurse**.

```
PS> Remove-Item C:\temp\New.Directory -Recurse
```

### Выполнение элементов (Invoke-Item)
Windows PowerShell использует командлет **Invoke-Item** для выполнения действия по умолчанию для файла или папки. Это действие по умолчанию определяется обработчиком приложений по умолчанию в реестре; эффект будет таким же, что и при двойном щелчке элемента в проводнике.

Предположим, вы запускаете следующую команду:

```
PS> Invoke-Item C:\WINDOWS
```

Появится окно проводника, расположенного в C:\Windows, как если бы вы дважды щелкнули папку C:\Windows.

При вызове файла **Boot.ini** в системе, предшествующей Windows Vista:

```
PS> Invoke-Item C:\boot.ini
```

Если тип INI-файла связан с Блокнотом, файл boot.ini будет открыт в Блокноте.



<!--HONumber=Apr16_HO1-->


