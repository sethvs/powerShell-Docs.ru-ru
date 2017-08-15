---
ms.date: 2017-06-05T00:00:00.000Z
keywords: "powershell,командлет"
title: "Установка пакета SDK для Windows PowerShell"
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: c6acba828e469e716c80603ec2432176652a7280
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="installing-the-windows-powershell-sdk"></a>Установка пакета SDK для Windows PowerShell

В следующей статье описывается, как установить пакет PowerShell SDK на разные версии Windows.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>Установка пакета SDK для Windows PowerShell 3.0 в Windows 8 и Windows Server 2012

Windows PowerShell 3.0 устанавливается автоматически вместе с Windows 8 и Windows Server 2012.
Вы также можете скачать и установить ссылочные сборки для Windows PowerShell 3.0 в составе Windows 8 SDK.
Эти сборки позволяют написать командлеты, поставщики и ведущие программы для Windows PowerShell 3.0.
При установке Windows SDK для Windows 8 сборки Windows PowerShell автоматически устанавливаются в папку ссылочной сборки, в "\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0".
Дополнительные сведения см. в статье [Веб-сайт скачивания пакета SDK для Windows 8](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).
Примеры кода Windows PowerShell также доступны в Центре разработки.
Дополнительные сведения см. на странице примеров кода классических приложений на [сайте центра разработки](http://code.msdn.microsoft.com/windowsdesktop/).

Кроме того, Windows PowerShell 3.0 обратно совместим с Windows PowerShell 2.0 SDK, в который входит ряд примеров кода.
Дополнительные сведения о том, как скачать Windows PowerShell 2.0 SDK, см. ниже.
(Обратите внимание, что, хотя примеры кода 2.0 совместимы с Windows 8 и Windows PowerShell 3.0, невозможно установить Windows PowerShell 2.0 на платформу Windows 8.)

##<a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>Установка пакета SDK для Windows PowerShell 3.0 в Windows 7 и Windows Server 2008 R2

Вместе с Windows 7 и Windows Server 2008 R2 автоматически устанавливается PowerShell 2.0.
Вы также можете установить PowerShell 3.0 в этих системах.
(Дополнительные сведения см. в статье [Установка Windows PowerShell](Installing-Windows-PowerShell.md).)
Как описано выше, вы также можете установить Windows 8 SDK на Windows 7 и Windows Server 2008 R2.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>Установка пакета SDK для Windows PowerShell 2.0 в Windows 7, Windows Vista, Windows XP, Windows Server 2003 и Windows Server 2008

Установка пакета SDK для Windows PowerShell 2.0 предоставляет эталонные сборки, необходимые для написания командлетов, поставщиков и ведущих приложений, а также пример кода C#, который можно использовать в качестве начальной точки при написании кода.

Инструкции по установке этого пакета SDK см. в статье [Пакет SDK для Windows PowerShell 2.0](http://go.microsoft.com/fwlink/?LinkId=184611).

## <a name="reference-assemblies"></a>Эталонные сборки

Эталонные сборки по умолчанию устанавливаются в следующий каталог: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.

> **Примечание**. Код, который компилируется с использованием сборок Windows PowerShell 2.0, нельзя загрузить в установках Windows PowerShell 1.0.
>Но код, который компилируется в сборках Windows PowerShell 1.0, можно загрузить в установках Windows PowerShell 2.0.

## <a name="samples"></a>примеры

Примеры кода по умолчанию устанавливаются в следующий каталог: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.

В следующих разделах приводится краткое описание каждого примера.

## <a name="cmdlet-samples"></a>Примеры командлетов
**GetProcessSample01**

Показывает, как написать простой командлет, который будет получать все процессы на локальном компьютере.

**GetProcessSample02**

Показывает, как добавить в командлет параметры.
Командлет принимает одно или несколько имен процессов и возвращает соответствующие процессы.

**GetProcessSample03**

Показывает, как добавить параметры, которые будут принимать входные данные из конвейера.

**GetProcessSample04**

Показывает, как обрабатывать устранимые ошибки.

**GetProcessSample05**

Показывает, как вывести на экран список указанных процессов.

**SelectObject**

Показывает, как написать фильтр, позволяющий отобрать только определенные объекты.

**SelectString**

Показывает, как искать в файлах заданные последовательности.

**StopProcessSample01**

Показывает, как реализовать параметр *PassThru* и запрашивать мнение пользователя, вызывая методы [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) и [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx).
Если пользователь хочет заставить командлет вернуть объект, он указывает параметр *PassThru*.

**StopProcessSample02**

Показывает, как остановить определенный процесс.

**StopProcessSample03**

Показывает, как объявлять псевдонимы для параметров и включать поддержку подстановочных знаков.

**StopProcessSample04**

Показывает, как объявлять набор параметров (объект, принимаемый командлетом как входные данные) и указывать, какой набор параметров должен использоваться по умолчанию.

## <a name="remoting-samples"></a>Примеры удаленного взаимодействия

**RemoteRunspace01**

Показывает, как создавать удаленное пространство выполнения, используемое для установления удаленного подключения.

**RemoteRunspacePool01**

Показывает, как формировать пул удаленных пространств выполнения и с его помощью выполнять сразу несколько команд одновременно.

**Serialization01**

Показывает, как проанализировать существующий класс .NET и сделать так, чтобы информация из определенных открытых свойств этого класса сохранялась в процессе сериализации и десериализации.

**Serialization02**

Показывает, как проанализировать существующий класс .NET и сделать так, чтобы информация из экземпляра этого класса сохранялась в процессе сериализации и десериализации на случай, если информация будет недоступна в открытых свойствах класса.

**Serialization03**

Показывает, как проанализировать существующий класс .NET и сделать так, чтобы экземпляры этого класса и классов, производных от него, десериализовывались (восстанавливались) в рабочие объекты .NET.

## <a name="event-samples"></a>Примеры событий

**Event01**

Показывает, как создать командлет для регистрации событий, наследуя от ObjectEventRegistrationBase.

**Event02**

Показывает, как получать уведомления о событиях Windows PowerShell, возникающих на удаленных компьютерах.
Использует событие PSEventReceived, предоставляемое классом [Runspace](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx).

## <a name="hosting-application-samples"></a>Примеры размещения приложений

**Runspace01**

Показывает, как использовать класс [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) для синхронного выполнения командлета [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324).
Командлет [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) возвращает объекты [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) для каждого процесса, запущенного на локальном компьютере.

**Runspace02**

Показывает, как использовать класс [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) для синхронного выполнения командлетов [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) и [Sort-Object](http://go.microsoft.com/fwlink/?LinkID=113403).
Командлет [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) возвращает объекты [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) для каждого процесса, запущенного на локальном компьютере, а командлет Sort-Object сортирует объекты на основании свойства [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx).
Результаты выполнения этих команд можно отобразить с помощью элемента управления [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx).

**Runspace03**

Показывает, как использовать класс [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) для синхронного выполнения скрипта и как обрабатывать устранимые ошибки.
Скрипт получает список имен процессов, а затем извлекает эти процессы.
Результаты выполнения скрипта, включая вызванные им устранимые ошибки, отображаются в окне консоли.

**Runspace04**

Показывает, как использовать класс [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) для выполнения команд и фиксации неустранимых ошибок, возникающих при их выполнении.
Выполняются две команды, и последняя получает недопустимый аргумент параметра.
В результате объекты не возвращаются и создается неустранимая ошибка.

**Runspace05**

Показывает, как добавить оснастку в объект [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), чтобы командлет оснастки был доступен при открытии пространства выполнения.
Оснастка предоставляет командлет Get-Proc (см. [GetProcessSample01](https://technet.microsoft.com/library/ff602028.aspx)), который запускается синхронно с помощью объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx).

**Runspace06**

Показывает, как добавить модуль в объект [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), чтобы модуль загружался при открытии пространства выполнения.
Модуль предоставляет командлет Get-Proc (см. [GetProcessSample02](https://technet.microsoft.com/library/ff602027.aspx)), который запускается синхронно с помощью объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx).

**Runspace07**

Показывает, как создать пространство выполнения и использовать его для синхронного запуска двух командлетов с помощью объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx).

**Runspace08**

Показывает, как добавить команды и аргументы в конвейер объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) и запустить команды синхронно.

**Runspace09**

Показывает, как добавить скрипт в конвейер объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) и запустить скрипт асинхронно.
События используются для обработки выходных данных скрипта.

**Runspace10**

Показывает, как создать начальное состояние сеанса по умолчанию, добавить командлет в [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), создать пространство выполнения с использованием начального состояния сеанса и выполнить команду с помощью объекта [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx).

**Runspace11**

Показывает, как использовать класс [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) для создания прокси-команды, которая вызывает существующий командлет, но ограничивает набор доступных параметров.
Прокси-команда затем добавляется в начальное состояние сеанса, который используется для создания ограниченного пространства выполнения.
Это означает, что пользователь может получить доступ к функциям командлета только с помощью прокси-команды.

**PowerShell01**

Показывает, как создать ограниченное пространство выполнения с помощью объекта [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx).

**PowerShell02**

Показывает, как использовать пул пространств выполнения для одновременного выполнения нескольких команд.

## <a name="host-samples"></a>Примеры узлов

**Host01**

Показывает, как реализовать ведущее приложение, которое использует пользовательский узел.
В этом примере создается пространство выполнения, которое использует пользовательский узел, а затем с помощью API [T:System.Management.Automation.PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) запускается скрипт, вызывающий команду "exit".
Затем ведущее приложение анализирует выходные данные скрипта и выводит на экран результаты.

**Host02**

Показывает, как написать ведущее приложение, использующее среду выполнения Windows PowerShell наряду с реализацией пользовательского узла.
Ведущее приложение задает в качестве региональных параметров немецкий язык, запускает командлет [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) и отображает результаты в том виде, в котором они отобразились бы при использовании pwrsh.exe, а затем выводит на экран текущие дату и время на немецком языке.

**Host03**

Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое считывает команды из командной строки, выполняет их, а затем отображает результаты в консоли.

**Host04**

Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое считывает команды из командной строки, выполняет их, а затем отображает результаты в консоли.
Это приложение также поддерживает отображение запросов, позволяющих пользователю выбрать несколько вариантов.

**Host05**

Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое считывает команды из командной строки, выполняет их, а затем отображает результаты в консоли.
Это ведущее приложение также поддерживает вызовы удаленных компьютеров с помощью командлетов [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) и [Exit-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212).

**Host06**

Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое считывает команды из командной строки, выполняет их, а затем отображает результаты в консоли.
Кроме того, в этом примере используются интерфейсы API создателя токенов для указания цвета текста, вводимого пользователем.

## <a name="provider-samples"></a>Примеры поставщиков

**AccessDBProviderSample01**

Показывает, как объявить класс поставщика, производный от класса [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx).
Он приводится здесь только для полноты картины.

**AccessDBProviderSample02**

Показывает, как перезаписать методы [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) и [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) таким образом, чтобы они поддерживали вызовы командлетов New-PSDrive и Remove-PSDrive.
Класс поставщика в этом примере является производным от класса [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx).

**AccessDBProviderSample03**

Показывает, как перезаписать методы [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) и [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) таким образом, чтобы они поддерживали вызовы командлетов Get-Item и Set-Item.
Класс поставщика в этом примере является производным от класса [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx).

**AccessDBProviderSample04**

Показывает, как перезаписать методы контейнера таким образом, чтобы они поддерживали вызовы командлетов Copy-Item, Get-ChildItem, New-Item и Remove-Item.
Эти методы должны быть реализованы, когда хранилище данных содержит элементы, являющиеся контейнерами.
Контейнер — это группа дочерних элементов в составе общего родительского элемента.
Класс поставщика в этом примере является производным от класса [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx).

**AccessDBProviderSample05**

Показывает, как перезаписать методы контейнера таким образом, чтобы они поддерживали вызовы командлетов Move-Item и Join-Path.
Эти методы должны быть реализованы, когда пользователю требуется переместить элементы в контейнере, если хранилище данных содержит вложенные контейнеры.
Класс поставщика в этом примере является производным от класса [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx).

**AccessDBProviderSample06**

Показывает, как перезаписать методы содержимого таким образом, чтобы они поддерживали вызовы командлетов Clear-Content, Get-Content и Set-Content.
Эти методы должны быть реализованы, когда пользователю требуется управлять содержимым элементов в хранилище данных.
Класс поставщика в этом примере является производным от класса [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) и реализует интерфейс [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx).

