# <a name="using-visual-studio-code-for-powershell-development"></a>Использование Visual Studio Code для разработки в PowerShell

В дополнение к [интегрированной среде сценариев PowerShell][ise] продукт PowerShell также хорошо поддерживается в Visual Studio Code.
Кроме того, интегрированная среда сценариев не поддерживается в PowerShell Core, хотя Visual Studio Code поддерживается для PowerShell Core на всех платформах (Windows, macOS и Linux)

Вы можете использовать Visual Studio Code для Windows вместе с PowerShell версии 5 в Windows 10 или установить [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для более низких версий Windows (например, Windows 8.1 и т. д.).

Перед запуском убедитесь, что PowerShell установлен в системе.
Сведения о современных рабочих нагрузках для Windows, macOS и Linux см. в следующих разделах:

- [Установка PowerShell Core в macOS и Linux][install-pscore-linux]
- [Установка PowerShell Core в Windows][install-pscore-windows]

Сведения о традиционных рабочих нагрузках Windows PowerShell см. в разделе [Установка Windows PowerShell][install-winps].

## <a name="editing-with-visual-studio-code"></a>Редактирование с помощью Visual Studio Code

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. Установка Visual Studio Code](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: следуйте инструкциям по установке на странице [Запуск VS Code в Linux](https://code.visualstudio.com/docs/setup/linux).

- **macOS**: следуйте инструкциям по установке на странице [Запуск VS Code в macOS](https://code.visualstudio.com/docs/setup/mac).

> [!IMPORTANT]
> В macOS нужно установить OpenSSL для правильной работы расширения PowerShell.
> Для этого проще всего установить [Homebrew](http://brew.sh/), а затем запустить `brew install openssl`.
> После этого расширение PowerShell будет загружено правильно.

- **Windows**: следуйте инструкциям по установке на странице [Запуск VS Code в Windows](https://code.visualstudio.com/docs/setup/windows).

### <a name="2-installing-powershell-extension"></a>2. Установка расширения PowerShell

- Запустите Visual Studio Code следующим образом:
    - **Windows**: введите `code` в сеансе PowerShell.
    - **Linux**: введите `code` в терминале.
    - **macOS**: введите `code` в терминале.

- Запустите **Quick Open**, нажав клавиши **CTRL+P** (**CMD+P** на Mac).
- В Quick Open введите `ext install powershell` и нажмите клавишу **ВВОД**.
- На боковой панели открывается представление **Расширения**. Выберите расширение PowerShell корпорации Майкрософт.
  Вы увидите примерно следующее:

  ![VSCode](../../images/vscode.png)

- Нажмите кнопку **Установить** для расширения PowerShell корпорации Майкрософт.
- После установки кнопка **Установить** изменится на **Перезагрузить**.
  Нажмите кнопку **Перезагрузить**.
- После перезагрузки Visual Studio Code можно приступать к редактированию.

Например, чтобы создать файл, выберите **Файл -> Создать**.
Чтобы сохранить его, выберите **Файл -> Сохранить** и укажите имя файла, например `HelloWorld.ps1`.
Чтобы закрыть файл, щелкните "x" рядом с его именем.
Чтобы завершить работу Visual Studio Code, выберите **Файл -> Выйти**.

#### <a name="using-a-specific-installed-version-of-powershell"></a>Использование определенной установленной версии PowerShell

Если вы хотите использовать с Visual Studio Code определенную установку PowerShell, нужно добавить в файл параметров пользователя новую переменную.

1. Щелкните **Файл -> Параметры -> Параметры**
1. Отображаются две панели редактора.
   На панели справа (`settings.json`) вставьте параметр в разделе соответствующей операционной системы между двумя фигурными скобками (`{` и `}`) и замените *<version>* на установленную версию PowerShell:

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. Замените параметр на путь к требуемому исполняемому файлу PowerShell.
1. Сохраните файл параметров и перезапустите Visual Studio Code.

#### <a name="configuration-settings-for-visual-studio-code"></a>Параметры конфигурации для Visual Studio Code

Следуя инструкциям в предыдущем абзаце, вы можете добавить параметры конфигурации в `settings.json`.

Мы рекомендуем использовать следующие параметры конфигурации для Visual Studio Code:

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a>Отладка с помощью Visual Studio Code

### <a name="no-workspace-debugging"></a>Отладка без рабочей области

Начиная с Visual Studio Code версии 1.9, вы можете отлаживать сценарии PowerShell, не открывая папку со сценарием PowerShell.
Просто откройте файл сценария PowerShell с помощью команды **Файл -> Открыть файл...** , установите точку останова на строке (нажав клавишу F9) и нажмите клавишу F5 для запуска отладки.
Отображается панель действий отладки, позволяющая прервать работу отладчика, возобновить отладку, выполнить ее пошагово или остановить.

### <a name="workspace-debugging"></a>Отладка с рабочей областью

Отладка с рабочей областью обозначает отладку в контексте папки, которую вы открыли в Visual Studio Code с помощью команды **Открыть папку...** из меню **Файл**.
Обычно открытая папка является папкой проекта PowerShell и (или) корнем репозитория Git.

Даже в этом режиме вы можете начать отладку выбранного сценария PowerShell, просто нажав клавишу F5.
Однако отладка с рабочей областью позволяет задать несколько конфигураций отладки, отличных от простой отладки открытого файла.
Например, можно добавить конфигурации следующего характера:

- Запуск тестов Pester в отладчике
- Запуск определенного файла с аргументами в отладчике
- Запуск интерактивного сеанса в отладчике
- Подключение отладчика к хост-процессу PowerShell

Выполните следующие действия, чтобы создать файл конфигурации отладки:

1. Откройте представление **Отладка**, нажав клавиши **CTRL+SHIFT+D** (**CMD+SHIFT+D** на Mac).
1. Щелкните значок с шестеренкой **Настройка** на панели инструментов.
1. Visual Studio Code предлагает вам **выбрать среду**.
   Выберите **PowerShell**.

   При этом Visual Studio Code создает каталог и файл ".vscode\launch.json" в корневой папке рабочей области.
   Именно там хранится ваша конфигурация отладки. Если ваши файлы хранятся в репозитории Git, скорее всего, вы захотите зафиксировать файл launch.json.
   Файла launch.json содержит следующее:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Launch (current file)",
            "script": "${file}",
            "args": [],
            "cwd": "${file}"
        },
        {
            "type": "PowerShell",
            "request": "attach",
            "name": "PowerShell Attach to Host Process",
            "processId": "${command.PickPSHostProcess}",
            "runspaceId": 1
        },
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Interactive Session",
            "cwd": "${workspaceRoot}"
        }
    ]
}
```

Это представляет типичные сценарии отладки.
Однако при открытии этого файла в редакторе вы увидите кнопку **Добавить конфигурацию...**.
Можете нажать ее, чтобы добавить дополнительные конфигурации отладки PowerShell. Одной из полезных конфигураций является **PowerShell: Launch Script**.
С помощью этой конфигурации можно указать определенный файл с дополнительными аргументами, которые нужно запускать при каждом нажатии клавиши F5 независимо от того, какой именно файл активен в редакторе.

После задания конфигурации отладки можно указать конфигурацию, используемую во время сеанса отладки, выбрав ее в раскрывающемся списке конфигураций отладки на панели инструментов представления **Отладка**.

Существует несколько блогов, которые могут оказаться полезными при начале работы с расширением PowerShell для Visual Studio Code:

- Visual Studio Code: [расширение PowerShell][ps-extension]
- [Написание и отладка в сценариев PowerShell в Visual Studio Code][debug]
- [Руководство по отладке Visual Studio Code][vscode-guide]
- [Отладка PowerShell в Visual Studio Code][ps-vscode]
- [Приступая к разработке PowerShell в Visual Studio Code][getting-started]
- [Функции редактирования Visual Studio Code для разработки PowerShell. Часть 1][editing-part1]
- [Функции редактирования Visual Studio Code для разработки PowerShell. Часть 2][editing-part2]
- [Отладка сценария PowerShell в Visual Studio Code. Часть 1][debugging-part1]
- [Отладка сценария PowerShell в Visual Studio Code. Часть 2][debugging-part2]

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-macOS-and-Linux.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]:https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]:https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]:https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]:https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]:https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a>Расширение PowerShell для Visual Studio Code

Исходный код расширения PowerShell доступен на [GitHub](https://github.com/PowerShell/vscode-powershell).