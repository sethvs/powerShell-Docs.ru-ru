---
title: "Установка Windows PowerShell"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 6fbb0409-5a54-48ec-95e6-7f8b7d8c4969
translationtype: Human Translation
ms.sourcegitcommit: f856f170c6e18be8758d52df9b50ac443531fdf2
ms.openlocfilehash: 415e68b372c831ed8dd4535c2968e5a36b5cb65d

---

# Установка Windows PowerShell
В состав Windows® 8 и Windows Server® 2012 входит Windows PowerShell 3.0 и все необходимые компоненты этой оболочки. Система также включает модуль Windows PowerShell 2.0 для обеспечения обратной совместимости с основными программами, которые не могут использовать Windows PowerShell 3.0.

В этой статье описана установка Windows PowerShell 3.0 в предыдущих версиях систем, а также установка и включение необходимых компонентов.

Эта статья содержит следующие разделы.

-   [Установка Windows PowerShell в Windows 8 и Windows Server 2012](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows8andWindowsServer2012)

-   [Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows7andWindowsServer2008R2)

-   [Установка Windows PowerShell в Windows Server 2008](Installing-Windows-PowerShell.md#BKMK_InstallingOnWindowsServer2008LH)

-   [Установка Windows PowerShell в основных серверных компонентах](Installing-Windows-PowerShell.md#BKMK_InstallingOnServerCore)

-   [Развертывание Windows PowerShell Web Access](https://technet.microsoft.com/en-us/library/639d0eff-98a3-4124-b52c-26921ebd98b0)

-   [Установка подсистемы Windows PowerShell 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md)

## <a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>Установка Windows PowerShell в Windows 8 и Windows Server 2012
Windows PowerShell 3.0 предоставляется установленной, настроенной и готовой к использованию. Интегрированная среда сценариев Windows PowerShell (ISE) установлена и включена. Дополнительные сведения о запуске Windows PowerShell см. в статьях [Starting Windows PowerShell on Windows 8](https://technet.microsoft.com/en-us/library/d7be1668-8617-4890-ad90-dd9765fbd2c3) (Запуск Windows PowerShell в Windows 8) и [Starting Windows PowerShell on Windows Server 2012](https://technet.microsoft.com/library/hh831491.aspx#BKMK_powershell) (Запуск Windows PowerShell в Windows Server 2012).

## <a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows 7 с пакетом обновления 1 (SP1) и Windows Server 2008 R2 с пакетом обновления 1 (SP1). Ниже приведены отдельные инструкции по установке для компьютеров под управлением Windows Server 2008 R2 с установкой основных серверных компонентов.

#### Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка Windows PowerShell 3.0

1.  Установите полную версию Microsoft .NET Framework 4 (dotNetFx40\_Full\_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Также можно установить Microsoft .NET Framework 4.5 (dotNetFx45\_Full\_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

2.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

Сведения о запуске Windows PowerShell 3.0 см. в статье [Запуск Windows PowerShell в более ранних версиях Windows](Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md).

## <a name="BKMK_InstallingOnServerCore"></a>Установка Windows PowerShell в основных серверных компонентах
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 R2 с пакетом обновления 1 (SP1) с установкой основных серверных компонентов.

Первые шаги в процедуре используют команды системы обслуживания образов развертывания и управления ими (DISM) для установки Microsoft .NET Framework 2.0 для основных серверных компонентов и Windows PowerShell 2.0. Эти программы являются необходимыми компонентами для Windows Management Framework 3.0, который устанавливается на последующем шаге.

#### Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка Windows PowerShell 3.0

1.  Запуск Cmd.exe

2.  Выполните указанные ниже команды DISM. Эти команды устанавливают .NET Framework 2.0 и Windows PowerShell 2.0.

    ```
    dism /online /enable-feature:NetFx2-ServerCore
    dism /online /enable-feature:MicrosoftWindowsPowerShell
    dism /online /enable-feature:NetFx2-ServerCore-WOW64
    ```

3.  Установите полную версию Microsoft .NET Framework 4.0 для основных серверных компонентов из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450).

4.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## <a name="BKMK_InstallingOnWindowsServer2008LH"></a>Установка Windows PowerShell в Windows Server 2008
Эти инструкции описывают установку Windows PowerShell 3.0 на компьютерах под управлением Windows Server 2008 с пакетом обновления 2 (SP2).

В системах Windows Server 2008 Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) является необходимым компонентом для Windows Management Framework 3.0. Компонент расширенной защиты для проверки подлинности защищает компьютер от атак перенаправления проверки подлинности и позволяет использовать параметр **UseSSL** при создании удаленных сеансов. Чтобы установить Windows PowerShell 3.0 и модуль Windows PowerShell 2.0, используйте следующую процедуру.

#### Подготовка к установке

-   Перед установкой Windows Management Framework 3.0 удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка Windows PowerShell 3.0

1.  Установите Microsoft .NET Framework 3.5 с пакетом обновления 1 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910).

2.  Установите Windows Management Framework (Windows PowerShell 2.0, статья базы знаний 968930) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035).

3.  Установите полную версию Microsoft .NET Framework 4 (dotNetFx40\_Full\_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Также можно установить Microsoft .NET Framework 4.5 (dotNetFx45\_Full\_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

4.  Установите компонент расширенной защиты для проверки подлинности (статья базы знаний 968389) по адресу [http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398).

5.  Установите Windows Management Framework 3.0 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## См. также
[Требования к системе для Windows PowerShell](Windows-PowerShell-System-Requirements.md)
[Запуск Windows PowerShell [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)



<!--HONumber=Jun16_HO4-->


