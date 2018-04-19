---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Работа с файлами и папками
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: 6b1fcd438570c8708aa87e4b213f33474921d5f8
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-files-and-folders"></a>Работа с файлами и папками

Просмотр содержимого дисков Windows PowerShell и управление хранящимися на них элементами аналогично управлению файлами и папками на физических дисках Windows. В этом разделе мы обсудим выполнение конкретных задач по управлению файлами и папками с помощью PowerShell.

### <a name="listing-all-the-files-and-folders-within-a-folder"></a>Получение списка файлов и папок, содержащихся в папке

Извлечь все элементы непосредственно из папки можно с помощью командлета **Get-ChildItem**. Для отображения скрытых и системных элементов добавьте необязательный параметр **Force**. Например, эта команда отображает непосредственное содержимое диска C Windows PowerShell (которое совпадает с содержимым физического диска C Windows):

```powershell
Get-ChildItem -Path C:\ -Force
```

Эта команда выводит только элементы, содержащиеся на диске непосредственно, так же как и команда **DIR** оболочки Cmd.exe или команда **ls** оболочки UNIX. Для показа вложенных элементов необходимо также указать параметр **-Recurse**. (Время выполнения этой операции будет очень велико.) Для вывода всего содержимого диска C введите:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

Командлет **Get-ChildItem** позволяет отфильтровать элементы с помощью параметров **Path**, **Filter**, **Include** и **Exclude**, но обычно осуществляется лишь фильтрация по имени. Сложную фильтрацию на основе других свойств элементов можно выполнить с помощью командлета **Where-Object**.

Следующая команда находит все исполняемые файлы в папке Program Files, которые были в последний раз изменены после 1 октября 2005 г. и размер которых не менее одного мегабайта и не более десяти мегабайт:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a>Копирование файлов и папок

Копирование выполняется с помощью командлета **Copy-Item**. Следующая команда создает резервную копию C:\\boot.ini в C:\\boot.bak:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Если целевой файл уже существует, то попытка копирования завершается неудачей. Чтобы перезаписать имеющийся целевой файл, используйте параметр **Force**.

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Эта команда работает, даже если целевой объект доступен только для чтения.

Так же выполняется и копирование папок. Эта команда рекурсивно копирует папку "C:\\temp\\test1" в новую папку "c:\\temp\\DeleteMe".

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

Можно также скопировать избранные элементы. Следующая команда копирует все файлы .txt, содержащиеся в папке "c:\\data", в папку "c:\\temp\\text":

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Для копирования элементов файловой системы можно использовать и другие средства. В Windows PowerShell по-прежнему работают команды XCOPY, ROBOCOPY и такие COM-объекты, как **Scripting.FileSystemObject**. Например, можно воспользоваться COM-классом **Scripting.FileSystem** сервера сценариев Windows для создания резервной копии файла C:\\boot.ini в файле C:\\boot.bak:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

### <a name="creating-files-and-folders"></a>Создание файлов и папок

Создание новых элементов осуществляется одинаковым образом всеми поставщиками Windows PowerShell. Если поставщик Windows PowerShell поддерживает более одного типа элементов (например, поставщик Windows PowerShell FileSystem различает каталоги и файлы), необходимо указать тип элемента.

Эта команда создает папку "C:\\temp\\New Folder":

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Эта команда создает пустой файл "C:\\temp\\New Folder\\file.txt":

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a>Удаление всех файлов и папок, содержащихся в папке

Удалить вложенные элементы можно с помощью командлета **Remove-Item**, однако он потребует подтверждения удаления, если элемент сам что-нибудь содержит. Например, при попытке удаления папки C:\\temp\\DeleteMe, которая содержит другие элементы, Windows PowerShell предварительно предложит подтвердить удаление этой папки:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Если подтверждение для каждого вложенного элемента нежелательно, задайте параметр **Recurse**:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a>Отображение локальной папки в виде диска, доступного в Windows

Отобразить локальную папку можно с помощью команды **subst**. Следующая команда создает локальный диск P:, корневым каталогом которого является локальный каталог Program Files:

```powershell
subst p: $env:programfiles
```

Как и в случае сетевых дисков, диски, отображенные в оболочке Windows PowerShell с помощью команды **subst**, немедленно становятся доступными оболочке Windows PowerShell.

### <a name="reading-a-text-file-into-an-array"></a>Чтение текстового файла в массив

Одним из наиболее общих форматов хранения текстовых данных является файл, отдельные строки которого рассматриваются как отдельные элементы. Командлет **Get-Content** используется для чтения всего файла за один шаг, как показано далее.

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional
with Data Execution Prevention" /noexecute=optin /fastdetect
```

Командлет **Get-Content** сразу рассматривает данные, считанные из файла, как массив с одним элементом на строку содержимого файла. Убедиться в этом можно, проверив свойство **Length** полученного содержимого:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Эта команда наиболее полезна для непосредственного ввода в Windows PowerShell информационных списков. Например, можно хранить в файле "C:\\temp\\domainMembers.txt" список имен компьютеров или IP-адресов по одному имени на каждую строку файла. Можно использовать командлет **Get-Content**, чтобы извлечь содержимое файла и поместить его в переменную **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

Теперь переменная **$Computers** представляет собой массив, содержащий в каждом элементе имя компьютера.
