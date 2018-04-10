---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Запуск Windows PowerShell
ms.assetid: 59b649a2-c90c-4cf4-bf95-a740c59148e7
ms.openlocfilehash: b56ddc2f577225646729b99f3a2abcb8cc60d307
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="starting-windows-powershell"></a>Запуск Windows PowerShell
PowerShell — это библиотека DLL обработчика скриптов, которая внедрена в несколько узлов.  Самый распространенный запускаемый узел — интерактивная командная строка (PowerShell.exe) и интерактивная среда скриптов (PowerShell_ISE.exe).

Информацию о запуске Windows PowerShell® в Windows Server® 2012 R2, Windows® 8.1, Windows Server 2012 и Windows 8 см. в статье [Общие задачи управления и навигации](http://technet.microsoft.com/library/hh831491.aspx).

## <a name="how-to-start-windows-powershell-on-earlier-versions-of-windows"></a>Запуск Windows PowerShell в более ранних версиях Windows

В этом разделе объясняется, как запустить Windows PowerShell и интегрированную среду скриптов Windows PowerShell (ISE) в Windows® 7, Windows Server® 2008 R2 и Windows Server® 2008. Кроме того, здесь поясняется, как включить дополнительный компонент Windows PowerShell ISE в Windows PowerShell 2.0 в ОС Windows Server® 2008 R2 и Windows Server® 2008.

Используйте любой из следующих методов для запуска установленной версии Windows PowerShell 3.0 или Windows PowerShell 4.0, где это возможно.

#### <a name="from-the-start-menu"></a>Из меню "Пуск"

- Нажмите кнопку **Пуск**, введите **PowerShell** и выберите **Windows PowerShell**.
- В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>В командной строке

В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:

```
PowerShell
```

Можно также использовать параметры программы PowerShell.exe для настройки сеанса. Дополнительные сведения см. в статье [Справка по командной строке PowerShell.exe](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### <a name="with-administrative-privileges-run-as-administrator"></a>С правами администратора ("Запуск от имени администратора")

Нажмите кнопку **Пуск**, введите **PowerShell**, щелкните правой кнопкой мыши **Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## <a name="how-to-start-windows-powershell-ise-on-earlier-releases-of-windows"></a>Запуск интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows

Используйте один из следующих методов для запуска интегрированной среды сценариев Windows PowerShell.

#### <a name="from-the-start-menu"></a>Из меню "Пуск"

- Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев** и выберите **Интегрированная среда сценариев Windows PowerShell**.
- В меню **Пуск** выберите **Пуск**, **Все программы**, **Стандартные**, откройте папку **Windows PowerShell** и щелкните **Интегрированная среда сценариев Windows PowerShell**.

#### <a name="at-the-command-prompt"></a>В командной строке

В Cmd.exe, Windows PowerShell или интегрированной среде сценариев Windows PowerShell для запуска Windows PowerShell введите следующее:

```
PowerShell_ISE
```

или

```
ISE
```

#### <a name="with-administrative-privileges-run-as-administrator"></a>С правами администратора ("Запуск от имени администратора")

Нажмите кнопку **Пуск**, введите **Интегрированная среда сценариев**, щелкните правой кнопкой мыши **Интегрированная среда сценариев Windows PowerShell** и выберите пункт **Запуск от имени администратора**.

## <a name="how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows"></a>Включение интегрированной среды сценариев Windows PowerShell в более ранних версиях Windows

При использовании Windows PowerShell 4.0 и Windows PowerShell 3.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена во всех версиях Windows. Если она еще не включена, Windows Management Framework 4.0 или Windows Management Framework 3.0 включает ее.

При использовании Windows PowerShell 2.0 интегрированная среда сценариев Windows PowerShell по умолчанию включена в Windows 7. В Windows Server 2008 R2 и Windows Server 2008 эта функция является дополнительной.

Чтобы включить интегрированную среду сценариев Windows PowerShell для Windows PowerShell 2.0 в Windows Server 2008 R2 или Windows Server 2008, выполните указанные ниже действия.

#### <a name="to-enable-windows-powershell-integrated-scripting-environment-ise"></a>Включение интегрированной среды сценариев Windows PowerShell Windows PowerShell (ISE)

1. Запустите диспетчер сервера.
2. Щелкните **Компоненты** и выберите **Добавить компоненты**.
3. В меню "Выберите компоненты" щелкните интегрированную среду сценариев Windows PowerShell.

## <a name="starting-the-32-bit-version-of-windows-powershell"></a>Запуск 32-разрядной версии Windows PowerShell

При установке Windows PowerShell на 64-разрядном компьютере в дополнение к 64-разрядной версии устанавливается **Windows PowerShell (x86)** — 32-разрядная версия Windows PowerShell. При открытии Windows PowerShell по умолчанию запускается 64-разрядная версия.

Однако в некоторых случаях нужно запустить **Windows PowerShell (x86)**, например при использовании модуля, которому требуется 32-разрядная версия, или при удаленном подключении к 32-разрядному компьютеру.

Для запуска 32-разрядной версии Windows PowerShell воспользуйтесь любой из следующих процедур.

#### <a name="in-windows-server-2012-r2"></a>Windows Server® 2012 R2

- На экране **Пуск** щелкните **Windows PowerShell (x86)**. Щелкните плитку **Windows PowerShell x86**.
- Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.
- На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.
- В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-server-2012"></a>Windows Server® 2012

- На экране **Пуск** введите **PowerShell** и выберите **Windows PowerShell (x86)**.
- Выберите пункт **Windows PowerShell (x86)** в меню **Сервис** **диспетчера сервера**.
- На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell** и выберите **Windows PowerShell (x86)**.
- В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-81"></a>Windows® 8.1

- На экране **Пуск** щелкните **Windows PowerShell (x86)**. Щелкните плитку **Windows PowerShell x86**.
- Если вы используете [средства удаленного администрирования сервера](http://go.microsoft.com/fwlink/?LinkID=304145) для Windows 8.1, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера.
  Выберите **Windows PowerShell (x86)**.
- На рабочем столе переместите курсор в правый верхний угол, щелкните элемент **Поиск**, введите **PowerShell x86** и выберите **Windows PowerShell (x86)**.
- В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`

#### <a name="in-windows-8"></a>Windows® 8

- На экране **Пуск** переместите курсор в правый верхний угол, щелкните **Параметры**, **Плитки**, а затем переместите ползунок **Показать средства администрирования** в значение "Да". Введите **PowerShell** и выберите **Windows PowerShell (x86)**.
- Если вы используете [средства удаленного администрирования сервера](http://www.microsoft.com/download/details.aspx?id=28972) для Windows 8, можно также открыть Windows PowerShell x86 из меню **Сервис** диспетчера сервера. Выберите **Windows PowerShell (x86)**.
- На экране **Пуск** или рабочем столе введите **PowerShell (x86)** и выберите **Windows PowerShell (x86)**.
- В командной строке введите следующее: `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`