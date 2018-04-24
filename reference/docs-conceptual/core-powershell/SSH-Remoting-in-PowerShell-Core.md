# <a name="powershell-remoting-over-ssh"></a>Удаленное взаимодействие с PowerShell через SSH

## <a name="overview"></a>Обзор

Функция удаленного взаимодействия PowerShell обычно использует WinRM для согласования соединения и передачи данных.
Протокол SSH был выбран для этой реализации удаленного взаимодействия, так как он теперь доступен для платформ Linux и Windows и позволяет реализовать действительно многоплатформенное удаленное взаимодействие PowerShell.
Однако WinRM также предоставляет надежную модель размещения для удаленных сеансов PowerShell, которой пока нет в этой реализации.
Это значит, что конфигурация удаленной конечной точки PowerShell и JEA (Just Enough Administration) в этой реализации пока не поддерживается.

Удаленное взаимодействие по SSH в PowerShell позволяет выполнять базовые операции удаленной работы с сеансами PowerShell между компьютерами с Windows и Linux.
Для этого на целевом компьютере создается ведущий процесс PowerShell в качестве подсистемы SSH.
В конечном счете, все это будет заменено более общей моделью размещения, которая аналогична тому, как WinRM обеспечивает поддержку конфигурации конечной точки и JEA.

Командлеты New-PSSession, Enter-PSSession и Invoke-Command теперь имеют новый набор параметров, призванный упростить новое удаленное подключение.

```powershell
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Этот новый набор параметров, скорее всего, изменится, но сейчас он позволяет создавать сеансы SSH PSSession, с которыми можно взаимодействовать с помощью командной строки либо вызова команд и сценариев.
Вы можете указать целевой компьютер с помощью параметра HostName и имя пользователя с помощью параметра UserName.
При интерактивном выполнении командлетов в командной строке PowerShell вам будет предложено ввести пароль.
Но вы также можете использовать проверку подлинности на основе ключа SSH и указать путь к файлу закрытого ключа с помощью параметра KeyFilePath.

## <a name="general-setup-information"></a>Общие сведения об установке

SSH должен быть установлен на всех компьютерах.
Вам нужно установить клиент (ssh.exe) и сервер (sshd.exe), чтобы можно было поэкспериментировать с удаленным обращением к компьютерам и с них.
Для Windows нужно установить [Win32 OpenSSH из GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).
Для Linux нужно установить SSH (включая сервер sshd) в соответствии с используемой платформой.
Вам также потребуется новая версия сборки или пакета PowerShell с GitHub, где есть функция удаленного взаимодействия SSH.
Подсистемы SSH используются для запуска процесса PowerShell на удаленном компьютере, поэтому сервер SSH нужно настроить соответствующим образом.
Кроме того, нужно включить проверку подлинности с помощью пароля и при необходимости проверку подлинности на основе ключа.

## <a name="setup-on-windows-machine"></a>Установка на компьютере с Windows

1. Установите последнюю версию [PowerShell Core для Windows]
    - Чтобы узнать о наличии поддержки удаленного взаимодействия SSH, просмотрите набор параметров для New-PSSession.
    ```powershell
    PS> Get-Command New-PSSession -syntax
    New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
    ```
1. Установите последнюю версию сборки [Win32 OpenSSH] из GitHub, используя [инструкции по установке].
1. Измените файл sshd_config в том расположении, куда вы установили Win32 OpenSSH.
    - Включите проверку подлинности с помощью пароля:
    ```none
    PasswordAuthentication yes
    ```
    - Добавьте запись подсистемы PowerShell, замените `c:/program files/powershell/6.0.0/pwsh.exe` на правильный путь к версии, которую хотите использовать:
    ```none
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```
    - При необходимости включите проверку подлинности на основе ключа:
    ```none
    PubkeyAuthentication yes
    ```
1. Перезапустите службу sshd.
    ```powershell
    Restart-Service sshd
    ```
1. Добавьте путь установки OpenSSH в свою переменную пути Env.
    - Это нужно сделать в соответствии с `C:\Program Files\OpenSSH\`.
    - Это позволяет найти ssh.exe.

## <a name="setup-on-linux-ubuntu-1404-machine"></a>Установка на компьютере с Linux (Ubuntu 14.04)

1. Установите последнюю сборку [PowerShell для Linux] из GitHub.
1. При необходимости установите [Ubuntu SSH].
    ```bash
    sudo apt install openssh-client
    sudo apt install openssh-server
    ```
1. Измените файл sshd_config в расположении /etc/ssh.
    - Включите проверку подлинности с помощью пароля:
    ```none
    PasswordAuthentication yes
    ```
    - Добавьте запись подсистемы PowerShell:
    ```none
    Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
    ```
    - При необходимости включите проверку подлинности на основе ключа:
    ```none
    PubkeyAuthentication yes
    ```
1. Перезапустите службу sshd.
    ```bash
    sudo service sshd restart
    ```

## <a name="setup-on-macos-machine"></a>Установка на компьютере с MacOS

1. Установите последнюю сборку [PowerShell для MacOS].
    - Убедитесь, что удаленное взаимодействие SSH включено, выполните следующие действия:
      - Откройте `System Preferences`.
      - Щелкните `Sharing`.
      - Убедитесь, что `Remote Login` имеет значение `Remote Login: On`.
      - Разрешите доступ соответствующим пользователям.
1. Измените файл `sshd_config` в расположении `/private/etc/ssh/sshd_config`.
    - Используйте привычный вам редактор или следующую команду:
    ```bash
    sudo nano /private/etc/ssh/sshd_config
    ```
    - Включите проверку подлинности с помощью пароля:
    ```none
    PasswordAuthentication yes
    ```
    - Добавьте запись подсистемы PowerShell:
    ```none
    Subsystem powershell /usr/local/bin/powershell -sshs -NoLogo -NoProfile
    ```
    - При необходимости включите проверку подлинности на основе ключа:
    ```none
    PubkeyAuthentication yes
    ```
1. Перезапустите службу sshd.
    ```bash
    sudo launchctl stop com.openssh.sshd
    sudo launchctl start com.openssh.sshd
    ```

## <a name="powershell-remoting-example"></a>Пример удаленного взаимодействия PowerShell

Проще всего проверить удаленное взаимодействие, просто попробовав использовать его на отдельном компьютере.
Здесь я создам удаленный сеанс на том же компьютере в окне Linux.
Обратите внимание, что я использую командлеты PowerShell из командной строки, поэтому мы видим запросы SSH о проверке главного компьютера, а также запросы на ввод пароля.
То же самое можно сделать на компьютере с Windows, чтобы убедиться в работе удаленного взаимодействия, а затем удаленно переключаться между компьютерами, просто изменяя имя узла.

```powershell
#
# Linux to Linux
#
PS /home/TestUser> $session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:

PS /home/TestUser> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available

PS /home/TestUser> Enter-PSSession $session

[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession

PS /home/TestUser> Invoke-Command $session -ScriptBlock { Get-Process powershell }

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1


#
# Linux to Windows
#
PS /home/TestUser> Enter-PSSession -HostName WinVM1 -UserName PTestName
PTestName@WinVM1s password:

[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver

Microsoft Windows [Version 10.0.10586]

[WinVM1]: PS C:\Users\PTestName\Documents>

#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.

PS C:\Users\PSUser\Documents> $session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
PS C:\Users\PSUser\Documents> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available


PS C:\Users\PSUser\Documents> Enter-PSSession -Session $session
[WinVM2]: PS C:\Users\PSRemoteUser\Documents> $PSVersionTable

Name                           Value
----                           -----
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
SerializationVersion           1.1.0.1
BuildVersion                   3.0.0.0
CLRVersion
PSVersion                      6.0.0-alpha
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
GitCommitId                    v6.0.0-alpha.17


[WinVM2]: PS C:\Users\PSRemoteUser\Documents>
```

### <a name="known-issues"></a>Известные проблемы

1. Команда sudo не работает во входящем удаленном сеансе на компьютер Linux.

[PowerShell for Windows]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi
[Win32 OpenSSH]: https://github.com/PowerShell/Win32-OpenSSH
[инструкции по установке]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[PowerShell для Linux]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#ubuntu-1404
[Ubuntu SSH]: https://help.ubuntu.com/lts/serverguide/openssh-server.html
[PowerShell для MacOS]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#macos-1012