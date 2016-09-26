---
title: "Использование профилей в интегрированной среде сценариев Windows PowerShell"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
translationtype: Human Translation
ms.sourcegitcommit: cb3db96ff87078756166df9f90d44d88cdfd155f
ms.openlocfilehash: 3543503655cc506c4c0f8a7f3d1056c05a66ecba

---

# Использование профилей в интегрированной среде сценариев Windows PowerShell
В этой статье объясняется, как использовать профили в интегрированной среде скриптов Windows PowerShell®. Перед выполнением задач из этого раздела рекомендуется ознакомиться со статьей [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630)) либо ввести `Get-Help about_Profiles` в области консоли и нажать клавишу **ВВОД**.

Профиль — это сценарий интегрированной среды сценариев Windows PowerShell, который выполняется автоматически при запуске нового сеанса.  Можно создать один или несколько профилей Windows PowerShell для интегрированной среды сценариев Windows PowerShell и использовать их для настройки среды Windows PowerShell для интегрированной среды сценариев Windows PowerShell, подготавливая ее к работе с помощью переменных, псевдонимов, функций, а также настроек цветов и шрифтов, которые должны быть доступны. Профиль затрагивает каждый запускаемый сеанс интегрированной среды сценариев Windows PowerShell.

> [!NOTE]
> Политика выполнения Windows PowerShell определяет, можно ли запускать сценарии и загружать профиль. Политика выполнения по умолчанию (Restricted) запрещает выполнение всех сценариев, включая профили. При использовании политики "Restricted" загрузить профиль нельзя. Дополнительные сведения о политике выполнения см. в статье [about_Execution_Policies [v4]](https://technet.microsoft.com/library/347708dc-1515-4d74-978b-8334603472e6(v=wps.630)).

## Выбор профиля для использования в интегрированной среде сценариев Windows PowerShell
Интегрированная среда сценариев Windows PowerShell поддерживает профили для текущего пользователя и для всех пользователей. Он также поддерживает профили Windows PowerShell, затрагивающие все узлы.

Выбор профиля зависит от того, каким образом вы используете Windows PowerShell и интегрированную среду сценариев Windows PowerShell.

-   Если для запуска Windows PowerShell используется только интегрированная среда сценариев Windows PowerShell, сохраните все элементы в одном из профилей интегрированной среды сценариев, таком как CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.

-   Если для запуска Windows PowerShell используется несколько основных программ, сохраните свои функции, псевдонимы, переменные и команды в профиле, затрагивающем все основные программы, таком как CurrentUserAllHosts или AllUsersAllHosts, и сохраните функции интегрированной среды сценариев, такие как настройки цветов и шрифтов, в CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.

Ниже указаны профили, которые можно создать и использовать в интегрированной среде сценариев Windows PowerShell. Каждый профиль сохраняется по собственному пути.

| Тип профиля | Путь к профилю |
| --- | --- |
| **Текущий пользователь, интегрированная среда скриптов PowerShell**| `$PROFILE.CurrentUserCurrentHost`или `$PROFILE` |
| **Все пользователи, интегрированная среда скриптов PowerShell**| `$PROFILE.AllUsersCurrentHost` |
| **Текущий пользователь, все узлы**| `$PROFILE.CurrentUserAllHosts` |
| **Все пользователи, все узлы** | `$PROFILE.AllUsersAllHosts` |

## Создание профиля
Для создания профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" выполните следующую команду:

```PowerShell
if (!(Test-Path -Path $PROFILE )) 
{ New-Item -Type File -Path $PROFILE -Force }
```

Для создания профиля "Все пользователи, интегрированная среда сценариев PowerShell" выполните следующую команду:

```PowerShell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost)) 
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Для создания профиля "Текущий пользователь, все узлы" выполните следующую команду:

```PowerShell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts)) 
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

Для создания профиля "Все пользователи, все узлы" введите следующее:

```PowerShell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts)) 
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## Изменение профиля

1.  Чтобы открыть профиль, запустите команду psedit с переменной, которая указывает изменяемый профиль. Например, для открытия профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" введите: `psEdit $PROFILE`

2.  Добавьте несколько элементов в профиль. Ниже приведено несколько примеров, как можно приступить к работе:

    -   Чтобы изменить цвет фона по умолчанию для области консоли на синий, введите в файле профиля следующее: `$psISE.Options.OutputPaneBackground = 'blue'` . Дополнительные сведения о переменной $psISE см. в статье [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](#windows-powershell-ise-object-model-reference).

    -   Чтобы изменить размер шрифта на 20, введите в файле профиля следующее: `$psISE.Options.FontSize =20`

3.  Чтобы сохранить файл профиля, в меню **Файл** щелкните **Сохранить**. Внесенные изменения применяются при следующем открытии интегрированной среды сценариев Windows PowerShell.

## См. также
- [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630))
- [Использование интегрированной среды сценариев Windows PowerShell](Using-the-Windows-PowerShell-ISE.md)




<!--HONumber=Sep16_HO3-->


