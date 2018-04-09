# <a name="powershell-core-support-lifecycle"></a>Жизненный цикл поддержки PowerShell Core

PowerShell Core — это отдельный набор средств и компонентов, поставляемых, устанавливаемых и настраиваемых отдельно от Windows PowerShell.
Поэтому на PowerShell Core не распространяются лицензионные соглашения Windows 7, 8.1, 10 или Windows Server.

Однако PowerShell Core поддерживается в рамках традиционных соглашений о поддержке корпорации Майкрософт, включая [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement] и [Microsoft Software Assurance][assurance].
Вы также можете оплатить [техническую поддержку][] по PowerShell Core, направив в службу поддержки запрос о своей проблеме.

Мы также предлагаем [поддержку сообщества][] на GitHub, где вы можете зарегистрировать вопрос, ошибку или запрос функции.
Кроме того, вы можете обратиться за помощью к другим членам сообщества на сайтах [Microsoft Community][] или Microsoft [PowerShell Tech Community][].
Мы не можем гарантировать, что там вы оперативно получите решение своей проблемы.
Если ваша проблема требует немедленного вмешательства, следует использовать традиционные платные варианты поддержки.

## <a name="lifecycle-of-powershell-core"></a>Жизненный цикл PowerShell Core

В PowerShell Core внедряется [политика современного жизненного цикла Майкрософт][modern].
Этот жизненный цикл поддержки предназначен для предоставления клиентам актуальных версий.

Ветвь версии 6.x продукта PowerShell Core будет обновляться примерно каждые шесть месяцев (то есть 6.0, 6.1, 6.2 и т. д.)

> [!IMPORTANT]
> Чтобы продолжить получать поддержку, вам нужно обновить продукт в течение шести месяцев после выпуска версии с новым дополнительным номером.

Например, если PowerShell Core 6.1 выпущена 1 июля 2018 года, для сохранения поддержки вам следует обновиться до PowerShell Core 6.1 к 1 января 2019 года.

![Жизненный цикл ветви PowerShell Core][lifecycle-chart]

Политика современного жизненного цикла также требует, чтобы корпорация Майкрософт предоставляла клиентам уведомление за 12 месяцев до прекращения поддержки продукта (т. е. PowerShell Core).

В конечном счете, мы планируем реализовать для PowerShell Core подход "долгосрочного обслуживания", чтобы нам требовалось лишь проводить обслуживание и выпускать обновления для системы безопасности, чтобы обеспечить поддержку определенной ветви или версии 6.x.

## <a name="supported-platforms"></a>Поддерживаемые платформы

PowerShell Core официально поддерживается на следующих платформах:

* Windows 7, 8.1 и 10
* Windows Server 2008 R2, 2012 R2, 2016
* [Windows Server Semi-Annual Channel][semi-annual]
* Ubuntu 14.04, 16.04 и 17.04
* Debian 8.7+ и 9
* CentOS 7
* Red Hat Enterprise Linux 7
* OpenSUSE 42.2
* Fedora 25, 26
* macOS 10.12+

Наше сообщество также предоставило пакеты для следующих платформ, однако они не поддерживаются официально:

* Arch Linux
* Kali Linux
* AppImage (работает на нескольких платформах Linux)

## <a name="notes-on-licensing"></a>Замечания по лицензированию

PowerShell Core выпускается по [лицензии MIT][].
Согласно этой лицензии и в отсутствие соглашения о платной подписке пользователи ограничены лишь [поддержку сообщества][].
В рамках поддержки сообщества корпорация Майкрософт не предоставляет никаких гарантий оперативного реагирования или выпуска исправлений.

## <a name="windows-powershell-module"></a>Модуль Windows PowerShell

Поддержка для PowerShell Core не распространяется на другие модули продукта, если только они не поддерживают PowerShell Core явным образом.
Например, использование модуля `ActiveDirectory`, который поставляется в составе Windows Server, является неподдерживаемым сценарием.

Однако в некоторых случаях модули, которые не поддерживают PowerShell Core явным образом, могут быть совместимы.
Установив модуль [`WindowsPSModulePath`][] можно добавить `PSModulePath` Windows PowerShell в `PSModulePath` PowerShell Core.

Сначала установите модуль `WindowsPSModulePath` из коллекции PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin 
Install-Module WindowsPSModulePath -Force
```

После установки модуля запустите командлет `Add-WindowsPSModulePath`, чтобы добавить `PSModulePath` Windows PowerShell в PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[поддержку сообщества]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[техническую поддержку]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[лицензии MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath"]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
