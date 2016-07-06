---
title: "Создание объектов .NET и COM с помощью New-Object"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: e986e85a5d7416d8deaec06c0784263ee09fc9ff

---

# Создание объектов .NET и COM (New-Object)
Существуют программные компоненты с интерфейсами платформы .NET Framework и COM, которые позволяют выполнять множество задач системного администрирования. Windows PowerShell позволяет использовать эти компоненты, поэтому доступные задачи не ограничиваются только применением командлетов. Множество командлетов в первом выпуске Windows PowerShell не работают с удаленными компьютерами. Мы покажем, как преодолеть это ограничение при управлении журналами событий с помощью класса **System.Diagnostics.EventLog** .NET Framework непосредственно из Windows PowerShell.

### Использование командлета New\-Object для доступа к журналу событий
Библиотека классов платформы .NET Framework включает класс **System.Diagnostics.EventLog**, позволяющий управлять журналами событий. Можно создать новый экземпляр класса .NET Framework с помощью командлета **New\-Object** с параметром **TypeName**. Например, следующая команда создает ссылку на журнал событий:

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

Хотя команда и создала экземпляр класса EventLog, этот экземпляр не содержит данных. Это вызвано тем, что не был указан определенный журнал событий. Как получить настоящий журнал событий?

#### Использование конструкторов с командлетом New\-Object
Чтобы сослаться на определенный журнал событий, нужно указать его имя. Командлет **New\-Object** имеет параметр **ArgumentList**. Аргументы, передаваемые в этот параметр, используются специальным методом запуска объекта. Этот метод называется *конструктором*, поскольку используется для создания объекта. Например, чтобы получить ссылку на журнал приложений, нужно указать строку "Application" в качестве аргумента:

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> Поскольку основные классы платформы .NET Framework содержатся в пространстве имен System, Windows PowerShell автоматически пытается найти в нем указанные классы, если не может найти совпадения для указанного имени типа. Это значит, что можно указать класс Diagnostics.EventLog вместо класса System.Diagnostics.EventLog.

#### Сохранение объектов в переменных
Вам может понадобиться сохранить ссылку на объект для использования в текущей оболочке. Хотя Windows PowerShell позволяет выполнять больше задач с помощью конвейеров, что снижает потребность в переменных, иногда сохранение ссылок на объекты в переменных помогает сделать работу с объектами более удобной.

Windows PowerShell позволяет создавать переменные, которые, по сути, являются именованными объектами. Выходные данные любой допустимой команды Windows PowerShell можно сохранить в переменной. Имена переменных всегда начинаются со знака "$". Если нужно сохранить ссылку на журнал приложений в переменной с именем $AppLog, введите имя переменной, знак равенства и команду, используемую для создания объекта журнала приложений:

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

Если после этого набрать $AppLog, будет выведено содержимое журнала приложения:

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### Доступ к удаленному журналу событий с помощью New\-Object
Команды, рассмотренные в предыдущем разделе, обращаются к локальному компьютеру. Для этого подходит и командлет **Get\-EventLog**. Чтобы получить доступ к журналу приложений на удаленном компьютере, необходимо в качестве аргументов ввести имя журнала и имя (или IP-адрес) компьютера.

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

Какие действия могут быть выполнены с переменной $RemoteAppLog после сохранения в ней ссылки на журнал событий?

#### Очистка журнала событий методами объектов
Для выполнения тех или иных действий у объектов часто имеются методы. Командлет **Get\-Member** позволяет вывести методы, связанные с объектом. Следующая команда и выделенный фрагмент выходных данных показывают некоторые методы класса EventLog:

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

Метод **Clear()** позволяет очистить журнал событий. При вызове метода после его имени обязательно должны следовать скобки, даже если методу не требуются аргументы. Таким образом оболочка Windows PowerShell отличает метод от возможного свойства с таким же именем. Чтобы вызвать метод **Clear**, нужно ввести следующую команду:

```
PS> $RemoteAppLog.Clear()
```

Введите следующую строку, чтобы отобразить журнал: Видно, что журнал событий очищен, и вместо 262 записей не содержит ни одной.

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### Создание COM-объектов с помощью New\-Object
Командлет **New\-Object** может использоваться для работы с СОМ-компонентами. Спектр этих компонентов довольно обширен — от различных библиотек, поставляемых с сервером сценариев Windows (WSH), до приложений ActiveX, например Internet Explorer, установленных на большинстве систем.

Командлет **New\-Object** создает СОМ-объекты с помощью вызываемых оболочек времени выполнения .NET Framework, поэтому для него действуют те же ограничения, что и для платформы .NET Framework во время вызова СОМ-объектов. Чтобы создать СОМ-объект, необходимо задать параметр **ComObject** для программного идентификатора *ProgId* нужного класса СОМ-объекта. Подробное обсуждение ограничений использования СОМ-объектов и определение доступных в системе программных идентификаторов выходит за рамки данного руководства пользователя, но с оболочкой Windows PowerShell может использоваться большинство хорошо известных объектов таких сред, как сервер сценариев Windows.

Объекты сервера сценариев Windows можно создать, задав следующие программные идентификаторы: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary** и **Scripting.FileSystemObject**. Эти объекты создаются следующими командами:

