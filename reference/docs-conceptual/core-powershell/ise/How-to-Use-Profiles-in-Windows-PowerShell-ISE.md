---
ms.date: 06/05/2017
keywords: powershell,командлет
title: Использование профилей в интегрированной среде сценариев Windows PowerShell
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: 8789d6283457f790fdea27657abb2612304e10a1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a>Использование профилей в интегрированной среде сценариев Windows PowerShell

В этой статье объясняется, как использовать профили в интегрированной среде скриптов Windows PowerShell®. Перед выполнением задач из этого раздела рекомендуется ознакомиться со статьей [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles) либо в области консоли ввести `Get-Help about_Profiles` и нажать клавишу **ВВОД**.

Профиль — это сценарий интегрированной среды сценариев Windows PowerShell, который выполняется автоматически при запуске нового сеанса.  Можно создать один или несколько профилей Windows PowerShell для интегрированной среды сценариев Windows PowerShell и использовать их для настройки среды Windows PowerShell для интегрированной среды сценариев Windows PowerShell, подготавливая ее к работе с помощью переменных, псевдонимов, функций, а также настроек цветов и шрифтов, которые должны быть доступны. Профиль затрагивает каждый запускаемый сеанс интегрированной среды сценариев Windows PowerShell.

> [!NOTE]
> Политика выполнения Windows PowerShell определяет, можно ли запускать сценарии и загружать профиль. Политика выполнения по умолчанию (Restricted) запрещает выполнение всех сценариев, включая профили. При использовании политики "Restricted" загрузить профиль нельзя. Дополнительные сведения о политике выполнения см. в статье [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a>Выбор профиля для использования в интегрированной среде сценариев Windows PowerShell

Интегрированная среда сценариев Windows PowerShell поддерживает профили для текущего пользователя и для всех пользователей. Он также поддерживает профили Windows PowerShell, затрагивающие все узлы.

Выбор профиля зависит от того, каким образом вы используете Windows PowerShell и интегрированную среду сценариев Windows PowerShell.

- Если для запуска Windows PowerShell используется только интегрированная среда сценариев Windows PowerShell, сохраните все элементы в одном из профилей интегрированной среды сценариев, таком как CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.

- Если для запуска Windows PowerShell используется несколько основных программ, сохраните свои функции, псевдонимы, переменные и команды в профиле, затрагивающем все основные программы, таком как CurrentUserAllHosts или AllUsersAllHosts, и сохраните функции интегрированной среды сценариев, такие как настройки цветов и шрифтов, в CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.

Ниже указаны профили, которые можно создать и использовать в интегрированной среде сценариев Windows PowerShell. Каждый профиль сохраняется по собственному пути.

| Тип профиля | Путь к профилю |
| --- | --- |
| **Текущий пользователь, интегрированная среда сценариев PowerShell**| `$PROFILE.CurrentUserCurrentHost` или `$PROFILE` |
| **Все пользователи, интегрированная среда сценариев PowerShell**| `$PROFILE.AllUsersCurrentHost` |
| **Текущий пользователь, все узлы**| `$PROFILE.CurrentUserAllHosts` |
| **Все пользователи, все узлы** | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a>Создание профиля

Для создания профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" выполните следующую команду:

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

Для создания профиля "Все пользователи, интегрированная среда сценариев PowerShell" выполните следующую команду:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Для создания профиля "Текущий пользователь, все узлы" выполните следующую команду:

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

Для создания профиля "Все пользователи, все узлы" введите следующее:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a>Изменение профиля

1. Чтобы открыть профиль, запустите команду psedit с переменной, которая указывает изменяемый профиль. Например, для открытия профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" введите: `psEdit $PROFILE`

2. Добавьте несколько элементов в профиль. Ниже приведено несколько примеров, как можно приступить к работе:

   - Чтобы изменить цвет фона по умолчанию для области консоли на синий, введите в файле профиля следующее: `$psISE.Options.OutputPaneBackground = 'blue'` . Дополнительные сведения о переменной $psISE см. в статье [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](The-ISE-Object-Model-Hierarchy.md).

   - Чтобы изменить размер шрифта на 20, введите в файле профиля следующее: `$psISE.Options.FontSize =20`

3. Чтобы сохранить файл профиля, в меню **Файл** щелкните **Сохранить**. Внесенные изменения применяются при следующем открытии интегрированной среды сценариев Windows PowerShell.

## <a name="see-also"></a>См. также

- [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [Введение в интегрированную среду сценариев Windows PowerShell](Introducing-the-Windows-PowerShell-ISE.md)