---
title: Использование профилей в интегрированной среде сценариев Windows PowerShell
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
---
# Использование профилей в интегрированной среде сценариев Windows PowerShell
Эта статья описывает использование профилей в [!INCLUDE[ise_1](../Token/ise_1_md.md)]. Перед выполнением задач из этого раздела рекомендуется ознакомиться со статьей [about_Profiles [v4]](assetId:///e1d9e30a-70cc-4f36-949f-fc7cd96b4054) либо ввести "get-help about_profiles" в области консоли и нажать клавишу **ВВОД**.

Профиль — это сценарий [!INCLUDE[ise_2](../Token/ise_2_md.md)], который выполняется автоматически при запуске нового сеанса.  Можно создать один или несколько профилей [!INCLUDE[wps_2](../Token/wps_2_md.md)] для [!INCLUDE[ise_2](../Token/ise_2_md.md)] и использовать их для настройки среды [!INCLUDE[wps_2](../Token/wps_2_md.md)] или [!INCLUDE[ise_2](../Token/ise_2_md.md)], подготавливая ее к работе с помощью переменных, псевдонимов, функций, а также настроек цветов и шрифтов, которые должны быть доступны. Профиль затрагивает каждый запускаемый сеанс [!INCLUDE[ise_2](../Token/ise_2_md.md)].

> [!NOTE]
> Политика выполнения [!INCLUDE[wps_2](../Token/wps_2_md.md)] определяет, можно ли запускать сценарии и загружать профиль. Политика выполнения по умолчанию (Restricted) запрещает выполнение всех сценариев, включая профили. При использовании политики "Restricted" загрузить профиль нельзя. Дополнительные сведения о политике выполнения см. в статье [about_Execution_Policies [v4]](assetId:///347708dc-1515-4d74-978b-8334603472e6).

## Выбор профиля для использования в интегрированной среде сценариев Windows PowerShell
[!INCLUDE[ise_2](../Token/ise_2_md.md)] поддерживает профили для текущего пользователя и для всех пользователей. Он также поддерживает профили [!INCLUDE[wps_2](../Token/wps_2_md.md)], затрагивающие все узлы.

Применяемый профиль определяется характером использования [!INCLUDE[wps_2](../Token/wps_2_md.md)] и [!INCLUDE[ise_2](../Token/ise_2_md.md)].

-   Если [!INCLUDE[ise_2](../Token/ise_2_md.md)] используется только для запуска Windows PowerShell, сохраните все элементы в одном из профилей интегрированной среды сценариев, таком как CurrentUserCurrentHost для [!INCLUDE[ise_2](../Token/ise_2_md.md)] или AllUsersCurrentHost для [!INCLUDE[ise_2](../Token/ise_2_md.md)].

-   Если используется несколько основных программ для запуска Windows PowerShell, сохраните свои функции, псевдонимы, переменные и команды в профиле, затрагивающем все основные программы, таком как CurrentUserAllHosts или AllUsersAllHosts, и сохраните функции интегрированной среды сценариев, такие как настройки цветов и шрифтов, в CurrentUserCurrentHost для [!INCLUDE[ise_2](../Token/ise_2_md.md)] или AllUsersCurrentHost для [!INCLUDE[ise_2](../Token/ise_2_md.md)].

Ниже указаны профили, которые можно создать и использовать в [!INCLUDE[ise_2](../Token/ise_2_md.md)]. Каждый профиль сохраняется по собственному пути.

|Тип профиля|Путь к профилю|
|----------------|----------------|
|"Текущий пользователь, интегрированная среда сценариев PowerShell"|$profile.CurrentUserCurrentHost или $profile|
|"Все пользователи, интегрированная среда сценариев PowerShell"|$profile.AllUsersCurrentHost|
|"Текущий пользователь, все узлы"|$profile.CurrentUserAllHosts|
|"Все пользователи, все узлы"|$profile.AllUsersAllHosts|

## Создание профиля
Для создания профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" выполните следующую команду:

```
if (!(test-path $profile )) 
{new-item -type file -path $profile -force}
```

Для создания профиля "Все пользователи, интегрированная среда сценариев PowerShell" выполните следующую команду:

```
if (!(test-path $profile.AllUsersCurrentHost)) 
{new-item -type file -path $profile.AllUsersCurrentHost -force}
```

Для создания профиля "Текущий пользователь, все узлы" выполните следующую команду:

```
if (!(test-path $profile.CurrentUserAllHosts)) 
{new-item -type file -path $profile.CurrentUserAllHosts -force}
```

Для создания профиля "Все пользователи, все узлы" введите следующее:

```
if (!(test-path $profile.AllUsersAllHosts)) 
{new-item -type file -path $profile.AllUsersAllHosts-force}
```

## Изменение профиля

1.  Чтобы открыть профиль, запустите команду psedit с переменной, которая указывает изменяемый профиль. Например, для открытия профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" введите: `psEdit $profile`

2.  Добавьте несколько элементов в профиль. Ниже приведено несколько примеров, как можно приступить к работе:

    -   Чтобы изменить цвет фона по умолчанию для области консоли на синий, введите в файле профиля следующее: `$psISE.Options.OutputPaneBackground = 'blue'` . Дополнительные сведения о переменной $psISE см. в статье [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](assetId:///e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c).

    -   Чтобы изменить размер шрифта на 20, введите в файле профиля следующее: `$psISE.Options.FontSize =20`

3.  Чтобы сохранить файл профиля, в меню **Файл** щелкните **Сохранить**. Внесенные изменения применяются при следующем открытии [!INCLUDE[ise_2](../Token/ise_2_md.md)].

## См. также
[about_Profiles [v4]](assetId:///e1d9e30a-70cc-4f36-949f-fc7cd96b4054)
[Использование интегрированной среды сценариев Windows PowerShell](../Topic/Using-the-Windows-PowerShell-ISE.md)



<!--HONumber=Apr16_HO1-->


