---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Выполнение удаленных команд"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 24648e8f35fbc28c9ba9f9b7176ac23e72ffbe78
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="running-remote-commands"></a>Выполнение удаленных команд

Вы можете запускать команды на одном или сотнях компьютеров одной командой Windows PowerShell. Windows PowerShell поддерживает удаленное вычисление с помощью разных технологий, включая WMI, RPC и WS-Management.

## <a name="remoting-in-powershell-core"></a>Удаленное взаимодействие в PowerShell Core

PowerShell Core, более новый выпуск PowerShell для Windows, macOS и Linux, поддерживает инструментарий WMI, WS-Management и удаленное взаимодействие SSH.
(RPC больше не поддерживается.)

Дополнительные сведения о настройке см. в указанных ниже разделах:

* [Удаленное взаимодействие через SSH в PowerShell Core][ssh-remoting]
* [Удаленное взаимодействие через WinRM в PowerShell Core][winrm-remoting]

## <a name="remoting-without-configuration"></a>Удаленное взаимодействие без настройки
Многие командлеты Windows PowerShell имеют параметр ComputerName, который позволяет собирать данные и изменять параметры одного или нескольких удаленных компьютеров. Они используют различные способы связи, многие из которых работают во всех операционных системах Windows, которые Windows PowerShell поддерживает без необходимости какой-либо настройки.

В эти командлеты входят следующие:

* [Restart-Computer](https://go.microsoft.com/fwlink/?LinkId=821625)
* [Test-Connection](https://go.microsoft.com/fwlink/?LinkId=821646)
* [Clear-EventLog](https://go.microsoft.com/fwlink/?LinkId=821568)
* [Get-EventLog](https://go.microsoft.com/fwlink/?LinkId=821585)
* [Get-HotFix](https://go.microsoft.com/fwlink/?LinkId=821586)
* [Get-Process](https://go.microsoft.com/fwlink/?linkid=821590)
* [Get-Service](https://go.microsoft.com/fwlink/?LinkId=821593)
* [Set-Service](https://go.microsoft.com/fwlink/?LinkId=821633)
* [Get-WinEvent](https://go.microsoft.com/fwlink/?linkid=821529)
* [Get-WmiObject](https://go.microsoft.com/fwlink/?LinkId=821595)

Обычно командлеты, которые поддерживают удаленное взаимодействие без специальной настройки, имеют параметр ComputerName, но не имеют параметра Session. Чтобы найти эти командлеты в сеансе, введите:

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a>Служба удаленного взаимодействия Windows PowerShell
Служба удаленного взаимодействия Windows PowerShell, использующая протокол WS-Management, позволяет запустить любую команду Windows PowerShell на одном или нескольких удаленных компьютерах. С ее помощью можно устанавливать постоянные подключения, запускать интерактивные сеансы 1:1 и сценарии на нескольких компьютерах.

Чтобы использовать службу удаленного взаимодействия Windows PowerShell, удаленный компьютер должен быть настроен для удаленного управления. Дополнительные сведения, в том числе инструкции, см. в разделе [about_Remote_Requirements](https://technet.microsoft.com/library/dd315349.aspx).

После настройки службы удаленного взаимодействия Windows PowerShell вам станут доступны многие стратегии удаленного взаимодействия. В остальной части этого документа перечислены только некоторые из них. Дополнительные сведения см. в разделах [about_Remote](https://technet.microsoft.com/library/dd347744.aspx) и [about_Remote_FAQ](https://technet.microsoft.com/library/dd347744.aspx).

### <a name="start-an-interactive-session"></a>Запуск интерактивного сеанса
Чтобы запустить интерактивный сеанс с одним удаленным компьютером, используйте командлет [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477).
Например, чтобы запустить интерактивный сеанс с удаленным компьютером Server01, введите:

```
Enter-PSSession Server01
```

В командной строке отобразится имя компьютера, к которому вы подключены. В дальнейшем все команды, введенные в командной строке, будут запускаться на удаленном компьютере, а результаты отобразятся на локальном компьютере.

Чтобы завершить интерактивный сеанс, введите:

```
Exit-PSSession
```

Дополнительные сведения о командлетах Enter-PSSession и Exit-PSSession см. в статьях [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) и [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).

### <a name="run-a-remote-command"></a>Выполнение удаленной команды
Чтобы выполнить любую команду на одном или нескольких удаленных компьютеров, используйте командлет [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).
Например, чтобы выполнить команду [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) на удаленных компьютерах Server01 и Server02, введите:

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

Выходные данные будут возвращены на ваш компьютер.

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="run-a-script"></a>Запуск сценария
Чтобы запустить сценарий на одном или нескольких удаленных компьютерах, используйте параметр FilePath командлета Invoke-Command. Сценарий должен быть включен или доступен для локального компьютера. Результаты будут возвращены на локальный компьютер.

Например, следующая команда выполняет сценарий DiskCollect.ps1 на удаленных компьютерах Server01 и Server02.

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

Дополнительные сведения о командлете Invoke-Command см. в статье [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).

### <a name="establish-a-persistent-connection"></a>Установка постоянного подключения
Чтобы выполнить ряд связанных команд с общими данными, создайте сеанс на удаленном компьютере, а затем используйте командлет Invoke-Command для выполнения команд в созданном сеансе. Чтобы создать удаленный сеанс, используйте командлет New-PSSession.

Например, следующая команда создает удаленный сеанс на компьютере Server01 и другой удаленный сеанс на компьютере Server02. Она сохраняет объекты сеанса в переменной $s.

```
$s = New-PSSession -ComputerName Server01, Server02
```

После установки сеансов в них можно выполнить любую команду. Так как сеансы являются постоянными, вы можете собирать данные в одной команде и использовать их в последующей.

Например, следующая команда выполняет команду Get-Hotfix в сеансах в переменной $s и сохраняет результаты в переменной $h. Переменная $h создается в каждом сеансе в $s, но она не существует в локальном сеансе.

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

Теперь данные в переменной $h можно использовать в последующих командах, таких как следующая. Результаты отобразятся на локальном компьютере.

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a>Расширенная служба удаленного взаимодействия
Это и есть служба удаленного взаимодействия Windows PowerShell. Используя командлеты, установленные с Windows PowerShell, можно установить и настроить удаленные сеансы с локальных и удаленных компьютеров, создать настраиваемые и ограниченные сеансы, разрешить пользователям импортировать команды из удаленного сеанса, которые могут неявно выполняться в удаленном сеансе, настроить безопасность удаленного сеанса и многое другое.

Для упрощения настройки в PowerShell включен поставщик WSMan. Диск WSMAN:, созданный поставщиком, позволяет перемещаться по иерархии параметров конфигурации на локальном и удаленном компьютерах.
Дополнительные сведения о поставщике WSMan см. в разделах [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) и [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx) или введите команду Get-Help wsman в консоли Windows PowerShell.

Дополнительная информация:
- [Часто задаваемые вопросы об удаленном взаимодействии](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)

Справку по ошибкам службы удаленного взаимодействия см. в статье [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).

## <a name="see-also"></a>См. также
- [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [about_Remote_FAQ](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [about_Remote_Requirements](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [about_PSSessions](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [about_WS-Management_Cmdlets](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493)
- [Import-PSSession](https://go.microsoft.com/fwlink/?LinkId=821821)
- [New-PSSession](https://go.microsoft.com/fwlink/?LinkId=821498)
- [Register-PSSessionConfiguration](https://go.microsoft.com/fwlink/?LinkId=821508)
- [Поставщик WSMan](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-resmoting]: SSH-Remoting-in-PowerShell-Core.md
