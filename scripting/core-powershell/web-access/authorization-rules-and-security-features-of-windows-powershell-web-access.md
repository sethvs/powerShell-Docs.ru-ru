# Правила авторизации и средства безопасности Windows PowerShell Web Access

Обновлено: 24 июня 2013 г.

Область применения: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell® Web Access в Windows Server® 2012 R2 и Windows Server® 2012 имеет ограничительную модель безопасности. Пользователям необходимо явно предоставить доступ, прежде чем они смогут входить в шлюз Windows PowerShell Web Access и использовать веб-консоль Windows PowerShell.

-   [Настройка правил авторизации и безопасности сайта](#BKMK_auth)

-   [Управление сеансом](#BKMK_sesmgmt)


После установки Windows PowerShell Web Access и настройки шлюза пользователи могут открывать страницу входа в браузере, но они не могут выполнить вход, пока администратор Windows PowerShell Web Access не предоставит им доступ в явном виде. Управление доступом в Windows PowerShell Web Access осуществляется с помощью набора командлетов Windows PowerShell, описанных в следующей таблице. Нет соответствующего графического пользовательского интерфейса для добавления правил авторизации или управления ими. Подробные сведения о командлетах Windows PowerShell Web Access см. в справочных разделах по командлетам [Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx)..

Администратор может определить 0-*n* правил проверки подлинности для Windows PowerShell Web Access или не определять их. Безопасность по умолчанию является ограничивающей, а не разрешающей. Отсутствие правил проверки подлинности означает, что ни один пользователь не имеет доступа к чему-либо.

Командлеты Add-PswaAuthorizationRule и Test-PswaAuthorizationRule в Windows Server 2012 R2 включают параметр Credential, который позволяет вам добавлять правила авторизации Windows PowerShell Web Access и тестировать их с удаленного компьютера или в активном сеансе Windows PowerShell Web Access. Как и при работе с другими командлетами Windows PowerShell, которые имеют параметр Credential, вы можете указать объект PSCredential в качестве значения этого параметра. Чтобы создать объект PSCredential, содержащий учетные данные, которые требуется передать на удаленный компьютер, выполните командлет [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx).

Правила проверки подлинности Windows PowerShell Web Access — это правила белого списка. Каждое правило является определением разрешенных подключений между пользователями, целевыми компьютерами и конкретными [конфигурациями сеансов](https://technet.microsoft.com/library/dd819508.aspx) Windows PowerShell (которые также называют конечными точками или пространствами выполнения) на указанных целевых компьютерах.

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
<td><p>Для получения доступа пользователю требуется, чтобы удовлетворялось хотя бы одно правило. Если пользователю предоставлен доступ с веб-консоли к одному компьютеру либо с полными языковыми правами, либо доступ только к командлетам удаленного управления Windows PowerShell, пользователь может войти (или перескочить) на другие компьютеры, подключенные к первому целевому компьютеру. Самым безопасным способом настройки Windows PowerShell Web Access является предоставление пользователям доступа только к ограниченным конфигурациям сеансов (которые также называют конечными точками или пространствами выполнения), в которых им разрешается выполнять только конкретные задачи, требующие удаленного выполнения.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Название</p></th>
<th><p>Описание</p></th>
<th><p>Параметры</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/library/jj592890.aspx">Add-PswaAuthorizationRule</a></p></td>
<td><p>Добавляет новое правило авторизации в набор правил авторизации Windows PowerShell Web Access.</p></td>
<td><ul>
<li><p>ComputerGroupName</p></li>
<li><p>имя_компьютера</p></li>
<li><p>ConfigurationName</p></li>
<li><p>RuleName</p></li>
<li><p>UserGroupName</p></li>
<li><p>UserName</p></li>
<li><p>Учетные данные (Windows Server 2012 R2 или более поздней версии)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/library/jj592893.aspx">Remove-PswaAuthorizationRule</a></p></td>
<td><p>Удаляет указанное правило авторизации из Windows PowerShell Web Access.</p></td>
<td><ul>
<li><p>Id</p></li>
<li><p>RuleName</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/library/jj592891.aspx">Get-PswaAuthorizationRule</a></p></td>
<td><p>Возвращает набор правил авторизации Windows PowerShell Web Access. При использовании без параметров командлет возвращает все правила.</p></td>
<td><ul>
<li><p>Id</p></li>
<li><p>RuleName</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/library/jj592892.aspx">Test-PswaAuthorizationRule</a></p></td>
<td><p>Проверяет правила авторизации, чтобы определить, являются ли авторизованными конкретный пользователь, компьютер или запрос на доступ к конфигурации сеанса. Если не добавлен ни один параметр, командлет по умолчанию проверяет все правила авторизации. Добавляя параметры, администраторы могут указать правило авторизации или подмножество правил для проверки.</p></td>
<td><ul>
<li><p>имя_компьютера</p></li>
<li><p>ConfigurationName</p></li>
<li><p>RuleName</p></li>
<li><p>UserName</p></li>
<li><p>Учетные данные (Windows Server 2012 R2 или более поздней версии)</p></li>
</ul></td>
</tr>
</tbody>
</table>

Предыдущие командлеты создают набор правил доступа, которые используются для авторизации пользователя на шлюзе Windows PowerShell Web Access. Правила отличаются от списков управления доступом на целевом компьютере и обеспечивают дополнительный уровень безопасности при доступе через Интернет. Дополнительные сведения о безопасности приводятся в следующем разделе.

Если пользователи не могут пройти какой-либо из предшествующих уровней безопасности, они получают универсальное сообщение "отказ в доступе" в окнах своих браузеров. Хотя подробные сведения о безопасности записываются в журнал на сервере шлюза, конечным пользователям не предоставляется информация о том, сколько уровней безопасности они прошли или на каком уровне был получен отказ на вход или авторизацию.

Дополнительные сведения о настройке правил авторизации см. в разделе [Настройка правил авторизации](#BKMK_configrules) в этой статье.

<a href="" id="BKMK_sec"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Безопасность</span></a>

------------------------------------------------------------------------

В модели безопасности Windows PowerShell Web Access имеется четыре уровня между пользователем веб-консоли и целевым компьютером. Администраторы Windows PowerShell Web Access могут добавлять уровни безопасности с помощью дополнительной настройки в диспетчере служб IIS. Дополнительные сведения о настройке безопасности веб-сайтов в консоли диспетчера служб IIS см. в статье [Настройка безопасности веб-сервера (IIS 7)](https://technet.microsoft.com/library/cc731278(v=ws.10).aspx). Дополнительные рекомендации для IIS и сведения о предотвращении атак типа "отказ в доступе" см. в статье [Рекомендации по предотвращению атак типа "отказ в доступе"](https://technet.microsoft.com/library/cc750213.aspx). Администратор также может купить дополнительное розничное программное обеспечение для проверки подлинности.

В следующей таблице описаны четыре уровня безопасности между конечными пользователями и целевыми компьютерами.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Порядок</p></th>
<th><p>Уровень</p></th>
<th><p>Описание</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>Компоненты безопасности веб-сервера (IIS), такие как проверка подлинности сертификатов клиента</p></td>
<td><p>Пользователи Windows PowerShell Web Access всегда должны указывать имя пользователя и пароль для проверки подлинности своих учетных записей на шлюзе. Однако администраторы Windows PowerShell Web Access могут также включать или отключать дополнительную проверку подлинности сертификата клиента (см. шаг 10 процедуры "Использование диспетчера служб IIS для настройки шлюза на существующем веб-сайте" в разделе <a href="https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx">Установка и использование Windows PowerShell Web Access</a>). Дополнительный компонент сертификата клиента, который является частью конфигурации веб-сервера (IIS), требует, чтобы конечные пользователи имели действительный сертификат клиента в дополнение к имени пользователя и паролю. Когда уровень сертификата клиента включен, на странице входа Windows PowerShell Web Access выводится приглашение пользователям предоставить действительные сертификаты перед проверкой их учетных данных для входа. При проверке подлинности сертификата клиента автоматически проверяется наличие сертификата клиента.</p>
<p>Если действительный сертификат не обнаружен, Windows PowerShell Web Access информирует пользователя о необходимости предоставить сертификат. Если действительный сертификат клиента обнаружен, Windows PowerShell Web Access открывает страницу входа для ввода имени пользователя и пароля.</p>
<p>Это один из примеров дополнительных параметров безопасности, которые предоставляет веб-сервер (IIS). Дополнительные сведения о других средствах безопасности IIS см. в статье <a href="https://technet.microsoft.com/library/cc731278(ws.10).aspx"> Настройка безопасности веб-сервера (IIS 7).</a>.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>Проверка подлинности шлюза Windows PowerShell Web Access на основании форм</p></td>
<td><p>Страница входа Windows PowerShell Web Access требует указать набор учетных данных (имя пользователя и пароль) и предлагает возможность указать другие учетные данные для целевого компьютера. Если пользователь не предоставил дополнительные учетные данные, основные имя пользователя и пароль, использованные для подключения к шлюзу, также используются для подключения к целевому компьютеру.</p>
<p>Подлинность требуемых учетных данных проверяется на шлюзе Windows PowerShell Web Access. Эти учетные данные должны представлять действительные учетные записи пользователей на локальном сервере шлюза Windows PowerShell Web Access или в Active Directory®.</p>
<p>После проверки подлинности пользователя на шлюзе Windows PowerShell Web Access проверяет правила авторизации, чтобы удостовериться, что у пользователя имеется доступ к целевому компьютеру. После успешной авторизации учетные данные пользователя передаются на целевой компьютер.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>Правила авторизации Windows PowerShell Web Access</p></td>
<td><p>После проверки подлинности пользователя на шлюзе Windows PowerShell Web Access проверяет правила авторизации, чтобы удостовериться, что у пользователя имеется доступ к целевому компьютеру. После успешной авторизации учетные данные пользователя передаются на целевой компьютер.</p>
<p>Эти правила проверяются только после проверки подлинности пользователя на шлюзе и перед проверкой подлинности пользователя на целевом компьютере.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>Проверка подлинности на целевом компьютере и правила авторизации</p></td>
<td><p>Конечным уровнем безопасности Windows PowerShell Web Access является собственная конфигурация безопасности целевого компьютера. Пользователи должны иметь достаточные права доступа, настроенные на целевом компьютере, а также в правилах авторизации Windows PowerShell Web Access, чтобы выполнять веб-консоль Windows PowerShell, которая взаимодействует с целевым компьютером через Windows PowerShell Web Access.</p>
<p>Этот уровень обеспечивает такие же механизмы безопасности, как и при проверке попыток подключения, когда пользователь пытается создать удаленный сеанс Windows PowerShell с целевым компьютером из Windows PowerShell, выполняя командлет <strong>Enter-PSSession</strong> или <strong>New-PSSession</strong>.</p>
<p>По умолчанию Windows PowerShell Web Access использует основное имя пользователя и пароль для проверки подлинности и на шлюзе, и на целевом компьютере. На веб-странице входа в разделе <strong>Дополнительные параметры подключения</strong> пользователям предлагается возможность указать другие учетные данные для целевого компьютера, если они требуются. Если пользователь не предоставил дополнительные учетные данные, основные имя пользователя и пароль, использованные для подключения к шлюзу, также используются для подключения к целевому компьютеру.</p>
<p>Правила авторизации можно использовать, чтобы разрешить доступ пользователей к конкретным конфигурациям сеанса. Можно создать ограниченные пространства выполнения или конфигурации сеансов для Windows PowerShell Web Access и разрешить конкретным пользователям подключаться только к определенным конфигурациям сеанса при входе в Windows PowerShell Web Access. Можно использовать списки управления доступом, чтобы определить, какие пользователи имеют доступ к конкретным конечным точкам, и далее ограничить доступ к конечной точке с помощью правил авторизации, описанных в данном разделе. Дополнительные сведения об ограничении доступа к пространствам выполнения см. в статье <a href="https://msdn.microsoft.com/library/windows/desktop/ee706589.aspx">Ограниченные пространства выполнения</a> в сети MSDN.</p></td>
</tr>
</tbody>
</table>

<a href="" id="BKMK_configrules"></a>
###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Настройка правил авторизации</span></a>

------------------------------------------------------------------------

Администраторам, вероятно, могут потребоваться для пользователей Windows PowerShell Web Access такие же правила авторизации, как и те, что определены в их среде для удаленного управления Windows PowerShell. В первой процедуре в этом разделе описано, как добавить правило авторизации для безопасности, предоставляющее одному пользователю доступ и регистрацию для управления одним компьютером в пределах единственной конфигурации сеанса. Во второй процедуре описано, как удалить правило авторизации, которое больше не требуется.

Если вы планируете использовать настраиваемые конфигурации сеансов, чтобы разрешить определенным пользователям работать только в ограниченных пространствах выполнения в Windows PowerShell Web Access, создайте эти конфигурации, прежде чем добавить правила авторизации, которые на них ссылаются. Командлеты Windows PowerShell Web Access нельзя использовать для создания настраиваемых конфигураций сеансов. Дополнительные сведения о создании настраиваемых конфигураций сеансов см. в описании [about\_Session\_Configuration\_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.

Командлеты Windows PowerShell Web Access поддерживают единственный подстановочный знак — звездочку ( * ). Подстановочные знаки в строковых значениях не поддерживаются; используйте одну звездочку для свойства (пользователи, компьютеры или конфигурации сеанса).

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
<td><p>Другие способы использования правил авторизации, чтобы предоставить доступ пользователям и обеспечить безопасность среды Windows PowerShell Web Access, см. в разделе <a href="#BKMK_others">Другие примеры сценария правил авторизации</a> данной статьи.</p></td>
</tr>
</tbody>
</table>

#### Добавление ограничивающего правила авторизации

1.  Выполните одно из следующих действий, чтобы открыть сеанс Windows PowerShell с повышенными правами.

    -   На рабочем столе Windows щелкните правой кнопкой мыши **Windows PowerShell** на панели задач и выберите команду **Запустить от имени администратора**..

    -   На **начальном экране** Windows щелкните правой кнопкой мыши **Windows PowerShell**, а затем щелкните **Запустить от имени администратора**..

2.  <span class="label">Необязательный шаг для ограничения доступа пользователей с помощью конфигураций сеансов: </span> убедитесь, что конфигурации сеансов, которые вы хотите использовать в своих правилах, уже существуют. В противном случае выполните инструкции по созданию конфигураций сеансов, приведенные в статье [about\_Session\_Configuration\_Files](https://msdn.microsoft.com/library/windows/desktop/hh847838.aspx) на сайте MSDN.

3.  Введите следующую команду и нажмите клавишу **ВВОД**:.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_1079478f-cd51-4d35-8022-4b532a9d57a4'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    Это правило авторизации разрешает конкретному пользователю доступ к одному сетевому компьютеру, к которому обычно требуется доступ, с доступом к конкретной конфигурации сеанса, область которого соответствует потребностям пользовательских скриптов и командлетов. В следующем примере пользователю с именем <span class="code">JSmith</span> в домене <span class="code">Contoso</span> предоставляется доступ для управления компьютером <span class="code">Contoso_214</span> и использования конфигурации сеанса с именем <span class="code"> NewAdminsOnly.</span>.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_4e760377-e401-4ef4-988f-7a0aec1b2a90'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4.  Убедитесь, что правило создано, выполнив командлет **Get-PswaAuthorizationRule** или **Test-PswaAuthorizationRule -UserName &lt;домен\пользователь | компьютер\пользователь&gt; -ComputerName**  &lt;computer_name&gt;. Например, **Test-PswaAuthorizationRule –UserName Contoso\\JSmith –ComputerName Contoso\_214**.

#### Удаление правила авторизации

1.  Если сеанс Windows PowerShell еще не открыт, см. шаг 1 процедуры [Добавление неограничивающего правила авторизации](#BKMK_arar) в этом разделе.

2.  Введите следующую команду и нажмите клавишу **ВВОД**, где *ИД правила* представляет уникальный идентификатор правила, которое требуется удалить.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_0daef66d-0ecf-47fb-a8a0-d4dbceb8409d'); "Копировать в буфер обмена".)

        Remove-PswaAuthorizationRule -ID <rule ID>

    Если вы не знаете идентификатор, но знаете понятное имя удаляемого правила, вы можете передать его в командлет <span class="code">Remove-PswaAuthorizationRule</span> для удаления правила, как показано в следующем примере: Get-PswaAuthorizationRule -RuleName &lt;*rule name*&gt; | Remove-PswaAuthorizationRule.

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
    <td><p>При попытке удалить указанное правило авторизации запрос на подтверждение удаления не выводится. Правило удаляется при нажатии клавиши <strong>ВВОД</strong>. Убедитесь, что действительно необходимо удалить правило авторизации перед выполнением командлета <strong>Remove-PswaAuthorizationRule</strong>.</p></td>
    </tr>
    </tbody>
    </table>

<a href="" id="BKMK_others"></a>
####

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Другие примеры сценария правил авторизации</span></a>

------------------------------------------------------------------------

Каждый сеанс Windows PowerShell использует конфигурацию сеанса. Если конфигурация не указана, Windows PowerShell по умолчанию использует встроенную конфигурацию сеанса Windows PowerShell с именем Microsoft.PowerShell. Конфигурация сеанса по умолчанию включает все командлеты, доступные на компьютере. Администраторы могут ограничить доступ ко всем компьютерам, определив конфигурацию сеанса с ограниченным пространством выполнения (ограниченный набор командлетов и задач, которые могут выполнять конечные пользователи). Пользователь, которому к одному компьютеру предоставлен либо полный языковый доступ, либо доступ только на удаленное управление командлетами Windows PowerShell, может подключаться к другим компьютерам, подключенным к первому компьютеру. Определение ограниченного пространства выполнения может предотвратить доступ пользователей к другим компьютерам из разрешенного пространства выполнения Windows PowerShell. Это повышает безопасность среды Windows PowerShell Web Access. Конфигурацию сеанса можно распространить (с помощью групповой политики) на все компьютеры, которые администраторы хотят сделать доступными через Windows PowerShell Web Access. Дополнительные сведения о конфигурациях сеансов см. в разделе [about\_Session\_Configurations](https://technet.microsoft.com/library/dd819508.aspx). Ниже приводятся примеры такого сценария.

-   Администратор создает конечную точку с именем **PswaEndpoint** с ограниченным пространством выполнения. Затем администратор создает правило, **\*,\*,PswaEndpoint**, и распространяет конечную точку на все компьютеры. Правило разрешает всем пользователям доступ ко всем компьютерам с конечной точкой **PswaEndpoint**. Если это правило авторизации является единственным в наборе правил, компьютеры без этой конечной точки будут недоступными.

-   Администратор создает конечную точку с именем **PswaEndpoint** и хочет ограничить доступ конкретными пользователями. Администратор создает группу пользователей с именем **Level1Support** и определяет следующее правило: **Level1Support,\*,PswaEndpoint**. Правило предоставляет всем пользователям из группы **Level1Support** доступ ко всем компьютерам с конфигурацией **PswaEndpoint**. Аналогичным образом доступ может быть ограничен конкретным набором компьютеров.

-   Некоторые администраторы предоставляют одним пользователям больше прав доступа, чем другим. Например, администратор создает две группы пользователей — **Admins** и **BasicSupport**. Администратор также создает конечную точку с ограниченным пространством выполнения с именем **PswaEndpoint**, а затем определяет два правила: **Admins,\*,\*** и **BasicSupport,*,PswaEndpoint**. Первое правило предоставляет всем пользователям в группе **Admins** доступ ко всем компьютерам, а второе правило предоставляет всем пользователям в группе **BasicSupport** доступ только к компьютерам с **PswaEndpoint**..

-   Администратор настроил частную тестовую среду и хочет разрешить всем авторизованным сетевым пользователям доступ ко всем компьютерам в сети, к которым они обычно имеют доступ, с доступом ко всем конфигурациям сеансов, к которым они обычно имеют доступ. Поскольку это частная тестовая среда, администратор создает правило авторизации, которое не является безопасным. Администратор выполняет командлет <span class="code">Add-PswaAuthorizationRule \* \* \*</span>, в котором подстановочный знак **\*** используется, чтобы представлять всех пользователей, все компьютеры и все конфигурации. Это правило эквивалентно следующему: <span class="code">Add-PswaAuthorizationRule ИмяПользователя \* -ИмяКомпьютера \* -ИмяКонфигурации \*</span>.

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
    <td><p>Это правило не рекомендуется к использованию в безопасной среде. В нем обходится уровень безопасности, предоставляемый Windows PowerShell Web Access.</p></td>
    </tr>
    </tbody>
    </table>

-   Администратор должен разрешить пользователям подключаться к конечным компьютерам в среде, включающей и рабочие группы, и домены, где компьютеры рабочей группы иногда используются для подключения к конечным компьютерам в доменах, а компьютеры в доменах иногда используются для подключения к конечным компьютерам в рабочих группах. У администратора есть сервер шлюза *PswaServer* в рабочей группе, а конечный компьютер *srv1.contoso.com* находится в домене. Пользователь *Олег* зарегистрирован как авторизованный локальный пользователь на сервере шлюза в рабочей группе и на конечном компьютере. Его имя пользователя на сервере рабочей группы — *olegLocal*, а на конечном компьютере — *contoso\oleg*. Чтобы разрешить Олегу доступ к srv1.contoso.com, администратор добавляет следующее правило.

    [Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_8d183d3d-1c19-44b8-9297-530b0efc7c79'); "Копировать в буфер обмена".)

        Add-PswaAuthorizationRule –userName PswaServer\chrisLocal –computerName srv1.contoso.com –configurationName Microsoft.PowerShell

    В предыдущем примере правила выполняется проверка подлинности учетной записи Олега на сервере шлюза, а затем авторизация его доступа к *srv1*. На странице входа Олег должен предоставить второй набор учетных данных в разделе **Дополнительные параметры подключения** (*contoso\oleg*). Сервер шлюза использует дополнительный набор учетных данных для проверки подлинности учетной записи Олега на конечном компьютере *srv1.contoso.com*..

    В предыдущем сценарии Windows PowerShell Web Access устанавливает подключение к конечному компьютеру, только если указанные ниже действия успешно выполнены и разрешены по крайней мере одним правилом авторизации.

    1.  Проверка подлинности на сервере шлюза рабочей группы путем добавления имени пользователя в формате *имя\_сервера*\\*имя\_пользователя* в правило авторизации.

    2.  Проверка подлинности на конечном компьютере при помощи альтернативных учетных данных, введенных на странице входа, в разделе **Дополнительные параметры подключения**.

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
    <td><p>Если шлюз и конечные компьютеры находятся в разных рабочих группах или доменах, то должно быть установлено отношение доверия между двумя компьютерами рабочей группы, между двумя доменами или между рабочей группой и доменом. Это отношение нельзя настроить при помощи командлетов правил авторизации Windows PowerShell Web Access. Правила авторизации не определяют отношение доверия между компьютерами. Они только разрешают пользователям подключаться к определенным конечным компьютерам и конфигурациям сеансов. Дополнительные сведения о настройке отношения доверия между разными доменами см. в статье о <a href="https://technet.microsoft.com/library/cc794775.aspx">создании отношений доверия между доменами и лесами</a>. Дополнительные сведения о добавлении компьютеров рабочей группы в список надежных узлов см. в статье об <a href="https://technet.microsoft.com/library/dd759202.aspx"> удаленном управлении при помощи диспетчера сервера.</a>.</p></td>
    </tr>
    </tbody>
    </table>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Использование одного набора правил авторизации для нескольких сайтов</span></a>

------------------------------------------------------------------------

Правила авторизации сохраняются в XML-файле. По умолчанию путь к XML-файлу имеет вид %windir%\\Web\\PowershellWebAccess\\data\\AuthorizationRules.xml.

Путь к XML-файлу правил авторизации сохраняется в файле **powwa.config** в папке %windir%\\Web\\PowershellWebAccess\\data. Администратор может легко изменить ссылку на путь по умолчанию в файле **powwa.config** соответственно своим параметрам и требованиям. Возможность изменения расположения файла администратором позволяет нескольким шлюзам Windows PowerShell Web Access использовать одни и те же правила авторизации, если требуется такая конфигурация.

<a href="" id="BKMK_sesmgmt"></a>

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Управление сеансом</span></a>
<a href="/en-us/library/dn282394(v=ws.11).aspx#Anchor_1" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

По умолчанию Windows PowerShell Web Access позволяет пользователю открывать не больше трех сеансов одновременно. Вы можете отредактировать файл **web.config** веб-приложения в диспетчере служб IIS, чтобы поддерживать другое количество сеансов на пользователя. Путь к файлу **web.config** имеет вид $Env:Windir\\Web\\PowerShellWebAccess\\wwwroot\\Web.config.

По умолчанию веб-сервер (IIS) настраивается на перезапуск пула приложений, если был изменен любой параметр. Например, пул приложений перезапускается, если были внесены изменения в файл **web.config**. Поскольку Windows PowerShell Web Access использует состояния сеансов в памяти, пользователи, вошедшие в сеансы Windows PowerShell Web Access, теряют свои сеансы при перезапуске пула приложений.

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Установка параметров по умолчанию на странице входа</span></a>

------------------------------------------------------------------------

Если шлюз Windows PowerShell Web Access работает под управлением Windows Server 2012 R2, вы можете настроить значения по умолчанию для параметров, которые отображаются на странице входа в Windows PowerShell Web Access. Вы можете настроить значения в файле **web.config**, описанном в предыдущем абзаце. Значения по умолчанию для параметров на странице входа находятся в разделе **appSettings** файла web.config, ниже приведен пример раздела **appSettings**. Допустимые значения для многих из этих параметров такие же, как для соответствующих параметров командлета [New-PSSession](https://technet.microsoft.com/library/hh849717.aspx) в Windows PowerShell. Например, ключ <span class="code">defaultApplicationName</span>, как показано в следующем блоке кода, является значением привилегированной переменной **$PSSessionApplicationName**.

[Copy](javascript:if%20(window.epx.codeSnippet)window.epx.codeSnippet.copyCode('CodeSnippetContainerCode_6ccfd0a1-485a-4ac5-9636-89ebab501bef'); "Копировать в буфер обмена".)

    <appSettings>
            <add key="maxSessionsAllowedPerUser" value="3"/>
            <add key="defaultPortNumber" value="5985"/>
            <add key="defaultSSLPortNumber" value="5986"/>
            <add key="defaultApplicationName" value="WSMAN"/>
            <add key="defaultUseSslSelection" value="0"/>
            <add key="defaultAuthenticationType" value="0"/>
            <add key="defaultAllowRedirection" value="0"/>
            <add key="defaultConfigurationName" value="Microsoft.PowerShell"/>
    </appSettings>

###

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">Время ожидания и незапланированные отключения</span></a>

------------------------------------------------------------------------

Время ожидания сеанса Windows PowerShell Web Access истекло. В Windows PowerShell Web Access под управлением Windows Server 2012 сообщение о времени ожидания отображается для вошедших пользователей после 15 минут отсутствия активности в сеансе. Если пользователь не отвечает в пределах пяти минут после вывода сообщения о времени ожидания, сеанс заканчивается и пользователь выводится из системы. Вы можете изменить значения времени ожидания для сеанса в параметрах веб-сайта в диспетчере служб IIS.

В Windows PowerShell Web Access, работающему под управлением Windows Server 2012 R2, время ожидания сеансов по умолчанию истекает через 20 минут бездействия. Если пользователи отключаются от сеансов в веб-консоли в результате сетевых ошибок или других незапланированных завершений работы или сбоев, а не потому, что они сами закрыли свои сеансы, сеансы Windows PowerShell Web Access продолжают выполнение, оставаясь подключенными к целевым компьютерам, пока не истечет время ожидания на стороне клиента. Сеанс отключается после истечения либо 20 минут, установленных по умолчанию, либо времени ожидания, заданного администратором шлюза, в зависимости от того, какой период короче.

Если сервер шлюза работает под управлением Windows Server 2012 R2, Windows PowerShell Web Access предоставляет пользователям возможность повторного подключения к сохраненным сеансам позднее, но, когда сеанс был отключен из-за сетевых ошибок, незапланированного завершения работы или другого сбоя, пользователи не смогут увидеть сохраненные сеансы и повторно к ним подключиться, пока не истечет время ожидания, заданное администратором шлюза.

<a href="javascript:void(0)" class="LW_CollapsibleArea_TitleAhref" title="Collapse"><span class="cl_CollapsibleArea_expanding LW_CollapsibleArea_Img"></span><span class="LW_CollapsibleArea_Title">См. также</span></a>
<a href="/en-us/library/dn282394(v=ws.11).aspx#Anchor_2" class="LW_CollapsibleArea_Anchor_Img" title="Right-click to copy and share the link for this section"></a>

------------------------------------------------------------------------

[Установка и использование Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
[about\_Session\_Configurations](https://technet.microsoft.com/library/dd819508.aspx)
[Командлеты Windows PowerShell Web Access](https://technet.microsoft.com/library/hh918342.aspx)

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


