# <a name="installing-powershell-core-on-macos-and-linux"></a>Установка PowerShell Core в macOS и Linux

Поддерживает [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch] и [macOS 10.12][mac].

Для дистрибутивов Linux без официальной поддержки попробуйте использовать [PowerShell AppImage][lai]. Можно также попытаться развернуть двоичные файлы PowerShell напрямую с помощью [архива`tar.gz`][tar] Linux, но при этом нужно отдельно настроить необходимые зависимости с учетом операционной системы.

Все пакеты доступны на нашей странице [выпусков][] GitHub. После установки пакета запустите `pwsh` из терминала.

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fed25]: #fedora-25
[fed26]: #fedora-26
[arch]: #arch-linux
[lai]: #linux-appimage
[mac]: #macos-1012
[tar]: #binary-archives

## <a name="ubuntu-1404"></a>Ubuntu 14.04

### <a name="installation-via-package-repository---ubuntu-1404"></a>Установка с помощью репозитория пакетов — Ubuntu 14.04

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов. Это предпочтительный метод.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.

### <a name="installation-via-direct-download---ubuntu-1404"></a>Установка с помощью прямого скачивания — Ubuntu 14.04

Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu.

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.14.04_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.

### <a name="uninstallation---ubuntu-1404"></a>Удаление — Ubuntu 14.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>Установка с помощью репозитория пакетов — Ubuntu 16.04

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.
Это предпочтительный метод.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.

### <a name="installation-via-direct-download---ubuntu-1604"></a>Установка с помощью прямого скачивания — Ubuntu 16.04

Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.

### <a name="uninstallation---ubuntu-1604"></a>Удаление — Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a>Ubuntu 17.04

### <a name="installation-via-package-repository---ubuntu-1704"></a>Установка с помощью репозитория пакетов — Ubuntu 17.04

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.
Это предпочтительный метод.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/17.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.

### <a name="installation-via-direct-download---ubuntu-1704"></a>Установка с помощью прямого скачивания — Ubuntu 17.04

Скачайте пакет Debian `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` со страницы [выпусков][] на компьютер с Ubuntu:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.17.04_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.

### <a name="uninstallation---ubuntu-1704"></a>Удаление — Ubuntu 17.04

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>Установка с помощью репозитория пакетов — Debian 8

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.
Это предпочтительный метод.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.

### <a name="installation-via-direct-download---debian-8"></a>Установка с помощью прямого скачивания — Debian 8

Скачайте пакет Debian `powershell_6.0.0-1.debian.8_amd64.deb` со страницы [выпусков][] на компьютер с Debian:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.8_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo dpkg -i powershell_6.0.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.

### <a name="uninstallation---debian-8"></a>Удаление — Debian 8

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>Установка с помощью репозитория пакетов — Debian 9

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в репозиториях пакетов.
Это предпочтительный метод.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo apt-get upgrade powershell` для его обновления.

### <a name="installation-via-direct-download---debian-9"></a>Установка с помощью прямого скачивания — Debian 9

Скачайте пакет Debian `powershell_6.0.0-1.debian.9_amd64.deb` со страницы [выпусков][] на компьютер с Debian:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo dpkg -i powershell_6.0.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

> Обратите внимание, что `dpkg -i` завершится со сбоем из-за несоблюдения зависимостей; следующая команда `apt-get install -f` разрешает их и завершает настройку пакета PowerShell.

### <a name="uninstallation---debian-9"></a>Удаление — Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> Этот пакет также работает в Oracle Linux 7.

### <a name="installation-via-package-repository-preferred---centos-7"></a>Установка с помощью репозитория пакетов (рекомендуется) — CentOS 7

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.

### <a name="installation-via-direct-download---centos-7"></a>Установка с помощью прямого скачивания — CentOS 7

Используя [CentOS 7][], скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с CentOS:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Затем выполните в терминале следующую команду:

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Кроме того, RPM можно установить без промежуточного скачивания:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>Удаление — CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>Установка с помощью репозитория пакетов (рекомендуется) — Red Hat Enterprise Linux (RHEL) 7

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Зарегистрировав репозиторий Майкрософт в качестве суперпользователя, в дальнейшем вам потребуется лишь использовать `sudo yum update powershell` для обновления PowerShell.

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>Установка с помощью прямого скачивания — Red Hat Enterprise Linux (RHEL) 7

Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Red Hat Enterprise Linux:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

Затем выполните в терминале следующую команду:

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Кроме того, RPM можно установить без промежуточного скачивания:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>Удаление — Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a>OpenSUSE 42.2

> **Примечание**. При установке PowerShell Core `zypper` может вывести следующее сообщение об ошибке:
>
> ```text
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> В этом случае убедитесь в наличии совместимой библиотеки `libcurl`, проверив, что в результате выполнения следующей команды пакет `libcurl4` отображается как установленный:
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> Затем при установке пакета `powershell` выберите решение `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies`.

