---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "powershell,командлет"
ms.date: 2016-12-12
title: "Установка Windows PowerShell"
ms.technology: powershell
ms.assetid: 6fbb0409-5a54-48ec-95e6-7f8b7d8c4969
ms.openlocfilehash: fd0336b66312293c434ae2c5ad5a7899c20777ff
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="installing-windows-powershell"></a>Установка Windows PowerShell
В состав Windows® 8 и Windows Server® 2012 входит Windows PowerShell 3.0 и все необходимые компоненты этой оболочки. Система также включает модуль Windows PowerShell 2.0 для обеспечения обратной совместимости с основными программами, которые не могут использовать Windows PowerShell 3.0.

В этой статье описана установка Windows PowerShell 3.0 в предыдущих версиях систем, а также установка и включение необходимых компонентов.

Эта статья содержит следующие разделы.

-   [Установка Windows PowerShell в Windows 8 и Windows Server 2012](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows8andWindowsServer2012)

-   [Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows7andWindowsServer2008R2)

-   [Установка Windows PowerShell в Windows Server 2008](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindowsServer2008LH)

-   [Установка Windows PowerShell в основных серверных компонентах](Installing-Windows-PowerShell.md#BKMK_InstallingOnServerCore)

-   [Развертывание Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/639d0eff-98a3-4124-b52c-26921ebd98b0)

-   [Установка подсистемы Windows PowerShell 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md)

## <a name="a-namebkmkinstallingonwindows8andwindowsserver2012ainstalling-windows-powershell-on-windows-8-and-windows-server-2012"></a><a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>Установка Windows PowerShell в Windows 8 и Windows Server 2012
Windows PowerShell 3.0 предоставляется установленной, настроенной и готовой к использованию. Интегрированная среда сценариев Windows PowerShell (ISE) установлена и включена. Дополнительные сведения о запуске Windows PowerShell см. в статьях [Starting Windows PowerShell on Windows 8](https://technet.microsoft.com/en-us/library/d7be1668-8617-4890-ad90-dd9765fbd2c3) (Запуск Windows PowerShell в Windows 8) и [Starting Windows PowerShell on Windows Server 2012](https://technet.microsoft.com/library/hh831491.aspx#BKMK_powershell) (Запуск Windows PowerShell в Windows Server 2012).

## <a name="a-namebkmkinstallingonwindows7andwindowsserver2008r2ainstalling-windows-powershell-on-windows-7-and-windows-server-2008-r2"></a><a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1). Ниже приведены отдельные инструкции по установке для компьютеров под управлением Windows Server 2008 R2 с установкой основных серверных компонентов.

#### <a name="getting-ready-to-install"></a>Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### <a name="to-install-windows-powershell-30"></a>Установка Windows PowerShell 3.0

1.  Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Можно также установить Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

2.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

Сведения о запуске Windows PowerShell 3.0 см. в статье [Запуск Windows PowerShell в более ранних версиях Windows](Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md).

## <a name="a-namebkmkinstallingonservercoreainstalling-windows-powershell-on-server-core"></a><a name="BKMK_InstallingOnServerCore"></a>Установка Windows PowerShell в основных серверных компонентах
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) с установкой основных серверных компонентов.

Первые шаги в процедуре используют команды системы обслуживания образов развертывания и управления ими (DISM) для установки Microsoft .NET Framework 2.0 для основных серверных компонентов и Windows PowerShell 2.0. Эти программы являются необходимыми компонентами для Windows Management Framework 3.0, который устанавливается на последующем шаге.

#### <a name="getting-ready-to-install"></a>Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### <a name="to-install-windows-powershell-30"></a>Установка Windows PowerShell 3.0

1.  Запуск Cmd.exe

2.  Выполните указанные ниже команды DISM. Эти команды устанавливают .NET Framework 2.0 и Windows PowerShell 2.0.

    ```
    dism /online /enable-feature:NetFx2-ServerCore
    dism /online /enable-feature:MicrosoftWindowsPowerShell
    dism /online /enable-feature:NetFx2-ServerCore-WOW64
    ```

3.  Установите полную версию Microsoft .NET Framework 4.0 для основных серверных компонентов из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450).

4.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## <a name="a-namebkmkinstallingonwindowsserver2008lhainstalling-windows-powershell-on-windows-server-2008"></a><a name="BKMK_InstallingOnWindowsServer2008LH"></a>Установка Windows PowerShell в Windows Server 2008
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 с пакетом обновления 2 (SP2).

В системах Windows Server 2008 Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) является необходимым компонентом для Windows Management Framework 3.0. Компонент расширенной защиты для проверки подлинности защищает компьютер от атак перенаправления проверки подлинности и позволяет использовать параметр **UseSSL** при создании удаленных сеансов. Чтобы установить Windows PowerShell 3.0 и модуль Windows PowerShell 2.0, используйте следующую процедуру.

#### <a name="getting-ready-to-install"></a>Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### <a name="to-install-windows-powershell-30"></a>Установка Windows PowerShell 3.0

1.  Установите Microsoft .NET Framework 3.5 с пакетом обновления 1 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910).

2.  Установите Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035).

3.  Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Можно также установить Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

4.  Установите компонент расширенной защиты для проверки подлинности (статья базы знаний 968389) по адресу [http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398).

5.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## <a name="see-also"></a>См. также
- [Требования Windows PowerShell к системе](Windows-PowerShell-System-Requirements.md)
- [Запуск Windows PowerShell](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)

