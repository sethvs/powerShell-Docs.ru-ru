---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: e8620cdeb90792e86d091d3e19a169f9dfa690f9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="known-issues-and-limitations"></a><span data-ttu-id="3f306-102">Известные проблемы и ограничения</span><span class="sxs-lookup"><span data-stu-id="3f306-102">Known Issues and Limitations</span></span>

<a name="powershell-shortcuts-are-broken-when-used-for-the-first-time"></a><span data-ttu-id="3f306-103">PowerShell ярлыки перестают работать при первом использовании</span><span class="sxs-lookup"><span data-stu-id="3f306-103">PowerShell Shortcuts are broken when used for the first time</span></span>
------------------------------------------------------------

<span data-ttu-id="3f306-104">**Решение.** Выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="3f306-104">**Resolution:** Perform one of the following actions:</span></span>

1.  <span data-ttu-id="3f306-105">Щелкните ярлык PowerShell правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="3f306-105">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="3f306-106">Выберите Windows PowerShell для запуска в режиме без повышенных прав.</span><span class="sxs-lookup"><span data-stu-id="3f306-106">Select “Windows PowerShell” to launch in a non-elevated mode.</span></span>
2.  <span data-ttu-id="3f306-107">Щелкните ярлык PowerShell правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="3f306-107">Right click on the PowerShell shortcut.</span></span> <span data-ttu-id="3f306-108">Щелкните Windows PowerShell правой кнопкой мыши и выберите пункт "Запуск от имени администратора" для запуска в режиме с повышенными правами.</span><span class="sxs-lookup"><span data-stu-id="3f306-108">Right click on “Windows PowerShell” and select “Run As Administrator” to launch in an elevated mode.</span></span>

<span data-ttu-id="3f306-109">После выполнения любого из указанных действий ярлыки PowerShell будут работать.</span><span class="sxs-lookup"><span data-stu-id="3f306-109">Once you have performed either of the above actions, the PowerShell shortcuts will work.</span></span> <span data-ttu-id="3f306-110">Эти действия требуется выполнить всего один раз.</span><span class="sxs-lookup"><span data-stu-id="3f306-110">These actions need to be performed only once.</span></span>


<a name="powershell-modules-and-dsc-resources-report-errors-about-executionpolicy-on-windows-7"></a><span data-ttu-id="3f306-111">Модули PowerShell и ресурсы DSC выдает ошибки для ExecutionPolicy в Windows 7</span><span class="sxs-lookup"><span data-stu-id="3f306-111">PowerShell Modules and DSC Resources report errors about ExecutionPolicy on Windows 7</span></span>
-------------------------------------------------------------------------------------
<span data-ttu-id="3f306-112">В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.</span><span class="sxs-lookup"><span data-stu-id="3f306-112">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

<span data-ttu-id="3f306-113">**Решение.** Задайте для ExecutionPolicy значение RemoteSigned, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):</span><span class="sxs-lookup"><span data-stu-id="3f306-113">**Resolution:** Set the ExecutionPolicy to RemoteSigned by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<a name="connecting-to-an-old-remote-exchange-endpoint-causes-a-crash"></a><span data-ttu-id="3f306-114">Подключение к старой удаленной конечной точки Exchange вызывает сбой</span><span class="sxs-lookup"><span data-stu-id="3f306-114">Connecting to an old remote Exchange endpoint causes a crash</span></span>
------------------------------------------------------------

<span data-ttu-id="3f306-115">Старая конечная точка Exchange выполняет перенаправление на новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="3f306-115">The old Exchange endpoint redirects to a new endpoint.</span></span> <span data-ttu-id="3f306-116">В логике перенаправления имеется ошибка, которая вызывает сбой.</span><span class="sxs-lookup"><span data-stu-id="3f306-116">There is a bug in the redirection logic that results in a crash.</span></span>

<span data-ttu-id="3f306-117">**Решение.** Подключитесь непосредственно к новой конечной точке.</span><span class="sxs-lookup"><span data-stu-id="3f306-117">**Resolution:** Connect directly to the new endpoint.</span></span>


<a name="software-inventory-logging-feature-is-erroneously-stopped-after-wmf-50-installation-on-windows-server-2012-r2"></a><span data-ttu-id="3f306-118">Функция инвентаризации программного обеспечения ошибочно остановлена после установки WMF 5.0 в Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3f306-118">Software Inventory Logging feature is erroneously stopped after WMF 5.0 installation on Windows Server 2012 R2</span></span>
-------------------------------------------------------------------------------------------------------------

