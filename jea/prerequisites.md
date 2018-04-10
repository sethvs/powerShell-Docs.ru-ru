---
ms.date: 06/12/2017
author: rpsqrd
ms.topic: conceptual
keywords: jea,powershell,безопасность
title: Предварительные условия JEA
ms.openlocfilehash: 92a74d89a0e982e9f45e69d92b261756de33c038
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="prerequisites"></a><span data-ttu-id="daaa3-103">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="daaa3-103">Prerequisites</span></span>

> <span data-ttu-id="daaa3-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="daaa3-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="daaa3-105">Just Enough Administration — это функция, входящая в состав Windows PowerShell 5.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="daaa3-105">Just Enough Administration is a feature included with Windows PowerShell 5.0 and higher.</span></span>
<span data-ttu-id="daaa3-106">В этом разделе описываются предварительные условия, которые нужно выполнить, чтобы начать работу с JEA.</span><span class="sxs-lookup"><span data-stu-id="daaa3-106">This topic describes the prerequisites that must be satisfied in order to start using JEA.</span></span>

## <a name="install-jea"></a><span data-ttu-id="daaa3-107">Установка JEA</span><span class="sxs-lookup"><span data-stu-id="daaa3-107">Install JEA</span></span>

<span data-ttu-id="daaa3-108">Функция JEA доступна в Windows PowerShell 5.0 и более поздних версий, но для обеспечения полной функциональности рекомендуется установить последнюю версию PowerShell, доступную для вашей системы.</span><span class="sxs-lookup"><span data-stu-id="daaa3-108">JEA is available with Windows PowerShell 5.0 and higher, but for full functionality it is recommended that you install the latest version of PowerShell available for your system.</span></span>
<span data-ttu-id="daaa3-109">В следующей таблице описывается доступность JEA на Windows Server:</span><span class="sxs-lookup"><span data-stu-id="daaa3-109">The following table describes JEA's availability on Windows Server:</span></span>

<span data-ttu-id="daaa3-110">операционная система сервера</span><span class="sxs-lookup"><span data-stu-id="daaa3-110">Server Operating System</span></span>   | <span data-ttu-id="daaa3-111">Доступность JEA</span><span class="sxs-lookup"><span data-stu-id="daaa3-111">JEA Availability</span></span>
--------------------------|--------------------------------
<span data-ttu-id="daaa3-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="daaa3-112">Windows Server 2016</span></span>       | <span data-ttu-id="daaa3-113">Предустанавливается</span><span class="sxs-lookup"><span data-stu-id="daaa3-113">Preinstalled</span></span>
<span data-ttu-id="daaa3-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="daaa3-114">Windows Server 2012 R2</span></span>    | <span data-ttu-id="daaa3-115">Полный набор функций с WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-115">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="daaa3-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="daaa3-116">Windows Server 2012</span></span>       | <span data-ttu-id="daaa3-117">Полный набор функций с WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-117">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="daaa3-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="daaa3-118">Windows Server 2008 R2</span></span>    | <span data-ttu-id="daaa3-119">Ограниченная функциональность<sup>1</sup> с WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-119">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="daaa3-120">Вы можете также использовать JEA на домашнем или рабочем компьютере:</span><span class="sxs-lookup"><span data-stu-id="daaa3-120">You can also use JEA on your home or work computer:</span></span>

