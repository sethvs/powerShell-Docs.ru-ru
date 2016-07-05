---
title: "Использование веб-консоли Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 03ac4b90d299b316194f1fa932e7dbf62d4b1c8e
ms.openlocfilehash: 02964dd763ccccbf27a963c0f8eef20aa23cc117

---

#  Использование веб-консоли Windows PowerShell

Обновлено: 24 июня 2013 г.

Область применения: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell® Web Access предоставляет пользователям Windows PowerShell® возможность войти на защищенный по технологии SSL веб-сайт, чтобы использовать сеансы, командлеты и сценарии Windows PowerShell для администрирования удаленного компьютера. Поскольку консоль Windows PowerShell выполняется в веб-браузере, ее можно открыть с различных клиентских устройств, включая мобильные телефоны, планшетные компьютеры, общедоступные компьютеры, ноутбуки, общие или арендованные компьютеры. Веб-консоль Windows PowerShell ориентирована на работу с удаленным компьютером, который пользователь указывает в процессе выполнения входа. В этом разделе рассказывается о том, как выполнить вход и приступить к использованию веб-консоли Windows PowerShell Web Access.

Данный раздел не касается способов использования Windows PowerShell или выполнения командлетов или сценариев. Сведения о том, как использовать Windows PowerShell и сценарии, см. в разделе "Дополнительная информация" в конце данного раздела.

Содержание раздела:

-   [Поддерживаемые браузеры и клиентские устройства](#BKMK_browser)

-   [Вход в систему Windows PowerShell Web Access](#BKMK_sign)

-   [Выход из системы и превышение времени ожидания](#BKMK_timeout)

-   [Отличительные особенности веб-консоли Windows PowerShell](#BKMK_web)

<a href="" id="BKMK_browser"></a>
------------------------------------------------------------------------

Windows PowerShell Web Access поддерживает перечисленные ниже браузеры. Хотя браузеры для мобильных устройств официально не поддерживаются, многие из них могут выполнять веб-консоль Windows PowerShell. Ожидается, что другие браузеры, которые принимают куки-файлы, выполняют JavaScript и выполняют веб-сайты HTTPS, также будут работать, но официально они не протестированы.

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

-   Windows Phone 7 и 7.5

-   Google Android WebKit 3.1 Browser Android 2.2.1 (Kernel 2.6)

-   Apple Safari для операционной системы 5.0.1 для iPhone

-   Apple Safari для операционной системы 5.0.1 для iPad 2

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Требования к браузерам</span></a>

------------------------------------------------------------------------

Чтобы использовать веб-консоль Windows PowerShell Web Access, браузеры должны иметь следующие возможности.

-   Разрешать файлы cookie с веб-сайта шлюза Windows PowerShell Web Access.

-   Открывать и читать HTTPS-страницы.

-   Открывать и выполнять веб-сайты, использующие JavaScript.

<a href="" id="BKMK_sign"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Вход в систему Windows PowerShell Web Access</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Администратор Windows PowerShell Web Access должен предоставить вам URL-адрес веб-сайта шлюза Windows PowerShell Web Access для вашей организации. По умолчанию используется следующий адрес веб-сайта: https://&lt;имя\_сервера&gt;/pswa. Прежде чем выполнить вход в Windows PowerShell Web Access, убедитесь, что у вас есть имя или IP-адрес удаленного компьютера, который предполагается администрировать. Вы должны быть полномочным пользователем удаленного компьютера, а компьютер должен быть настроен для удаленного администрирования. Дополнительные сведения о настройке компьютера для удаленного администрирования см. в разделе [Включение и использование удаленных команд в Windows PowerShell](https://technet.microsoft.com/magazine/ff700227.aspx). Настроить компьютер для удаленного администрирования проще всего, выполнив на нем командлет **Enable-PSRemoting -force** в сеансе Windows PowerShell с повышенными привилегиями пользователя (**Запуск от имени администратора**).

### Вход в систему Windows PowerShell Web Access

1.  Откройте веб-сайт Windows PowerShell Web Access в браузере или на вкладке.

2.  На странице входа Windows PowerShell Web Access укажите имя пользователя сети, пароль и имя компьютера, который вы хотите администрировать (вы должны быть полномочным пользователем этого компьютера). Если администратор Windows PowerShell Web Access проинструктировал о необходимости использовать вместо имени компьютера URI-адрес пользовательского сайта или прокси-сервера, выберите **URI подключения** в поле **Тип подключения**, а затем укажите URI.

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
    <td><ul>
    <li><p>Если целевой компьютер входит в рабочую группу, используйте следующий синтаксис, чтобы указать имя пользователя и войти на компьютер: &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em>имя_пользователя</em>&gt;.</p></li>
    <li><p>Если целевой компьютер является сервером шлюза, то в поле <strong>Имя компьютера</strong> можно указать <strong>localhost</strong>.</p></li>
    <li><p>Если целевой компьютер является сервером шлюза и входит в рабочую группу, можно указать <strong>localhost</strong> в поле <strong>Имя компьютера</strong>, но в этом случае нельзя использовать localhost\&lt;<em>имя_пользователя</em>&gt; в поле <strong>Имя пользователя</strong>. Вы должны указать &lt;<em>имя_рабочей_группы</em>&gt;\&lt;<em>имя_пользователя</em>&gt;.</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>

3.  Раздел **Дополнительные параметры подключения** касается требований к проверке подлинности удаленного компьютера, который предполагается администрировать. Дополнительные сведения о параметрах, эквивалентных дополнительным параметрам подключения, см. в разделе [Справка по командлету Enter-PSSession](https://technet.microsoft.com/library/dd315384.aspx).

    Как правило, учетные данные, которые передаются через шлюз Windows PowerShell Web Access, — это те же данные, которые принимаются удаленным компьютером, который предполагается администрировать. Тем не менее, если для администрирования удаленного компьютера, указанного на шаге 2, необходимо использовать другие учетные данные, разверните раздел **Дополнительные параметры подключения** и укажите альтернативные учетные данные. В противном случае переходите к шагу 6.

4.  Если администратор Windows PowerShell Web Access создал пользовательскую конфигурацию сеанса для пользователей Windows PowerShell Web Access, укажите имя данной пользовательской конфигурации в поле **Имя конфигурации**. Дополнительные сведения о конфигурации сеанса см. в разделе [about\_Session\_Configurations](https://technet.microsoft.com/library/dd819508.aspx) на веб-сайте Майкрософт.

5.  Не изменяйте значение **Тип проверки подлинности** (**По умолчанию**), если администратор Windows PowerShell Web Access не выдал вам иные инструкции.

6.  Нажмите кнопку **Войти**.

<a href="" id="BKMK_timeout"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Выход из системы и превышение времени ожидания</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

Любое из следующих действий приводит к завершению сеанса Windows PowerShell.

-   Нажатие кнопки **Выйти** в правом нижнем углу консоли. (только для Windows Server 2012)

-   Нажатие кнопки **Сохранить** или **Выход** в правом нижнем углу консоли (только в Windows Server 2012 R2). При нажатии кнопки **Сохранить** ваш сеанс Windows PowerShell Web Access сохраняется и закрывается; позднее вы можете заново подключиться к этому сеансу. При повторном входе в Windows PowerShell Web Access отображается список сохраненных сеансов; вы можете выбрать сохраненный сеанс и повторно подключиться к нему или начать новый сеанс. Максимальное количество сеансов, как сохраненных, так и активных, которое разрешено открывать пользователю, настраивается администратором шлюза.

    При нажатии кнопки **Выход** вы выходите из сеанса Windows PowerShell Web Access без его сохранения.

-   Попытка войти в систему для администрирования другого удаленного компьютера в том же сеансе браузера или в новой вкладке того же сеанса. (Это не применимо, если сервер шлюза работает под управлением Windows Server 2012 R2; Windows PowerShell Web Access, работающий в Windows Server 2012 R2, разрешает несколько сеансов пользователя в новых вкладках в одном и том же сеансе браузера.) Дополнительные сведения о том, как использовать более одного активного сеанса на одном компьютере см. в пункте "Одновременное подключение к нескольким конечным компьютерам" подраздела [Ограничения веб-консоли](#BKMK_limits) данного раздела.

-   20 минут бездействия в сеансе. Администратор шлюза может изменить время ожидания при бездействии; дополнительные сведения см. в разделе [Управление сеансами](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx#BKMK_sesmgmt).

    -   Если вы отключились от сеанса в веб-консоли в результате сетевых ошибок или другого незапланированного завершения работы или сбоя, а не потому, что сами закрыли свой сеанс, этот сеанс Windows PowerShell Web Access продолжает работать, оставаясь подключенными к целевому компьютеру, пока не истечет время ожидания на стороне клиента. По умолчанию это время ожидания составляет 20 минут и настраивается администратором шлюза. Сеанс отключается после истечения либо 20 минут, установленных по умолчанию, либо времени ожидания, заданного администратором шлюза, в зависимости от того, какой период короче.

        Если сервер шлюза работает под управлением Windows Server 2012 R2, Windows PowerShell Web Access предоставляет пользователям возможность повторного подключения к сохраненным сеансам позднее, но пользователи не смогут увидеть сохраненные сеансы и повторно к ним подключиться, пока не истечет время ожидания, заданное администратором шлюза.

-   Закрытие окна или вкладки браузера.

-   Выключение клиентского устройства, на котором открыт браузер или отключение его от сети.

-   Выполнение команды **Exit** в веб-консоли. Эта команда не действует, если в конфигурации сеанса, которая используется для подключения, настроена поддержка режима [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) или пространство выполнения ограничено.

Если необходимо снова выполнить вход, откройте веб-страницу Windows PowerShell Web Access и войдите, выполняя шаги, описанные в подразделе [Вход в систему Windows PowerShell Web Access](#BKMK_signin) данного раздела.

<a href="" id="BKMK_web"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Отличительные особенности веб-консоли Windows PowerShell</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_3" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

После входа в Windows PowerShell Web в браузер или на вкладке открывается веб-консоль Windows PowerShell. Поскольку консоль подключается к удаленному компьютеру, который вы указали в процессе входа, можно использовать только те командлеты или сценарии Windows PowerShell, которые доступны на удаленном компьютере. В этом разделе описываются другие ограничения консолей Windows PowerShell Web Access, а также различия между консолями Windows PowerShell Web Access и установленной консолью **PowerShell.exe**.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Принципиальные функциональные отличия от PowerShell.exe</span></a>

------------------------------------------------------------------------

Большая часть базового функционала Windows PowerShell доступна в веб-консоли Windows PowerShell Web Access, но некоторые функции все же отсутствуют.

-   <span class="label">Многоуровневое отображение хода выполнения.</span>  Windows PowerShell Web Access отображает элемент управления пользовательского интерфейса "Ход выполнения" для командлетов, которые сообщают о ходе выполнения, но выводится только информация верхнего уровня.

-   <span class="label">Изменение цветов ввода.</span>  Цвета ввода (фоновый и основной) нельзя изменить. Стиль вывода, предупреждения, подробности и сообщения об ошибках можно изменить путем выполнения сценария.

-   <span class="label">PSHostRawUserInterface.</span>  Windows PowerShell Web Access реализуется через удаленное управление Windows PowerShell и использует удаленное пространство выполнения. Windows PowerShell Web Access в своем интерфейсе не реализует ряд методов, например любые команды, осуществляющие запись в консоль Windows. Такие команды как **PowerTab** в Windows PowerShell Web Access не работают.

-   <span class="label">Сочетания клавиш.</span>  Windows PowerShell Web Access не поддерживает некоторые сочетания клавиш, во многих случаях потому, что эти клавиши зарезервированы для команд браузера.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Неподдерживаемые сочетания клавиш</p></th>
<th><p>Действие</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTRL+C</p></td>
<td><p>В Windows PowerShell Web Access для копирования содержимого с помощью браузера используется сочетание клавиш <strong>Ctrl+C</strong>. Для отмены команд в консоли имеется кнопка <strong>Отмена</strong>; кроме этой кнопки пользователи могут использовать клавиши <strong>CTRL+Q</strong>.</p></td>
</tr>
<tr class="even">
<td><p>ALT-ПРОБЕЛ, e, l</p></td>
<td><p>Прокрутка буфера экрана</p></td>
</tr>
<tr class="odd">
<td><p>ALT+ПРОБЕЛ, e, f</p></td>
<td><p>Поиск текста в буфере экрана</p></td>
</tr>
<tr class="even">
<td><p>ALT+ПРОБЕЛ, e, k</p></td>
<td><p>Выбор текста для копирования из буфера экрана</p></td>
</tr>
<tr class="odd">
<td><p>ALT+ПРОБЕЛ, e, p</p></td>
<td><p>Вставка содержимого буфера обмена в консоль Windows PowerShell</p></td>
</tr>
<tr class="even">
<td><p>ALT+ПРОБЕЛ, c</p></td>
<td><p>Закрытие консоли Windows PowerShell</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+BREAK.</p></td>
<td><p>Принудительное закрытие окна Windows PowerShell</p></td>
</tr>
<tr class="even">
<td><p>CTRL+HOME</p></td>
<td><p>Удаление символов с начала текущей командной строки до курсора</p></td>
</tr>
<tr class="odd">
<td><p>CTRL+END</p></td>
<td><p>Удаление символов от курсора до конца командной строки</p></td>
</tr>
<tr class="even">
<td><p>F1</p></td>
<td><p>Перемещение курсора в командной строке на один символ вправо</p></td>
</tr>
<tr class="odd">
<td><p>F2</p></td>
<td><p>Создание новой команды посредством копирования последней команды до текущего символа</p></td>
</tr>
<tr class="even">
<td><p>F3</p></td>
<td><p>Завершение командной строки посредством вставки содержимого последней командной строки</p></td>
</tr>
<tr class="odd">
<td><p>F4</p></td>
<td><p>Удаление символов в позиции курсора</p></td>
</tr>
<tr class="even">
<td><p>F5</p></td>
<td><p>Просмотр введенных ранее команд. Для доступа к введенным ранее командам в Windows PowerShell Web Access нажмите кнопку прокрутки <strong>Журнал</strong> в веб-консоли.</p></td>
</tr>
<tr class="odd">
<td><p>F7</p></td>
<td><p>Интерактивный выбор команд из журнала команд</p></td>
</tr>
<tr class="even">
<td><p>F8</p></td>
<td><p>Просмотр журнала с выводом команд, содержащих текущий текст</p></td>
</tr>
<tr class="odd">
<td><p>F9</p></td>
<td><p>Запуск команды с определенным номером в журнале</p></td>
</tr>
<tr class="even">
<td><p>PAGE UP</p></td>
<td><p>Запуск первой команды в журнале</p></td>
</tr>
<tr class="odd">
<td><p>PAGE DOWN</p></td>
<td><p>Запуск последней команды в журнале</p></td>
</tr>
<tr class="even">
<td><p>ALT+F7</p></td>
<td><p>Очистка списка журнала команд</p></td>
</tr>
</tbody>
</table>

<a href="" id="BKMK_limits"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Ограничения веб-консоли</span></a>

------------------------------------------------------------------------

-   <span class="label">Двойной прыжок.</span>   Вы можете столкнуться с ограничением двойного прыжка (или подключения ко второму компьютеру из первого подключения) при попытке создания нового сеанса с помощью Windows PowerShell Web Access или работы в нем. Windows PowerShell Web Access использует удаленное пространство выполнения, и на данный момент **PowerShell.exe** не поддерживает установление удаленного подключения ко второму компьютеру из удаленного пространства выполнения. При попытке подключиться ко второму удаленному компьютеру из существующего подключения, например с помощью командлета **Enter-PSSession**, возможно возникновение различных ошибок типа "Не удается получить сетевые ресурсы".

    Чтобы избежать ошибок двойного подключения, администратор должен настроить в сетевой среде организации проверку подлинности CredSSP. Дополнительные сведения о настройке проверки подлинности CredSSP см. в разделе [CredSSP для двойного удаленного подключения](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) веб-сайта Майкрософт. Кроме того, можно также явно указать учетные данные для администрирования второго удаленного компьютера; неявное указание учетных данных для двойного подключения вряд ли позволит выполнить второе подключение.

-   В Windows PowerShell Web Access используются и действуют те же ограничения, как и в удаленном сеансе Windows PowerShell. Команды, которые напрямую вызывают API консоли Windows, например команды для консольных редакторов или программы текстовых меню, не действуют, поскольку эти команды не могут выполнять чтение или запись в стандартный ввод, вывод и каналы ошибок. Следовательно, команды, запускающие исполняемые файлы, например **notepad.exe**, или отображающие графический интерфейс пользователя, например <span class="code">OpenGridView</span> или <span class="code">ogv</span>, также не работают. Это поведение влияет на взаимодействие с пользователем; создается впечатление, что Windows PowerShell Web Access не реагирует на команды.

-   Заполнение нажатием клавиши TAB не действует в сеансах, сконфигурированных для работы в ограниченном пространстве выполнения или в режиме **NoLanguage**. Хотя администраторы могут настроить поддержку заполнения клавишей TAB для сеанса, этого не рекомендуется делать из соображений безопасности, потому что случайный пользователь сможет получить несанкционированный доступ к следующим сведениям.

    -   Внутренние пути файловой системы

    -   Общие папки на внутренних компьютерах

    -   Переменные в пространстве выполнения

    -   Загруженные типы пространств имен или пространства имен .NET Framework

    -   Переменные среды

-   Пользователи, выполнившие вход в конфигурацию сеанса **NoLanguage** или в ограниченное пространство выполнения в Windows PowerShell Web Access, не могут запустить команду **Exit** для завершения сеанса. Для выхода такие пользователи должны нажать кнопку **Выйти** на странице консоли.

-   <span class="label">Одновременное подключение к нескольким целевым компьютерам.</span>   Если сервер шлюза работает под управлением Windows Server 2012, Windows PowerShell Web Access разрешает только одно подключение к удаленному компьютеру в одном сеансе браузера; пользователям не разрешается выполнить один вход и подключиться к нескольким удаленным компьютерам, используя отдельные вкладки браузера. Если вы откроете новую вкладку или новое окно браузера, Windows PowerShell Web Access предложит вам завершить текущий сеанс и начать новый, чтобы обеспечить возможность подключения к новому (или тому же) удаленному компьютеру. Если все же желательно запустить два или более отдельных сеансов для разных удаленных компьютеров, в Internet Explorer есть средство, с помощью которого можно начать новый сеанс. Чтобы начать новый сеанс браузера в Internet Explorer, нажмите клавишу **ALT**, откройте меню **Файл**, а затем выберите **Новый сеанс**. Затем откройте веб-сайт Windows PowerShell Web Access в этом новом сеансе и выполните вход, чтобы получить доступ к другому удаленному компьютеру.

    Если шлюз Windows PowerShell Web Access работает под управлением Windows Server 2012 R2, пользователи могут открывать несколько подключений к удаленным компьютерам на разных вкладках браузера. Если вы хотите открыть несколько подключений к удаленному компьютеру с помощью веб-консоли Windows PowerShell, узнайте у вашего администратора шлюза Windows PowerShell Web Access, поддерживается ли эта функциональность сервером шлюза.

-   <span class="label">Постоянные сеансы Windows PowerShell (повторное подключение).</span>   После истечения времени ожидания шлюза Windows PowerShell Web Access удаленное подключение между шлюзом и целевым компьютером закрывается. При этом прекращается выполнение всех командлетов или сценариев. При выполнении продолжительных задач рекомендуется использовать инфраструктуру **-Job** Windows PowerShell, чтобы можно было запустить задания, отключиться от компьютера, а затем снова подключиться без прекращения выполнения заданий. Другое преимущество использования командлетов **-Job** состоит в том, что их можно запустить с помощью Windows PowerShell Web Access, выйти из системы и подключиться снова, запустив Windows PowerShell Web Access или другой узел (например, интегрированную среду сценариев (ISE) Windows PowerShell®).

-   <span class="label">Изменение размеров окна консоли.</span>   Размеры окна консоли **PowerShell.exe** можно изменить следующими тремя способами.

    -   Отрегулировать размер окна консоли при помощи мыши.

    -   Изменить свойства "высота" и "ширина" при помощи пользовательского интерфейса для изменения свойств консоли.

    -   Изменить высоту и ширину окна консоли при помощи командлета.

        Далее показано, как настроить окно консоли для Windows PowerShell Web Access при помощи командлетов. В следующем примере пользователь изменяет ширину окна консоли Windows PowerShell Web Access до **20**.

        [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_778d5e55-9195-4bd7-b313-d1fbca7876e4'); "Копировать в буфер обмена".)

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        Таким же способом изменяется высота окна консоли.

        Дополнительные примеры по настройке внешнего вида консоли доступны в [блоге группы Windows PowerShell](http://blogs.msdn.com/b/powershell/).

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/hh831417(v=ws.11).aspx#Anchor_4" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Справочник по командлетам Windows PowerShell](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
[Windows PowerShell в Microsoft TechNet](https://technet.microsoft.com/library/bb978526.aspx)
[Репозиторий центра сценариев TechNet](http://gallery.technet.microsoft.com/scriptcenter)
[Центр сценариев — эй, сценарист!](https://technet.microsoft.com/scriptcenter)
[Блог группы Windows PowerShell](http://blogs.msdn.com/b/powershell/)

<span>Демонстрация: </span> унаследованная защита

<span class="stdr-votetitle">Эта страница была полезной?</span>
Да Нет

Дополнительные отзывы?

<span class="stdr-count"><span class="stdr-charcnt">Осталось 1500</span> символов</span> Отправить Пропустить

<span class="stdr-thankyou">Спасибо!</span> <span class="stdr-appreciate">Мы ценим ваши отзывы.</span>

[Управление профилем](https://social.technet.microsoft.com/profile)

|

<a href="javascript:void(0)" id="SiteFeedbackLinkOpener"><span id="FeedbackButton" class="FeedbackButton clip20x21"> <img src="https://i-technet.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635975720914499532" alt="Site Feedback" id="feedBackImg" class="cl_footer_feedback_icon" /> </span> Отзыв о сайте</a> Отзыв о сайте

<a href="javascript:void(0)" id="SiteFeedbackLinkCloser">x</a>

Расскажите о своих впечатлениях...

Быстро ли загрузилась страница?

<span> Да<span> </span></span> <span> Нет<span> </span></span>

Вам нравится дизайн страницы?

<span> Да<span> </span></span> <span> Нет<span> </span></span>

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




<!--HONumber=Jun16_HO4-->


