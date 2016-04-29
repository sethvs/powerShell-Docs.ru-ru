---
title: Работа с разделами реестра
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
---
# Работа с разделами реестра
Поскольку разделы реестра представляют собой элементы на дисках Windows PowerShell, работа с ними очень похожа на работу с файлами и папками. Одно важное различие заключается в том, что каждый элемент реестрового диска Windows PowerShell представляет собой контейнер, как и папка на диске файловой системы. Однако записи реестра и связанные с ними значения являются свойствами элементов, а не отдельными элементами.

### Получение всех подразделов раздела реестра
Показать все элементы, непосредственно содержащиеся в разделе реестра, можно с помощью командлета **Get-ChildItem**. Для отображения скрытых и системных элементов добавьте необязательный параметр **Force**. Например, эта команда отображает элементы, непосредственно расположенные на диске HKCU: Windows PowerShell, который соответствует кусту HKEY_CURRENT_USER:

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

Это разделы верхнего уровня, отображаемые внутри HKEY_CURRENT_USER в редакторе реестра (Regedit.exe).

Указать этот путь в реестре можно также, задав имя поставщика реестра с последующей строкой "**::**". Полное имя поставщика реестра имеет вид **Microsoft.PowerShell.Core\Registry**, но может быть сокращено до **Registry**. Любая из следующих команд выводит содержимое элементов, непосредственно расположенных внутри HKCU:

```
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

Эти команды выводят только элементы, содержащиеся на диске непосредственно, так же как и команда **DIR** оболочки Cmd.exe или команда **ls** оболочки UNIX Для показа вложенных элементов необходимо указать параметр **Recurse**. Для вывода всех разделов в HKCU используется следующая команда (эта операция может занять очень продолжительное время):

```
Get-ChildItem -Path hkcu:\ -Recurse
```

Командлет **Get-ChildItem** позволяет выполнять сложные операции фильтрации с помощью параметров **Path**, **Filter**, **Include** и **Exclude**, но обычно осуществляется лишь фильтрация по имени. Сложную фильтрацию на основе других свойств элементов можно выполнить с помощью командлета **Where-Object**. Следующая команда находит все разделы в HKCU:\Software, у которых не более одного подраздела и ровно четыре значения:

```
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### Копирование разделов
Копирование выполняется с помощью командлета **Copy-Item**. Следующая команда копирует HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion и все его свойства в HKCU:\, создавая новый раздел с именем "CurrentVersion":

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

Если изучить этот новый раздел в редакторе реестра или с помощью командлета **Get-ChildItem**, можно увидеть, что в новом расположении отсутствуют копии подразделов, содержавшихся в исходном разделе. Чтобы скопировать все содержимое контейнера, необходимо указать параметр **Recurse**. Копирование в предыдущем примере можно сделать рекурсивным, если использовать следующую команду:

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

Для копирования файловой системы можно использовать и другие доступные средства. В оболочке Windows PowerShell можно использовать любые средства для редактирования реестра (в том числе reg.exe, regini.exe и regedit.exe), а также COM-объекты, поддерживающие редактирование реестра (такие как WScript.Shell и WMI-класс StdRegProv).

### Создание разделов
Создание новых разделов в реестре проще, чем создание нового элемента в файловой системе. Поскольку все разделы реестра являются контейнерами, нет необходимости указывать тип элемента. Достаточно указать явный путь, например:

```
New-Item -Path hkcu:\software\_DeleteMe
```

Для указания раздела можно также использовать путь на основе имени поставщика:

```
New-Item -Path Registry::HKCU\_DeleteMe
```

### Удаление разделов
Удаление элементов в принципе осуществляется одинаково для всех поставщиков. Следующие команды удаляют элементы, не выводя никаких сообщений:

```
Remove-Item -Path hkcu:\Software\_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### Удаление всех разделов внутри определенного раздела
Удалить вложенные элементы можно с помощью командлета **Remove-Item**, однако он потребует подтверждения удаления, если элемент сам что-нибудь содержит. Например, при попытке удаления созданного нами подраздела HKCU:\CurrentVersion будет отображено следующее:

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Для удаления вложенных элементов без подтверждения следует указать параметр **-Recurse**:

```
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

Если нужно удалить все элементы в HKCU:\CurrentVersion, но не сам раздел, вместо этого введите следующее:

```
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```



<!--HONumber=Apr16_HO1-->


