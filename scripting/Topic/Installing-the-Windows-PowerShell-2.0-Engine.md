---
title: Установка подсистемы Windows PowerShell 2.0
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
---
# Установка подсистемы Windows PowerShell 2.0
В этой статье описана установка подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)].

[!INCLUDE[psversion3](../Token/psversion3_md.md)] обеспечивает обратную совместимость с [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Командлеты, поставщики, оснастки, модули и сценарии, написанные для [!INCLUDE[psversion2](../Token/psversion2_md.md)], выполняются в [!INCLUDE[psversion3](../Token/psversion3_md.md)] и [!INCLUDE[psversion4](../Token/psversion4_md.md)] без изменений. Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы Windows PowerShell, написанные для [!INCLUDE[psversion2](../Token/psversion2_md.md)] и скомпилированные с помощью среды CLR 2.0, не могут выполняться без изменения в более поздних выпусках [!INCLUDE[wps_2](../Token/wps_2_md.md)], которые компилируются в среде CLR 4.0.

Чтобы обеспечить обратную совместимость с командами и основными программами, которые были затронуты этими изменениями, подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)], [!INCLUDE[psversion3](../Token/psversion3_md.md)] и [!INCLUDE[psversion4](../Token/psversion4_md.md)] рассчитаны на параллельное выполнение. Кроме того, подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] входит в состав [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)], [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] и [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)]. Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] предназначена для использования только в том случае, если выполнение существующего сценария или существующей основной программы невозможно из-за несовместимости с [!INCLUDE[psversion3](../Token/psversion3_md.md)], [!INCLUDE[psversion4](../Token/psversion4_md.md)] или Microsoft .NET Framework 4. Такие ситуации довольно редки.

Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] является дополнительным компонентом [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)], [!INCLUDE[win8_client_1](../Token/win8_client_1_md.md)] и [!INCLUDE[win8_server_1](../Token/win8_server_1_md.md)]. В более ранних версиях Windows при установке [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] установка [!INCLUDE[psversion3](../Token/psversion3_md.md)] полностью заменяет [!INCLUDE[psversion2](../Token/psversion2_md.md)] в каталоге установки [!INCLUDE[wps_2](../Token/wps_2_md.md)]. Однако подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] при этом сохраняется.

Дополнительные сведения о запуске подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] см. в статье [Запуск подсистемы Windows PowerShell 2.0](../Topic/Starting-the-Windows-PowerShell-2.0-Engine.md).

## В [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)] и [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)]
В [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)] и [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)] компонент подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] включен по умолчанию. Однако для его использования следует включить параметр для необходимой ему платформы Microsoft .NET Framework 3.5. Этот раздел также поясняет, как включить и выключить компонент подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)].

#### Включение .NET Framework 3.5

1.  На экране **Пуск** введите **компоненты Windows**.

2.  В панели **Приложения** щелкните **Параметры**, а затем выберите **Включение или отключение компонентов Windows**.

3.  В поле **Компоненты Windows** выберите элемент **.NET Framework 3.5 (включает .NET 2.0 и 3.0)**.

    При выборе элемента **.NET Framework 3.5 (включает .NET 2.0 и 3.0)** поле заливается, указывая, что выбрана только часть компонента. Однако этого достаточно для подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)].

#### Включение и отключение подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]

1.  На экране **Пуск** введите **компоненты Windows**.

2.  В панели **Приложения** щелкните **Параметры**, а затем выберите **Включение или отключение компонентов Windows**.

3.  В поле **Компоненты Windows** разверните узел **[!INCLUDE[psversion2](../Token/psversion2_md.md)]** и щелкните флажок **Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)]**, чтобы установить или снять его.

## В [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] и [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)]
Используйте следующие процедуры для добавления компонентов подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] и Microsoft .NET Framework 3.5. Подсистеме [!INCLUDE[psversion2](../Token/psversion2_md.md)] требуется Microsoft .NET Framework версии не ниже 2.0.50727. Этому требованию удовлетворяет Microsoft .NET Framework 3.5.

#### Добавление компонента .NET Framework 3.5

1.  В меню **Управление** **диспетчера сервера** выберите **Добавить роли и компоненты**.

    Можно также щелкнуть элемент **Все серверы** в **диспетчере сервера**, щелкнуть имя сервера правой кнопкой мыши и выбрать **Добавить роли и компоненты**.

2.  На странице **Тип установки** выберите **Установка ролей или компонентов**.

3.  На странице **Компоненты** разверните узел **Компоненты .NET Framework 3.5** и выберите команду **.NET Framework 3.5 (включает .NET 2.0 и 3.0)**.

    Другие параметры в этом узле для подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] не требуются.

#### Добавление компонента подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]

-   В меню **Управление** **диспетчера сервера** выберите **Добавить роли и компоненты**.

    Можно также щелкнуть элемент **Все серверы** в **диспетчере сервера**, щелкнуть имя сервера правой кнопкой мыши и выбрать **Добавить роли и компоненты**.

-   На странице **Тип установки** выберите **Установка ролей или компонентов**.

-   На странице **Компоненты** разверните узел **[!INCLUDE[mshshort](../Token/mshshort_md.md)] (Установлено)** и выберите команду **Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)]**.

Дополнительные сведения о запуске подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] см. в статье [Запуск подсистемы Windows PowerShell 2.0](../Topic/Starting-the-Windows-PowerShell-2.0-Engine.md).

## В предыдущих версиях систем
Пакет [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881), устанавливающий [!INCLUDE[psversion4](../Token/psversion4_md.md)] в [!INCLUDE[win7_client_secondref](../Token/win7_client_secondref_md.md)], [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] и [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], содержит подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] включена и готова к использованию без дополнительной установки, настройки или конфигурации.

Пакет [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)], устанавливающий [!INCLUDE[psversion3](../Token/psversion3_md.md)] в [!INCLUDE[win7_client_secondref](../Token/win7_client_secondref_md.md)], [!INCLUDE[win7_server_secondref](../Token/win7_server_secondref_md.md)] и [!INCLUDE[lserver](../Token/lserver_md.md)], содержит подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] включена и готова к использованию без дополнительной установки, настройки или конфигурации.

## См. также
[Требования к системе для Windows PowerShell](../Topic/Windows-PowerShell-System-Requirements.md)
[Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md)
[Запуск Windows PowerShell [ps]](assetId:///8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
[Запуск подсистемы Windows PowerShell 2.0](../Topic/Starting-the-Windows-PowerShell-2.0-Engine.md)



<!--HONumber=Apr16_HO1-->


