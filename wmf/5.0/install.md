# Инструкции по установке

Скачайте подходящий пакет для своей операционной системы и архитектуры:

| Операционная система       | Архитектура | Имя пакета              | 
|------------------------|--------------|---------------------------| 
| Windows Server 2012 R2 | x64      | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) | 
| Windows Server 2012    | x64      | [W2K12-KB3134759-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) | 
| Windows Server 2008 R2 | x64      | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 8.1            | x64          | [Win8.1AndW2K12R2-KB3134758-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows 8.1            | x86          | [Win8.1-KB3134758-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963) |
| Windows 7 с пакетом обновления 1 (SP1)          | x64          | [Win7AndW2K8R2-KB3134760-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 7 с пакетом обновления 1 (SP1)          | x86          | [Win7-KB3134760-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962) |


**Установка WMF 5.0 из проводника Windows Explorer (или File Explorer в Windows Server 2012 R2 и Windows 8.1):**

1. Перейдите в папку, куда был скачан MSU-файл.

2. Дважды щелкните этот файл для его запуска.

**Установка WMF 5.0 из командной строки:** 

1. После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора"). В установке основных серверных компонентов для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.

2. Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.0.

3. Выполните одну из следующих команд:
    - На компьютерах под управлением Windows Server 2012 R2 или Windows 8.1 (x64) запустите **Win8.1AndW2K12R2-KB3134758-x64.msu /quiet**.
    - На компьютерах под управлением Windows Server 2012 запустите **W2K12-KB3134759-x64.msu /quiet**.
    - На компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) (x64) запустите **Win7AndW2K8R2-KB3134760-x64.msu /quiet**.
    - На компьютерах под управлением Windows 8.1 (x86) запустите **Win8.1-KB3134758-x86.msu /quiet**.
    - На компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) (x86) запустите **Win7-KB3134760-x86.msu /quiet**.

**Дополнительные замечания по установке для Windows Server 2008 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1):**

Убедитесь, что выполнены следующие предварительные условия.
- Установлен самый последний пакет обновления.
- Установлен [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855).

*Зависимость от WinRM:* служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM. По умолчанию WinRM не включен в Windows Server 2008 R2 и Windows 7. Чтобы включить WinRM, запустите **Set-WSManQuickConfig** в сеансе с повышенными привилегиями Windows PowerShell.




<!--HONumber=Jun16_HO4-->