<span data-ttu-id="daaa3-121">клиентская операционная система</span><span class="sxs-lookup"><span data-stu-id="daaa3-121">Client Operating System</span></span>   | <span data-ttu-id="daaa3-122">Доступность JEA</span><span class="sxs-lookup"><span data-stu-id="daaa3-122">JEA Availability</span></span>
--------------------------|-----------------------------------------------------
<span data-ttu-id="daaa3-123">Windows 10 1607+</span><span class="sxs-lookup"><span data-stu-id="daaa3-123">Windows 10 1607+</span></span>          | <span data-ttu-id="daaa3-124">Предустанавливается</span><span class="sxs-lookup"><span data-stu-id="daaa3-124">Preinstalled</span></span>
<span data-ttu-id="daaa3-125">Windows 10 1603, 1511</span><span class="sxs-lookup"><span data-stu-id="daaa3-125">Windows 10 1603, 1511</span></span>     | <span data-ttu-id="daaa3-126">Предустанавливается, с неполной функциональностью<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="daaa3-126">Preinstalled, with reduced functionality<sup>2</sup></span></span>
<span data-ttu-id="daaa3-127">Windows 10 1507</span><span class="sxs-lookup"><span data-stu-id="daaa3-127">Windows 10 1507</span></span>           | <span data-ttu-id="daaa3-128">Недоступно</span><span class="sxs-lookup"><span data-stu-id="daaa3-128">Not available</span></span>
<span data-ttu-id="daaa3-129">Windows 8, 8.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-129">Windows 8, 8.1</span></span>            | <span data-ttu-id="daaa3-130">Полный набор функций с WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-130">Full functionality with WMF 5.1</span></span>
<span data-ttu-id="daaa3-131">Windows 7</span><span class="sxs-lookup"><span data-stu-id="daaa3-131">Windows 7</span></span>                 | <span data-ttu-id="daaa3-132">Ограниченная функциональность<sup>1</sup> с WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="daaa3-132">Reduced functionality<sup>1</sup> with WMF 5.1</span></span>

<span data-ttu-id="daaa3-133"><sup>1</sup> JEA нельзя настроить для использования групповых управляемых учетных записей служб в операционных системах Windows Server 2008 R2 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="daaa3-133"><sup>1</sup> JEA cannot be configured to use group managed service accounts on Windows Server 2008 R2 or Windows 7.</span></span>
<span data-ttu-id="daaa3-134">Виртуальные учетные записи и другие возможности JEA *поддерживаются*.</span><span class="sxs-lookup"><span data-stu-id="daaa3-134">Virtual accounts and other JEA features *are* supported.</span></span>

<span data-ttu-id="daaa3-135"><sup>2</sup> Версии 1511 и 1603 Windows 10 не поддерживают следующие функции JEA: запуск в качестве групповой управляемой учетной записи службы, правила условного доступа в конфигурациях сеанса, диск пользователя и предоставление разрешений для учетных записей локальных пользователей.</span><span class="sxs-lookup"><span data-stu-id="daaa3-135"><sup>2</sup> Windows 10 versions 1511 and 1603 do not support the following JEA features: running as a group managed service account, conditional access rules in session configurations, the user drive, and granting access to local user accounts.</span></span>
<span data-ttu-id="daaa3-136">Для обеспечения поддержки этих функций выполните обновление Windows до версии 1607 (юбилейное обновление) или более поздней.</span><span class="sxs-lookup"><span data-stu-id="daaa3-136">To get support for these features, update Windows to version 1607 (Anniversary Update) or higher.</span></span>

### <a name="check-which-version-of-powershell-is-installed"></a><span data-ttu-id="daaa3-137">Определение установленной версии PowerShell</span><span class="sxs-lookup"><span data-stu-id="daaa3-137">Check which version of PowerShell is installed</span></span>

<span data-ttu-id="daaa3-138">Чтобы узнать, какая версия PowerShell установлена на компьютере, проверьте переменную `$PSVersionTable` в командной строке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daaa3-138">To check which version of PowerShell is installed on your system, check the `$PSVersionTable` variable in a Windows PowerShell prompt.</span></span>

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

<span data-ttu-id="daaa3-139">Вы готовы к использованию JEA, если *основной* номер версии больше или равен **5**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-139">You are ready to use JEA if the *Major* version is equal to or greater than **5**.</span></span>
<span data-ttu-id="daaa3-140">Для получения наилучших результатов и доступа к новейшим возможностям рекомендуется обновить PowerShell до версии **5.1**, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="daaa3-140">For the best experience, and to have access to all the latest features, it is recommended that you upgrade to PowerShell version **5.1** when possible.</span></span>

### <a name="install-windows-management-framework"></a><span data-ttu-id="daaa3-141">Установка Windows Management Framework</span><span class="sxs-lookup"><span data-stu-id="daaa3-141">Install Windows Management Framework</span></span>

