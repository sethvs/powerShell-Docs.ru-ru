#  Устранение неполадок с доступом в Windows PowerShell Web Access

Обновлено: 24 июня 2013 г.

Область применения: Windows Server 2012 R2, Windows Server 2012

<a href="" id="BKMK_trouble"></a>

------------------------------------------------------------------------

В следующей таблице перечислены часто возникающие проблемы пользователей при попытках подключения к удаленному компьютеру с помощью Windows PowerShell Web Access и предложения по разрешению таких проблем.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Проблема</p></th>
<th><p>Возможная причина и решение</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Сбой при входе</p></td>
<td><p>Сбой может возникать по любой из следующих причин.</p>
<ul>
<li><p>Отсутствуют правило авторизации, которое позволяет пользователю получить доступ к компьютеру, или конкретная конфигурация сеанса на удаленном компьютере. Безопасность Windows PowerShell Web Access является ограничивающей. Пользователям необходимо явным образом предоставлять доступ к удаленным компьютерам с помощью правил авторизации. Дополнительные сведения о создании правил авторизации см. в разделе <a href="https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx">Правила авторизации и средства безопасности Windows PowerShell Web Access</a> данного руководства.</p></li>
<li><p>У пользователя отсутствует авторизованный доступ к целевому компьютеру. Это определяется списками управления доступом. Дополнительные сведения см. в разделе "Вход в Windows PowerShell Web Access" в статье <a href="https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx">Использование веб-консоли Windows PowerShell</a> или в <a href="https://msdn.microsoft.com/library/windows/desktop/ee706585.aspx">блоге группы разработчиков для Windows PowerShell.</a>.</p>
<ul>
<li><p>Возможно, удаленное управление Windows PowerShell не включено на целевом компьютере. Убедитесь, что оно включено на компьютере, к которому пытается подключиться пользователь. Дополнительные сведения см. в разделе "Инструкции по настройке удаленных операций" в описании <a href="https://technet.microsoft.com/library/dd315349.aspx">about_Remote_Requirements</a> в разделах справки "О программе" Windows PowerShell.</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td><p>При попытке войти в Windows PowerShell Web Access в окне Internet Explorer пользователи видят страницу <strong>Внутренняя ошибка сервера</strong> или Internet Explorer перестает реагировать на запросы. Эта проблема специфична для Internet Explorer.</p></td>
<td><p>Она может возникнуть, если пользователь вошел в систему с именем домена, содержащим китайские символы, или если такие символы встречаются в имени сервера шлюза. Чтобы обойти эту проблему, пользователю нужно <a href="http://ie.microsoft.com/testdrive/info/downloads/Default.html">установить и запустить Internet Explorer 10</a>, а затем выполнить следующие действия.</p>
<ol>
<li><p>Заменить <strong>Режим документов</strong> в Internet Explorer на <strong>Стандарты IE10.</strong>.</p>
<ol>
<li><p>Нажать клавишу <strong>F12</strong>, чтобы открыть консоль "Средства разработчика".</p></li>
<li><p>В Internet Explorer 10 щелкнуть <strong>Режим браузера</strong> и выбрать <strong>Internet Explorer 10.</strong>.</p></li>
<li><p>Щелкнуть <strong>Режим документов</strong> и выбрать <strong>Стандарты IE10.</strong>.</p></li>
<li><p>Снова нажать клавишу <strong>F12</strong>, чтобы закрыть консоль "Средства разработчика".</p></li>
</ol></li>
<li><p>Отключить автоматическую конфигурацию прокси.</p>
<ol>
<li><p>В Internet Explorer 10 в меню <strong>Сервис</strong> выбрать <strong> Свойства браузера.</strong>.</p></li>
<li><p>В диалоговом окне <strong>Свойства браузера</strong> на вкладке <strong>Подключения</strong> выбрать <strong> Настройка сети.</strong>.</p></li>
<li><p>Снять флажок <strong>Автоматическое определение параметров</strong>. Нажать кнопку <strong>ОК</strong>, а затем нажать кнопку <strong>ОК</strong> еще раз, чтобы закрыть диалоговое окно <strong>Свойства браузера</strong>.</p></li>
</ol></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Невозможно подключиться к удаленному компьютеру в рабочей группе</p></td>
<td><p>Если целевой компьютер входит в рабочую группу, используйте следующий синтаксис, чтобы указать имя пользователя и войти на компьютер: &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em> имя_пользователя.</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>Невозможно найти инструменты управления веб-сервера (IIS), даже если роль была установлена</p></td>
<td><p>Если вы установили Windows PowerShell Web Access с помощью командлета <span class="code">Install-WindowsFeature</span>, средства управления не устанавливаются, если к командлету добавлен параметр <span class="code">IncludeManagementTools</span>. Например, см. раздел "Установка Windows PowerShell Web Access с помощью командлетов Windows PowerShell" в статье <a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">Установка и использование Windows PowerShell Web Access</a>. Вы можете добавить консоль диспетчера служб IIS и другие нужные инструменты управления IIS, выбрав инструменты в сеансе мастера добавления ролей и функций, который нацелен на сервер шлюза. Мастер добавления ролей и функций открывается из диспетчера сервера.</p></td>
</tr>
<tr class="odd">
<td><p>Веб-сайт Windows PowerShell Web Access недоступен</p></td>
<td><p>Если включена конфигурация повышенной безопасности в Internet Explorer (IE ESC), можно добавить веб-сайт Windows PowerShell Web Access в список надежных сайтов или отключить IE ESC. Отключить IE ESC можно с помощью плитки <strong>Свойства</strong> на странице <strong>Локальный сервер</strong> в диспетчере серверов.</p></td>
</tr>
<tr class="even">
<td><p>Если сервер шлюза является конечным компьютером и в то же время входит в рабочую группу, при попытке соединения выводится следующее сообщение об ошибке: <strong> Произошел сбой авторизации. Убедитесь, что вы имеете права на подключение к конечному компьютеру.</strong></p></td>
<td><p>Когда сервер шлюза также является конечным сервером и входит в рабочую группу, укажите имя пользователя, имя компьютера и имя группы пользователей, как показано в следующей таблице. Не используйте точку (.) в качестве имени компьютера.</p>
<div>
<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Сценарий</p></th>
<th><p>Параметр UserName</p></th>
<th><p>Параметр UserGroup</p></th>
<th><p>Параметр ComputerName</p></th>
<th><p>Параметр ComputerGroup</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Сервер шлюза входит в домен</p></td>
<td><p><em>Имя_сервера </em>\<em>имя_пользователя</em>, Localhost\<em>имя_пользователя</em> или .\<em>имя_пользователя</em></p></td>
<td><p><em>Имя_сервера </em>\<em>группа_пользователей</em>, Localhost\<em>группа_пользователей</em> или .\<em>группа_пользователей</em></p></td>
<td><p>Полное имя сервера шлюза или Localhost</p></td>
<td><p><em>Имя_сервера </em>\<em>группа_компьютеров</em>, Localhost\<em>группа_компьютеров</em> или .\<em>группа_компьютеров</em></p></td>
</tr>
<tr class="even">
<td><p>Сервер шлюза входит в рабочую группу</p></td>
<td><p><em>Имя_сервера </em>\<em>имя_пользователя</em>, Localhost\<em>имя_пользователя</em> или .\<em>имя_пользователя</em></p></td>
<td><p><em>Имя_сервера </em>\<em>группа_пользователей</em>, Localhost\<em>группа_пользователей</em> или .\<em>группа_пользователей</em></p></td>
<td><p>Имя сервера</p></td>
<td><p><em>Имя_сервера </em>\<em>группа_компьютеров</em>, Localhost\<em>группа_компьютеров</em> или .\<em>группа_компьютеров</em></p></td>
</tr>
</tbody>
</table>
</div>
<p>Войдите на сервер шлюза как на конечный компьютер, используя учетные данные в одном из следующих форматов.</p>
<ul>
<li><p><em>Имя_сервера </em>\<em> имя_пользователя</em></p></li>
<li><p>Localhost\<em>имя_пользователя</em></p></li>
<li><p>.\<em>имя_пользователя</em></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Вместо синтаксиса <em>имя_пользователя</em>/<em> computer_name в правиле авторизации отображается идентификатор безопасности (SID)</em> </p></td>
<td><p>Либо правило больше не действительно, либо произошла ошибка запроса к доменным службам Active Directory. Правило авторизации недействительно обычно в том случае, если сервер шлюза когда-то входил в рабочую группу, но позднее был присоединен к домену.</p></td>
</tr>
<tr class="even">
<td><p>Не удается войти на конечный компьютер, указанный в правилах авторизации под IPv6-адресом с доменом.</p></td>
<td><p>Правила авторизации не поддерживают IPv6-адреса в форме имени домена. Чтобы указать конечный компьютер с помощью IPv6-адреса, используйте в правиле авторизации исходный IPv6-адрес (содержащий двоеточия). IPv6-адреса в форме имени домена и в числовой форме (с двоеточиями) поддерживаются в качестве имени конечного компьютера на странице входа в Windows PowerShell Web Access, но не в правилах авторизации. Дополнительные сведения об IPv6-адресах см. в статье <a href="https://technet.microsoft.com/library/cc781672.aspx"> Принципы работы IPv6</a>.</p></td>
</tr>
</tbody>
</table>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/dn282395(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Правила авторизации и средства безопасности Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
[Использование веб-консоли Windows PowerShell](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
[about\_Remote\_Requirements](https://technet.microsoft.com/library/dd315349.aspx)

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