### <a name="installation-via-package-repository-preferred---opensuse-422"></a>Установка с помощью репозитория пакетов (рекомендуется) — OpenSUSE 42.2

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Product feed
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/zypp/repos.d/microsoft.repo

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-422"></a>Установка с помощью прямого скачивания — OpenSUSE 42.2

Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с OpenSUSE:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Кроме того, RPM можно установить без промежуточного скачивания:

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a>Удаление — OpenSUSE 42.2

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a>Fedora 25

### <a name="installation-via-package-repository-preferred---fedora-25"></a>Установка с помощью репозитория пакетов (рекомендуется) — Fedora 25

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-25"></a>Установка с помощью прямого скачивания — Fedora 25

Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Fedora:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Затем выполните в терминале следующую команду:

```sh
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Кроме того, RPM можно установить без промежуточного скачивания:

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a>Удаление — Fedora 25

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a>Fedora 26

### <a name="installation-via-package-repository-preferred---fedora-26"></a>Установка с помощью репозитория пакетов (рекомендуется) — Fedora 26

Для упрощения установки (и обновления) PowerShell Core для Linux публикуются в официальных репозиториях Майкрософт.

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-26"></a>Установка с помощью прямого скачивания — Fedora 26

Скачайте пакет RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` со страницы [выпусков][] на компьютер с Fedora:

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Затем выполните в терминале следующую команду:

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

Кроме того, RPM можно установить без промежуточного скачивания:

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a>Удаление — Fedora 26

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

PowerShell можно получить из пользовательского репозитория [Arch Linux][] (AUR).

* Его можно скомпилировать с помощью [последнего выпуска с тегами][arch-release].
* Его можно скомпилировать из [последней фиксации в основной репозиторий][arch-git].
* Его можно установить с помощью [двоичного файла последнего выпуска][arch-bin].

Пакеты в AUR обслуживаются сообществом — официальная поддержка отсутствует.

Дополнительные сведения об установке пакетов из AUR см. на [вики-сайте Arch Linux](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) или в [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile) сообщества.

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a>Linux AppImage

Используя последний дистрибутив Linux, скачайте AppImage `powershell-6.0.0-x86_64.AppImage` со страницы [выпусков][] на компьютер с Linux.

Затем выполните в терминале следующую команду:

```bash
chmod a+x powershell-6.0.0-x86_64.AppImage
./powershell-6.0.0-x86_64.AppImage
```

[AppImage][] позволяет запустить PowerShell, не устанавливая его. Это переносимое приложение, которое объединяет PowerShell и его зависимости (включая системные зависимости .NET Core) в единый пакет. Этот пакет работает независимо от дистрибутива Linux пользователя и представляет собой отдельный двоичный файл.

[appimage]: http://appimage.org/

## <a name="macos-1012"></a>macOS 10.12

### <a name="installation-via-homebrew-preferred---macos-1012"></a>Установка с помощью Homebrew (рекомендуется) — macOS 10.12

[Homebrew][brew] — это диспетчер отсутствующих пакетов для macOS. Если команда `brew` не найдена, нужно установить Homebrew по [соответствующим инструкциям][brew].

После установки Homebrew установка PowerShell не вызывает проблем. Сначала установите [Homebrew-Cask][cask], чтобы можно было установить дополнительные пакеты:

```sh
brew tap caskroom/cask
```

Теперь можно установить PowerShell:

```sh
brew cask install powershell
```

После выпуска новых версий PowerShell просто обновите формулы Homebrew и PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> Примечание. Приведенные выше команды можно вызвать из узла PowerShell (pwsh), но затем потребуется выйти из оболочки PowerShell и повторно войти в нее, чтобы завершить обновление и обновить значения в таблице $PSVersionTable.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download---macos-1012"></a>Установка с помощью прямого скачивания — macOS 10.12

Используя macOS 10.12, скачайте пакет PKG `powershell-6.0.0-osx.10.12-x64.pkg` со страницы [выпусков][] на компьютер с macOS.

