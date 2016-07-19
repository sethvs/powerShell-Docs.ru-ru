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
ms.sourcegitcommit: 4c1b57f221d0f502313eecb21dd36b5e85c2de4d
ms.openlocfilehash: 5a7aa50eb4ad5ea2788dc2cbdd189d5632f5c15f

---

# Установка и настройка WMF 5.1 (предварительная версия) #

Скачайте пакет WMF 5.1 для той операционной системы и архитектуры, в которой будет производиться установка.

| Операционная система       | Архитектура | Имя пакета              |
|------------------------|--------------|---------------------------|
| Windows Server 2012 R2 | x64      | [Win8.1AndW2K12R2-KB3156422-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows Server 2012    | x64      | [W2K12-KB3156423-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717506) |
| Windows Server 2008 R2 | x64      | [Win7AndW2K8R2-KB3156424-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 8.1            | x64          | [Win8.1AndW2K12R2-KB3156422-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717507) |
| Windows 8.1            | x86          | [Win8.1-KB3156422-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717963) |
| Windows 7 с пакетом обновления 1 (SP1)          | x64          | [Win7AndW2K8R2-KB3156424-x64.msu](http://go.microsoft.com/fwlink/?LinkId=717504) |
| Windows 7 с пакетом обновления 1 (SP1)          | x86          | [Win7-KB3156424-x86.msu](http://go.microsoft.com/fwlink/?LinkID=717962) |


## Установка WMF 5.1 из проводника

1. Перейдите в папку, куда был скачан MSU-файл.

2. Дважды щелкните этот файл для его запуска.

## Установка WMF 5.1 из командной строки##

1. После скачивания подходящего пакета для архитектуры вашего компьютера откройте окно командной строки с повышенными правами (используйте "Запуск от имени администратора"). В установке основных серверных компонентов для Windows Server 2012 R2, Windows Server 2012 или Windows Server 2008 R2 с пакетом обновления 1 (SP1) командная строка по умолчанию открывается с повышенными правами.

2. Перейдите в папку, куда был скачан или скопирован пакет установки WMF 5.1.

3. Выполните одну из следующих команд:
    - На компьютерах с ОС Windows Server 2012 R2 или Windows 8.1 (64-разрядная версия) выполните команду `Win8.1AndW2K12R2-KB3156422-x64.msu /quiet`.
    - На компьютерах с ОС Windows Server 2012 выполните команду `W2K12-KB3156423-x64.msu /quiet`.
    - На компьютерах с ОС Windows Server 2008 R2 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) (64-разрядная версия) выполните команду `Win7AndW2K8R2-KB3156424-x64.msu /quiet`.
    - На компьютерах с ОС Windows 8.1 (32-разрядная версия) выполните команду `Win8.1-KB3156422-x86.msu /quiet`.
    - На компьютерах с ОС Windows 7 с пакетом обновления 1 (SP1) (32-разрядная версия) выполните команду `Win7-KB3156424-x86.msu /quiet`.

## Дополнительные замечания по установке для Windows Server 2008 с пакетом обновления 1 (SP1) и Windows 7 с пакетом обновления 1 (SP1)##
Для установки WMF 5.1 на компьютере с ОС Windows Server 2008 с пакетом обновления 1 (SP1) или Windows 7 с пакетом обновления 1 (SP1) необходимо установить следующие компоненты:
- последний пакет обновления;
- [WMF 4.0.](http://www.microsoft.com/en-us/download/details.aspx?id=40855)

> **Зависимость от WinRM**: служба настройки требуемого состояния (DSC) Windows PowerShell зависит от WinRM. По умолчанию WinRM не включен в Windows Server 2008 R2 и Windows 7. Чтобы включить WinRM, выполните команду `Set-WSManQuickConfig` в сеансе Windows PowerShell с повышенными привилегиями.



<!--HONumber=Jul16_HO1-->


