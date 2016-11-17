---
title: "Установка и настройка WMF 5.1 (предварительная версия)"
ms.date: 2016-05-16
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
contributor: kriscv
manager: dongill
ms.prod: powershell
ms.technology: WMF
translationtype: Human Translation
ms.sourcegitcommit: 0c136264c9fe4e92771e4423011c2fa959f30e93
ms.openlocfilehash: 21f26830cdc20a90ce48aa09bc7013d733242ae9

---

# <a name="install-and-configure-wmf-51-preview"></a>Установка и настройка WMF 5.1 (предварительная версия) #

## <a name="install-net-46"></a>Установка .NET 4.6
Для использования WMF 5.1 необходимо установить платформу .NET Framework 4.6. Это нужно, чтобы обеспечить работу новых функций подписывания каталогов, которые влияют на некоторые аспекты загрузки модулей и скриптов в WMF 5.1. 

[Платформа .NET Framework 4.6 доступна в статье базы знаний 3045560](https://support.microsoft.com/en-us/kb/3045560). Инструкции по установке доступны по месту скачивания.

> **Примечание**. Требование иметь .NET 4.6 не обнаруживается установщиком предварительной версии WMF 5.1, поэтому возможно установить ее и без установки .NET 4.6. Это известная проблема. Тестирование показало, что вы можете установить .NET 4.6 после установки предварительной версии WMF 5.1. В финальной версии WMF 5.1 правильно проверит необходимые компоненты перед установкой. 

## <a name="download-and-install-the-wmf-51-preview"></a>Скачивание и установка WMF 5.1 Preview

Скачайте пакет WMF 5.1 для той операционной системы и архитектуры, в которой будет производиться установка.

| Операционная система       | Необходимые компоненты | Ссылки на пакеты             |
|------------------------|---------------|---------------------------|
| Windows Server 2012 R2 | [.NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560) | [Win8.1AndW2K12R2-KB3156422-x64.msu](http://go.microsoft.com/fwlink/?LinkID=823586)|
| Windows Server 2012    | [.NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560) | [W2K12-KB3156423-x64.msu](http://go.microsoft.com/fwlink/?LinkID=823587)|
| Windows Server 2008 R2 | [.NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560) </br> [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) </br> Обновление для системы безопасности для [подписывания кода SHA-2](https://technet.microsoft.com/en-us/library/security/3033929) | [Win7AndW2K8R2-KB3156424-x64.msu](http://go.microsoft.com/fwlink/?LinkID=823588) |
| Windows 8.1            | [.NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560) | **x64:** [Win8.1AndW2K12R2-KB3156422-x64.msu](http://go.microsoft.com/fwlink/?LinkID=823586) </br> **x86:** [Win8.1-KB3156422-x86.msu](http://go.microsoft.com/fwlink/?LinkID=823589) |
| Windows 7 с пакетом обновления 1 (SP1)          | [.NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560) </br> [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855) </br> Обновление для системы безопасности для [подписывания кода SHA-2](https://technet.microsoft.com/en-us/library/security/3033929) | **x64:** [Win7AndW2K8R2-KB3156424-x64.msu](http://go.microsoft.com/fwlink/?LinkID=823588) </br> **x86:** [Win7-KB3156424-x86.msu](http://go.microsoft.com/fwlink/?LinkID=823590) |


## <a name="install-wmf-51-from-windows-explorer-or-file-explorer-in-windows-server-2012-r2-or-windows-81"></a>Установка WMF 5.1 из проводника

1. Перейдите в папку, куда был скачан MSU-файл.

2. Дважды щелкните этот файл для его запуска.

## <a name="install-wmf-51-from-the-command-prompt"></a>Установка WMF 5.1 из командной строки##

1. После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора"). При выборе варианта "Установка основных серверных компонентов" для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.

2. Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.1.

3. Выполните одну из следующих команд:
    - На компьютерах с ОС Windows Server 2012 R2 или Windows 8.1 (64-разрядная версия) выполните команду `Win8.1AndW2K12R2-KB3156422-x64.msu /quiet`.
    - На компьютерах с ОС Windows Server 2012 выполните команду `W2K12-KB3156423-x64.msu /quiet`.
    - На компьютерах с ОС Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) (64-разрядная версия) выполните команду `Win7AndW2K8R2-KB3156424-x64.msu /quiet`.
    - На компьютерах с ОС Windows 8.1 (32-разрядная версия) выполните команду `Win8.1-KB3156422-x86.msu /quiet`.
    - На компьютерах с ОС Windows 7 с пакетом обновления 1 (SP1) (32-разрядная версия) выполните команду `Win7-KB3156424-x86.msu /quiet`.

## <a name="additional-installation-notes-for-windows-server-2008-r2-sp1-and-windows-7-sp1"></a>Дополнительные замечания по установке для Windows Server 2008 R2 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1)##
Для установки WMF 5.1 на компьютере с ОС Windows Server 2008 R2 с пакетом обновления 1 или Windows 7 с пакетом обновления 1 (SP1) необходимо установить следующие компоненты:
- последний пакет обновления;
- [WMF 4.0](http://www.microsoft.com/en-us/download/details.aspx?id=40855)
- Для WMF 5.1 нужна платформа [Microsoft .NET Framework 4.6](https://support.microsoft.com/en-us/kb/3045560). Вы можете установить Microsoft .NET Framework 4.6, выполнив следующие инструкции по месту скачивания.
- Обновление для системы безопасности для [подписывания кода SHA-2](https://technet.microsoft.com/en-us/library/security/3033929). Оно необходимо, чтобы использовать новые командлеты PowerShell для файлов каталога Windows. 

> **Зависимость от WinRM**: служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM. По умолчанию WinRM не включен в Windows Server 2008 R2 и Windows 7. Чтобы включить WinRM, выполните команду `Set-WSManQuickConfig` в сеансе Windows PowerShell с повышенными привилегиями.




<!--HONumber=Nov16_HO2-->


