---
title: Установка Windows PowerShell
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fbb0409-5a54-48ec-95e6-7f8b7d8c4969
---
# Установка Windows PowerShell
[!INCLUDE[win8_client_1](../Token/win8_client_1_md.md)] и [!INCLUDE[win8_server_1](../Token/win8_server_1_md.md)] включают [!INCLUDE[psversion3](../Token/psversion3_md.md)] и все ее необходимые компоненты. Система также включает подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)] для обеспечения обратной совместимости с основными программами, которые не могут использовать [!INCLUDE[psversion3](../Token/psversion3_md.md)].

В этой статье описана установка [!INCLUDE[psversion3](../Token/psversion3_md.md)] в предыдущих версиях систем, а также установка и включение необходимых компонентов.

Эта статья содержит следующие разделы.

-   [Установка Windows PowerShell в Windows 8 и Windows Server 2012](../Topic/Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows8andWindowsServer2012)

-   [Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2](../Topic/Installing-Windows-PowerShell.md#BKMK_InstallingOnWindows7andWindowsServer2008R2)

-   [Установка Windows PowerShell в Windows Server 2008](../Topic/Installing-Windows-PowerShell.md#BKMK_InstallingOnWindowsServer2008LH)

-   [Установка Windows PowerShell в основных серверных компонентах](../Topic/Installing-Windows-PowerShell.md#BKMK_InstallingOnServerCore)

-   [Развертывание Windows PowerShell Web Access](assetId:///639d0eff-98a3-4124-b52c-26921ebd98b0)

-   [Установка подсистемы Windows PowerShell 2.0](../Topic/Installing-the-Windows-PowerShell-2.0-Engine.md)

## <a name="BKMK_InstallingOnWindows8andWindowsServer2012"></a>Установка Windows PowerShell в Windows 8 и Windows Server 2012
[!INCLUDE[psversion3](../Token/psversion3_md.md)] предоставляется установленной, настроенной и готовой к использованию. [!INCLUDE[mshgraphicalhost](../Token/mshgraphicalhost_md.md)] установлена и включена. Дополнительные сведения о запуске [!INCLUDE[mshshort](../Token/mshshort_md.md)] см. в статьях [Starting Windows PowerShell on Windows 8](assetId:///d7be1668-8617-4890-ad90-dd9765fbd2c3) (Запуск Windows PowerShell в Windows 8) и [Starting Windows PowerShell on Windows Server 2012](assetId:///4fc0110a-cc0c-42a4-bbb5-3cc89a0fc968) (Запуск Windows PowerShell в Windows Server 2012).

## <a name="BKMK_InstallingOnWindows7andWindowsServer2008R2"></a>Установка Windows PowerShell в Windows 7 и Windows Server 2008 R2
Эти инструкции описывают установку [!INCLUDE[psversion3](../Token/psversion3_md.md)] на компьютерах под управлением [!INCLUDE[win7_client_secondref](../Token/win7_client_secondref_md.md)] с пакетом обновления 1 (SP1) и [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] с пакетом обновления 1 (SP1). Ниже приведены отдельные инструкции по установке для компьютеров под управлением [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] с установкой основных серверных компонентов.

#### Подготовка к установке

-   Перед установкой [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка [!INCLUDE[psversion3](../Token/psversion3_md.md)]

1.  Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Либо установите Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

2.  Установите [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

Сведения о запуске [!INCLUDE[psversion3](../Token/psversion3_md.md)] см. в статье [Запуск Windows PowerShell в более ранних версиях Windows](../Topic/Starting-Windows-PowerShell-on-Earlier-Versions-of-Windows.md).

## <a name="BKMK_InstallingOnServerCore"></a>Установка Windows PowerShell в основных серверных компонентах
Эти инструкции описывают установку [!INCLUDE[psversion3](../Token/psversion3_md.md)] на компьютерах под управлением [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] с пакетом обновления 1 (SP1) с установкой основных серверных компонентов.

Первые шаги в процедуре используют команды системы обслуживания образов развертывания и управления ими (DISM) для установки Microsoft [!INCLUDE[dnprdnlong](../Token/dnprdnlong_md.md)] для основных серверных компонентов и [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Эти программы являются необходимыми компонентами для [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)], который устанавливается на последующем шаге.

#### Подготовка к установке

-   Перед установкой [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка [!INCLUDE[psversion3](../Token/psversion3_md.md)]

1.  Запуск Cmd.exe

2.  Выполните указанные ниже команды DISM. Эти команды устанавливают [!INCLUDE[dnprdnlong](../Token/dnprdnlong_md.md)] и [!INCLUDE[psversion2](../Token/psversion2_md.md)].

    ```
    dism /online /enable-feature:NetFx2-ServerCore
    dism /online /enable-feature:MicrosoftWindowsPowerShell
    dism /online /enable-feature:NetFx2-ServerCore-WOW64
    ```

3.  Установите полную версию Microsoft [!INCLUDE[netfx40_short](../Token/netfx40_short_md.md)] для основных серверных компонентов из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=248450](http://go.microsoft.com/fwlink/?LinkID=248450).

4.  Установите [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## <a name="BKMK_InstallingOnWindowsServer2008LH"></a>Установка Windows PowerShell в Windows Server 2008
Эти инструкции описывают установку [!INCLUDE[psversion3](../Token/psversion3_md.md)] на компьютерах под управлением [!INCLUDE[lserver](../Token/lserver_md.md)] с пакетом обновления 2 (SP2).

В системах [!INCLUDE[lserver](../Token/lserver_md.md)] Windows Management Framework ([!INCLUDE[psversion2](../Token/psversion2_md.md)], статья базы знаний 968930) является необходимым компонентом для [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)]. Компонент расширенной защиты для проверки подлинности защищает компьютер от атак перенаправления проверки подлинности и позволяет использовать параметр **UseSSL** при создании удаленных сеансов. Чтобы установить [!INCLUDE[psversion3](../Token/psversion3_md.md)] и подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)], выполните описанную ниже процедуру.

#### Подготовка к установке

-   Перед установкой [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] удалите все предыдущие версии Windows Management Framework 3.0.

#### Установка [!INCLUDE[psversion3](../Token/psversion3_md.md)]

1.  Установите Microsoft .NET Framework 3.5 с пакетом обновления 1 из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242910](http://go.microsoft.com/fwlink/?LinkID=242910).

2.  Установите Windows Management Framework ([!INCLUDE[psversion2](../Token/psversion2_md.md)], статья базы знаний 968930) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkId=243035](http://go.microsoft.com/fwlink/?LinkId=243035).

3.  Выполните полную установку Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=212547](http://go.microsoft.com/fwlink/?LinkID=212547).

    Либо установите Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe) из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=242919](http://go.microsoft.com/fwlink/?LinkID=242919).

4.  Установите компонент расширенной защиты для проверки подлинности (статья базы знаний 968389) по адресу [http://go.microsoft.com/fwlink/?LinkID=186398](http://go.microsoft.com/fwlink/?LinkID=186398).

5.  Установите [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] из Центра загрузки Майкрософт по адресу [http://go.microsoft.com/fwlink/?LinkID=240290](http://go.microsoft.com/fwlink/?LinkID=240290).

## См. также
[Требования к системе для Windows PowerShell](../Topic/Windows-PowerShell-System-Requirements.md)
[Запуск Windows PowerShell [ps]](assetId:///8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)



<!--HONumber=Apr16_HO1-->


