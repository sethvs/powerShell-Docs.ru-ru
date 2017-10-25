---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Создание объектов .NET и COM (New-Object)"
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 534e1a9a759d67cfc62ce658a7abddf02f767212
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="creating-net-and-com-objects-new-object"></a><span data-ttu-id="bff82-103">Создание объектов .NET и COM (New-Object)</span><span class="sxs-lookup"><span data-stu-id="bff82-103">Creating .NET and COM Objects (New-Object)</span></span>
<span data-ttu-id="bff82-104">Существуют программные компоненты с интерфейсами платформы .NET Framework и COM, которые позволяют выполнять множество задач системного администрирования.</span><span class="sxs-lookup"><span data-stu-id="bff82-104">There are software components with .NET Framework and COM interfaces that enable you to perform many system administration tasks.</span></span> <span data-ttu-id="bff82-105">Windows PowerShell позволяет использовать эти компоненты, поэтому доступные задачи не ограничиваются только применением командлетов.</span><span class="sxs-lookup"><span data-stu-id="bff82-105">Windows PowerShell lets you use these components, so you are not limited to the tasks that can be performed by using cmdlets.</span></span> <span data-ttu-id="bff82-106">Множество командлетов в первом выпуске Windows PowerShell не работают с удаленными компьютерами.</span><span class="sxs-lookup"><span data-stu-id="bff82-106">Many of the cmdlets in the initial release of Windows PowerShell do not work against remote computers.</span></span> <span data-ttu-id="bff82-107">Мы покажем, как преодолеть это ограничение при управлении журналами событий с помощью класса **System.Diagnostics.EventLog** .NET Framework непосредственно из Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bff82-107">We will demonstrate how to get around this limitation when managing event logs by using the .NET Framework **System.Diagnostics.EventLog** class directly from Windows PowerShell.</span></span>

### <a name="using-new-object-for-event-log-access"></a><span data-ttu-id="bff82-108">Использование командлета New-Object для доступа к журналу событий</span><span class="sxs-lookup"><span data-stu-id="bff82-108">Using New-Object for Event Log Access</span></span>
<span data-ttu-id="bff82-109">Библиотека классов платформы .NET Framework включает класс **System.Diagnostics.EventLog**, позволяющий управлять журналами событий.</span><span class="sxs-lookup"><span data-stu-id="bff82-109">The .NET Framework Class Library includes a class named **System.Diagnostics.EventLog** that can be used to manage event logs.</span></span> <span data-ttu-id="bff82-110">Можно создать новый экземпляр класса .NET Framework с помощью командлета **New-Object** с параметром **TypeName**.</span><span class="sxs-lookup"><span data-stu-id="bff82-110">You can create a new instance of a .NET Framework class by using the **New-Object** cmdlet with the **TypeName** parameter.</span></span> <span data-ttu-id="bff82-111">Например, следующая команда создает ссылку на журнал событий:</span><span class="sxs-lookup"><span data-stu-id="bff82-111">For example, the following command creates an event log reference:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

<span data-ttu-id="bff82-112">Хотя команда и создала экземпляр класса EventLog, этот экземпляр не содержит данных.</span><span class="sxs-lookup"><span data-stu-id="bff82-112">Although the command has created an instance of the EventLog class, the instance does not include any data.</span></span> <span data-ttu-id="bff82-113">Это вызвано тем, что не был указан определенный журнал событий.</span><span class="sxs-lookup"><span data-stu-id="bff82-113">That is because we did not specify a particular event log.</span></span> <span data-ttu-id="bff82-114">Как получить настоящий журнал событий?</span><span class="sxs-lookup"><span data-stu-id="bff82-114">How do you get a real event log?</span></span>

