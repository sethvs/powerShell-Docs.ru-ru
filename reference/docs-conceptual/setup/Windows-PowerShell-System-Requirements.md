---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Требования к системе для Windows PowerShell"
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
ms.openlocfilehash: 33824eac4de28de97990ffa1ea2500e61e03e847
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2017
---
# <a name="windows-powershell-system-requirements"></a>Требования к системе для Windows PowerShell
В этой статье описаны требования к системе для Windows PowerShell 3.0, Windows PowerShell 4.0 и Windows PowerShell 5.0, а также для специальных функций, таких как интегрированная среда сценариев (ISE) Windows PowerShell, команды CIM и рабочие процессы.

Windows® 8.1 и Windows Server® 2012 R2 включают все необходимые программы. Эта статья предназначена для пользователей более ранних версий Windows.

## <a name="operating-system-requirements"></a>Требования к операционной системе
Windows PowerShell 5.0 работает в следующих версиях Windows.

- Windows Server 2016 — устанавливается по умолчанию.

- Windows Server 2012 R2 — установите [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для запуска Windows PowerShell 5.0.

- Windows Server 2012 — установите [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для запуска Windows PowerShell 5.0.

- Windows Server 2008 R2 с пакетом обновления 1 (SP1) — установите [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для запуска Windows PowerShell 5.0.

- Windows 8.1

- Windows 7 с пакетом обновления 1 (SP1) — установите [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) для запуска Windows PowerShell 5.0.

Windows PowerShell 4.0 выполняется в следующих версиях Windows:

- Windows 8.1, устанавливается по умолчанию

- Windows Server 2012 R2, устанавливается по умолчанию

- Windows® 7 с пакетом обновления 1 (SP1), установите [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) для запуска Windows PowerShell 4.0

- Windows Server® 2008 R2 с пакетом обновления 1 (SP1), установите [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) для запуска Windows PowerShell 4.0

Windows PowerShell 3.0 выполняется в следующих версиях Windows:

- Windows 8, устанавливается по умолчанию

- Windows Server 2012, устанавливается по умолчанию

- Windows® 7 с пакетом обновления 1 (SP1), установите [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

- Windows Server® 2008 R2 с пакетом обновления 1 (SP1), установите [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

- Windows Server 2008 R2 с пакетом обновления 2, установите [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) для запуска Windows PowerShell 3.0

## <a name="microsoft-net-framework-requirements"></a>Требования к Microsoft .NET Framework
Windows PowerShell 5.0 требует полной установки Microsoft .NET Framework 4.5. Windows 8.1 и Windows Server 2012 R2 включают Microsoft .NET Framework 4.5 по умолчанию.

Windows PowerShell 4.0 требует полной установки Microsoft .NET Framework 4.5. Windows 8.1 и Windows Server 2012 R2 включают Microsoft .NET Framework 4.5 по умолчанию.

Windows PowerShell 3.0 требует полной установки Microsoft .NET Framework 4. Windows 8 и Windows Server 2012 содержат Microsoft .NET Framework 4.5 по умолчанию, что удовлетворяет этому требованию.

Для установки Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) см. статью [Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkID=242919) в Центре загрузки Майкрософт.

Для установки полной версии Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) см. статью [Microsoft .NET Framework 4 (веб-установщик)](http://go.microsoft.com/fwlink/?LinkID=212931) в Центре загрузки Майкрософт.

## <a name="windows-management-framework-40"></a>Windows Management Framework 4.0
Для работы Windows PowerShell 5.0 необходимо установить Windows Management Framework 4.0 в Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1).

## <a name="ws-management-30"></a>WS-Management 3.0
Windows PowerShell 3.0 и Windows PowerShell 4.0 требуют наличия WS-Management 3.0, поддерживающей службу WinRM и протокол WSMan. Эта программа входит в Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 и Windows Management Framework 3.0.

## <a name="windows-management-instrumentation-30"></a>Инструментарий управления Windows 3.0
Windows PowerShell 3.0 и Windows PowerShell 4.0 требуют инструментарий управления Windows (WMI) 3.0. Эта программа входит в Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 и Windows Management Framework 3.0. Если эта программа не установлена на компьютере, компоненты, нуждающиеся в инструментарии WMI, например команды CIM, не выполняются.

## <a name="common-language-runtime-40"></a>Среда CLR 4.0
Windows PowerShell 3.0, Windows PowerShell 4.0 и Windows PowerShell 5.0 компилируются для среды CLR версии 4.0.

## <a name="graphical-user-interface-requirements"></a>Требования к графическому пользовательскому интерфейсу
Windows PowerShell — это основанное на консоли приложение, для работы которого не требуется графический пользовательский интерфейс. Поэтому оно хорошо подходит для компьютеров без экранов или мониторов либо пользовательского интерфейса, таких как Windows Server 2012 R2 или Windows Server 2012, с установкой основных серверных компонентов.

Однако некоторым элементам, например приведенным ниже, графический пользовательский интерфейс необходим. Дополнительные сведения см. в разделе справки для каждого элемента.

- Интегрированная среда сценариев Windows PowerShell Windows PowerShell (ISE)

- Командлеты

    1.  [Out-GridView](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview)

    2.  [Show-Command](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Utility/Show-Command)

    3.  [Show-ControlPanelItem](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-ControlPanelItem)

    4.  [Show-EventLog](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-EventLog)

- Параметры

    1.  Параметр **ShowWindow** командлета [Get-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Get-Help).

    2.  Параметр **ShowSecurityDescriptorUI** командлетов [Register-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Register-PSSessionConfiguration) и [Set-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Set-PSSessionConfiguration).

## <a name="windows-powershell-engine-requirements"></a>Требования к подсистеме Windows PowerShell
Windows PowerShell 4.0 предназначен для обратной совместимости с Windows PowerShell 3.0 и Windows PowerShell 2.0. Командлеты, поставщики, оснастки, модули и сценарии, написанные для Windows PowerShell 2.0, выполняются и в Windows PowerShell 3.0, и в Windows PowerShell 4.0 без изменений.

Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы Windows PowerShell, написанные для Windows PowerShell 2.0 и скомпилированные с помощью среды CLR 2.0, не могут выполняться без изменения в Windows PowerShell 3.0, которые компилируются в среде CLR 4.0.

Подсистеме Windows PowerShell 2.0 требуется Microsoft .NET Framework версии не ниже 2.0.50727. Этому требованию удовлетворяет Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1). Этому требованию не удовлетворяет Microsoft .NET Framework 4 и более поздних версий.

Дополнительные сведения о добавлении или установке подсистемы Windows PowerShell 2.0 и требуемых версий Microsoft .NET Framework см. в статье [Установка подсистемы Windows PowerShell 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md). Дополнительные сведения о запуске подсистемы Windows PowerShell 2.0 см. в статье [Запуск подсистемы Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="windows-preinstallation-environment"></a>Среда предустановки Windows
Windows PowerShell 2.0, Windows PowerShell 3.0 и Windows PowerShell 4.0 выполняются в среде предустановки Windows (Windows PE). Однако не поддерживаются следующие командлеты:

- [Командлеты фоновой интеллектуальной службы передачи (BITS)](http://go.microsoft.com/fwlink/?LinkId=257514)

- [Get-EventLog](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Get-EventLog)

- [Get-WinEvent](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent)

- [Save-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Save-Help)

- [Update-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Update-Help)

Кроме того, в Windows PE отсутствует служба **WinRM**.

## <a name="see-also"></a>См. также
- [Начало работы с Windows PowerShell](../getting-started/Getting-Started-with-Windows-PowerShell.md)
- [Установка Windows PowerShell](Installing-Windows-PowerShell.md)
- [Запуск Windows PowerShell](Starting-Windows-PowerShell.md)