<span data-ttu-id="daaa3-142">Если вы используете более старую версию PowerShell, потребуется установить в системе последнее обновление Windows Management Framework (WMF).</span><span class="sxs-lookup"><span data-stu-id="daaa3-142">If you are running an older version of PowerShell, you will need to update your system with the latest Windows Management Framework (WMF) update.</span></span>
<span data-ttu-id="daaa3-143">Пакеты обновлений и ссылка на актуальные заметки о выпуске WMF доступны в [Центре загрузки](https://aka.ms/WMF5).</span><span class="sxs-lookup"><span data-stu-id="daaa3-143">Update packages and a link to the latest WMF release notes are available in the [Download Center](https://aka.ms/WMF5).</span></span>

<span data-ttu-id="daaa3-144">Настоятельно рекомендуется проверить совместимость рабочей нагрузки с WMF до обновления всех серверов.</span><span class="sxs-lookup"><span data-stu-id="daaa3-144">It is strongly recommended that you test your workload's compatibility with WMF before upgrading all of your servers.</span></span>

<span data-ttu-id="daaa3-145">Пользователям Windows 10 нужно установить последние обновления компонентов для получения текущей версии Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daaa3-145">Windows 10 users should install the latest feature updates to obtain the current version of Windows PowerShell.</span></span>

## <a name="enable-powershell-remoting"></a><span data-ttu-id="daaa3-146">Включение удаленного взаимодействия PowerShell</span><span class="sxs-lookup"><span data-stu-id="daaa3-146">Enable PowerShell Remoting</span></span>

<span data-ttu-id="daaa3-147">Удаленное взаимодействие PowerShell предоставляет собой основу, на которой построена функция JEA.</span><span class="sxs-lookup"><span data-stu-id="daaa3-147">PowerShell Remoting provides the foundation on which JEA is built.</span></span>
<span data-ttu-id="daaa3-148">Поэтому перед использованием JEA необходимо включить удаленное взаимодействие PowerShell и [должным образом защитить](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) его в своей системе.</span><span class="sxs-lookup"><span data-stu-id="daaa3-148">It is therefore necessary to ensure PowerShell Remoting is enabled and [properly secured](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) on your system before you can use JEA.</span></span>

<span data-ttu-id="daaa3-149">В Windows Server 2012, 2012 R2 и 2016 удаленное взаимодействие PowerShell включено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="daaa3-149">PowerShell Remoting is enabled by default on Windows Server 2012, 2012 R2, and 2016.</span></span>
<span data-ttu-id="daaa3-150">Удаленное взаимодействие PowerShell можно включить, выполнив приведенную ниже команду в окне PowerShell с повышенными привилегиями.</span><span class="sxs-lookup"><span data-stu-id="daaa3-150">You can enable PowerShell Remoting by running the following command in an elevated PowerShell window.</span></span>

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a><span data-ttu-id="daaa3-151">Включение ведения журнала для блока сценариев и модуля PowerShell (необязательно)</span><span class="sxs-lookup"><span data-stu-id="daaa3-151">Enable PowerShell module and script block logging (optional)</span></span>

<span data-ttu-id="daaa3-152">Указанные ниже действия позволят включить ведение журнала действий PowerShell в вашей системе.</span><span class="sxs-lookup"><span data-stu-id="daaa3-152">The following steps enable logging for all PowerShell actions on your system.</span></span>
<span data-ttu-id="daaa3-153">Ведение журнала модуля PowerShell не является обязательным для JEA, однако настоятельно рекомендуется включить его, чтобы выполняемые пользователями команды регистрировались в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="daaa3-153">PowerShell Module Logging is not required for JEA, however it is strongly recommended that you turn it on to ensure the commands users run are logged in a central location.</span></span>

<span data-ttu-id="daaa3-154">Политику ведения журнала модуля PowerShell можно настроить с помощью групповой политики.</span><span class="sxs-lookup"><span data-stu-id="daaa3-154">You can configure the PowerShell Module Logging policy using Group Policy.</span></span>

1. <span data-ttu-id="daaa3-155">Откройте редактор локальных групповых политик на рабочей станции или объект групповой политики в консоли управления групповыми политиками на контроллере домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="daaa3-155">Open the Local Group Policy Editor on a workstation or a Group Policy Object in the Group Policy Management Console on an Active Directory Domain Controller</span></span>
2. <span data-ttu-id="daaa3-156">Откройте папку **Конфигурация компьютера\\Административные шаблоны\\Компоненты Windows\\Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-156">Navigate to **Computer Configuration\\Administrative Templates\\Windows Components\\Windows PowerShell**</span></span>
3. <span data-ttu-id="daaa3-157">Дважды щелкните пункт **Включить ведение журнала модулей**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-157">Double click on **Turn on Module Logging**</span></span>
4. <span data-ttu-id="daaa3-158">Нажмите кнопку **Включено**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-158">Click **Enabled**</span></span>
5. <span data-ttu-id="daaa3-159">В разделе "Параметры" нажмите кнопку **Показать** рядом с именами модулей.</span><span class="sxs-lookup"><span data-stu-id="daaa3-159">In the Options section, click on **Show** next to Module Names</span></span>
6. <span data-ttu-id="daaa3-160">Введите "**\***" во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="daaa3-160">Type "**\***" in the pop up window.</span></span> <span data-ttu-id="daaa3-161">Это означает, что PowerShell будет регистрировать в журнале команды из всех модулей.</span><span class="sxs-lookup"><span data-stu-id="daaa3-161">This instructs PowerShell to log commands from all modules.</span></span>
7. <span data-ttu-id="daaa3-162">Нажмите кнопку **ОК** для применения политики.</span><span class="sxs-lookup"><span data-stu-id="daaa3-162">Click **OK** to set the policy</span></span>
8. <span data-ttu-id="daaa3-163">Дважды щелкните **Включить регистрацию блоков сценариев PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-163">Double click on **Turn on PowerShell Script Block Logging**</span></span>
9. <span data-ttu-id="daaa3-164">Нажмите кнопку **Включено**.</span><span class="sxs-lookup"><span data-stu-id="daaa3-164">Click **Enabled**</span></span>
10. <span data-ttu-id="daaa3-165">Нажмите кнопку **ОК** для применения политики.</span><span class="sxs-lookup"><span data-stu-id="daaa3-165">Click **OK** to set the policy</span></span>
11. <span data-ttu-id="daaa3-166">Запустите **gpupdate** или дождитесь обработки обновленной политики и применения этих параметров групповой политикой (только на компьютерах, присоединенных к домену).</span><span class="sxs-lookup"><span data-stu-id="daaa3-166">(On domain-joined machines only) Run **gpupdate** or wait for Group Policy to process the updated policy and apply the settings</span></span>

<span data-ttu-id="daaa3-167">С помощью групповой политики также можно включить запись действий PowerShell в масштабе всей системы.</span><span class="sxs-lookup"><span data-stu-id="daaa3-167">You can also enable system-wide PowerShell transcription through Group Policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daaa3-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="daaa3-168">Next steps</span></span>

- [<span data-ttu-id="daaa3-169">Создание файла возможностей ролей</span><span class="sxs-lookup"><span data-stu-id="daaa3-169">Create a role capability file</span></span>](role-capabilities.md)
- [<span data-ttu-id="daaa3-170">Создание файла конфигурации сеанса</span><span class="sxs-lookup"><span data-stu-id="daaa3-170">Create a session configuration file</span></span>](session-configurations.md)

## <a name="see-also"></a><span data-ttu-id="daaa3-171">См. также:</span><span class="sxs-lookup"><span data-stu-id="daaa3-171">See also</span></span>

- [<span data-ttu-id="daaa3-172">Дополнительные сведения о безопасности удаленного взаимодействия PowerShell и WinRM</span><span class="sxs-lookup"><span data-stu-id="daaa3-172">Additional information about PowerShell Remoting and WinRM security</span></span>](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity)
- [<span data-ttu-id="daaa3-173">Запись блога *PowerShell ♥ the Blue Team* по безопасности</span><span class="sxs-lookup"><span data-stu-id="daaa3-173">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)