#### <a name="using-constructors-with-new-object"></a><span data-ttu-id="bff82-115">Использование конструкторов с командлетом New-Object</span><span class="sxs-lookup"><span data-stu-id="bff82-115">Using Constructors with New-Object</span></span>
<span data-ttu-id="bff82-116">Чтобы сослаться на определенный журнал событий, нужно указать его имя.</span><span class="sxs-lookup"><span data-stu-id="bff82-116">To refer to a specific event log, you need to specify the name of the log.</span></span> <span data-ttu-id="bff82-117">Командлет **New-Object** имеет параметр **ArgumentList**.</span><span class="sxs-lookup"><span data-stu-id="bff82-117">**New-Object** has an **ArgumentList** parameter.</span></span> <span data-ttu-id="bff82-118">Аргументы, передаваемые в этот параметр, используются специальным методом запуска объекта.</span><span class="sxs-lookup"><span data-stu-id="bff82-118">The arguments you pass as values to this parameter are used by a special startup method of the object.</span></span> <span data-ttu-id="bff82-119">Этот метод называется *конструктором*, поскольку используется для создания объекта.</span><span class="sxs-lookup"><span data-stu-id="bff82-119">The method is called a *constructor* because it is used to construct the object.</span></span> <span data-ttu-id="bff82-120">Например, чтобы получить ссылку на журнал приложений, нужно указать строку "Application" в качестве аргумента:</span><span class="sxs-lookup"><span data-stu-id="bff82-120">For example, to get a reference to the Application log, you specify the string 'Application' as an argument:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> <span data-ttu-id="bff82-121">Поскольку основные классы платформы .NET Framework содержатся в пространстве имен System, Windows PowerShell автоматически пытается найти в нем указанные классы, если не может найти совпадения для указанного имени типа.</span><span class="sxs-lookup"><span data-stu-id="bff82-121">Since most of the .NET Framework core classes are contained in the System namespace, Windows PowerShell will automatically attempt to find classes you specify in the System namespace if it cannot find a match for the typename you specify.</span></span> <span data-ttu-id="bff82-122">Это значит, что можно указать класс Diagnostics.EventLog вместо класса System.Diagnostics.EventLog.</span><span class="sxs-lookup"><span data-stu-id="bff82-122">This means that you can specify Diagnostics.EventLog instead of System.Diagnostics.EventLog.</span></span>

#### <a name="storing-objects-in-variables"></a><span data-ttu-id="bff82-123">Сохранение объектов в переменных</span><span class="sxs-lookup"><span data-stu-id="bff82-123">Storing Objects in Variables</span></span>
<span data-ttu-id="bff82-124">Вам может понадобиться сохранить ссылку на объект для использования в текущей оболочке.</span><span class="sxs-lookup"><span data-stu-id="bff82-124">You might want to store a reference to an object, so you can use it in the current shell.</span></span> <span data-ttu-id="bff82-125">Хотя Windows PowerShell позволяет выполнять больше задач с помощью конвейеров, что снижает потребность в переменных, иногда сохранение ссылок на объекты в переменных помогает сделать работу с объектами более удобной.</span><span class="sxs-lookup"><span data-stu-id="bff82-125">Although Windows PowerShell lets you do a lot of work with pipelines, lessening the need for variables, sometimes storing references to objects in variables makes it more convenient to manipulate those objects.</span></span>

<span data-ttu-id="bff82-126">Windows PowerShell позволяет создавать переменные, которые, по сути, являются именованными объектами.</span><span class="sxs-lookup"><span data-stu-id="bff82-126">Windows PowerShell lets you create variables that are essentially named objects.</span></span> <span data-ttu-id="bff82-127">Выходные данные любой допустимой команды Windows PowerShell можно сохранить в переменной.</span><span class="sxs-lookup"><span data-stu-id="bff82-127">The output from any valid Windows PowerShell command can be stored in a variable.</span></span> <span data-ttu-id="bff82-128">Имена переменных всегда начинаются со знака "$".</span><span class="sxs-lookup"><span data-stu-id="bff82-128">Variable names always begin with $.</span></span> <span data-ttu-id="bff82-129">Если нужно сохранить ссылку на журнал приложений в переменной с именем $AppLog, введите имя переменной, знак равенства и команду, используемую для создания объекта журнала приложений:</span><span class="sxs-lookup"><span data-stu-id="bff82-129">If you want to store the Application log reference in a variable named $AppLog, type the name of the variable, followed by an equal sign and then type the command used to create the Application log object:</span></span>

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

<span data-ttu-id="bff82-130">Если после этого набрать $AppLog, будет выведено содержимое журнала приложения:</span><span class="sxs-lookup"><span data-stu-id="bff82-130">If you then type $AppLog, you can see that it contains the Application log:</span></span>

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a><span data-ttu-id="bff82-131">Доступ к удаленному журналу событий с помощью New-Object</span><span class="sxs-lookup"><span data-stu-id="bff82-131">Accessing a Remote Event Log with New-Object</span></span>
<span data-ttu-id="bff82-132">Команды, рассмотренные в предыдущем разделе, обращаются к локальному компьютеру. Для этого подходит и командлет **Get-EventLog**.</span><span class="sxs-lookup"><span data-stu-id="bff82-132">The commands used in the preceding section target the local computer; the **Get-EventLog** cmdlet can do that.</span></span> <span data-ttu-id="bff82-133">Чтобы получить доступ к журналу приложений на удаленном компьютере, необходимо в качестве аргументов ввести имя журнала и имя (или IP-адрес) компьютера.</span><span class="sxs-lookup"><span data-stu-id="bff82-133">To access the Application log on a remote computer, you must supply both the log name and a computer name (or IP address) as arguments.</span></span>

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

