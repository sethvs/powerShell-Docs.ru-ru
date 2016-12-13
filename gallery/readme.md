# <a name="the-powershell-gallery"></a>Коллекция PowerShell

Коллекция PowerShell — это центральный репозиторий для хранения содержимого PowerShell. Именно в коллекции можно найти новые команды PowerShell или ресурсы настройки требуемого состояния (DSC).

# <a name="powershellget-overview"></a>Обзор PowerShellGet

Модуль PowerShellGet содержит командлеты для обнаружения, установки, обновления и публикации артефактов PowerShell, таких как модули, ресурсы DSC, возможности ролей и скрипты с веб-сайта https://www.PowerShellGallery.com и других частных репозиториев.

## <a name="getting-started-with-the-gallery"></a>Начало работы с коллекцией

Для установки элементов из коллекции требуется последняя версия модуля PowerShellGet, доступная в Windows 10, в Windows Management Framework (WMF) 5.0 или в установщике на основе MSI (для PowerShell 3 и 4).

- [**Скачать Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),
- [**Скачать WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175) или
- [**Скачать установщик MSI**](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

Последняя версия модуля [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) позволяет:

-   Выполнять поиск по элементам в коллекции командлетами [**Find-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Find-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
-   Сохранять элементы в систему из коллекции командлетами [**Save-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Save-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
-   Устанавливать элементы из коллекции командлетами [**Install-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Install-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
-   Отправлять элементы в коллекцию командлетами [**Publish-Module**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) и [**Publish-Script**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).
-   Добавлять собственный репозиторий командлетом [**Register-PSRepository**](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409).

Дополнительные сведения об использовании команд PowerShellGet при работе с коллекцией см. в статье [Начало работы](psgallery/psgallery_gettingstarted.md). Вы также можете запустить командлет *Update-Help -Module PowerShellGet*, чтобы установить локальную справку по этим командам.

## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы

Для модуля **PowerShellGet** требуется **PowerShell 3.0 или более поздней версии**.

Таким образом, для **PowerShellGet** требуется одна из следующих операционных систем:

- Windows 10
- Windows 8.1 Профессиональная
- Windows 8.1 Корпоративная
- Windows 7 с пакетом обновления 1 (SP1)
- Windows Server 2016 TP5
- Windows Server 2012 R2
- Windows Server 2008 R2 с пакетом обновления 1 (SP1)

Для **PowerShellGet** также требуется .NET Framework 4.5 или более поздней версии. Установить .NET Framework 4.5 или более поздней версии можно [отсюда](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).


## <a name="got-a-question-have-feedback"></a>Возник вопрос? Хотите поделиться мнением?

Дополнительные сведения о коллекции PowerShell и PowerShellGet см. на странице [Начало работы](psgallery/psgallery_gettingstarted.md). Оставить отзыв или сообщить о проблеме можно на сайте [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).

