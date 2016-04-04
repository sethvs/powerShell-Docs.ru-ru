# Системные требования

- Перед установкой WMF 5.0 RTM установите последние обновления для Windows.
- WMF 5.0 RTM работает только в следующих операционных системах:

    | Операционная система | Выпуски | Необходимые условия | Ссылки на пакеты |
    |------------------------|--------------|------------------|----------------------| --------------|
    | Windows Server 2012 R2 |  |  | <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkId=717507)">Win8.1AndW2K12R2-KB3134758-x64.msu</ctype="x-NOTFOUND"> |
    | Windows Server 2012    |  |  | <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkId=717506)">W2K12-KB3134759-x64.msu</ctype="x-NOTFOUND"> |
    | Windows Server 2008 R2 с пакетом обновления 1 (SP1) | Все, кроме IA64 | Установлены <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://www.microsoft.com/en-us/download/details.aspx?id=40855)">WMF 4.0</ctype="x-NOTFOUND"> и <ctype="x-NOTFOUND" mdpre="[" mdpost="](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)">.NET Framework 4.5 или более ранней версии</ctype="x-NOTFOUND">| <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkId=717504)">Win7AndW2K8R2-KB3134760-x64.msu</ctype="x-NOTFOUND">|
    | Windows 8.1 | Профессиональная, Корпоративная | | <ctype="x-NOTFOUND" mdpre="**" mdpost="**">x64:</ctype="x-NOTFOUND"> <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkId=717507)">Win8.1AndW2K12R2-KB3134758-x64.msu</ctype="x-NOTFOUND"> </br> <ctype="x-NOTFOUND" mdpre="**" mdpost="**">x86:</ctype="x-NOTFOUND"> <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkID=717963)">Win8.1-KB3134758-x86.msu</ctype="x-NOTFOUND">|
    | Windows 7 с пакетом обновления 1 (SP1) | Все | Установлены <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://www.microsoft.com/en-us/download/details.aspx?id=40855)">WMF 4.0</ctype="x-NOTFOUND"> и <ctype="x-NOTFOUND" mdpre="[" mdpost="](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)">.NET Framework 4.5 или более ранней версии</ctype="x-NOTFOUND"> | <ctype="x-NOTFOUND" mdpre="**" mdpost="**">x64:</ctype="x-NOTFOUND"> <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkId=717504)">Win7AndW2K8R2-KB3134760-x64.msu</ctype="x-NOTFOUND">  </br> <ctype="x-NOTFOUND" mdpre="**" mdpost="**">x86:</ctype="x-NOTFOUND">  <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://go.microsoft.com/fwlink/?LinkID=717962)">Win7-KB3134760-x86.msu</ctype="x-NOTFOUND">|

# Инструкции по установке

### Установка WMF 5.0 из проводника Windows Explorer (или File Explorer):

1. Перейдите в папку, куда был скачан MSU-файл.

2. Дважды щелкните этот файл для его запуска.

### Установка WMF 5.0 из командной строки:

1. После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора"). В установке основных серверных компонентов для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.

2. Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.0.

3. Выполните одну из следующих команд:
    - На компьютерах под управлением Windows Server 2012 R2 или Windows 8.1 (x64) запустите команду <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Win8.1AndW2K12R2-KB3134758-x64.msu /quiet</ctype="x-NOTFOUND">.
    - На компьютерах под управлением Windows Server 2012 запустите команду <ctype="x-NOTFOUND" mdpre="**" mdpost="**">W2K12-KB3134759-x64.msu /quiet</ctype="x-NOTFOUND">.
    - На компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) (x64) запустите команду <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Win7AndW2K8R2-KB3134760-x64.msu /quiet</ctype="x-NOTFOUND">.
    - На компьютерах под управлением Windows 8.1 (x86) запустите команду <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Win8.1-KB3134758-x86.msu /quiet</ctype="x-NOTFOUND">.
    - На компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) (x86) запустите команду <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Win7-KB3134760-x86.msu /quiet</ctype="x-NOTFOUND">.

### Дополнительные замечания по установке для Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):