<span data-ttu-id="bff82-134">Какие действия могут быть выполнены с переменной $RemoteAppLog после сохранения в ней ссылки на журнал событий?</span><span class="sxs-lookup"><span data-stu-id="bff82-134">Now that we have a reference to an event log stored in the $RemoteAppLog variable, what tasks can we perform on it?</span></span>

#### <a name="clearing-an-event-log-with-object-methods"></a><span data-ttu-id="bff82-135">Очистка журнала событий методами объектов</span><span class="sxs-lookup"><span data-stu-id="bff82-135">Clearing an Event Log with Object Methods</span></span>
<span data-ttu-id="bff82-136">Для выполнения тех или иных действий у объектов часто имеются методы.</span><span class="sxs-lookup"><span data-stu-id="bff82-136">Objects often have methods that can be called to perform tasks.</span></span> <span data-ttu-id="bff82-137">Командлет **Get-Member** позволяет вывести методы, связанные с объектом.</span><span class="sxs-lookup"><span data-stu-id="bff82-137">You can use **Get-Member** to display the methods associated with an object.</span></span> <span data-ttu-id="bff82-138">Следующая команда и выделенный фрагмент выходных данных показывают некоторые методы класса EventLog:</span><span class="sxs-lookup"><span data-stu-id="bff82-138">The following command and selected output show some the methods of the EventLog class:</span></span>

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

<span data-ttu-id="bff82-139">Метод **Clear()** позволяет очистить журнал событий.</span><span class="sxs-lookup"><span data-stu-id="bff82-139">The **Clear()** method can be used to clear the event log.</span></span> <span data-ttu-id="bff82-140">При вызове метода после его имени обязательно должны следовать скобки, даже если методу не требуются аргументы.</span><span class="sxs-lookup"><span data-stu-id="bff82-140">When calling a method, you must always follow the method name by parentheses, even if the method does not require arguments.</span></span> <span data-ttu-id="bff82-141">Таким образом оболочка Windows PowerShell отличает метод от возможного свойства с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="bff82-141">This lets Windows PowerShell distinguish between the method and a potential property with the same name.</span></span> <span data-ttu-id="bff82-142">Чтобы вызвать метод **Clear**, нужно ввести следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bff82-142">Type the following to call the **Clear** method:</span></span>

```
PS> $RemoteAppLog.Clear()
```

<span data-ttu-id="bff82-143">Введите следующую строку, чтобы отобразить журнал:</span><span class="sxs-lookup"><span data-stu-id="bff82-143">Type the following to display the log.</span></span> <span data-ttu-id="bff82-144">Видно, что журнал событий очищен, и вместо 262 записей не содержит ни одной.</span><span class="sxs-lookup"><span data-stu-id="bff82-144">You will see that the event log was cleared, and now has 0 entries instead of 262:</span></span>

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a><span data-ttu-id="bff82-145">Создание COM-объектов с помощью New-Object</span><span class="sxs-lookup"><span data-stu-id="bff82-145">Creating COM Objects with New-Object</span></span>
<span data-ttu-id="bff82-146">Командлет **New-Object** может использоваться для работы с СОМ-компонентами.</span><span class="sxs-lookup"><span data-stu-id="bff82-146">You can use **New-Object** to work with Component Object Model (COM) components.</span></span> <span data-ttu-id="bff82-147">Спектр этих компонентов довольно обширен — от различных библиотек, поставляемых с сервером сценариев Windows (WSH), до приложений ActiveX, например Internet Explorer, установленных на большинстве систем.</span><span class="sxs-lookup"><span data-stu-id="bff82-147">Components range from the various libraries included with Windows Script Host (WSH) to ActiveX applications such as Internet Explorer that are installed on most systems.</span></span>