```
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

Хотя функциональность этих классов в большой степени может быть реализована другими способами в Windows PowerShell, некоторые действия (например создание ярлыков) проще выполнить с помощью классов сервера сценариев Windows.

### Создание ярлыков на рабочем столе с помощью WScript.Shell
Одной из функций, быстро выполняемых с помощью СОМ-объектов, является создание ярлыков. Допустим, на рабочем столе требуется создать ярлык для корневой папки Windows PowerShell. Сначала необходимо создать ссылку на объект **WScript.Shell**, которая сохраняется в переменной **$WshShell**:

```
$WshShell = New-Object -ComObject WScript.Shell
```

Командлет Get\-Member работает и с СОМ-объектами, поэтому элементы объекта можно изучить, введя следующее:

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

У командлета **Get\-Member** имеется необязательный параметр **InputObject**, который можно использовать вместо передачи по конвейеру, чтобы предоставить входные данные для **Get\-Member**. При использовании команды **Get\-Member \-InputObject $WshShell** в примере выше выходные данные были бы такими же. При указании параметра **InputObject** командлет обрабатывает свои аргументы как одно целое. Это означает, что, если в переменной содержится несколько объектов, командлет **Get\-Member** обрабатывает их как массив объектов. Например:

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

Метод **WScript.Shell CreateShortcut** допускает использование одного аргумента — пути к создаваемому файлу ярлыка. Можно указать полный путь к рабочему столу, но существует и более простой способ. Рабочий стол обычно представлен папкой с именем Desktop внутри домашней папки текущего пользователя. В Windows PowerShell имеется переменная **$Home**, в которой содержится путь к этой домашней папке. Таким образом, путь к домашней папке может быть задан указанием этой переменной, после чего нужно ввести только имя папки Desktop и имя создаваемого ярлыка:

```
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

Если похожая на переменную строка заключена в двойные кавычки, Windows PowerShell пытается заменить ее подходящим значением. При использовании одиночных кавычек значение переменной не подставляется. Например, попробуйте ввести следующие команды:

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

В переменной **$lnk** теперь хранится новая ссылка на ярлык. Чтобы просмотреть элементы переменной, ее можно передать по конвейеру в **Get\-Member**. Выходные данные (см. ниже) показывают все элементы, необходимые, чтобы завершить создание ярлыка:

<pre>PS> $lnk | Get-Member TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b} Name             MemberType   Definition ----             ----------   ---------- ... Save             Method       void Save () ... TargetPath       Property     string TargetPath () {get} {set} ...</pre>

Осталось определить свойство **TargetPath**, указывающее путь к папке Windows PowerShell, и вызвать метод **Save**, чтобы сохранить **$lnk** ярлыка. Путь к папке Windows PowerShell хранится в переменной **$PSHome**, поэтому это можно сделать, введя следующее:

<pre>$lnk.TargetPath = $PSHome $lnk.Save()</pre>

### Использование Internet Explorer из Windows PowerShell
С помощью СОМ-объектов можно автоматизировать многие приложения (включая семейство приложений Microsoft Office и Internet Explorer). На примере Internet Explorer можно рассмотреть некоторые типичные приемы и тонкости, связанные с работой приложений, основанных на СОМ-технологии.

Экземпляр Internet Explorer создается указанием программного идентификатора этого приложения **InternetExplorer.Application**:

```
$ie = New-Object -ComObject InternetExplorer.Application
```

Эта команда запускает Internet Explorer, но не отображает его. Если запустить командлет Get\-Process, то можно увидеть выполняющийся процесс iexplore. Причем после выхода из Windows PowerShell выполнение этого процесса будет продолжаться. Чтобы завершить процесс iexplore, необходимо перезагрузить компьютер или воспользоваться средством наподобие диспетчера задач.

> [!NOTE]
> СОМ-объекты, запускаемые в виде отдельных процессов, обычно называются *исполняемыми файлами ActiveX*. При их запуске окно пользовательского интерфейса отображается не всегда. Если окно создается, но не отображается, как в случае с приложением Internet Explorer, фокус обычно перемещается на рабочий стол Windows, и для взаимодействия с окном его необходимо сделать видимым.

Введя **$ie | Get\-Member**, можно получить список свойств и методов для Internet Explorer. Чтобы отобразить окно Internet Explorer, свойству Visible нужно присвоить значение $true, введя следующее:

```
$ie.Visible = $true
```

После этого можно перейти по какому-либо веб-адресу, используя метод Navigate:

```
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

Другие элементы объектной модели Internet Explorer позволяют получить текстовое содержание веб-страниц. Следующая команда отображает HTML-текст в теле текущей веб-страницы:

```
$ie.Document.Body.InnerText
```

Чтобы закрыть Internet Explorer из PowerShell, необходимо вызвать метод Quit():

```
$ie.Quit()
```

Это приведет к принудительному закрытию приложения. Переменная $ie больше не содержит действительную ссылку, хотя все еще отображается как СОМ-объект. Попытка использования этой переменной приводит к ошибке автоматизации:

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

В этой ситуации можно либо удалить оставшуюся ссылку с помощью команды $ie \= $null, либо полностью удалить переменную:

```
Remove-Variable ie
```

> [!NOTE]
> Для исполняемых файлов ActiveX нет общего стандарта, по которому выполнение их процессов завершается или продолжается после удаления ссылки на них. Выход из приложения зависит от обстоятельств (видимо ли приложение, открыт ли в нем какой-либо отредактированный документ, а также продолжается ли выполнение Windows PowerShell). Поэтому требуется проверка поведения при завершении работы каждого исполняемого файла ActiveX, используемого в Windows PowerShell.

### Получение предупреждений о вызываемых COM-объектах .NET Framework
В некоторых случаях у СОМ-объекта имеется соответствующая *вызываемая оболочка времени выполнения* (RCW) .NET Framework, и именно она используется командлетом **New\-Object**. Поведение оболочки RCW может отличаться от поведения обычного СОМ-объекта, поэтому у командлета **New\-Object** имеется параметр **Strict**, используемый для предупреждения о доступе к RCW. Если указать параметр **Strict** и создать СОМ-объект, использующий оболочку RCW, выводится предупреждение:

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

Объект создается, но предупреждение указывает на то, что он не является стандартным СОМ-объектом.




<!--HONumber=Jun16_HO4-->