Дважды щелкните файл и следуйте инструкциям на экране либо установите его из терминала:

```sh
sudo installer -pkg powershell-6.0.0-osx.10.12-x64.pkg -target /
```

### <a name="uninstallation---macos-1012"></a>Удаление — macOS 10.12

Если вы установили PowerShell с помощью Homebrew, удаление осуществляется очень просто:

```sh
brew cask uninstall powershell
```

Если вы установили PowerShell с помощью прямого скачивания, PowerShell нужно удалить вручную:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Чтобы удалить дополнительные пути PowerShell (например, путь к профилю пользователя), см. раздел [Пути][paths] ниже и удалите требуемые пути с помощью `sudo rm`. (Примечание. Это не требуется в случае установки с помощью Homebrew.)

[paths]:#paths

## <a name="kali"></a>Kali

### <a name="installation"></a>Установка

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Download & Install PowerShell
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a>Запуск PowerShell в последней версии Kali (Kali GNU/Linux Rolling) без его установки

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.0-x86_64.AppImage

# Start PowerShell
./powershell-6.0.0-x86_64.AppImage
```

### <a name="uninstallation---kali"></a>Удаление — Kali

```sh
sudo dpkg -r powershell-6.0.0-x86_64.AppImage
```

## <a name="raspbian"></a>Raspbian

Сейчас PowerShell поддерживается только в Raspbian Stretch.

### <a name="installation"></a>Установка

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

### <a name="uninstallation---raspbian"></a>Удаление — Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>Архивы двоичных файлов

Для поддержки расширенных сценариев развертывания на платформах macOS и Linux доступны архивы двоичных файлов PowerShell `tar.gz`.

### <a name="dependencies"></a>Зависимости

Для Linux PowerShell создает переносимые двоичные файлы для всех дистрибутивов Linux.
Однако среда выполнения .NET Core требует различные зависимости для разных дистрибутивов, и поэтому то же самое делает и PowerShell.

Следующая таблица содержит зависимости .NET Core 2.0 для различных дистрибутивов Linux, которые поддерживаются официально.

| ОС                 | Зависимости |
| ------------------ | ------------ |
| Ubuntu 14.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Ubuntu 16.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55 |
| Ubuntu 17.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57 |
| Debian 8 (Jessie)  | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Debian 9 (Stretch) | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 <br> OpenSUSE 42.2 <br> Fedora 25 | libunwind, libcurl, openssl-libs, libicu |
| Fedora 26          | libunwind, libcurl, openssl-libs, libicu, compat-openssl10 |

Чтобы развернуть двоичные файлы PowerShell в дистрибутивах Linux без официальной поддержки, вам потребуется отдельно установить необходимые зависимости для целевой ОС. Например, наш [Amazon Linux dockerfile][amazon-dockerfile] сначала устанавливает зависимости, а затем извлекает архив Linux `tar.gz`.

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a>Установка — архивы двоичных файлов

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.0/pwsh /usr/bin/pwsh
```

#### <a name="macos"></a>macOS

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.0/pwsh /usr/local/bin/pwsh
```

### <a name="uninstallation---binary-archives"></a>Удаление — архивы двоичных файлов

#### <a name="linux"></a>Linux

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

#### <a name="macos"></a>macOS

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

## <a name="paths"></a>Пути

* `$PSHOME` имеет значение `/opt/microsoft/powershell/6.0.0/`.
* Профили пользователей будут считаны из `~/.config/powershell/profile.ps1`.
* Профили по умолчанию будут считаны из `$PSHOME/profile.ps1`.
* Модули пользователей будут считаны из `~/.local/share/powershell/Modules`.
* Общие модули будут считаны из `/usr/local/share/powershell/Modules`.
* Модули по умолчанию будут считаны из `$PSHOME/Modules`.
* Журнал PSReadline будет записан в `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`.

Профили учитывают конфигурацию PowerShell для отдельных узлов, поэтому профили конкретных узлов по умолчанию находятся в `Microsoft.PowerShell_profile.ps1` в тех же расположениях.

В Linux и macOS учитывается [спецификация базовых каталогов XDG][xdg-bds].

Обратите внимание, что, так как macOS является производной от BSD, вместо `/opt` используется префикс `/usr/local`. Таким образом, `$PSHOME` имеет значение `/usr/local/microsoft/powershell/6.0.0/`, а символьная ссылка размещается в `/usr/local/bin/pwsh`.

[выпусков]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