<span data-ttu-id="bff82-148">Командлет **New-Object** создает СОМ-объекты с помощью вызываемых оболочек времени выполнения .NET Framework, поэтому для него действуют те же ограничения, что и для платформы .NET Framework во время вызова СОМ-объектов.</span><span class="sxs-lookup"><span data-stu-id="bff82-148">**New-Object** uses .NET Framework Runtime-Callable Wrappers to create COM objects, so it has the same limitations that .NET Framework does when calling COM objects.</span></span> <span data-ttu-id="bff82-149">Чтобы создать СОМ-объект, необходимо задать параметр **ComObject** для программного идентификатора *ProgId* нужного класса СОМ-объекта.</span><span class="sxs-lookup"><span data-stu-id="bff82-149">To create a COM object, you need to specify the **ComObject** parameter with the Programmatic Identifier or *ProgId* of the COM class you want to use.</span></span> <span data-ttu-id="bff82-150">Подробное обсуждение ограничений использования СОМ-объектов и определение доступных в системе программных идентификаторов выходит за рамки данного руководства пользователя, но с оболочкой Windows PowerShell может использоваться большинство хорошо известных объектов таких сред, как сервер сценариев Windows.</span><span class="sxs-lookup"><span data-stu-id="bff82-150">A complete discussion of the limitations of COM use and determining what ProgIds are available on a system is beyond the scope of this user's guide, but most well-known objects from environments such as WSH can be used within Windows PowerShell.</span></span>

<span data-ttu-id="bff82-151">Объекты сервера сценариев Windows можно создать, задав следующие программные идентификаторы: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary** и **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="bff82-151">You can create the WSH objects by specifying these progids: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, and **Scripting.FileSystemObject**.</span></span> <span data-ttu-id="bff82-152">Эти объекты создаются следующими командами:</span><span class="sxs-lookup"><span data-stu-id="bff82-152">The following commands create these objects:</span></span>

```
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

<span data-ttu-id="bff82-153">Хотя функциональность этих классов в большой степени может быть реализована другими способами в Windows PowerShell, некоторые действия (например создание ярлыков) проще выполнить с помощью классов сервера сценариев Windows.</span><span class="sxs-lookup"><span data-stu-id="bff82-153">Although most of the functionality of these classes is made available in other ways in Windows PowerShell, a few tasks such as shortcut creation are still easier to do using the WSH classes.</span></span>

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a><span data-ttu-id="bff82-154">Создание ярлыков на рабочем столе с помощью WScript.Shell</span><span class="sxs-lookup"><span data-stu-id="bff82-154">Creating a Desktop Shortcut with WScript.Shell</span></span>
<span data-ttu-id="bff82-155">Одной из функций, быстро выполняемых с помощью СОМ-объектов, является создание ярлыков.</span><span class="sxs-lookup"><span data-stu-id="bff82-155">One task that can be performed quickly with a COM object is creating a shortcut.</span></span> <span data-ttu-id="bff82-156">Допустим, на рабочем столе требуется создать ярлык для корневой папки Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bff82-156">Suppose you want to create a shortcut on your desktop that links to the home folder for Windows PowerShell.</span></span> <span data-ttu-id="bff82-157">Сначала необходимо создать ссылку на объект **WScript.Shell**, которая сохраняется в переменной **$WshShell**:</span><span class="sxs-lookup"><span data-stu-id="bff82-157">You first need to create a reference to **WScript.Shell**, which we will store in a variable named **$WshShell**:</span></span>

```
$WshShell = New-Object -ComObject WScript.Shell
```

<span data-ttu-id="bff82-158">Командлет Get-Member работает и с СОМ-объектами, поэтому элементы объекта можно изучить, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="bff82-158">Get-Member works with COM objects, so you can explore the members of the object by typing:</span></span>

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

<span data-ttu-id="bff82-159">У командлета **Get-Member** есть необязательный параметр **InputObject**, который можно использовать вместо передачи по конвейеру, чтобы предоставить входные данные для **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="bff82-159">**Get-Member** has an optional **InputObject** parameter you can use instead of piping to provide input to **Get-Member**.</span></span> <span data-ttu-id="bff82-160">При использовании команды **Get-Member -InputObject $WshShell** в примере выше выходные данные были бы такими же.</span><span class="sxs-lookup"><span data-stu-id="bff82-160">You would get the same output as shown above if you instead used the command **Get-Member -InputObject $WshShell**.</span></span> <span data-ttu-id="bff82-161">При указании параметра **InputObject** командлет обрабатывает свои аргументы как одно целое.</span><span class="sxs-lookup"><span data-stu-id="bff82-161">If you use **InputObject**, it treats its argument as a single item.</span></span> <span data-ttu-id="bff82-162">Это означает, что если в переменной содержится несколько объектов, командлет **Get-Member** обрабатывает их как массив объектов.</span><span class="sxs-lookup"><span data-stu-id="bff82-162">This means that if you have several objects in a variable, **Get-Member** treats them as an array of objects.</span></span> <span data-ttu-id="bff82-163">Например:</span><span class="sxs-lookup"><span data-stu-id="bff82-163">For example:</span></span>


```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

