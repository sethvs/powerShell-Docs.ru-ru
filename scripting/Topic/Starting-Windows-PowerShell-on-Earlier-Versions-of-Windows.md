---
title: Запуск Windows PowerShell в более ранних версиях Windows
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
---
# Запуск Windows PowerShell в более ранних версиях Windows
Этот раздел содержит сведения о запуске [!INCLUDE[wps_2](../Token/wps_2_md.md)] и [!INCLUDE[mshgraphicalhost](../Token/mshgraphicalhost_md.md)] в [!INCLUDE[win7_client_firstref](../Token/win7_client_firstref_md.md)], [!INCLUDE[win7_server_firstref](../Token/win7_server_firstref_md.md)] и [!INCLUDE[lserver](../Token/lserver_md.md)]. Он также описывает включение дополнительного компонента для [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] в [!INCLUDE[psversion2](../Token/psversion2_md.md)] под управлением [!INCLUDE[win7_server_firstref](../Token/win7_server_firstref_md.md)] и [!INCLUDE[lserver](../Token/lserver_md.md)].

Чтобы установить [!INCLUDE[psversion4](../Token/psversion4_md.md)] на поддерживаемых системах, скачайте и установите [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881). Дополнительные сведения см. в статье [Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md).

Чтобы установить [!INCLUDE[psversion3](../Token/psversion3_md.md)] на поддерживаемых системах, скачайте и установите [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290). Дополнительные сведения см. в статье [Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md).

## Запуск [!INCLUDE[mshshort](../Token/mshshort_md.md)] в предыдущих версиях Windows
Используйте любой из следующих методов для запуска установленной версии [!INCLUDE[psversion3](../Token/psversion3_md.md)] или [!INCLUDE[psversion4](../Token/psversion4_md.md)], где это возможно.

#### Из меню "Пуск"

-   Нажмите кнопку **Пуск**, введите **PowerShell** и выберите **Windows PowerShell**.

-   В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Windows PowerShell**.

#### В командной строке

-   Для запуска [!INCLUDE[wps_2](../Token/wps_2_md.md)] в Cmd.exe, [!INCLUDE[wps_2](../Token/wps_2_md.md)] или интегрированной среде сценариев [!INCLUDE[wps_2](../Token/wps_2_md.md)] введите следующее:

    ```
    PowerShell
    ```

    Можно также использовать параметры программы PowerShell.exe для настройки сеанса. Дополнительные сведения см. в статье [Справка по командной строке PowerShell.exe](../Topic/PowerShell.exe-Command-Line-Help.md).

#### С правами администратора ("Запуск от имени администратора")

1.  Нажмите кнопку **Пуск**, введите **PowerShell**, щелкните правой кнопкой мыши элемент **Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## Запуск [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] в предыдущих выпусках Windows
Используйте один из следующих методов для запуска [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)].

#### Из меню "Пуск"

-   Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев** и выберите **Интегрированная среда сценариев Windows PowerShell**.

-   В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Интегрированная среда сценариев Windows PowerShell**.

#### В командной строке

-   Для запуска [!INCLUDE[wps_2](../Token/wps_2_md.md)] в Cmd.exe, [!INCLUDE[wps_2](../Token/wps_2_md.md)] или интегрированной среде сценариев [!INCLUDE[wps_2](../Token/wps_2_md.md)] введите следующее:

    ```
    PowerShell_ISE
    ```

    или

    ```
    ISE
    ```

#### С правами администратора ("Запуск от имени администратора")

1.  Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев**, щелкните правой кнопкой мыши элемент **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## Включение [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] в предыдущих выпусках Windows
В [!INCLUDE[psversion4](../Token/psversion4_md.md)] и [!INCLUDE[psversion3](../Token/psversion3_md.md)], [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] включена по умолчанию для всех версий Windows. Если она еще не включена, Windows Management Framework 4.0 или [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] включает ее.

В [!INCLUDE[psversion2](../Token/psversion2_md.md)], [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] включена по умолчанию для [!INCLUDE[win7_client_secondref](../Token/win7_client_secondref_md.md)]. Однако в [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] и [!INCLUDE[lserver](../Token/lserver_md.md)] она является дополнительным компонентом.

Чтобы включить [!INCLUDE[mshgraphicalhostshort](../Token/mshgraphicalhostshort_md.md)] в [!INCLUDE[psversion2](../Token/psversion2_md.md)] для [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] или [!INCLUDE[lserver](../Token/lserver_md.md)], используйте следующую процедуру.

#### Включение [!INCLUDE[mshgraphicalhost](../Token/mshgraphicalhost_md.md)]

1.  Запустите диспетчер сервера.

2.  Щелкните **Компоненты** и выберите **Добавить компоненты**.

3.  В области выбора компонентов щелкните [!INCLUDE[mshgraphicalhost](../Token/mshgraphicalhost_md.md)].



<!--HONumber=Apr16_HO1-->