<span data-ttu-id="3f306-119">При установке WMF 5.0 в Windows Server 2012 R2, где уже выполняется инвентаризации программного обеспечения, эта функция ошибочно останавливается после установки.</span><span class="sxs-lookup"><span data-stu-id="3f306-119">When installing WMF 5.0 on a Windows Server 2012 R2 that is already running SIL, the Software Inventory Logging feature is erroneously stopped after installation.</span></span>

<span data-ttu-id="3f306-120">**Решение.** Запустите командлет Start-SilLogging один раз после установки WMF, так как процесс его установки ошибочно останавливает функцию инвентаризации программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="3f306-120">**Resolution:** Run the Start-SilLogging cmdlet once after the WMF installation, as the installation process will errantly stop the Software Inventory Logging feature.</span></span>

<a name="get-childitem-does-not-work-if--literalpath-and--recurse-are-used-together"></a><span data-ttu-id="3f306-121">Get-ChildItem не работает, если -LiteralPath и -Recurse используются совместно</span><span class="sxs-lookup"><span data-stu-id="3f306-121">Get-ChildItem does not work if -LiteralPath and -Recurse are used together</span></span>
--------------------------------------------------------------------------

<span data-ttu-id="3f306-122">Если имя каталога содержит недопустимый подстановочный знак, то Get-ChildItem не дает ожидаемые результаты при совместном использовании -LiteralPath и -Recurse.</span><span class="sxs-lookup"><span data-stu-id="3f306-122">If a directory name contains an invalid wildcard character, then Get-ChildItem will not produce expected results when both -LiteralPath and -Recurse are used together.</span></span>

<span data-ttu-id="3f306-123">**Решение.** В настоящее время обходной путь, хотя он и не является оптимальным, заключается в реализации рекурсии в скрипте вместо использования командлета.</span><span class="sxs-lookup"><span data-stu-id="3f306-123">**Resolution:** Not ideal, but current workaround is to implement recursion in the script rather than rely on the cmdlet.</span></span>


<a name="sysprep-fails-after-wmf-50-installation"></a><span data-ttu-id="3f306-124">Sysprep не работает после установки WMF 5.0</span><span class="sxs-lookup"><span data-stu-id="3f306-124">Sysprep fails after WMF 5.0 installation</span></span>
----------------------------------------

<span data-ttu-id="3f306-125">Существует два способа решения этой проблемы в зависимости от используемой версии Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3f306-125">There are two workarounds for this issue depending on the version of Windows Server you are running.</span></span>

<span data-ttu-id="3f306-126">**Решение**</span><span class="sxs-lookup"><span data-stu-id="3f306-126">**Resolution:**</span></span>
- <span data-ttu-id="3f306-127">Для систем под управлением **Windows Server 2008 R2**</span><span class="sxs-lookup"><span data-stu-id="3f306-127">For systems running **Windows Server 2008 R2**</span></span>
  1. <span data-ttu-id="3f306-128">Откройте PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="3f306-128">Open Powershell as an administrator</span></span>
  2. <span data-ttu-id="3f306-129">Выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="3f306-129">Run the following command</span></span> 
  
  ```powershell
    Set-SilLogging –TargetUri https://BlankTarget –CertificateThumbprint 0123456789
  ```
  3. <span data-ttu-id="3f306-130">Выполните команду и пропустите ошибку, так как она ожидалась.</span><span class="sxs-lookup"><span data-stu-id="3f306-130">Run the command and ignore the error, as they are expected.</span></span>
  
  ```powershell
    Publish-SilData
   ```
  4. <span data-ttu-id="3f306-131">Удалите файлы в каталоге \Windows\System32\Logfiles\SIL\.</span><span class="sxs-lookup"><span data-stu-id="3f306-131">Delete the files in  \Windows\System32\Logfiles\SIL\ directory</span></span>
  
  ```powershell
    Remove-Item -Recurse $env:SystemRoot\System32\Logfiles\SIL\
  ```
  5. <span data-ttu-id="3f306-132">Установите все доступные важные обновления Windows и запустите Sysyprep в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="3f306-132">Install all available important Windows Updates, and begin Sysyprep operation normally.</span></span>
  