<span data-ttu-id="bff82-164">Метод **WScript.Shell CreateShortcut** допускает использование одного аргумента — пути к создаваемому файлу ярлыка.</span><span class="sxs-lookup"><span data-stu-id="bff82-164">The **WScript.Shell CreateShortcut** method accepts a single argument, the path to the shortcut file to create.</span></span> <span data-ttu-id="bff82-165">Можно указать полный путь к рабочему столу, но существует и более простой способ.</span><span class="sxs-lookup"><span data-stu-id="bff82-165">We could type in the full path to the desktop, but there is an easier way.</span></span> <span data-ttu-id="bff82-166">Рабочий стол обычно представлен папкой с именем Desktop внутри домашней папки текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="bff82-166">The desktop is normally represented by a folder named Desktop inside the home folder of the current user.</span></span> <span data-ttu-id="bff82-167">В Windows PowerShell имеется переменная **$Home**, в которой содержится путь к этой домашней папке.</span><span class="sxs-lookup"><span data-stu-id="bff82-167">Windows PowerShell has a variable **$Home** that contains the path to this folder.</span></span> <span data-ttu-id="bff82-168">Таким образом, путь к домашней папке может быть задан указанием этой переменной, после чего нужно ввести только имя папки Desktop и имя создаваемого ярлыка:</span><span class="sxs-lookup"><span data-stu-id="bff82-168">We can specify the path to the home folder by using this variable, and then add the name of the Desktop folder and the name for the shortcut to create by typing:</span></span>

