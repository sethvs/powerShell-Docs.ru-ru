---
ms.date: 2017-06-05
keywords: "powershell,командлет"
title: "Использование профилей в интегрированной среде сценариев Windows PowerShell"
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: 6b16291b7025928a307380cbae75fcdbdb51a73d
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2017
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a><span data-ttu-id="ff28b-103">Использование профилей в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff28b-103">How to Use Profiles in Windows PowerShell ISE</span></span>
<span data-ttu-id="ff28b-104">В этой статье объясняется, как использовать профили в интегрированной среде скриптов Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="ff28b-104">This topic explains how to use Profiles in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ff28b-105">Перед выполнением задач из этого раздела рекомендуется ознакомиться со статьей [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630)) либо ввести `Get-Help about_Profiles` в области консоли и нажать клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="ff28b-105">We recommend that before performing the tasks in this section, you review [about_Profiles [v4]](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630)), or in the Console Pane, type, `Get-Help about_Profiles` and press **ENTER**.</span></span>

<span data-ttu-id="ff28b-106">Профиль — это сценарий интегрированной среды сценариев Windows PowerShell, который выполняется автоматически при запуске нового сеанса.</span><span class="sxs-lookup"><span data-stu-id="ff28b-106">A profile is a Windows PowerShell ISE script that runs automatically when you start a new session.</span></span>  <span data-ttu-id="ff28b-107">Можно создать один или несколько профилей Windows PowerShell для интегрированной среды сценариев Windows PowerShell и использовать их для настройки среды Windows PowerShell для интегрированной среды сценариев Windows PowerShell, подготавливая ее к работе с помощью переменных, псевдонимов, функций, а также настроек цветов и шрифтов, которые должны быть доступны.</span><span class="sxs-lookup"><span data-stu-id="ff28b-107">You can create one or more Windows PowerShell profiles for Windows PowerShell ISE and use them to add the configure the Windows PowerShell or Windows PowerShell ISE environment, preparing it for your use, with variables, aliases, functions, and color and font preferences that you want available.</span></span> <span data-ttu-id="ff28b-108">Профиль затрагивает каждый запускаемый сеанс интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-108">A profile affects every Windows PowerShell ISE session that you start.</span></span>

