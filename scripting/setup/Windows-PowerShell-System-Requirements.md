---
title: Требования к системе для Windows PowerShell
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
---
# Требования к системе для Windows PowerShell
В этой статье описаны системные требования для Windows PowerShell 3.0 и Windows PowerShell 4.0, а также специальные функции, такие как интегрированная среда сценариев (ISE) Windows PowerShell, команды CIM и рабочие процессы.

WindowsÂ® 8.1 и ServerÂ Windows® 2012 R2 включают все необходимые программы. Эта статья предназначена для пользователей более ранних версий Windows.

## Требования к операционной системе
Windows PowerShell 4.0 выполняется в следующих версиях Windows:

-   Windows 8.1, устанавливается по умолчанию

-   Windows Server 2012 R2, устанавливается по умолчанию

-   WindowsÂ® 7 с пакетом обновления 7 (SP1), установите [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkId=293881) для запуска Windows PowerShell 4.0

-   Windows ServerÂ® 2008 R2 с пакетом обновления 7 (SP1), установите [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkId=293881) для запуска Windows PowerShell 4.0

Windows PowerShell 3.0 выполняется в следующих версиях Windows:

-   Windows 8, устанавливается по умолчанию

-   Windows Server 2012, устанавливается по умолчанию

-   WindowsÂ® 7 с пакетом обновления 7 (SP1), установите [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

-   Windows ServerÂ® 2008 R2 с пакетом обновления 7 (SP1), установите [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

-   Windows Server 2008 R2 с пакетом обновления 2, установите [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

## Требования к Microsoft .NET Framework
Windows PowerShell 4.0 требует полной установки Microsoft .NET Framework 4.5. Windows 8.1 и Windows Server 2012 R2 включают Microsoft .NET Framework 4.5 по умолчанию.

Windows PowerShell 3.0 требует полной установки Microsoft .NET Framework 4. Windows 8 и Windows Server 2012 содержат Microsoft .NET Framework 4.5 по умолчанию, что удовлетворяет этому требованию.

Для установки Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) см. статью [Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkID=242919) в Центре загрузки Майкрософт.

Для установки полной версии Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) см. статью [Microsoft .NET Framework 4 (веб-установщик)](http://go.microsoft.com/fwlink/?LinkID=212931) в Центре загрузки Майкрософт.

## WS-Management 3.0
Windows PowerShell 3.0 и Windows PowerShell 4.0 требуют наличия WS-Management 3.0, поддерживающей службу WinRM и протокол WSMan. Эта программа входит в Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 и Windows Management Framework 3.0.

## Инструментарий управления Windows 3.0
Windows PowerShell 3.0 и Windows PowerShell 4.0 требуют инструментарий управления Windows (WMI) 3.0. Эта программа входит в Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 и Windows Management Framework 3.0. Если эта программа не установлена на компьютере, компоненты, нуждающиеся в инструментарии WMI, например команды CIM, не выполняются.

## Среда CLR 4.0
Windows PowerShell 3.0 и Windows PowerShell 4.0 компилируются для среды CLR 4.0.

## Требования к графическому пользовательскому интерфейсу
Windows PowerShell — это основанное на консоли приложение, для работы которого не требуется графический пользовательский интерфейс. Поэтому оно хорошо подходит для компьютеров без экранов или мониторов либо пользовательского интерфейса, таких как Windows Server 2012 R2 или Windows Server 2012, с установкой основных серверных компонентов.

Однако некоторым элементам, например приведенным ниже, графический пользовательский интерфейс необходим. Дополнительные сведения см. в разделе справки для каждого элемента.

-   Интегрированная среда сценариев Windows PowerShell Windows PowerShell (ISE)

-   Командлеты

    1.  [Out-GridView](https://technet.microsoft.com/en-us/library/70915a86-d753-464e-8349-cba02316154c)

    2.  [Show-Command](https://technet.microsoft.com/en-us/library/65bba50b-91a8-49d5-80a2-a30fc684ba41)

    3.  [Show-ControlPanelItem](https://technet.microsoft.com/en-us/library/0685d42c-37cc-498f-acf6-0ecfeb0cb162)

    4.  [Show-EventLog](https://technet.microsoft.com/en-us/library/a3b0f5ad-0438-42c7-915b-d1b4793a431c)

-   Параметры

    1.  Параметр **ShowWindow** командлета [Get-Help](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a).

    2.  Параметр **ShowSecurityDescriptorUi** командлетов [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) и [Set-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea).

## Требования к подсистеме Windows PowerShell
Windows PowerShell 4.0 предназначен для обратной совместимости с Windows PowerShell 3.0 и Windows PowerShell 2.0. Командлеты, поставщики, оснастки, модули и сценарии, написанные для Windows PowerShell 2.0 и Windows PowerShell 3.0, выполняются в Windows PowerShell 4.0 без изменений.

Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы Windows PowerShell, написанные для Windows PowerShell 2.0 и скомпилированные с помощью среды CLR 2.0, не могут выполняться без изменения в Windows PowerShell 3.0, которые компилируются в среде CLR 4.0.

Подсистеме Windows PowerShell 2.0 требуется Microsoft .NET Framework версии не ниже 2.0.50727. Этому требованию удовлетворяет Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1). Этому требованию не удовлетворяет Microsoft .NET Framework 4 и более поздних версий.

Дополнительные сведения о добавлении или установке подсистемы Windows PowerShell 2.0 и требуемых версий Microsoft .NET Framework см. в статье [Установка подсистемы Windows PowerShell 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md). Дополнительные сведения о запуске подсистемы Windows PowerShell 2.0 см. в статье [Запуск подсистемы Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md)..

## Среда предустановки Windows
Windows PowerShell 2.0, Windows PowerShell 3.0 и Windows PowerShell 4.0 выполняются в среде предустановки Windows (Windows PE). Однако не поддерживаются следующие командлеты:

-   [Командлеты фоновой интеллектуальной службы передачи (BITS)](http://go.microsoft.com/fwlink/?LinkId=257514)

-   [Get-EventLog](https://technet.microsoft.com/en-us/library/b4985b11-82bf-487d-928d-becd96fc0419)

-   [Get-WinEvent[PSITPro5_Diagnostic]](https://technet.microsoft.com/en-us/library/5fe94870-ed6b-4ce2-9500-93846cc65c95)

-   [Save-Help](https://technet.microsoft.com/en-us/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa)

-   [Update-Help](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545)

Кроме того, в Windows PE отсутствует служба **WinRm**.

## См. также
[Начало работы с Windows PowerShell](../getting-started/Getting-Started-with-Windows-PowerShell.md)
[Установка Windows PowerShell](Installing-Windows-PowerShell.md)
[Запуск Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)



<!--HONumber=May16_HO2-->