```
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

<span data-ttu-id="bff82-169">Если похожая на переменную строка заключена в двойные кавычки, Windows PowerShell пытается заменить ее подходящим значением.</span><span class="sxs-lookup"><span data-stu-id="bff82-169">When you use something that looks like a variable name inside double-quotes, Windows PowerShell tries to substitute a matching value.</span></span> <span data-ttu-id="bff82-170">При использовании одиночных кавычек значение переменной не подставляется.</span><span class="sxs-lookup"><span data-stu-id="bff82-170">If you use single-quotes, Windows PowerShell does not try to substitute the variable value.</span></span> <span data-ttu-id="bff82-171">Например, попробуйте ввести следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bff82-171">For example, try typing the following commands:</span></span>

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

<span data-ttu-id="bff82-172">В переменной **$lnk** теперь хранится новая ссылка на ярлык.</span><span class="sxs-lookup"><span data-stu-id="bff82-172">We now have a variable named **$lnk** that contains a new shortcut reference.</span></span> <span data-ttu-id="bff82-173">Чтобы просмотреть элементы переменной, ее можно передать по конвейеру в **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="bff82-173">If you want to see its members, you can pipe it to **Get-Member**.</span></span> <span data-ttu-id="bff82-174">Выходные данные (см. ниже) показывают все элементы, необходимые, чтобы завершить создание ярлыка:</span><span class="sxs-lookup"><span data-stu-id="bff82-174">The output below shows the members we need to use to finish creating our shortcut:</span></span>

```
PS> $lnk | Get-Member
TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b}
Name             MemberType   Definition
----             ----------   ----------
...
Save             Method       void Save ()
...
TargetPath       Property     string TargetPath () {get} {set}
```

<span data-ttu-id="bff82-175">Осталось определить свойство **TargetPath**, указывающее путь к папке Windows PowerShell, и вызвать метод **Save**, чтобы сохранить **$lnk** ярлыка.</span><span class="sxs-lookup"><span data-stu-id="bff82-175">We need to specify the **TargetPath**, which is the application folder for Windows PowerShell, and then save the shortcut **$lnk** by calling the **Save** method.</span></span> <span data-ttu-id="bff82-176">Путь к папке Windows PowerShell хранится в переменной **$PSHome**, поэтому это можно сделать, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="bff82-176">The Windows PowerShell application folder path is stored in the variable **$PSHome**, so we can do this by typing:</span></span>

```
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a><span data-ttu-id="bff82-177">Использование Internet Explorer из Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bff82-177">Using Internet Explorer from Windows PowerShell</span></span>
<span data-ttu-id="bff82-178">С помощью СОМ-объектов можно автоматизировать многие приложения (включая семейство приложений Microsoft Office и Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="bff82-178">Many applications (including the Microsoft Office family of applications and Internet Explorer) can be automated by using COM.</span></span> <span data-ttu-id="bff82-179">На примере Internet Explorer можно рассмотреть некоторые типичные приемы и тонкости, связанные с работой приложений, основанных на СОМ-технологии.</span><span class="sxs-lookup"><span data-stu-id="bff82-179">Internet Explorer illustrates some of the typical techniques and issues involved in working with COM-based applications.</span></span>

<span data-ttu-id="bff82-180">Экземпляр Internet Explorer создается указанием программного идентификатора этого приложения **InternetExplorer.Application**:</span><span class="sxs-lookup"><span data-stu-id="bff82-180">You create an Internet Explorer instance by specifying the Internet Explorer ProgId, **InternetExplorer.Application**:</span></span>

```
$ie = New-Object -ComObject InternetExplorer.Application
```

<span data-ttu-id="bff82-181">Эта команда запускает Internet Explorer, но не отображает его.</span><span class="sxs-lookup"><span data-stu-id="bff82-181">This command starts Internet Explorer, but does not make it visible.</span></span> <span data-ttu-id="bff82-182">Если запустить командлет Get-Process, то можно увидеть выполняющийся процесс iexplore.</span><span class="sxs-lookup"><span data-stu-id="bff82-182">If you type Get-Process, you can see that a process named iexplore is running.</span></span> <span data-ttu-id="bff82-183">Причем после выхода из Windows PowerShell выполнение этого процесса будет продолжаться.</span><span class="sxs-lookup"><span data-stu-id="bff82-183">In fact, if you exit Windows PowerShell, the process will continue to run.</span></span> <span data-ttu-id="bff82-184">Чтобы завершить процесс iexplore, необходимо перезагрузить компьютер или воспользоваться средством наподобие диспетчера задач.</span><span class="sxs-lookup"><span data-stu-id="bff82-184">You must reboot the computer or use a tool like Task Manager to end the iexplore process.</span></span>

> [!NOTE]
> <span data-ttu-id="bff82-185">СОМ-объекты, запускаемые в виде отдельных процессов, обычно называются *исполняемыми файлами ActiveX*. При их запуске окно пользовательского интерфейса отображается не всегда.</span><span class="sxs-lookup"><span data-stu-id="bff82-185">COM objects that start as separate processes, commonly called *ActiveX executables*, may or may not display a user interface window when they start up.</span></span> <span data-ttu-id="bff82-186">Если окно создается, но не отображается, как в случае с приложением Internet Explorer, фокус обычно перемещается на рабочий стол Windows, и для взаимодействия с окном его необходимо сделать видимым.</span><span class="sxs-lookup"><span data-stu-id="bff82-186">If they create a window but do not make it visible, like Internet Explorer, the focus will generally move to the Windows desktop and you must make the window visible to interact with it.</span></span>

<span data-ttu-id="bff82-187">Введя **$ie | Get-Member**, можно получить список свойств и методов для Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="bff82-187">By typing **$ie | Get-Member**, you can view properties and methods for Internet Explorer.</span></span> <span data-ttu-id="bff82-188">Чтобы отобразить окно Internet Explorer, свойству Visible нужно присвоить значение $true, введя следующее:</span><span class="sxs-lookup"><span data-stu-id="bff82-188">To see the Internet Explorer window, set the Visible property to $true by typing:</span></span>

```
$ie.Visible = $true
```

<span data-ttu-id="bff82-189">После этого можно перейти по какому-либо веб-адресу, используя метод Navigate:</span><span class="sxs-lookup"><span data-stu-id="bff82-189">You can then navigate to a specific Web address by using the Navigate method:</span></span>

```
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

<span data-ttu-id="bff82-190">Другие элементы объектной модели Internet Explorer позволяют получить текстовое содержание веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="bff82-190">Using other members of the Internet Explorer object model, it is possible to retrieve text content from the Web page.</span></span> <span data-ttu-id="bff82-191">Следующая команда отображает HTML-текст в теле текущей веб-страницы:</span><span class="sxs-lookup"><span data-stu-id="bff82-191">The following command will display the HTML text in the body of the current Web page:</span></span>

```
$ie.Document.Body.InnerText
```

<span data-ttu-id="bff82-192">Чтобы закрыть Internet Explorer из PowerShell, необходимо вызвать метод Quit():</span><span class="sxs-lookup"><span data-stu-id="bff82-192">To close Internet Explorer from within PowerShell, call its Quit() method:</span></span>

```
$ie.Quit()
```

<span data-ttu-id="bff82-193">Это приведет к принудительному закрытию приложения.</span><span class="sxs-lookup"><span data-stu-id="bff82-193">This will force it to close.</span></span> <span data-ttu-id="bff82-194">Переменная $ie больше не содержит действительную ссылку, хотя все еще отображается как СОМ-объект.</span><span class="sxs-lookup"><span data-stu-id="bff82-194">The $ie variable no longer contains a valid reference even though it still appears to be a COM object.</span></span> <span data-ttu-id="bff82-195">Попытка использования этой переменной приводит к ошибке автоматизации:</span><span class="sxs-lookup"><span data-stu-id="bff82-195">If you attempt to use it, you will get an automation error:</span></span>

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

<span data-ttu-id="bff82-196">В этой ситуации можно либо удалить оставшуюся ссылку с помощью команды $ie = $null, либо полностью удалить переменную:</span><span class="sxs-lookup"><span data-stu-id="bff82-196">You can either remove the remaining reference with a command like $ie = $null, or completely remove the variable by typing:</span></span>

```
Remove-Variable ie
```

> [!NOTE]
> <span data-ttu-id="bff82-197">Для исполняемых файлов ActiveX нет общего стандарта, по которому выполнение их процессов завершается или продолжается после удаления ссылки на них.</span><span class="sxs-lookup"><span data-stu-id="bff82-197">There is no common standard for whether ActiveX executables exit or continue to run when you remove a reference to one.</span></span> <span data-ttu-id="bff82-198">Выход из приложения зависит от обстоятельств (видимо ли приложение, открыт ли в нем какой-либо отредактированный документ, а также продолжается ли выполнение Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="bff82-198">Depending on circumstances such as whether the application is visible, whether an edited document is running in it, and even whether Windows PowerShell is still running, the application may or may not exit.</span></span> <span data-ttu-id="bff82-199">Поэтому требуется проверка поведения при завершении работы каждого исполняемого файла ActiveX, используемого в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bff82-199">For this reason, you should test termination behavior for each ActiveX executable you want to use in Windows PowerShell.</span></span>

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a><span data-ttu-id="bff82-200">Получение предупреждений о вызываемых COM-объектах .NET Framework</span><span class="sxs-lookup"><span data-stu-id="bff82-200">Getting Warnings About .NET Framework-Wrapped COM Objects</span></span>
<span data-ttu-id="bff82-201">В некоторых случаях у СОМ-объекта есть соответствующая *вызываемая оболочка времени выполнения* (RCW) .NET Framework, и именно она используется командлетом **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="bff82-201">In some cases, a COM object might have an associated .NET Framework *Runtime-Callable Wrapper* or RCW, and this will be used by **New-Object**.</span></span> <span data-ttu-id="bff82-202">Поведение оболочки RCW может отличаться от поведения обычного СОМ-объекта, поэтому у командлета **New-Object** есть параметр **Strict**, используемый для предупреждения о доступе к RCW.</span><span class="sxs-lookup"><span data-stu-id="bff82-202">Since the behavior of the RCW may be different from the behavior of the normal COM object, **New-Object** has a **Strict** parameter to warn you about RCW access.</span></span> <span data-ttu-id="bff82-203">Если указать параметр **Strict** и создать СОМ-объект, использующий оболочку RCW, выводится предупреждение:</span><span class="sxs-lookup"><span data-stu-id="bff82-203">If you specify the **Strict** parameter and then create a COM object that uses an RCW, you get a warning message:</span></span>

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

<span data-ttu-id="bff82-204">Объект создается, но предупреждение указывает на то, что он не является стандартным СОМ-объектом.</span><span class="sxs-lookup"><span data-stu-id="bff82-204">Although the object is still created, you are warned that it is not a standard COM object.</span></span>

