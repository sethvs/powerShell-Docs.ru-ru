# <a name="installing-powershell-core-on-windows"></a>Установка PowerShell Core в Windows

## <a name="msi"></a>MSI

Чтобы установить PowerShell на клиенте Windows или в Windows Server (работает в Windows 7 с пакетом обновления 1 (SP1), Server 2008 R2 и более поздних версий), скачайте пакет MSI из с нашей страницы [выпусков][] GitHub.

MSI-файл имеет следующий вид: `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`.
<!-- TODO: should be updated to point to the Download Center as well -->

После скачивания дважды щелкните установщик и следуйте инструкциям на экране.

После установки в меню "Пуск" появляется ярлык.

* По умолчанию пакет устанавливается в каталог `$env:ProgramFiles\PowerShell\`.
* Вы можете запустить PowerShell с помощью меню "Пуск" или файла `$env:ProgramFiles\PowerShell\pwsh.exe`.

### <a name="prerequisites"></a>Необходимые компоненты

Чтобы включить удаленное взаимодействие PowerShell через WSMan, нужно выполнить следующие условия:

* Установите [универсальную среду выполнения C](https://www.microsoft.com/download/details.aspx?id=50410) в версиях Windows, предшествующих Windows 10.
  Ее можно скачать самостоятельно или через Центр обновления Windows.
  Поддерживаемые системы, где установлены все исправления (включая дополнительные пакеты), уже содержат ее.
* Установите Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) или более поздней версии ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) в Windows 7 и Windows Server 2008 R2.

## <a name="zip"></a>ZIP

Для поддержки расширенных сценариев развертывания доступны ZIP-архивы двоичных файлов PowerShell.
Следует отметить, что при использовании ZIP-архива проверка предварительных условий, как в случае с пакетом MSI, не производится.
Поэтому для правильной работы удаленного взаимодействия через WSMan в версиях Windows, предшествующих Windows 10, убедитесь, что [предварительные условия](#prerequisites) соблюдены.

## <a name="deploying-on-nano-server"></a>Развертывание на Nano Server

Эти инструкции предполагают, что версия PowerShell уже запущена на образе Nano Server и была создана с помощью [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).
ОС Nano Server работает без монитора, и двоичные файлы PowerShell Core можно развернуть двумя способами:

1. Автономно — подключите виртуальный жесткий диск Nano Server и распакуйте содержимое ZIP-файла в выбранное расположение в этом образе.
1. В сети — передайте ZIP-файл через сеанс PowerShell и распакуйте его в выбранное расположение.

В обоих случаях вам понадобится ZIP-пакет выпуска x64 Windows 10 и потребуется выполнять команды в экземпляре PowerShell с правами администратора.

### <a name="offline-deployment-of-powershell-core"></a>Автономное развертывание PowerShell Core

1. С помощью любой служебной программы ZIP распакуйте пакет в каталог, находящийся внутри подключенного образа Nano Server.
1. Отключите образ и загрузите его.
1. Подключитесь к входящему экземпляру Windows PowerShell.
1. Следуйте инструкциям, чтобы создать конечную точку удаленного взаимодействия с помощью [методики использования другого экземпляра](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Автономное PowerShell Core в сети

Следующие шаги описывают развертывание PowerShell Core в запущенном экземпляре Nano Server, а также настройку его удаленной конечной точки.

* Подключитесь к входящему экземпляру Windows PowerShell:

```powershell
$session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
```

* Скопируйте файл на экземпляр Nano Server:

```powershell
Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
```

* Войдите в сеанс:

```powershell
Enter-PSSession $session
```

* Извлеките ZIP-файл:

```powershell
# Insert the appropriate version.
Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
```

* Если вам требуется удаленное взаимодействие на основе WSMan, следуйте инструкциям, чтобы создать конечную точку удаленного взаимодействия с помощью [методики использования другого экземпляра](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="instructions-to-create-a-remoting-endpoint"></a>Инструкции по созданию конечной точки удаленного взаимодействия

PowerShell Core поддерживает протокол удаленного взаимодействия PowerShell (PSRP) через SSH и WSMan. Дополнительная информация:

* [Удаленное взаимодействие через SSH в PowerShell Core][ssh-remoting]
* [Удаленное взаимодействие через WSMan в PowerShell Core][wsman-remoting]

## <a name="artifact-installation-instructions"></a>Указания по установке артефакта

Мы публикуем архив с кодом CoreCLR для каждой сборки CI с [AppVeyor][].

## <a name="coreclr-artifacts"></a>Артефакты CoreCLR

* Скачайте ZIP-пакет с вкладки **artifacts** конкретной сборки.
* Разблокируйте ZIP-файл: щелкните правой кнопкой мыши в проводнике, выберите "Свойства", установите флажок "Разблокировать" и выберите "Применить".
* Извлеките содержимое ZIP-файла в каталог `bin`.
* `./bin/pwsh.exe`

<!-- [download-center]: TODO -->
[выпусков]: https://github.com/PowerShell/PowerShell/releases
[signing]: ../../tools/Sign-Package.ps1
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell