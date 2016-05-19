#  Удаление Windows PowerShell Web Access

Обновлено: 24 июня 2013 г.

Область применения: Windows Server 2012 R2, Windows Server 2012

Выполните процедуры в этом разделе, чтобы удалить веб-сайт и приложение Windows PowerShell Web Access с сервера шлюза, который работает под управлением Windows Server 2012 R2 или Windows Server 2012. Прежде чем начать, известите пользователей веб-консоли, что вы удаляете веб-сайт.

<a href="" id="BKMK_uninstall"></a>

------------------------------------------------------------------------

Перед удалением Windows PowerShell Web Access с сервера шлюза выполните командлет <span class="code">Uninstall-PswaWebApplication</span>, чтобы удалить веб-сайт и веб-приложения Windows PowerShell Web Access, или используйте процедуру диспетчера служб IIS [Удаление веб-сайта и веб-приложений Windows PowerShell Web Access](#BKMK_delsite)..

Удаление Windows PowerShell Web Access не приводит к удалению IIS или любых других компонентов, которые были установлены автоматически, поскольку они требуются для выполнения Windows PowerShell Web Access. В процессе удаления остаются установленными компоненты, от которых зависит Windows PowerShell Web Access. Вы можете удалить эти компоненты при необходимости.

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Рекомендуемое (быстрое) удаление</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

В этом разделе приводятся процедуры для удаления веб-приложения Windows PowerShell Web Access и компонента Windows PowerShell Web Access с помощью командлетов Windows PowerShell.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Удаление веб-приложения</span></a>

------------------------------------------------------------------------

Если вы задали настраиваемое имя веб-сайта, добавьте параметр <span class="code">WebsiteName</span> в команду и укажите имя веб-сайта. Если использовалось настраиваемое веб-приложение (не приложение **pswa** по умолчанию), добавьте параметр <span class="code">WebApplicationName</span> в команду и укажите имя веб-приложения.

#### Удаление веб-сайта и веб-приложений с помощью командлета Uninstall-PswaWebApplication

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач.

    -   На экране **Пуск** Windows щелкните **Windows PowerShell**..

2.  Введите **Uninstall-PswaWebApplication** и нажмите клавишу **ВВОД**..

3.  Если используется тестовый сертификат, добавьте в командлет параметр <span class="code">DeleteTestCertificate</span>, как показано в следующем примере.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_28147344-ab2f-49e7-b1c2-6dbe649d4366'); "Копировать в буфер обмена".)

        Uninstall-PswaWebApplication -DeleteTestCertificate

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Удаление Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### Удаление Windows PowerShell Web Access с помощью командлетов Windows PowerShell

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами. Если сеанс уже открыт, переходите к следующему шагу.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**..

    -   На экране **Пуск** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем щелкните **Запустить от имени администратора**..

2.  Введите следующую команду и нажмите клавишу **ВВОД**, где *computer_name* представляет удаленный сервер, с которого требуется удалить Windows PowerShell Web Access. Параметр <span class="code">–Restart</span> автоматически перезапускает целевые серверы, если это требуется при удалении.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_7b534520-f292-471f-89e3-a1079c03e369'); "Копировать в буфер обмена".)

        Uninstall-WindowsFeature –Name WindowsPowerShellWebAccess -ComputerName <computer_name> -Restart

    Чтобы удалить роли и компоненты с автономного виртуального жесткого диска (VHD), необходимо добавить оба параметра — <span class="code">-ComputerName</span> и <span class="code">-VHD</span>. Параметр <span class="code">-ComputerName</span> содержит имя сервера, на котором следует подключить виртуальный жесткий диск, а параметр <span class="code">-VHD</span> — путь к VHD-файлу на указанном сервере.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_5d8f91ee-b91a-4653-b7df-e745187fd72d'); "Копировать в буфер обмена".)

        Uninstall-WindowsFeature –Name WindowsPowerShellWebAccess –VHD <path> -ComputerName <computer_name> -Restart

3.  После завершения удаления Windows PowerShell Web Access откройте для проверки страницу **Все серверы** в диспетчере серверов, выберите сервер, с которого был удален компонент, и просмотрите плитку **Роли и компоненты** на странице для выбранного сервера. Можно также выполнить командлет <span class="code">Get-WindowsFeature</span>, адресованный выбранному серверу (Get-WindowsFeature -ComputerName &lt;*имя_компьютера*&gt;), чтобы просмотреть список ролей и компонентов, установленных на сервере.

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Настраиваемое удаление</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

В этом разделе приводятся процедуры для удаления веб-приложения Windows PowerShell Web Access и компонента Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов в диспетчере серверов и на консоли диспетчера служб IIS.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 1. Удаление веб-приложения</span></a>

------------------------------------------------------------------------

#### Удаление веб-сайта Windows PowerShell Web Access и веб-приложений с помощью диспетчера служб IIS

1.  Откройте консоль "Диспетчер служб IIS", выполнив одно из следующих действий. Если консоль уже открыта, переходите к следующему шагу.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows. В диспетчере серверов откройте меню **Сервис** и выберите пункт **Диспетчер служб IIS**..

    -   На **начальном** экране Windows введите любую часть имени **Диспетчер служб IIS**. Щелкните ярлык, когда он появится в списке результатов **Приложения**.

2.  В области дерева диспетчера служб IIS выберите веб-сайт, на котором выполняется веб-приложение Windows PowerShell Web Access.

3.  В области **Действия** в разделе **Управление веб-сайтом** щелкните **Остановить**..

4.  В области дерева щелкните правой кнопкой мыши веб-приложение на веб-сайте, на котором выполняется веб-приложение Windows PowerShell Web Access, а затем щелкните **Удалить**..

5.  В области дерева выберите **Пулы приложений**, выберите папку пула приложений Windows PowerShell Web Access, щелкните **Остановить** в области **Действия**, а затем щелкните **Удалить** в области содержимого.

6.  Закройте диспетчер IIS.

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
    <td><p>Сертификат не удаляется при этой операции удаления. Если вы создали самозаверяющий сертификат или использовали тестовый сертификат и хотите удалить его, удалите сертификат в диспетчере служб IIS.</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Шаг 2. Удаление Windows PowerShell Web Access</span></a>

------------------------------------------------------------------------

#### Удаление Windows PowerShell Web Access с помощью мастера удаления ролей и компонентов

1.  Если диспетчер серверов уже открыт, переходите к следующему шагу. Если диспетчер серверов еще не открыт, откройте его одним из следующих способов.

    -   На рабочем столе Windows запустите диспетчер серверов, щелкнув **Диспетчер серверов** на панели задач Windows.

    -   На **начальном** экране в Windows выберите **Диспетчер серверов**..

2.  В меню **Управление** выберите команду **Удалить роли и компоненты**..

3.  На странице **Выбор целевого сервера** выберите сервер или виртуальный жесткий диск, с которого следует удалить компонент. Чтобы выбрать автономный виртуальный жесткий диск, сначала выберите сервер, на котором будет подключен виртуальный жесткий диск, а затем выберите VHD-файл. Выбрав конечный сервер, нажмите кнопку **Далее**..

4.  Еще раз щелкните **Далее**, чтобы пропустить страницу **Удаление компонентов**.

5.  Снимите флажок **Windows PowerShell Web Access** и щелкните **Далее**..

6.  На странице **Подтверждение выборов для удаления** щелкните **Удалить**..

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/dn282396(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Установка и использование Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[Справка IIS Manager 7.0](https://technet.microsoft.com/library/cc732664.aspx)

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

Сторонние сценарии или код, на которые ссылается этот сайт, предоставляются вам по лицензии третьими лицами, являющимися владельцами такого кода, а не корпорацией Майкрософт. См. условия использования ASP.NET Ajax CDN http://www.asp.net/ajaxlibrary/CDN.ashx.
<img src="https://m.webtrends.com/dcsjwb9vb00000c932fd0rjc7_5p3t/njs.gif?dcsuri=/nojavascript&amp;WT.js=No" alt="DCSIMG" id="Img1" width="1" height="1" />


<!--HONumber=May16_HO2-->


