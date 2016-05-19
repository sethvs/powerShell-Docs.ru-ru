#  Установка и использование Windows PowerShell Web Access

Обновлено: 5 ноября 2013 г.

Область применения: Windows Server 2012 R2, Windows Server 2012

Компонент Windows PowerShell® Web Access, впервые представленный в Windows Server® 2012, действует как шлюз Windows PowerShell, предоставляя веб-консоль Windows PowerShell для удаленного компьютера. Она позволяет ИТ-специалистам выполнять команды и сценарии Windows PowerShell с консоли Windows PowerShell в веб-браузере без установки Windows PowerShell, программ для удаленного управления или подключаемых модулей браузера, необходимых на устройстве клиента. Для работы веб-консоли Windows PowerShell требуется только правильно настроенный шлюз Windows PowerShell и браузер на устройстве клиента, который поддерживает JavaScript® и принимает cookie-файлы.

Примерами клиентских устройств могут служить ноутбуки, персональные компьютеры, не являющиеся служебными, арендованные компьютеры, планшетные компьютеры, веб-киоски, компьютеры без операционной системы на базе Windows и браузеры сотовых телефонов. ИТ-специалисты могут выполнять важные задачи управления на удаленных серверах на базе ОС Windows с устройств, имеющих доступ к Интернету и веб-браузер.

После успешной установки и настройки шлюза пользователи получают доступ к консоли Windows PowerShell с помощью веб-браузера. Пользователи, открывающие защищенный веб-сайт Windows PowerShell, могут запускать веб-консоль Windows PowerShell после успешной проверки подлинности.

Для установки и настройки Windows PowerShell Web Access требуются три шага.

1.  Установка Windows PowerShell Web Access

2.  Настройка шлюза

3.  Настройка правил авторизации, которые разрешают пользователям осуществлять доступ к веб-консоли Windows PowerShell

Перед установкой и настройкой Windows PowerShell Web Access рекомендуется внимательно ознакомиться с этим руководством, поскольку здесь содержатся инструкции по установке, удалению и обеспечению безопасности Windows PowerShell Web Access. В разделе [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx) описан вход пользователей в веб-консоль, представлены ограничения и различия между веб-консолью Windows PowerShell и консолью **powershell.exe**. Конечным пользователям веб-консоли необходимо ознакомиться со статьей [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx), но нет необходимости читать остальное руководство.

В этой статье не приводятся подробные рекомендации по работе с веб-сервером (IIS). Описаны только шаги, необходимые для настройки шлюза Windows PowerShell Web Access. Дополнительные сведения о настройке и обеспечении безопасности веб-сайтов в IIS см. в документации по IIS (в разделе "См. также").

Следующая схема демонстрирует работу Windows PowerShell Web Access.

<span><img src="https://i-technet.sec.s-msft.com/dynimg/IC564303.jpeg" title="Windows PowerShell Web Access diagram" alt="Windows PowerShell Web Access diagram" id="ee15fa8f-ce13-49e5-933d-514f6d60a2b1" /></span>

Содержание раздела:

-   [Требования для запуска веб-доступа Windows PowerShell](#BKMK_reqs)

-   [Поддержка браузеров и клиентских устройств](#BKMK_browser)

-   [Рекомендованная схема (быстрого) развертывания](#BKMK_recm)

-   [Пользовательское развертывание](#BKMK_custom)

-   [Настройка подлинного сертификата](#BKMK_configcert)

<a href="" id="BKMK_reqs"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования для запуска веб-доступа Windows PowerShell</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_0" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Для работы Windows PowerShell Web Access необходимо, чтобы веб-сервер (IIS), .NET Framework 4.5 и Windows PowerShell 3.0 или Windows PowerShell 4.0 выполнялись на сервере, на котором предполагается запустить шлюз. Можно установить Windows PowerShell Web Access на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью мастера добавления ролей и компонентов в диспетчере серверов или командлетов развертывания Windows PowerShell для диспетчера серверов. При установке Windows PowerShell Web Access с помощью диспетчера серверов или командлетов развертывания необходимые роли и компоненты добавляются автоматически в процессе установки.

Windows PowerShell Web Access позволяет удаленным пользователям получать доступ к компьютерам в вашей организации, используя Windows PowerShell в веб-браузере. Хотя Windows PowerShell Web Access является удобным и мощным инструментом управления, доступ через Интернет связан с рисками для безопасности и должен настраиваться с максимально возможной безопасностью. Мы рекомендуем администраторам, настраивающим шлюз Windows PowerShell Web Access, использовать как уровни безопасности, доступные в правилах авторизации на основе командлетов, включаемых в Windows PowerShell Web Access, так и уровни безопасности, доступные в веб-сервере (IIS) и приложениях сторонних производителей. В данную документацию включены как небезопасные примеры, которые рекомендуются только для тестовых сред, так и примеры, рекомендуемые для безопасного развертывания.

<a href="" id="BKMK_browser"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Поддержка браузеров и клиентских устройств</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Windows PowerShell Web Access поддерживает перечисленные ниже веб-браузеры. Хотя браузеры для мобильных устройств официально не поддерживаются, многие их них могут выполнять веб-консоль Windows PowerShell. Ожидается, что другие браузеры, которые принимают куки-файлы, выполняют JavaScript и выполняют веб-сайты HTTPS, также будут работать, но официально они не протестированы.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Поддерживаемые браузеры для настольных компьютеров</span></a>

------------------------------------------------------------------------

-   Windows® Internet Explorer® для Microsoft Windows® 8.0, 9.0, 10.0 и 11.0

-   Mozilla Firefox® 10.0.2

-   Google Chrome™ 17.0.963.56m для Windows

-   Apple Safari® 5.1.2 для Windows

-   Apple Safari 5.1.2 для Mac OS®

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Минимально протестированные мобильные устройства или браузеры</span></a>

------------------------------------------------------------------------

-   Windows Phone 7 и 7.5

-   Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)

-   Apple Safari для операционной системы 5.0.1 для iPhone

-   Apple Safari для операционной системы 5.0.1 для iPad 2

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования к браузерам</span></a>

------------------------------------------------------------------------

Чтобы использовать веб-консоль Windows PowerShell Web Access, браузеры должны иметь следующие возможности.

-   Разрешать файлы cookie с веб-сайта шлюза Windows PowerShell Web Access.

-   Открывать и читать HTTPS-страницы.

-   Открывать и выполнять веб-сайты, использующие JavaScript.

<a href="" id="BKMK_recm"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Рекомендованная схема (быстрого) развертывания</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Шлюз Windows PowerShell Web Access можно установить на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью командлетов развертывания Windows PowerShell или мастера добавления ролей и компонентов в диспетчере серверов. Для быстрой установки и настройки воспользуйтесь командлетами Windows PowerShell, как описано в этом разделе.

-   [Шаг 1. Установка Windows PowerShell Web Access](#BKMK_step1)

-   [Шаг 2. Настройка шлюза](#BKMK_step2)

-   [Шаг 3. Настройка ограничивающего правила авторизации](#BKMK_step3)

<a href="" id="BKMK_step1"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Установка Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**..

    -   На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем щелкните **Запустить от имени администратора**..

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>В Windows PowerShell 3.0 и 4.0 не нужно импортировать модуль командлета диспетчера серверов в сеанс Windows PowerShell перед запуском командлетов, которые являются частью этого модуля. Модуль автоматически импортируется при первом выполнении командлета, входящего в модуль. Кроме того, командлеты Windows PowerShell не учитывают регистр.</p></td>
    </tr>
    </tbody>
    </table>

2.  Введите следующую команду и нажмите клавишу **ВВОД**, где *computer_name* представляет имя удаленного компьютера, на который требуется установить Windows PowerShell Web Access, если это применимо. Параметр <span class="code">Restart</span> автоматически перезапускает целевой сервер при необходимости.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_374a9c21-4f6e-471e-b957-bb190a594533'); "Копировать в буфер обмена".)

        Install-WindowsFeature –Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell не добавляет средства управления веб-сервера (IIS) по умолчанию. Если требуется установить средства управления на тот же сервер, на котором выполняется шлюз Windows PowerShell Web Access, добавьте в команду установки параметр <span class="code">IncludeManagementTools</span> (как указано в этом шаге). Если управление веб-сайтом Windows PowerShell Web Access осуществляется с удаленного компьютера, установите оснастку "Диспетчер служб IIS", установив <a href="http://go.microsoft.com/fwlink/?LinkID=304145">Средства удаленного администрирования сервера для Windows 8.1</a> или <a href="http://go.microsoft.com/fwlink/p/?LinkID=238560">Средства удаленного администрирования сервера для Windows 8</a> на компьютере, с которого будет осуществляться управление шлюзом.</p></td>
    </tr>
    </tbody>
    </table>

    Чтобы установить роли и компоненты на автономном виртуальном жестком диске (VHD), необходимо добавить оба параметра — <span class="code">ComputerName</span> и <span class="code">VHD</span>. Параметр <span class="code">ComputerName</span> содержит имя сервера, на котором следует подключить виртуальный жесткий диск, а параметр <span class="code">VHD</span> — путь к VHD-файлу на указанном сервере.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_d841d509-347e-49d0-bf54-8d1f306bece6'); "Копировать в буфер обмена".)

        Install-WindowsFeature –Name WindowsPowerShellWebAccess –VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart

3.  Когда установка завершена, убедитесь, что Windows PowerShell Web Access установлен на целевых серверах, запустив командлет **Get-WindowsFeature** на целевом сервере в консоли Windows PowerShell, которая была открыта с повышенными правами пользователя. Можно также проверить установку Windows PowerShell Web Access в консоли диспетчера серверов, выбрав целевой сервер на странице **Все серверы**, а затем просмотрев плитку **Роли и компоненты** для выбранного сервера. Можно также просмотреть файл сведений для Windows PowerShell Web Access.

4.  После завершения установки Windows PowerShell Web Access выводится приглашение прочитать файл сведений, содержащий основные инструкции по установке шлюза. Эти инструкции по установке приводятся также в следующем разделе [Шаг 2. Настройка шлюза](#BKMK_step2). Путь к файлу сведений: <span class="computerOutputInline"> C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt.</span>.

<a href="" id="BKMK_step2"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Настройка шлюза</span></a>

------------------------------------------------------------------------

Командлет **Install-PswaWebApplication** позволяет быстро выполнить настройку Windows PowerShell Web Access. Хотя можно добавить параметр <span class="code">UseTestCertificate</span> в командлет <span class="code">Install-PswaWebApplication</span>, чтобы установить самозаверяющий SSL-сертификат для целей тестирования, это небезопасно. Для безопасной производственной среды всегда используйте действительный SSL-сертификат, подписанный центром сертификации. Администраторы могут заменить тестовый сертификат на подписанный сертификат по своему выбору с помощью консоли "Диспетчер служб IIS".

Вы можете завершить настройку веб-приложения Windows PowerShell Web Access с помощью командлета <span class="code">Install-PswaWebApplication</span> или выполнив процедуру настройки через пользовательский интерфейс диспетчера служб IIS. По умолчанию командлет устанавливает веб-приложение **pswa** (и пул приложений для него, **pswa_pool**) в контейнер **Веб-сайт по умолчанию**, как показано в диспетчере служб IIS. Если требуется, вы можете изменить в командлете контейнер сайта по умолчанию для веб-приложения. Диспетчер служб IIS предлагает параметры настройки, доступные для веб-приложений, например, изменение номера порта или SSL-сертификата.

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Примечание о безопасности </span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Мы настоятельно рекомендуем администраторам настраивать шлюз на использование действительного сертификата, подписанного центром сертификации.</p></td>
</tr>
</tbody>
</table>

-   [Настройка шлюза Windows PowerShell Web Access с тестовым сертификатом с помощью Install-PswaWebApplication](#BKMK_testcert)

-   [Настройка шлюза Windows PowerShell Web Access с подлинным сертификатом с использованием командлета Install-PswaWebApplication и диспетчера IIS](#BKMK_gencert)

#### Настройка шлюза Windows PowerShell Web Access с тестовым сертификатом с помощью Install-PswaWebApplication

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.

    -   На **начальном** экране Windows щелкните **Windows PowerShell**..

2.  Введите следующую команду и нажмите клавишу **ВВОД**:.

    **Install-PswaWebApplication -UseTestCertificate**

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC17938.jpeg" title="System_CAPS_security" alt="System_CAPS_security" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-security" /></span><span class="alertTitle"> Примечание о безопасности </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Параметр <span class="code">UseTestCertificate</span> следует использовать только в частной тестовой среде. Для безопасной производственной среды мы рекомендуем использовать действительный сертификат, подписанный центром сертификации.</p></td>
    </tr>
    </tbody>
    </table>

    При выполнении командлета веб-приложение Windows PowerShell Web Access устанавливается в контейнер IIS "Веб-сайт по умолчанию". Этот командлет создает инфраструктуру, необходимую для выполнения Windows PowerShell Web Access на веб-сайте по умолчанию https://&lt;server_name&gt;/pswa. Чтобы установить веб-приложение на другой веб-сайт, введите имя веб-сайта, добавив параметр <span class="code">WebSiteName</span>. Чтобы изменить имя веб-приложения (по умолчанию <span class="code">pswa</span>), добавьте параметр <span class="code">WebApplicationName</span>.

    Следующие параметры настраиваются при выполнении командлета. Если требуется, вы можете изменить их вручную в консоли "Диспетчер служб IIS".

    -   Path: /pswa

    -   ApplicationPool: pswa_pool

    -   EnabledProtocols: http

    -   PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

    <span class="label">Пример: </span> <span class="code"> Install-PswaWebApplication –webApplicationName myWebApp –useTestCertificate</span>

    В этом примере полученный веб-сайт для Windows PowerShell Web Access имеет вид https://&lt; *server_name*&gt;/myWebApp.

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации. Дополнительные сведения см. в разделе <a href="#BKMK_step3">Шаг 3. Настройка ограничивающего правила авторизации</a> и <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access.</a>.</p></td>
    </tr>
    </tbody>
    </table>

#### Настройка шлюза Windows PowerShell Web Access с подлинным сертификатом с использованием командлета Install-PswaWebApplication и диспетчера IIS

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.

    -   На **начальном** экране Windows щелкните **Windows PowerShell**..

2.  Введите следующую команду и нажмите клавишу **ВВОД**:.

    **Install-PswaWebApplication**

    Следующие параметры шлюза настраиваются при выполнении командлета. Если требуется, вы можете изменить их вручную в консоли "Диспетчер служб IIS". Можно также указать значения для параметров <span class="code">WebsiteName</span> и <span class="code">WebApplicationName</span> командлета <span class="code">Install-PswaWebApplication</span>.

    -   Path: /pswa

    -   ApplicationPool: pswa_pool

    -   EnabledProtocols: http

    -   PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

3.  Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows. В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**..

    -   На **начальном** экране в Windows выберите **Диспетчер серверов**..

4.  В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**. Разверните папку **Сайты**.

5.  Выберите веб-сайт, на котором было установлено веб-приложение Windows PowerShell Web Access. В области **Действия** щелкните элемент **Привязки**..

6.  В диалоговом окне **Привязки сайта** щелкните **Добавить**..

7.  В диалоговом окне **Добавление привязки сайта** выберите в поле **Тип** значение **https**..

8.  В поле **Сертификат SSL** выберите ваш подписанный сертификат в раскрывающемся меню. Нажмите кнопку **ОК**. Дополнительные сведения о получении сертификата см. в разделе [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) в данной статье.

    Теперь веб-приложение Windows PowerShell Web Access настроено для использования вашего подписанного сертификата. Чтобы получить доступ к Windows PowerShell Web Access, откройте https://&lt;имя_сервера&gt;/pswa в окне браузера.

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации. Дополнительные сведения см. в разделе <a href="#BKMK_step3">Шаг 3. Настройка ограничивающего правила авторизации</a> и <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access.</a>.</p></td>
    </tr>
    </tbody>
    </table>

<a href="" id="BKMK_step3"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 3. Настройка ограничивающего правила авторизации</span></a>

------------------------------------------------------------------------

После установки Windows PowerShell Web Access и настройки шлюза пользователи могут открывать страницу входа в браузере, но они не могут выполнить вход, пока администратор Windows PowerShell Web Access не предоставит им доступ в явном виде. Управление доступом в Windows PowerShell Web Access осуществляется с помощью набора командлетов Windows PowerShell, описанных в следующей таблице. Нет соответствующего графического пользовательского интерфейса для добавления правил авторизации или управления ими. Подробные сведения о командлетах Windows PowerShell Web Access см. в справочных разделах по командлетам [Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx)..

Дополнительные сведения о безопасности и правилах авторизации Windows PowerShell Web Access см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)..

#### Добавление ограничивающего правила авторизации

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**..

    -   На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем щелкните **Запустить от имени администратора**..

2.  <span class="label">Необязательный шаг для ограничения доступа пользователей с помощью конфигураций сеансов: </span> убедитесь, что конфигурации сеансов, которые вы хотите использовать в своих правилах, уже существуют. В противном случае выполните инструкции по созданию конфигураций сеансов, приведенные в статье [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.

3.  Введите следующую команду и нажмите клавишу **ВВОД**:.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_f9e7959b-75d0-4d63-8f8e-02334a8dd09d'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    Это правило авторизации разрешает конкретному пользователю доступ к одному сетевому компьютеру, к которому обычно требуется доступ, с доступом к конкретной конфигурации сеанса, область которого соответствует потребностям пользовательских скриптов и командлетов. В следующем примере пользователю с именем <span class="code">JSmith</span> в домене <span class="code">Contoso</span> предоставляется доступ для управления компьютером <span class="code">Contoso_214</span> и использования конфигурации сеанса с именем <span class="code"> NewAdminsOnly.</span>.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ebd5bc5e-ec5d-4955-a86a-63843e480e37'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  Убедитесь, что правило создано, выполнив командлет **Get-PswaAuthorizationRule** или **Test-PswaAuthorizationRule -UserName &lt;домен\пользователь | компьютер\пользователь&gt; -ComputerName**  &lt;computer_name&gt;. Например, **Test-PswaAuthorizationRule –UserName Contoso\JSmith –ComputerName Contoso_214**..

После настройки правила авторизации авторизованные пользователи могут выполнить вход в веб-консоль и приступить к использованию Windows PowerShell Web Access.

<a href="" id="BKMK_custom"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Пользовательское развертывание</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Шлюз Windows PowerShell Web Access можно установить на сервер под управлением Windows Server 2012 R2 или Windows Server 2012 с помощью мастера добавления ролей и компонентов в диспетчере серверов. После установки Windows PowerShell Web Access можно настроить конфигурацию шлюза в диспетчере IIS.

<a href="" id="BKMK_custom1"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Установка Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### Установка Windows PowerShell Web Access с помощью мастера добавления ролей и компонентов

1.  Если диспетчер серверов уже открыт, переходите к следующему шагу. Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.

    -   На **начальном** экране в Windows выберите **Диспетчер серверов**..

2.  В меню **Управление** выберите команду **Добавить роли и компоненты**..

3.  На странице **Выбор типа установки** выберите **Установка ролей или компонентов**. Нажмите кнопку **Далее**..

4.  На странице **Выбор целевого сервера** выберите сервер из пула серверов или автономный виртуальный жесткий диск. Чтобы выбрать автономный виртуальный жесткий диск в качестве конечного сервера, сначала выберите сервер, на котором будет подключен виртуальный жесткий диск, а затем выберите VHD-файл. Сведения о добавлении серверов в пул серверов см. в справке диспетчера серверов. Выбрав конечный сервер, нажмите кнопку **Далее**..

5.  На странице **Выбор компонентов** мастера разверните узел **Windows PowerShell** и выберите **Windows PowerShell Web Access**..

6.  Отметим, что выводится приглашение добавить необходимые компоненты, такие как .NET Framework 4.5 и службы ролей веб-сервера (IIS). Добавьте необходимые компоненты и продолжайте работу.

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>При установке Windows PowerShell Web Access с помощью мастера добавления ролей и компонентов также устанавливается веб-сервер (IIS), включая оснастку диспетчера служб IIS. Если используется мастер добавления ролей и компонентов, оснастка и другие средства управления IIS устанавливаются по умолчанию. При установке Windows PowerShell Web Access с помощью командлетов Windows PowerShell, как описано в следующей процедуре, средства управления не устанавливаются по умолчанию.</p></td>
    </tr>
    </tbody>
    </table>

7.  На странице **Подтверждение выбранных элементов для установки**, если файлы компонентов для Windows PowerShell Web Access не сохраняются на целевом сервере, выбранном на шаге 4, щелкните **Указать альтернативный исходный путь** и укажите путь к файлам компонентов. В противном случае щелкните **Установить**..

8.  После щелчка **Установить** на странице **Ход установки** отображаются ход выполнения установки, результаты и сообщения, такие как предупреждения, сообщения об ошибках и шаги по настройке после установки, необходимые для Windows PowerShell Web Access. После завершения установки Windows PowerShell Web Access выводится приглашение прочитать файл сведений, содержащий основные инструкции по установке шлюза. Эти инструкции также являются частью этого раздела. Путь к файлу сведений: <span class="computerOutputInline"> C:\\Windows\\Web\\PowerShellWebAccess\\wwwroot\\README.txt.</span>.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Настройка шлюза</span></a>

------------------------------------------------------------------------

Этот раздел содержит инструкции по установке веб-приложения Windows PowerShell Web Access в подкаталог, а не в корневой каталог веб-сайта. Данная процедура, выполняемая через пользовательский интерфейс, эквивалентна действиям, выполняемым с помощью командлета <span class="code">Install-PswaWebApplication</span>. В раздел также включены инструкции по использованию диспетчера служб IIS для настройки шлюза Windows PowerShell Web Access в качестве корневого веб-сайта.

-   [Использование диспетчера служб IIS для настройки шлюза в существующем веб-сайте](#BKMK_configman)

-   [Использование диспетчера служб IIS для настройки шлюза в качестве корневого веб-сайта с тестовым сертификатом](#BKMK_configroot)

-   

#### Использование диспетчера служб IIS для настройки шлюза в существующем веб-сайте

1.  Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows. В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**..

    -   На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**. Щелкните ярлык, когда он появится в списке результатов **Приложения**.

2.  Создайте новый пул приложений для Windows PowerShell Web Access. Разверните узел сервера шлюза в области дерева диспетчера служб IIS, выберите **Пулы приложений** и щелкните **Добавить пул приложений** в области **Действия**.

3.  Добавьте новый пул приложений с именем **pswa_pool** или укажите другое имя. Нажмите кнопку **ОК**..

4.  В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**. Выберите папку **Сайты**.

5.  Щелкните правой кнопкой мыши веб-сайт (например, **Веб-сайт по умолчанию**), в который следует добавить веб-сайт Windows PowerShell Web Access, а затем щелкните **Добавить приложение**..

6.  В поле **Псевдоним** введите pswa или укажите другой псевдоним. Псевдоним становится именем виртуального каталога. Так **pswa** в следующем URL-адресе представляет псевдоним, заданный в этом шаге: https://&lt;имя_сервера&gt;/pswa.

7.  В поле **Пул приложений** выберите пул приложений, созданный на шаге 3.

8.  В поле **Физический путь** найдите расположение приложения. Можно использовать расположение по умолчанию %windir%/Web/PowerShellWebAccess/wwwroot. Нажмите кнопку **ОК**..

9.  Выполните шаги, описанные в процедуре [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) в данной статье.

10. <span class="label">Дополнительный шаг по обеспечению безопасности.</span> Когда веб-сайт выбран в области дерева, дважды щелкните **Параметры SSL** на панели содержимого. Выберите **Требовать SSL**, а затем в области **Действия** щелкните **Применить**. Дополнительно в области **Параметры SSL** можно потребовать, чтобы пользователи, подключающиеся к веб-сайту Windows PowerShell Web Access, имели клиентские сертификаты. Клиентские сертификаты помогают проверить идентификацию пользователя клиентского устройства. Дополнительные сведения о том, как требование клиентских сертификатов может повысить безопасность Windows PowerShell Web Access, см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx) в этом руководстве.

11. Откройте сеанс браузера на клиентском устройстве. Дополнительные сведения о поддерживаемых браузерах и устройствах см. в разделе [Поддержка браузеров и клиентских устройств](#BKMK_browser) в этой статье.

12. Откройте новый веб-сайт Windows PowerShell Web Access — https://&lt; *имя_сервера_шлюза*&gt;/pswa.

    В браузере должна появиться страница входа в консоль Windows PowerShell Web Access.

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</p></td>
    </tr>
    </tbody>
    </table>

13. В сеансе Windows PowerShell, который был открыт с повышенными правами (запуск от имени администратора), выполните следующий сценарий, в котором *application_pool_name* представляет имя пула приложений, созданного на шаге 3, чтобы предоставить пулу приложений права доступа к файлу авторизации.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_c1a80a93-8fcf-4beb-a025-5f81bfb8bdae'); "Копировать в буфер обмена".)

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Чтобы просмотреть права доступа к файлу авторизации, выполните следующую команду:

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_ac2179c2-9548-4a17-8663-267fdd105380'); "Копировать в буфер обмена".)

        c:\windows\system32\icacls.exe $authorizationFile

#### Использование диспетчера служб IIS для настройки шлюза в качестве корневого веб-сайта с тестовым сертификатом

1.  Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows. В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**..

    -   На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**. Щелкните ярлык, когда он появится в списке результатов **Приложения**.

2.  В области дерева диспетчера служб IIS разверните узел для сервера, на котором установлен компонент Windows PowerShell Web Access, и перейдите к папке **Сайты**. Выберите папку **Сайты**.

3.  В области **Действия** щелкните **Добавить веб-сайт**..

4.  Введите имя веб-сайта, например **Windows PowerShell Web Access**..

5.  Автоматически создается пул приложений для нового веб-сайта. Чтобы использовать другой пул приложений, щелкните **Выбрать**, чтобы выбрать пул приложений, связываемый с новым веб-сайтом. Выберите другой пул приложений в диалоговом окне **Выбор пула приложений** и нажмите кнопку **ОК**..

6.  В поле **Физический путь** перейдите к папке %*windir*%/Web/PowerShellWebAccess/wwwroot.

7.  В поле **Тип** в области **Привязка** выберите **https**..

8.  Назначьте веб-сайту номер порта, который еще не используется другим сайтом или приложением. Чтобы найти открытые порты, можно выполнить команду **netstat** в окне командной строки. Номер порта по умолчанию: 443.

    Измените номер порта по умолчанию, если порт 443 уже используется другим веб-сайтом или имеются другие соображения безопасности для изменения номера порта. Если выбранный вами порт используется другим веб-сайтом, который выполняется на вашем сервере шлюза, при нажатии кнопки **ОК** выводится предупреждение в диалоговом окне **Добавление веб-сайта**. Для запуска Windows PowerShell Web Access необходимо использовать неиспользуемый порт.

9.  Дополнительно, если требуется для вашей организации, укажите понятное имя узла, например **www.contoso.com**. Нажмите кнопку **ОК**..

10. Чтобы обезопасить производственную среду, мы настоятельно рекомендуем предоставить действительный сертификат, подписанный центром сертификации. Вы должны предоставить SSL-сертификат, поскольку пользователи могут подключаться к Windows PowerShell Web Access только по протоколу HTTPS. Дополнительные сведения о получении сертификата см. в разделе [Настройка SSL-сертификата в диспетчере служб IIS](#BKMK_cert) в данной статье.

11. Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление веб-сайта**.

12. В сеансе Windows PowerShell, который был открыт с повышенными правами (запуск от имени администратора), выполните следующий сценарий, в котором *application_pool_name* представляет имя пула приложений, созданного на шаге 4, чтобы предоставить пулу приложений права доступа к файлу авторизации.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_35ae9944-ca44-4af7-9c96-616083b3e3db'); "Копировать в буфер обмена".)

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Чтобы просмотреть права доступа к файлу авторизации, выполните следующую команду:

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_0eb6d70a-2807-498b-b088-fa5233ed68d5'); "Копировать в буфер обмена".)

        c:\windows\system32\icacls.exe $authorizationFile

13. Когда новый веб-сайт выбран в области дерева диспетчера служб IIS, в области **Действия** щелкните **Запуск**, чтобы запустить веб-сайт.

14. Откройте сеанс браузера на клиентском устройстве. Дополнительные сведения о поддерживаемых браузерах и устройствах см. в разделе [Поддержка браузеров и клиентских устройств](#BKMK_browser) в данном документе.

15. Откройте новый веб-сайт Windows PowerShell Web Access.

    Поскольку корневой веб-сайт указывает на папку Windows PowerShell Web Access, в браузере при открытии адреса https://&lt; *имя_сервера_шлюза*&gt; должна открываться страница входа Windows PowerShell Web Access. Нет необходимости добавлять **/pswa** в URL-адрес.

    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><span><img src="https://i-technet.sec.s-msft.com/dynimg/IC101471.jpeg" title="System_CAPS_note" alt="System_CAPS_note" id="s-e6f6a65cf14f462597b64ac058dbe1d0-system-media-system-caps-note" /></span><span class="alertTitle">Примечание </span></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Вы не можете выполнить вход до предоставления пользователям доступа к веб-сайту с помощью добавления прав авторизации.</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 3. Настройка ограничивающего правила авторизации</span></a>

------------------------------------------------------------------------

После установки Windows PowerShell Web Access и настройки шлюза пользователи могут открывать страницу входа в браузере, но они не могут выполнить вход, пока администратор Windows PowerShell Web Access не предоставит им доступ в явном виде. Управление доступом в Windows PowerShell Web Access осуществляется с помощью набора командлетов Windows PowerShell, описанных в следующей таблице. Нет соответствующего графического пользовательского интерфейса для добавления правил авторизации или управления ими. Подробные сведения о командлетах Windows PowerShell Web Access см. в справочных разделах по командлетам [Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx)..

Дополнительные сведения о безопасности и правилах авторизации Windows PowerShell Web Access см. в разделе [Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)..

#### Добавление ограничивающего правила авторизации

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**..

    -   На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем щелкните **Запустить от имени администратора**..

2.  <span class="label">Необязательный шаг для ограничения доступа пользователей с помощью конфигураций сеансов: </span> убедитесь, что конфигурации сеансов, которые вы хотите использовать в своих правилах, уже существуют. В противном случае выполните инструкции по созданию конфигураций сеансов, приведенные в статье [about_Session_Configuration_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.

3.  Введите следующую команду и нажмите клавишу **ВВОД**:.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_4df22c91-f56f-4bb5-91e7-99f9b365ed5d'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    Это правило авторизации разрешает конкретному пользователю доступ к одному сетевому компьютеру, к которому обычно требуется доступ, с доступом к конкретной конфигурации сеанса, область которого соответствует потребностям пользовательских скриптов и командлетов. В следующем примере пользователю с именем <span class="code">JSmith</span> в домене <span class="code">Contoso</span> предоставляется доступ для управления компьютером <span class="code">Contoso_214</span> и использования конфигурации сеанса с именем <span class="code"> NewAdminsOnly.</span>.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_efc3999a-2905-453f-86cd-014b41658ffc'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  Убедитесь, что правило создано, выполнив командлет **Get-PswaAuthorizationRule** или **Test-PswaAuthorizationRule -UserName &lt;домен\пользователь | компьютер\пользователь&gt; -ComputerName**  &lt;computer_name&gt;. Например, **Test-PswaAuthorizationRule –UserName Contoso\JSmith –ComputerName Contoso_214**..

После настройки правила авторизации авторизованные пользователи могут выполнить вход в веб-консоль и приступить к использованию Windows PowerShell Web Access.

<a href="" id="BKMK_configcert"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Настройка подлинного сертификата</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Для безопасной производственной среды следует всегда использовать действительный сертификат SSL, подписанный центром сертификации (ЦС). В этом разделе описано, как получить и установить действительный SSL-сертификат от центра сертификации.

### Настройка SSL-сертификата в диспетчере служб IIS

1.  В области дерева диспетчера служб IIS выберите сервер, на котором установлен компонент Windows PowerShell Web Access.

2.  В области содержимого дважды щелкните **Сертификаты сервера**..

3.  В области **Действия** выполните одно из следующих действий. Дополнительные сведения о настройке сертификатов сервера в IIS см. в статье [Настройка сертификатов сервера в IIS 7](https://technet.microsoft.com/library/cc732230.aspx)..

    -   Щелкните **Импорт**, чтобы импортировать имеющийся действительный сертификат из расположения в вашей сети.

    -   Щелкните **Создать запрос сертификата**, чтобы запросить сертификат из центра сертификации, например из VeriSign™, Thawte или GeoTrust®. Общее имя сертификата должно совпадать с заголовком узла в запросе. Например, если браузер клиента запрашивает http://www.contoso.com/, общим именем также должно быть http://www.contoso.com/. Это самый безопасный и рекомендуемый вариант предоставления сертификата для шлюза Windows PowerShell Web Access.

    -   Щелкните **Создать самозаверяющий сертификат**, чтобы создать сертификат, который можно использовать немедленно, а при необходимости подписать в ЦС позже. Введите понятное имя самозаверяющего сертификата, например **Windows PowerShell Web Access**. Этот вариант не считается безопасным и рекомендуется только для частной тестовой среды.

4.  После создания или получения сертификата выберите веб-сайт, к которому применяется сертификат (например, **Веб-сайт по умолчанию**) в области дерева диспетчера служб IIS, а затем щелкните **Привязки** в области **Действия**.

5.  В диалоговом окне **Добавление привязки сайта** добавьте привязку **https** для сайта, если такая привязка еще не отображается. Если вы не используете самозаверяющий сертификат, укажите имя узла из шага 3 данной процедуры. Если вы используете самозаверяющий сертификат, этот шаг не требуется.

6.  Выберите сертификат, полученный или созданный на шаге 3 данной процедуры, и нажмите кнопку **ОК**..

<a href="" id="BKMK_using"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Использование веб-консоли Windows PowerShell</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_5" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

После установки Windows PowerShell Web Access и завершения настройки шлюза, описанной в этой статье, веб-консоль Windows PowerShell готова к использованию. Дополнительные сведения о начале работы с веб-консолью см. в статье [Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)..

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/hh831611(v=ws.11).aspx#Anchor_6" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Документация Internet Information Services (IIS) 7.0](https://technet.microsoft.com/library/cc753433.aspx)
[Справка IIS Manager 7.0](https://technet.microsoft.com/library/cc732664.aspx)
[Настройка безопасности веб-сервера (IIS 7)](https://technet.microsoft.com/library/cc731278.aspx)
[Ресурсы развертывания IPsec](https://technet.microsoft.com/network/bb531150)

<span>Демонстрация: </span> унаследованная защита

<span class="stdr-votetitle">Эта страница была полезной?</span>
Да
Нет

Дополнительные отзывы?

<span class="stdr-count"><span class="stdr-charcnt">Осталось 1500 </span> символов</span>
Отправить
Пропустить

<span class="stdr-thankyou">Спасибо! </span> <span class="stdr-appreciate"> Мы ценим ваши отзывы.</span>

[Управление профилем](https://social.technet.microsoft.com/profile)

|

<a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a>
Отзыв о сайте

<a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a>

Расскажите о своих впечатлениях...

Быстро ли загрузилась страница?

<span> Да <span> </span></span> <span> Нет<span> </span></span>

Вам нравится дизайн страницы?

<span> Да <span> </span></span> <span> Нет<span> </span></span>

Расскажите подробнее

-   [Информационный бюллетень Flash](https://technet.microsoft.com/cc543196.aspx)
-   |
-   [Свяжитесь с нами](https://technet.microsoft.com/cc512759.aspx)
-   |
-   [Заявление о конфиденциальности](https://privacy.microsoft.com/privacystatement)
-   |
-   [Условия использования](https://technet.microsoft.com/cc300389.aspx)
-   |
-   [Товарные знаки](https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/)
-   |

© Корпорация Майкрософт (Microsoft Corporation), 2016 г.

© Корпорация Майкрософт (Microsoft Corporation), 2016 г.

Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющими владельцами такого кода, а не корпорацией Майкрософт. См. условия использования ASP.NET Ajax CDN http://www.asp.net/ajaxlibrary/CDN.ashx.
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />


<!--HONumber=May16_HO2-->


