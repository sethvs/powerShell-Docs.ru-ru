# <a name="ws-management-wsman-remoting-in-powershell-core"></a>Удаленное взаимодействие с WS-Management (WSMan) в PowerShell Core

## <a name="instructions-to-create-a-remoting-endpoint"></a>Инструкции по созданию конечной точки удаленного взаимодействия

Пакет PowerShell Core для Windows включает подключаемый модуль WinRM (`pwrshplugin.dll`) и сценарий установки (`Install-PowerShellRemoting.ps1`) в `$PSHome`.
Эти файлы позволяют PowerShell принимать входящие удаленные подключения PowerShell, когда указана его конечная точка.

### <a name="motivation"></a>Причины для использования

Установка PowerShell может устанавливать удаленные сеансы PowerShell с компьютерами, используя `New-PSSession` и `Enter-PSSession`.
Чтобы включить прием входящих удаленных подключений PowerShell, пользователю нужно создать конечную точку удаленного взаимодействия WinRM.
Это сценарий, требующий явного согласия, в котором пользователь запускает Install-PowerShellRemoting.ps1 для создания конечной точки WinRM.
Сценарий установки — это временное решение, пока в `Enable-PSRemoting` не будет добавлена дополнительная функциональность для выполнения данной задачи.
Дополнительные сведения см. в описании вопроса [1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>Действия сценария

Сценарий

1. Создает каталог для подключаемого модуля в расположении %windir%\System32\PowerShell.
1. Копирует туда pwrshplugin.dll.
1. Создает файл конфигурации.
1. Регистрирует этот подключаемый модуль в службе WinRM.

### <a name="registration"></a>Регистрация

Сценарий следует запускать в сеансе PowerShell с правами администратора, и выполняется он в двух режимах.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Выполнение экземпляром PowerShell, где он будет зарегистрирован

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Выполнение экземпляром PowerShell, отличным от того, где он будет зарегистрирован

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Пример:

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

**Примечание**. Сценарий регистрации удаленного взаимодействия перезапускает WinRM, поэтому сразу после его запуска все существующие сеансы PSRP завершаются. Если запустить его во время удаленного сеанса, соединение будет разорвано.

## <a name="how-to-connect-to-the-new-endpoint"></a>Подключение к новой конечной точке

Создайте сеанс PowerShell с новой конечной точкой PowerShell, указав `-ConfigurationName "some endpoint name"`. Чтобы подключиться к экземпляру PowerShell из примера выше, используйте одну из следующих команд:

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Обратите внимание, что вызовы `New-PSSession` и `Enter-PSSession`, которые не указывают `-ConfigurationName`, ориентируются на конечную точку PowerShell по умолчанию — `microsoft.powershell`.