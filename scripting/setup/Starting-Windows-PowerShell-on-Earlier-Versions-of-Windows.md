---
title: "Запуск Windows PowerShell в более ранних версиях Windows"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 57125436-3d1e-4e7f-b5c4-8f0ecb49d642
translationtype: Human Translation
ms.sourcegitcommit: 3222a0ba54e87b214c5ebf64e587f920d531956a
ms.openlocfilehash: 6cdb6bb5d901c9bc7d2b7f5051e372337bbb69f9

---

# Запуск Windows PowerShell в более ранних версиях Windows
В этой статье объясняется, как запустить Windows PowerShell и интегрированную среду сценариев Windows PowerShell в WindowsÂ® 7, Windows ServerÂ® 2008 R2 и Windows Server 2008. Кроме того, здесь поясняется, как включить дополнительный компонент для Windows PowerShell ISE в Windows PowerShell 2.0 под управлением Windows ServerÂ® 2008 R2 и Windows Server 2008.

Чтобы установить Windows PowerShell 4.0 на поддерживаемых системах, скачайте и установите [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881). Дополнительные сведения см. в статье [Установка Windows PowerShell](Installing-Windows-PowerShell.md).

Чтобы установить Windows PowerShell 3.0 на поддерживаемых системах, скачайте и установите [Windows Management Framework 3.0](http://go.microsoft.com/fwlink/?LinkID=240290). Дополнительные сведения см. в статье [Установка Windows PowerShell](Installing-Windows-PowerShell.md).

## Запуск Windows PowerShell в более ранних версиях Windows
Используйте любой из следующих методов для запуска установленной версии Windows PowerShell 3.0 или Windows PowerShell 4.0, где это возможно.

#### Из меню "Пуск"

-   Нажмите кнопку **Пуск**, введите **PowerShell** и выберите **Windows PowerShell**.

-   В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Windows PowerShell**.

#### В командной строке

-   В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:

    ```
    PowerShell
    ```

    Можно также использовать параметры программы PowerShell.exe для настройки сеанса. Дополнительные сведения см. в статье [Справка по командной строке PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### С правами администратора ("Запуск от имени администратора")

1.  Нажмите кнопку **Пуск**, введите **PowerShell**, щелкните правой кнопкой мыши **Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## Запуск интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows
Используйте один из следующих методов для запуска интегрированной среды сценариев Windows PowerShell.

#### Из меню "Пуск"

-   Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев** и выберите **Интегрированная среда сценариев Windows PowerShell**.

-   В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Интегрированная среда сценариев Windows PowerShell**.

#### В командной строке

-   В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:

    ```
    PowerShell_ISE
    ```

    или

    ```
    ISE
    ```

#### С правами администратора ("Запуск от имени администратора")

1.  Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев**, щелкните правой кнопкой мыши **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## Включение интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows
При использовании Windows PowerShell 4.0 и Windows PowerShell 3.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена во всех версиях Windows. Если она еще не включена, Windows Management Framework 4.0 или Windows Management Framework 3.0 включает ее.

При использовании Windows PowerShell 2.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена в Windows 7. В Windows Server 2008 R2 и Windows Server 2008 эта функция является дополнительной.

Чтобы включить интегрированную среду сценариев Windows PowerShell для Windows PowerShell 2.0 в Windows Server 2008 R2 или Windows Server 2008, выполните указанные ниже действия.

#### Включение интегрированной среды сценариев Windows PowerShell Windows PowerShell (ISE)

1.  Запустите диспетчер сервера.

2.  Щелкните **Компоненты** и выберите **Добавить компоненты**.

3.  В меню "Выберите компоненты" щелкните интегрированную среду сценариев Windows PowerShell.




<!--HONumber=Aug16_HO4-->