Убедитесь, что выполнены следующие предварительные условия.
- Установлен самый последний пакет обновления.
- Установлен <ctype="x-NOTFOUND" mdpre="[" mdpost="](http://www.microsoft.com/en-us/download/details.aspx?id=40855)">WMF 4.0</ctype="x-NOTFOUND">.
- Установлена <ctype="x-NOTFOUND" mdpre="[" mdpost="](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx)">платформа .NET Framework 4.5 или более ранней версии</ctype="x-NOTFOUND">.

**Зависимость WMF 4.0**

Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1) содержат встроенные PowerShell 2.0, WinRM и WMI. Пакеты WMF 3.0 и WMF 4.0, которые обновляют эти встроенные компоненты, были выпущены после выпуска Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1). При установке или удалении пакетов WMF 3.0 и WMF 4.0 были выявлены некоторые проблемы при следующих вариантах обновления:

- Встроенные методы --> WMF 4.0.
- Встроенные методы --> WMF 3.0--> WMF4.0. 

Все эти проблемы были устранены в пакетах WMF 4.0. Таким образом, для установки WMF 5.0 в системе Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) в ней должен быть установлен WMF 4.0. Ниже приведены конкретные проблемы, которые могут возникнуть при установке WMF 4.0 перед обновлением до WMF 5.0.

- Журнал перенаправленных событий недоступен, и журнал EventCollector не отображается в окне просмотра событий после удаления WMF 3.0 или WMF 5.0 (без предварительной установки WMF 4.0) в Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1) (<ctype="x-NOTFOUND" mdpre="[" mdpost="](https://support.microsoft.com/en-us/kb/2809215)">KB2809215</ctype="x-NOTFOUND">).
- Установленное значение переменной среды <ctype="x-NOTFOUND" mdpre="*" mdpost="*">PSModulePath</ctype="x-NOTFOUND"> сбрасывается в значение по умолчанию при обновлении до WMF 5.0 напрямую из встроенного PowerShell 2.0 (<ctype="x-NOTFOUND" mdpre="[" mdpost="](https://support.microsoft.com/en-us/kb/2872035)">KB2872035</ctype="x-NOTFOUND">) или при обновлении с WMF 3.0 до WMF 5.0. (<ctype="x-NOTFOUND" mdpre="[" mdpost="](https://support.microsoft.com/en-us/kb/2872047)">KB2872047</ctype="x-NOTFOUND">) в Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1).

**Зависимость от WinRM**

Служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM. По умолчанию WinRM не включена в Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1). Чтобы включить WinRM, выполните командлет <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Set-WSManQuickConfig</ctype="x-NOTFOUND"> в сеансе Windows PowerShell с повышенными привилегиями.

# Инструкции по удалению

### Использование командной строки

1.  Откройте <ctype="x-NOTFOUND" mdpre="**" mdpost="**">командную строку</ctype="x-NOTFOUND">.

2.  Запустите <ctype="x-NOTFOUND" mdpre="[" mdpost="](https://support.microsoft.com/en-us/kb/934307)">Автономное средство запуска Центра обновления Windows</ctype="x-NOTFOUND">, как показано ниже:

В Windows Server 2012 R2 и Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
В Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
В Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):
```powershell
wusa /uninstall /kb:3134760
```

### Использование панели управления

1.  Откройте <ctype="x-NOTFOUND" mdpre="**" mdpost="**">панель управления</ctype="x-NOTFOUND">.

2.  Откройте раздел <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Программы</ctype="x-NOTFOUND"> и выберите <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Удаление программы</ctype="x-NOTFOUND">.

3.  Щелкните <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Просмотр установленных обновлений</ctype="x-NOTFOUND">.

4.  Выберите <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Windows Management Framework 5.0</ctype="x-NOTFOUND"> в списке установленных обновлений. Это соответствует <ctype="x-NOTFOUND" mdpre="*" mdpost="*">KB3134758</ctype="x-NOTFOUND">, <ctype="x-NOTFOUND" mdpre="*" mdpost="*">KB3134759</ctype="x-NOTFOUND"> или <ctype="x-NOTFOUND" mdpre="*" mdpost="*">KB3134760</ctype="x-NOTFOUND">. Щелкните <ctype="x-NOTFOUND" mdpre="**" mdpost="**">Удалить</ctype="x-NOTFOUND">.


<!--HONumber=Mar16_HO4-->