> [!NOTE]
> <span data-ttu-id="ff28b-109">Политика выполнения Windows PowerShell определяет, можно ли запускать сценарии и загружать профиль.</span><span class="sxs-lookup"><span data-stu-id="ff28b-109">The Windows PowerShell execution policy determines whether you can run scripts and load a profile.</span></span> <span data-ttu-id="ff28b-110">Политика выполнения по умолчанию (Restricted) запрещает выполнение всех сценариев, включая профили.</span><span class="sxs-lookup"><span data-stu-id="ff28b-110">The default execution policy, “Restricted,” prevents all scripts from running, including profiles.</span></span> <span data-ttu-id="ff28b-111">При использовании политики "Restricted" загрузить профиль нельзя.</span><span class="sxs-lookup"><span data-stu-id="ff28b-111">If you use the “Restricted” policy, the profile cannot load.</span></span> <span data-ttu-id="ff28b-112">Дополнительные сведения о политике выполнения см. в статье [about_Execution_Policies [v4]](https://technet.microsoft.com/library/347708dc-1515-4d74-978b-8334603472e6(v=wps.630)).</span><span class="sxs-lookup"><span data-stu-id="ff28b-112">For more information about execution policy, see [about_Execution_Policies [v4]](https://technet.microsoft.com/library/347708dc-1515-4d74-978b-8334603472e6(v=wps.630)).</span></span>

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a><span data-ttu-id="ff28b-113">Выбор профиля для использования в интегрированной среде сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff28b-113">Selecting a profile to use in the Windows PowerShell ISE</span></span>
<span data-ttu-id="ff28b-114">Интегрированная среда сценариев Windows PowerShell поддерживает профили для текущего пользователя и для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="ff28b-114">Windows PowerShell ISE supports profiles for the current user and all users.</span></span> <span data-ttu-id="ff28b-115">Он также поддерживает профили Windows PowerShell, затрагивающие все узлы.</span><span class="sxs-lookup"><span data-stu-id="ff28b-115">It also supports the Windows PowerShell profiles that apply to all hosts.</span></span>

<span data-ttu-id="ff28b-116">Выбор профиля зависит от того, каким образом вы используете Windows PowerShell и интегрированную среду сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-116">The profile that you use is determined by how you use Windows PowerShell and Windows PowerShell ISE.</span></span>

-   <span data-ttu-id="ff28b-117">Если для запуска Windows PowerShell используется только интегрированная среда сценариев Windows PowerShell, сохраните все элементы в одном из профилей интегрированной среды сценариев, таком как CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-117">If you use only Windows PowerShell ISE to run Windows PowerShell, then save all your items in one of the ISE-specific profiles, such as the CurrentUserCurrentHost profile for Windows PowerShell ISE or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

-   <span data-ttu-id="ff28b-118">Если для запуска Windows PowerShell используется несколько основных программ, сохраните свои функции, псевдонимы, переменные и команды в профиле, затрагивающем все основные программы, таком как CurrentUserAllHosts или AllUsersAllHosts, и сохраните функции интегрированной среды сценариев, такие как настройки цветов и шрифтов, в CurrentUserCurrentHost или AllUsersCurrentHost для интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-118">If you use multiple host programs to run Windows PowerShell, save your functions, aliases, variables, and commands in a profile that affects all host programs, such as the CurrentUserAllHosts or the AllUsersAllHosts profile, and save ISE-specific features, like color and font customization in the CurrentUserCurrentHost profile for Windows PowerShell ISE profile or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

<span data-ttu-id="ff28b-119">Ниже указаны профили, которые можно создать и использовать в интегрированной среде сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-119">The following are profiles that can be created and used in Windows PowerShell ISE.</span></span> <span data-ttu-id="ff28b-120">Каждый профиль сохраняется по собственному пути.</span><span class="sxs-lookup"><span data-stu-id="ff28b-120">Each profile is saved to its own specific path.</span></span>

| <span data-ttu-id="ff28b-121">Тип профиля</span><span class="sxs-lookup"><span data-stu-id="ff28b-121">Profile Type</span></span> | <span data-ttu-id="ff28b-122">Путь к профилю</span><span class="sxs-lookup"><span data-stu-id="ff28b-122">Profile Path</span></span> |
| --- | --- |
| <span data-ttu-id="ff28b-123">**Текущий пользователь, интегрированная среда сценариев PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ff28b-123">**Current user, PowerShell ISE**</span></span>| <span data-ttu-id="ff28b-124">`$PROFILE.CurrentUserCurrentHost` или `$PROFILE`</span><span class="sxs-lookup"><span data-stu-id="ff28b-124">`$PROFILE.CurrentUserCurrentHost`, or `$PROFILE`</span></span> |
| <span data-ttu-id="ff28b-125">**Все пользователи, интегрированная среда сценариев PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ff28b-125">**All users, PowerShell ISE**</span></span>| `$PROFILE.AllUsersCurrentHost` |
| <span data-ttu-id="ff28b-126">**Текущий пользователь, все узлы**</span><span class="sxs-lookup"><span data-stu-id="ff28b-126">**Current user, All hosts**</span></span>| `$PROFILE.CurrentUserAllHosts` |
| <span data-ttu-id="ff28b-127">**Все пользователи, все узлы**</span><span class="sxs-lookup"><span data-stu-id="ff28b-127">**All users, All hosts**</span></span> | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a><span data-ttu-id="ff28b-128">Создание профиля</span><span class="sxs-lookup"><span data-stu-id="ff28b-128">To create a new profile</span></span>
<span data-ttu-id="ff28b-129">Для создания профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff28b-129">To create a new “Current user, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE )) 
{ New-Item -Type File -Path $PROFILE -Force }
```

<span data-ttu-id="ff28b-130">Для создания профиля "Все пользователи, интегрированная среда сценариев PowerShell" выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff28b-130">To create a new “All users, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost)) 
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

<span data-ttu-id="ff28b-131">Для создания профиля "Текущий пользователь, все узлы" выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ff28b-131">To create a new “Current user, All Hosts” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts)) 
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

<span data-ttu-id="ff28b-132">Для создания профиля "Все пользователи, все узлы" введите следующее:</span><span class="sxs-lookup"><span data-stu-id="ff28b-132">To create a new “All users, All Hosts” profile, type:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts)) 
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a><span data-ttu-id="ff28b-133">Изменение профиля</span><span class="sxs-lookup"><span data-stu-id="ff28b-133">To edit a profile</span></span>

1.  <span data-ttu-id="ff28b-134">Чтобы открыть профиль, запустите команду psedit с переменной, которая указывает изменяемый профиль.</span><span class="sxs-lookup"><span data-stu-id="ff28b-134">To open the profile, run the command psedit with the variable that specifies the profile you want to edit.</span></span> <span data-ttu-id="ff28b-135">Например, для открытия профиля "Текущий пользователь, интегрированная среда сценариев PowerShell" введите: `psEdit $PROFILE`</span><span class="sxs-lookup"><span data-stu-id="ff28b-135">For example, to open the “Current user, Windows PowerShell ISE” profile, type: `psEdit $PROFILE`</span></span>

2.  <span data-ttu-id="ff28b-136">Добавьте несколько элементов в профиль.</span><span class="sxs-lookup"><span data-stu-id="ff28b-136">Add some items to your profile.</span></span> <span data-ttu-id="ff28b-137">Ниже приведено несколько примеров, как можно приступить к работе:</span><span class="sxs-lookup"><span data-stu-id="ff28b-137">The following are a few examples to get you started:</span></span>

    -   <span data-ttu-id="ff28b-138">Чтобы изменить цвет фона по умолчанию для области консоли на синий, введите в файле профиля следующее: `$psISE.Options.OutputPaneBackground = 'blue'` .</span><span class="sxs-lookup"><span data-stu-id="ff28b-138">To change the default background color of the Console Pane to blue, in the profile file type: `$psISE.Options.OutputPaneBackground = 'blue'` .</span></span> <span data-ttu-id="ff28b-139">Дополнительные сведения о переменной $psISE см. в статье [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell]().</span><span class="sxs-lookup"><span data-stu-id="ff28b-139">For more information about the $psISE variable, see [Windows PowerShell ISE Object Model Reference]().</span></span>

    -   <span data-ttu-id="ff28b-140">Чтобы изменить размер шрифта на 20, введите в файле профиля следующее: `$psISE.Options.FontSize =20`</span><span class="sxs-lookup"><span data-stu-id="ff28b-140">To change font size to 20, in the profile file type: `$psISE.Options.FontSize =20`</span></span>

3.  <span data-ttu-id="ff28b-141">Чтобы сохранить файл профиля, в меню **Файл** щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ff28b-141">To save your profile file, on the **File** menu, click **Save**.</span></span> <span data-ttu-id="ff28b-142">Внесенные изменения применяются при следующем открытии интегрированной среды сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff28b-142">Next time you open the Windows PowerShell ISE, your customizations are applied.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff28b-143">См. также</span><span class="sxs-lookup"><span data-stu-id="ff28b-143">See Also</span></span>
- [<span data-ttu-id="ff28b-144">about_Profiles [v4]</span><span class="sxs-lookup"><span data-stu-id="ff28b-144">about_Profiles [v4]</span></span>](https://technet.microsoft.com/library/e1d9e30a-70cc-4f36-949f-fc7cd96b4054(v=wps.630))
- [<span data-ttu-id="ff28b-145">Использование интегрированной среды сценариев Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff28b-145">Using the Windows PowerShell ISE</span></span>](Using-the-Windows-PowerShell-ISE.md)

