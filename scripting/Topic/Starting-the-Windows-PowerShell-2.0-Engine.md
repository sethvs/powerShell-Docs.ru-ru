---
title: Запуск подсистемы Windows PowerShell 2.0
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edafc2fa-7576-49c2-bbba-9336f4bcfc28
---
# Запуск подсистемы Windows PowerShell 2.0
В этом разделе объясняется, как запустить подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)] в [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)], [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)] и [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], которые включают в себя подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)], и в других системах, где установлены [!INCLUDE[psversion2](../Token/psversion2_md.md)], [!INCLUDE[psversion3](../Token/psversion3_md.md)] и [!INCLUDE[psversion4](../Token/psversion4_md.md)].

[!INCLUDE[psversion4](../Token/psversion4_md.md)] и [!INCLUDE[psversion3](../Token/psversion3_md.md)] обеспечивают обратную совместимость с [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Командлеты, поставщики, оснастки, модули и сценарии, написанные для [!INCLUDE[psversion2](../Token/psversion2_md.md)], выполняются в [!INCLUDE[psversion4](../Token/psversion4_md.md)] и [!INCLUDE[psversion3](../Token/psversion3_md.md)] без изменений. Однако из-за изменений в политике активации среды выполнения в Microsoft .NET Framework 4 основные программы [!INCLUDE[wps_2](../Token/wps_2_md.md)], написанные для [!INCLUDE[psversion2](../Token/psversion2_md.md)] и скомпилированные с помощью среды CLR 2.0, не могут выполняться без изменения в [!INCLUDE[psversion3](../Token/psversion3_md.md)] или [!INCLUDE[psversion4](../Token/psversion4_md.md)], которые компилируются в среде CLR 4.0. Подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] предназначена для использования только в том случае, если выполнение существующего сценария или существующей основной программы невозможно из-за несовместимости с [!INCLUDE[psversion4](../Token/psversion4_md.md)], [!INCLUDE[psversion3](../Token/psversion3_md.md)] или Microsoft .NET Framework 4. Такие ситуации довольно редки.

Многие программы, требующие использования подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)], запускают ее автоматически. Эти инструкции предназначены для редких случаев, когда подсистему необходимо запустить вручную.

## Установка и включение требуемых программ
Перед запуском подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)] включите подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)] и Microsoft .NET Framework 3.5 с пакетом обновления 1 (SP1). Инструкции см. в статье [Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md).

Системы, где установлена [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) или [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)], имеют все необходимые компоненты. Никакая дополнительная настройка не требуется. Дополнительные сведения об установке [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) или [!INCLUDE[ps_wmf_3.0](../Token/ps_wmf_3.0_md.md)] см. в статье [Установка Windows PowerShell](../Topic/Installing-Windows-PowerShell.md).

## Запуск подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]
При запуске [!INCLUDE[mshshort](../Token/mshshort_md.md)] по умолчанию открывается самая новая версия. Чтобы запустить [!INCLUDE[mshshort](../Token/mshshort_md.md)] с подсистемой [!INCLUDE[psversion2](../Token/psversion2_md.md)], используйте параметр Version для PowerShell.exe. Команду можно выполнить в любой командной строке, включая Windows PowerShell и Cmd.exe.

```
PowerShell.exe -Version 2
```

## Открытие удаленного сеанса с использованием подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]
Чтобы запустить подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)] в удаленном сеансе, создайте его конфигурацию (которая также называется "конечной точкой") на удаленном компьютере, которая загружает подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Конфигурация сеанса сохраняется на удаленном компьютере и может использоваться любым авторизованным пользователем для создания сеансов с подсистемой [!INCLUDE[psversion2](../Token/psversion2_md.md)].

Это сложная задача, которая обычно выполняется системным администратором.

Следующая процедура использует параметр **PSVersion** командлета [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) для создания конфигурации сеанса с подсистемой [!INCLUDE[psversion2](../Token/psversion2_md.md)]. Можно также использовать параметр **PowerShellVersion** командлета [New-PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866), чтобы создать файл конфигурации для сеанса, который загружает подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)], и параметр **PSVersion** командлета [Set-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea), чтобы изменить конфигурацию сеанса для использования подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)].

Дополнительные сведения о файлах конфигурации сеанса см. в статье [about_Session_Configuration_Files](https://technet.microsoft.com/en-us/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). Сведения о конфигурациях сеанса, включая настройку и обеспечение безопасности, см. в статье [about_Session_Configurations [v4]](https://technet.microsoft.com/en-us/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### Открытие удаленного сеанса [!INCLUDE[psversion2](../Token/psversion2_md.md)]

1.  Для создания конфигурации сеанса, требующей подсистему [!INCLUDE[psversion2](../Token/psversion2_md.md)], используйте параметр **PSVersion** командлета [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) со значением "2.0". Выполните команду на компьютере на "стороне сервера" или на принимающей стороне подключения.

    Следующий пример команды создает конфигурацию сеанса PS2 на компьютере Server01. Чтобы выполнить эту команду, запустите [!INCLUDE[psversion4](../Token/psversion4_md.md)] или [!INCLUDE[psversion3](../Token/psversion3_md.md)] с параметром **Запуск от имени администратора**.

    ```
    Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
    ```

2.  Чтобы создать на компьютере Server01 сеанс, использующий конфигурацию сеанса PS2, примените параметр **ConfigurationName** для командлетов, создающих удаленный сеанс, таких как [New-PSSession](https://technet.microsoft.com/en-us/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f).

    При запуске сеанса, использующего конфигурацию, подсистема [!INCLUDE[psversion2](../Token/psversion2_md.md)] автоматически загружается в него.

    Следующая команда запускает сеанс на компьютере Server01, который использует конфигурацию PS2. Сеанс сохраняется в переменную $s.

    ```
    $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
    ```

## Запуск фонового задания с помощью подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]
Чтобы запустить фоновое задание с помощью подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)], используйте параметр **PSVersion** командлета [Start-Job](https://technet.microsoft.com/en-us/library/2bc04935-0deb-4ec0-b856-d7290cca6442).

Следующая команда запускает фоновое задание с помощью подсистемы [!INCLUDE[psversion2](../Token/psversion2_md.md)]:

```
Start-Job {Get-Process} -PSVersion 2.0
```

Подробнее о фоновых заданиях см. в статье [about_Jobs [v4]](https://technet.microsoft.com/en-us/library/7362512a-8a4e-4575-b2ea-a740e5c4f002).



<!--HONumber=Apr16_HO2-->


