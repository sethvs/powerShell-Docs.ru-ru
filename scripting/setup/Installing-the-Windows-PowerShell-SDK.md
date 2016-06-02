---
title:  Установка пакета SDK для Windows PowerShell
ms.date:  2016-05-11
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
ms.assetid:  c3636b45-61aa-4720-85f0-58312c4fc8f9
---

# Установка пакета SDK для Windows PowerShell
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://dduestorage.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>В следующей статье описывается, как установить пакет PowerShell SDK на разные версии Windows.</para>
  </introduction>
  <section>
    <title>Установка Windows PowerShell 3.0 SDK для Windows 8 и Windows Server 2012</title>
    <content>
      <para>Windows PowerShell 3.0 устанавливается автоматически с Windows 8 и Windows Server 2012. Вы также можете скачать и установить ссылочные сборки для Windows PowerShell 3.0 в составе Windows 8 SDK. Эти сборки позволяют написать командлеты, поставщики и ведущие программы для Windows PowerShell 3.0. При установке Windows SDK для Windows 8 сборки Windows PowerShell автоматически устанавливаются в папку ссылочной сборки, в "\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0". Дополнительные сведения см. <externalLink><linkText>на сайте скачивания Windows 8 SDK</linkText><linkUri>http://msdn.microsoft.com/windows/hardware/hh852363.aspx</linkUri></externalLink>. Примеры кода Windows PowerShell также доступны в Центре разработки. Дополнительные сведения см. на странице примеров кода классических приложений на <externalLink><linkText>сайте Центра разработки</linkText><linkUri>http://code.msdn.microsoft.com/windowsdesktop/</linkUri></externalLink>. </para>
      <para>Кроме того, Windows PowerShell 3.0 обратно совместим с Windows PowerShell 2.0 SDK, в который входит ряд примеров кода. Дополнительные сведения о том, как скачать Windows PowerShell 2.0 SDK, см. ниже. (Обратите внимание, что, хотя примеры кода 2.0 совместимы с Windows 8 и Windows PowerShell 3.0, невозможно установить Windows PowerShell 2.0 на платформу Windows 8.) </para>
    </content>
  </section>
  <section>
    <title>Установка Windows PowerShell 3.0 SDK в Windows 7 и Windows Server 2008 R2</title>
    <content>
      <para>Windows 7 и Windows Server 2008 R2 автоматически включают PowerShell 2.0 в установку. Вы также можете установить PowerShell 3.0 в этих системах. (Дополнительные сведения см. в статье <link xlink:href="6fbb0409-5a54-48ec-95e6-7f8b7d8c4969">Установка Windows PowerShell</link>.) Как описано выше, вы также можете установить Windows 8 SDK на Windows 7 и Windows Server 2008 R2.</para>
    </content>
  </section>
  <section>
    <title>Установка Windows PowerShell 2.0 SDK в Windows 7, Windows Vista, Windows XP, Windows Server 2003 и Windows Server 2008</title>
    <content>
      <para>Пакет <token>mshshort</token> 2.0 SDK предоставляет ссылочные сборки, необходимые для написания командлетов, поставщиков и ведущих приложений, а также пример кода C#, который можно использовать в качестве начальной точки при написании кода. </para>
      <para>Сведения об установке этого пакета SDK см. в статье <externalLink><linkText>Windows PowerShell 2.0 SDK</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=184611</linkUri></externalLink>.</para>
    </content>
    <sections>
      <section>
        <title>Ссылочные сборки</title>
        <content>
          <para>Ссылочные сборки устанавливаются в следующем расположении по умолчанию: <codeInline>c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0</codeInline>.</para>
          <alert class="note">
            <para>Код, который компилируется в сборках Windows PowerShell 2.0, невозможно загрузить в установках Windows PowerShell 1.0. Однако код, который компилируется в сборках Windows PowerShell 1.0, можно загрузить в установках Windows PowerShell 2.0.</para>
          </alert>
        </content>
      </section>
      <section>
        <title>Примеры</title>
        <content>
          <para>Примеры кода устанавливаются в следующем расположении по умолчанию: <codeInline>C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\</codeInline>.</para>
          <para>В следующих разделах предоставляется краткое описание функций каждого примера.</para>
        </content>
        <sections>
          <section>
            <title>Примеры командлетов</title>
            <content>
              <definitionTable>
                <definedTerm>GetProcessSample01</definedTerm>
                <definition>
                  <para>Показывает, как написать простой командлет, который получает все процессы на локальном компьютере.</para>
                </definition>
                <definedTerm>GetProcessSample02</definedTerm>
                <definition>
                  <para>Показывает, как добавить параметры в командлет. Командлет принимает одно имя процесса или несколько и возвращает совпадающие процессы.</para>
                </definition>
                <definedTerm>GetProcessSample03</definedTerm>
                <definition>
                  <para>Показывает, как добавить параметры, принимающие входящие данные конвейера.</para>
                </definition>
                <definedTerm>GetProcessSample04</definedTerm>
                <definition>
                  <para>Показывает, как обработать устранимые ошибки.</para>
                </definition>
                <definedTerm>GetProcessSample05</definedTerm>
                <definition>
                  <para>Показывает, как отобразить список указанных процессов.</para>
                </definition>
                <definedTerm>SelectObject</definedTerm>
                <definition>
                  <para>Показывает, как написать фильтр для выбора только определенных объектов. </para>
                </definition>
                <definedTerm>SelectString</definedTerm>
                <definition>
                  <para>Показывает, как искать в файлах указанные шаблоны.</para>
                </definition>
                <definedTerm>StopProcessSample01</definedTerm>
                <definition>
                  <para>Показывает, как реализовать параметр <parameterReference>PassThru</parameterReference> и запросить отзывы пользователей вызовами в методы <codeEntityReference>Overload:System.Management.Automation.Cmdlet.ShouldProcess</codeEntityReference> и <codeEntityReference>Overload:System.Management.Automation.Cmdlet.ShouldContinue</codeEntityReference>. Пользователи указывают параметр <parameterReference>PassThru</parameterReference>, когда хотят принудительно вернуть объект. </para>
                </definition>
                <definedTerm>StopProcessSample02</definedTerm>
                <definition>
                  <para>Показывает, как остановить определенный процесс.</para>
                </definition>
                <definedTerm>StopProcessSample03</definedTerm>
                <definition>
                  <para>Показывает, как объявить псевдонимы для параметров и как обеспечить поддержку для подстановочных знаков.</para>
                </definition>
                <definedTerm>StopProcessSample04</definedTerm>
                <definition>
                  <para>Показывает, как объявить наборы параметров, объект, который командлет принимает как входные данные, и как указать набор параметров для использования по умолчанию.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
          <section>
            <title>Примеры удаленного взаимодействия</title>
            <content>
              <definitionTable>
                <definedTerm>RemoteRunspace01</definedTerm>
                <definition>
                  <para>Показывает, как создать удаленное пространство выполнения, которое используется для установки удаленного подключения.</para>
                </definition>
                <definedTerm>RemoteRunspacePool01</definedTerm>
                <definition>
                  <para>Показывает, как создать пул удаленных пространств выполнения и запустить несколько команд одновременно с помощью этого пула.</para>
                </definition>
                <definedTerm>Serialization01</definedTerm>
                <definition>
                  <para>Показывает, как проанализировать существующий класс .NET и гарантировать, что данные из выбранных общедоступных свойств этого класса сохранятся при сериализации и десериализации.</para>
                </definition>
                <definedTerm>Serialization02</definedTerm>
                <definition>
                  <para>Показывает, как проанализировать существующий класс .NET и гарантировать, что данные из экземпляра этого класса сохранятся при сериализации и десериализации, когда они отсутствуют в общедоступных свойствах этого класса.</para>
                </definition>
                <definedTerm>Serialization03</definedTerm>
                <definition>
                  <para>Показывает, как проанализировать существующий класс .NET и гарантировать, что экземпляры этого и производных классов десериализуются (восстанавливаются) в рабочие объекты .NET.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
          <section>
            <title>Примеры событий</title>
            <content>
              <definitionTable>
                <definedTerm>Event01</definedTerm>
                <definition>
                  <para>Показывает, как создать командлет для регистрации событий, производных от ObjectEventRegistrationBase.</para>
                </definition>
                <definedTerm>Event02</definedTerm>
                <definition>
                  <para>Показывает, как получить уведомления о событиях <token>mshshort</token>, которые создаются на удаленных компьютерах. Использует событие PSEventReceived, предоставленное в классе <codeEntityReference>T:System.Management.Automation.Runspaces.Runspace</codeEntityReference>.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
          <section>
            <title>Примеры ведущих приложений</title>
            <content>
              <definitionTable>
                <definedTerm>Runspace01</definedTerm>
                <definition>
                  <para>Показывает, как использовать класс <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> для синхронного запуска командлета <externalLink><linkText>Get-Process</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=113324</linkUri></externalLink>. Командлет <externalLink><linkText>Get-Process</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=113324</linkUri></externalLink> возвращает объекты <codeEntityReference>T:System.Diagnostics.Process</codeEntityReference> для каждого процесса, запущенного на локальном компьютере.</para>
                </definition>
                <definedTerm>Runspace02</definedTerm>
                <definition>
                  <para>Показывает, как использовать класс <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> для синхронного запуска командлетов <externalLink><linkText>Get-Process</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=113324</linkUri></externalLink> и <externalLink><linkText>Sort-Object</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkID=113403</linkUri></externalLink>. Командлет <externalLink><linkText>Get-Process</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=113324</linkUri></externalLink> возвращает объекты <codeEntityReference>T:System.Diagnostics.Process</codeEntityReference> для каждого процесса, выполняющегося на локальном компьютере, а Sort-Object сортирует объекты на основе свойства <codeEntityReference>P:System.Diagnostics.Process.Id</codeEntityReference>. Результаты этих команд отображаются с помощью элемента управления <codeEntityReference>T:System.Windows.Forms.DataGridView</codeEntityReference>.</para>
                </definition>
                <definedTerm>Runspace03</definedTerm>
                <definition>
                  <para>Показывает, как использовать класс <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> для синхронного запуска скрипта и как обработать устранимые ошибки. Скрипт получает список имен процессов, а затем извлекает эти процессы. Результаты работы скрипта, включая устранимые ошибки, созданные при запуске скрипта, отображаются в окне консоли.</para>
                </definition>
                <definedTerm>Runspace04</definedTerm>
                <definition>
                  <para>Показывает, как использовать класс <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> для запуска команд и как собирать неустранимые ошибки, возникающие при их запуске. Выполняются две команды, и последняя получает недопустимый аргумент параметра. В результате объекты не возвращаются и возникает неустранимая ошибка.</para>
                </definition>
                <definedTerm>Runspace05</definedTerm>
                <definition>
                  <para>Показывает, как добавить оснастку в объект <codeEntityReference>T:System.Management.Automation.Runspaces.InitialSessionState</codeEntityReference>, чтобы командлет оснастки был доступен при открытии пространства выполнения. Оснастка предоставляет командлет Get-Proc (определенный <legacyLink xlink:href="7b48bf80-cbf0-4cb1-8d5b-3b8d06196598">примером GetProcessSample01</legacyLink>), который выполняется синхронно, используя объект <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference>.</para>
                </definition>
                <definedTerm>Runspace06</definedTerm>
                <definition>
                  <para>Показывает, как добавить модуль в объект <codeEntityReference>T:System.Management.Automation.Runspaces.InitialSessionState</codeEntityReference>, чтобы он загрузился при открытии пространства выполнения. Модуль предоставляет командлет Get-Proc (определенный <legacyLink xlink:href="481f557d-3344-4d33-b2da-4736a0165181">примером GetProcessSample02</legacyLink>), который выполняется синхронно, используя объект <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference>.</para>
                </definition>
                <definedTerm>Runspace07</definedTerm>
                <definition>
                  <para>Показывает, как создать область выполнения, а затем использовать ее для синхронного выполнения двух командлетов с использованием объекта <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference>.</para>
                </definition>
                <definedTerm>Runspace08</definedTerm>
                <definition>
                  <para>Показывает, как добавлять команды и аргументы в конвейер объекта <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> и как синхронно выполнять команды.</para>
                </definition>
                <definedTerm>Runspace09</definedTerm>
                <definition>
                  <para>Показывает, как добавить скрипт в конвейер объекта <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> и как асинхронно выполнить скрипт. События используются для обработки выходных данных скрипта.</para>
                </definition>
                <definedTerm>Runspace10</definedTerm>
                <definition>
                  <para>Показывает, как создать начальное состояние сеанса по умолчанию, добавить командлет в <codeEntityReference>T:System.Management.Automation.Runspaces.InitialSessionState</codeEntityReference>, создать пространство выполнения, которое использует начальное состояние сеанса, и как выполнить команду с использованием объекта <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference>.</para>
                </definition>
                <definedTerm>Runspace11</definedTerm>
                <definition>
                  <para>Показывает, как использовать класс <codeEntityReference>T:System.Management.Automation.ProxyCommand</codeEntityReference> для создания прокси-команды, которая вызывает существующий командлет, но ограничивает набор доступных параметров. Прокси-команда затем добавляется в начальное состояние сеанса, который используется для создания ограниченного пространства выполнения. Это означает, что пользователь может получить доступ к функциям этого командлета только через прокси-команду.</para>
                </definition>
                <definedTerm>PowerShell01</definedTerm>
                <definition>
                  <para>Показывает, как создать ограниченное пространство выполнения с помощью объекта <codeEntityReference>T:System.Management.Automation.Runspaces.InitialSessionState</codeEntityReference>.</para>
                </definition>
                <definedTerm>PowerShell02</definedTerm>
                <definition>
                  <para>Показывает, как использовать пул пространств выполнения для одновременного запуска нескольких команд.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
          <section>
            <title>Примеры узлов</title>
            <content>
              <definitionTable>
                <definedTerm>Host01</definedTerm>
                <definition>
                  <para>Показывает, как реализовать ведущее приложение, которое использует пользовательский узел. В этом примере создается пространство выполнения, которое использует пользовательский узел, а затем API <codeEntityReference>T:System.Management.Automation.PowerShell</codeEntityReference> используется для выполнения скрипта, который вызывает "exit". После ведущее приложение ищет выходные данные скрипта и отображает результаты.</para>
                </definition>
                <definedTerm>Host02</definedTerm>
                <definition>
                  <para>Показывает, как написать ведущее приложение, которое использует среду выполнения <token>mshshort</token> с реализацией пользовательского узла. Ведущее приложение задает в качестве языка и региональных параметров узла немецкий, запускает командлет <externalLink><linkText>Get-Process</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=113324</linkUri></externalLink> и отображает результаты, как при использовании pwrsh.exe, а затем отображает текущие дату и время на немецком.</para>
                </definition>
                <definedTerm>Host03</definedTerm>
                <definition>
                  <para>Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое читает команды командной строки, выполняет их, а затем отображает результаты в консоли.</para>
                </definition>
                <definedTerm>Host04</definedTerm>
                <definition>
                  <para>Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое читает команды из командной строки, выполняет их, а затем отображает результаты в консоли. Это ведущее приложение также поддерживает отображение подсказок, которые позволяют пользователю указать несколько вариантов.</para>
                </definition>
                <definedTerm>Host05</definedTerm>
                <definition>
                  <para>Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое читает команды из командной строки, выполняет их, а затем отображает результаты в консоли. Это ведущее приложение также поддерживает вызов удаленных компьютеров с использованием командлетов <externalLink><linkText>Enter-PsSession</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=135210</linkUri></externalLink> и <externalLink><linkText>Exit-PsSession</linkText><linkUri>http://go.microsoft.com/fwlink/?LinkId=135212</linkUri></externalLink>.</para>
                </definition>
                <definedTerm>Host06</definedTerm>
                <definition>
                  <para>Показывает, как выполнить сборку интерактивного консольного ведущего приложения, которое читает команды из командной строки, выполняет их, а затем отображает результаты в консоли. Кроме того, в этом примере используются интерфейсы API создателя токенов для указания цвета текста, вводимого пользователем.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
          <section>
            <title>Примеры поставщиков</title>
            <content>
              <definitionTable>
                <definedTerm>AccessDBProviderSample01</definedTerm>
                <definition>
                  <para>Показывает, как объявить класс поставщика, производный непосредственно от класса <codeEntityReference>T:System.Management.Automation.Provider.CmdletProvider</codeEntityReference>. Он включается здесь только для полноты.</para>
                </definition>
                <definedTerm>AccessDBProviderSample02</definedTerm>
                <definition>
                  <para>Показывает, как перезаписать методы <codeEntityReference>M:System.Management.Automation.Provider.DriveCmdletProvider.NewDrive(System.Management.Automation.PSDriveInfo)</codeEntityReference> и <codeEntityReference>M:System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive(System.Management.Automation.PSDriveInfo)</codeEntityReference> для поддержки вызовов в командлеты New-PSDrive и Remove-PSDrive. Класс поставщика в этом примере является производным от класса <codeEntityReference>T:System.Management.Automation.Provider.DriveCmdletProvider</codeEntityReference>.</para>
                </definition>
                <definedTerm>AccessDBProviderSample03</definedTerm>
                <definition>
                  <para>Показывает, как перезаписать методы <codeEntityReference>M:System.Management.Automation.Provider.ItemCmdletProvider.GetItem(System.String)</codeEntityReference> и <codeEntityReference>M:System.Management.Automation.Provider.ItemCmdletProvider.SetItem(System.String,System.Object)</codeEntityReference> для поддержки вызовов в командлеты Get-Item и Set-Item. Класс поставщика в этом примере является производным от класса <codeEntityReference>T:System.Management.Automation.Provider.ItemCmdletProvider</codeEntityReference>.</para>
                </definition>
                <definedTerm>AccessDBProviderSample04</definedTerm>
                <definition>
                  <para>Показывает, как перезаписать методы контейнера для поддержки вызовов в командлеты Copy-Item, Get-ChildItem, New-Item и Remove-Item. Эти методы должны быть реализованы, когда хранилище данных содержит элементы, являющиеся контейнерами. Контейнер — это группа дочерних элементов в составе общего родительского элемента. Класс поставщика в этом примере является производным от класса <codeEntityReference>T:System.Management.Automation.Provider.ItemCmdletProvider</codeEntityReference>.</para>
                </definition>
                <definedTerm>AccessDBProviderSample05</definedTerm>
                <definition>
                  <para>Показывает, как перезаписать методы контейнера для поддержки вызовов в командлеты Move-Item и Join-Path. Эти методы должны быть реализованы, когда пользователю требуется переместить элементы в контейнере, если хранилище данных содержит вложенные контейнеры. Класс поставщика в этом примере является производным от класса <codeEntityReference>T:System.Management.Automation.Provider.NavigationCmdletProvider</codeEntityReference>.</para>
                </definition>
                <definedTerm>AccessDBProviderSample06</definedTerm>
                <definition>
                  <para>Показывает, как перезаписать методы содержимого для поддержки вызовов в командлеты Clear-Content, Get-Content и Set-Content. Эти методы должны быть реализованы, когда пользователю требуется управлять содержимым элементов в хранилище данных. Класс поставщика в этом примере является производным от класса <codeEntityReference>T:System.Management.Automation.Provider.NavigationCmdletProvider</codeEntityReference>, он реализует интерфейс <codeEntityReference>T:System.Management.Automation.Provider.IContentCmdletProvider</codeEntityReference>.</para>
                </definition>
              </definitionTable>
            </content>
          </section>
        </sections>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>



<!--HONumber=May16_HO4-->