- <span data-ttu-id="3f306-133">Для систем под управлением **Windows Server 2012**</span><span class="sxs-lookup"><span data-stu-id="3f306-133">For systems running **Windows Server 2012**</span></span>
  1.    <span data-ttu-id="3f306-134">После установки WMF 5.0 на сервере, где предполагается выполнить Sysprep, войдите в систему как администратор.</span><span class="sxs-lookup"><span data-stu-id="3f306-134">After installing WMF 5.0 on the server to be Sysprep’d, login as administrator.</span></span>
  2.    <span data-ttu-id="3f306-135">Скопируйте файл Generize.xml из папки \Windows\System32\Sysprep\ActionFiles\ в расположение за пределами каталога Windows, например C:\.</span><span class="sxs-lookup"><span data-stu-id="3f306-135">Copy Generize.xml from directory \Windows\System32\Sysprep\ActionFiles\ to a location outside of the Windows directory, C:\ for example.</span></span>
  3.    <span data-ttu-id="3f306-136">Откройте копию Generalize.xml в блокноте.</span><span class="sxs-lookup"><span data-stu-id="3f306-136">Open your Generalize.xml copy with notepad.</span></span>
  4.    <span data-ttu-id="3f306-137">Найдите и удалите следующий текст: нужно удалить по одному экземпляру каждой строки (они находятся ближе к концу документа).</span><span class="sxs-lookup"><span data-stu-id="3f306-137">Find and remove the following text, one instance of each needs to be deleted (they will be near the end of the document).</span></span>

    ```
    <sysprepOrder order="0x3200"></sysprepOrder>
    <sysprepOrder order="0x3300"></sysprepOrder>
    ```

  5.    <span data-ttu-id="3f306-138">Сохраните измененную копию Generalize.xml и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3f306-138">Save the edited copy of Generalize.xml and close the file.</span></span>
  6.    <span data-ttu-id="3f306-139">Откройте командную строку от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="3f306-139">Open a command prompt as administrator</span></span>
  7.    <span data-ttu-id="3f306-140">Выполните следующую команду, чтобы стать владельцем файла Generalize.xml в папке system32:</span><span class="sxs-lookup"><span data-stu-id="3f306-140">Run the following command to take ownership of the Generalize.xml file in system32 folder:</span></span>

    ```
    Takeown /f C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```

  8.    <span data-ttu-id="3f306-141">Выполните следующую команду, чтобы установить соответствующее разрешение для доступа к файлу:</span><span class="sxs-lookup"><span data-stu-id="3f306-141">Run the following command to set appropriate permission on the file:</span></span>

    ```
    Cacls C:\Windows\System32\ Sysprep\ActionFiles\Generalize.xml /G `<AdministratorUserName>`:F 
    ```
      * <span data-ttu-id="3f306-142">Ответьте "Да" в запросе на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="3f306-142">Answer Yes at the prompt for confirmation.</span></span> 
      * <span data-ttu-id="3f306-143">Обратите внимание, что `<AdministratorUserName>` следует заменить именем пользователя, который является администратором на данном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f306-143">Note that `<AdministratorUserName>` should be replaced by the username who is administrator on the machine.</span></span> <span data-ttu-id="3f306-144">Например, "Administrator".</span><span class="sxs-lookup"><span data-stu-id="3f306-144">For example, "Administrator".</span></span>
      
  9.    <span data-ttu-id="3f306-145">Скопируйте измененный и сохраненный файл в каталог Sysprep, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3f306-145">Copy the file you edited and saved over to the Sysprep directory using the following command:</span></span>

    ```
    xcopy C:\Generalize.xml C:\Windows\System32\Sysprep\ActionFiles\Generalize.xml 
    ```
      * <span data-ttu-id="3f306-146">В запросе ответьте "Да", чтобы перезаписать файл (если запрос на перезапись не появится, перепроверьте введенный путь).</span><span class="sxs-lookup"><span data-stu-id="3f306-146">Answer Yes to overwrite (note that if there is no prompt to overwrite, double check the path entered).</span></span>
      * <span data-ttu-id="3f306-147">Предполагается, что измененная копия Generalize.xml скопирована в каталог C:\.</span><span class="sxs-lookup"><span data-stu-id="3f306-147">Assumes your edited copy of Generalize.xml was copied to C:\ .</span></span>

  10.   <span data-ttu-id="3f306-148">Теперь файл Generalize.xml изменен.</span><span class="sxs-lookup"><span data-stu-id="3f306-148">Generalize.xml is now updated with the workaround.</span></span> <span data-ttu-id="3f306-149">Запустите программу Sysprep с включенным параметром generalize.</span><span class="sxs-lookup"><span data-stu-id="3f306-149">Please run Sysprep with the generalize option enabled.</span></span>

