---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "dsc,powershell,конфигурация,установка"
title: "Использование DSC на сервере Nano Server"
ms.openlocfilehash: c8f3669ee9c2ed6107c14ba9f4460d82276e1932
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="f1b32-103">Использование DSC на сервере Nano Server</span><span class="sxs-lookup"><span data-stu-id="f1b32-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="f1b32-104">Область применения: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f1b32-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="f1b32-105">**DSC для Nano Server** — это дополнительный пакет в папке `NanoServer\Packages` носителей Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f1b32-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="f1b32-106">Пакет можно установить при создании виртуального жесткого диска для сервера Nano Server, указав значение **Microsoft-NanoServer-DSC-Package** для параметра **Packages** функции **New-NanoServerImage**.</span><span class="sxs-lookup"><span data-stu-id="f1b32-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="f1b32-107">Например, при создании виртуального жесткого диска для виртуальной машины команда будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f1b32-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="f1b32-108">Сведения об установке и использовании сервера Nano Server, а также об управлении этим сервером с помощью удаленного взаимодействия PowerShell см. в статье [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx) (Приступая к работе с сервером Nano Server).</span><span class="sxs-lookup"><span data-stu-id="f1b32-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx).</span></span>


## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="f1b32-109">Функции DSC, доступные на сервере Nano Server</span><span class="sxs-lookup"><span data-stu-id="f1b32-109">DSC features available on Nano Server</span></span>

 <span data-ttu-id="f1b32-110">Так как сервер Nano Server поддерживает только ограниченный набор API по сравнению с полной версией Windows Server, набор функций DSC в системе Nano Server на данный момент несравним с DSC в полнофункциональных SKU.</span><span class="sxs-lookup"><span data-stu-id="f1b32-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="f1b32-111">DSC для Nano Server в настоящее время активно разрабатывается и не является законченным компонентом.</span><span class="sxs-lookup"><span data-stu-id="f1b32-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>
 
 <span data-ttu-id="f1b32-112">Следующие функции DSC в настоящее время доступны для Nano Server:</span><span class="sxs-lookup"><span data-stu-id="f1b32-112">The following DSC features are currently available on Nano Server:</span></span> 


* <span data-ttu-id="f1b32-113">Режимы опроса и принудительной отправки</span><span class="sxs-lookup"><span data-stu-id="f1b32-113">Both push and pull modes</span></span>

* <span data-ttu-id="f1b32-114">Все командлеты DSC, которые существуют в полной версии Windows Server, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="f1b32-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span> 
  * [<span data-ttu-id="f1b32-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f1b32-115">Get-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn407378.aspx)
  * [<span data-ttu-id="f1b32-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f1b32-116">Set-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn521621.aspx)     
  * [<span data-ttu-id="f1b32-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="f1b32-117">Enable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [<span data-ttu-id="f1b32-118">Disable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="f1b32-118">Disable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [<span data-ttu-id="f1b32-119">Start-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-119">Start-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [<span data-ttu-id="f1b32-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-120">Stop-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [<span data-ttu-id="f1b32-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-121">Get-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [<span data-ttu-id="f1b32-122">Test-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-122">Test-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [<span data-ttu-id="f1b32-123">Publish-DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="f1b32-123">Publish-DscConfiguraiton</span></span>](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [<span data-ttu-id="f1b32-124">Update-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-124">Update-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [<span data-ttu-id="f1b32-125">Restore-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1b32-125">Restore-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [<span data-ttu-id="f1b32-126">Remove-DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="f1b32-126">Remove-DscConfigurationDocument</span></span>](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [<span data-ttu-id="f1b32-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="f1b32-127">Get-DscConfigurationStatus</span></span>](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [<span data-ttu-id="f1b32-128">Invoke-DscResource</span><span class="sxs-lookup"><span data-stu-id="f1b32-128">Invoke-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [<span data-ttu-id="f1b32-129">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="f1b32-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [<span data-ttu-id="f1b32-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="f1b32-130">Get-DscResource</span></span>](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [<span data-ttu-id="f1b32-131">New-DscChecksum</span><span class="sxs-lookup"><span data-stu-id="f1b32-131">New-DscChecksum</span></span>](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* <span data-ttu-id="f1b32-132">Компиляция конфигураций (см. раздел [Конфигурации DSC](configurations.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-132">Compiling configurations (see [DSC configurations](configurations.md))</span></span>

  <span data-ttu-id="f1b32-133">**Проблема**. Не работает шифрование паролей (см. раздел [Защита MOF-файла](securemof.md)) во время компиляции конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f1b32-133">**Issue:** Password encryption (see [Securing the MOF File](securemof.md)) during configuration compilation doesn't work.</span></span>

* <span data-ttu-id="f1b32-134">Компиляция метаконфигураций (см. раздел [Настройка локального диспетчера конфигураций](metaConfig.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](metaConfig.md))</span></span>

* <span data-ttu-id="f1b32-135">Выполнение ресурса в контексте пользователя (см. раздел [Запуск DSC с учетными данными пользователя (запуск от имени)](runAsUser.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](runAsUser.md))</span></span>

* <span data-ttu-id="f1b32-136">Ресурсы на основе класса (см. раздел [Написание пользовательских ресурсов DSC с использованием классов PowerShell](authoringResourceClass.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](authoringResourceClass.md))</span></span>

* <span data-ttu-id="f1b32-137">Отладка ресурсов DSC (см. раздел [Отладка ресурсов DSC](debugresource.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-137">Debugging of DSC resources (see [Debugging DSC resources](debugresource.md))</span></span>
  
  <span data-ttu-id="f1b32-138">**Проблема**. Отладка не работает, если ресурс использует PsDscRunAsCredential (см. раздел [Запуск DSC с учетными данными пользователя](runAsUser.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](runAsUser.md))</span></span>

* [<span data-ttu-id="f1b32-139">Указание межузловых зависимостей</span><span class="sxs-lookup"><span data-stu-id="f1b32-139">Specifying cross-node dependencies</span></span>](crossNodeDependencies.md) 

* [<span data-ttu-id="f1b32-140">Управление версиями ресурсов</span><span class="sxs-lookup"><span data-stu-id="f1b32-140">Resource versioning</span></span>](sxsResource.md)

* <span data-ttu-id="f1b32-141">Опрашивающий клиент (конфигурации и ресурсы) (см. раздел [Настройка опрашивающего клиента с помощью имен конфигураций](pullClientConfigNames.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](pullClientConfigNames.md))</span></span>

* [<span data-ttu-id="f1b32-142">Частичные конфигурации (по запросу и принудительная отправка)</span><span class="sxs-lookup"><span data-stu-id="f1b32-142">Partial configurations (pull & push)</span></span>](partialConfigs.md)

* [<span data-ttu-id="f1b32-143">Передача отчетов на опрашивающий сервер</span><span class="sxs-lookup"><span data-stu-id="f1b32-143">Reporting to pull server</span></span>](reportServer.md) 

* <span data-ttu-id="f1b32-144">Шифрование MOF-файлов</span><span class="sxs-lookup"><span data-stu-id="f1b32-144">MOF encryption</span></span>

* <span data-ttu-id="f1b32-145">Ведение журналов событий</span><span class="sxs-lookup"><span data-stu-id="f1b32-145">Event logging</span></span>

* <span data-ttu-id="f1b32-146">Отчеты DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="f1b32-146">Azure Automation DSC reporting</span></span>

* <span data-ttu-id="f1b32-147">Полнофункциональные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f1b32-147">Resources that are fully functional</span></span>
  * [<span data-ttu-id="f1b32-148">Archive</span><span class="sxs-lookup"><span data-stu-id="f1b32-148">Archive</span></span>](archiveResource.md)
  * [<span data-ttu-id="f1b32-149">Environment</span><span class="sxs-lookup"><span data-stu-id="f1b32-149">Environment</span></span>](environmentResource.md)
  * [<span data-ttu-id="f1b32-150">File</span><span class="sxs-lookup"><span data-stu-id="f1b32-150">File</span></span>](fileResource.md)
  * [<span data-ttu-id="f1b32-151">Log</span><span class="sxs-lookup"><span data-stu-id="f1b32-151">Log</span></span>](logResource.md)
  * <span data-ttu-id="f1b32-152">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="f1b32-152">ProcessSet</span></span>
  * [<span data-ttu-id="f1b32-153">Registry</span><span class="sxs-lookup"><span data-stu-id="f1b32-153">Registry</span></span>](registryResource.md)
  * [<span data-ttu-id="f1b32-154">Script</span><span class="sxs-lookup"><span data-stu-id="f1b32-154">Script</span></span>](scriptResource.md)
  * <span data-ttu-id="f1b32-155">WindowsPackageCab</span><span class="sxs-lookup"><span data-stu-id="f1b32-155">WindowsPackageCab</span></span>
  * [<span data-ttu-id="f1b32-156">WindowsProcess</span><span class="sxs-lookup"><span data-stu-id="f1b32-156">WindowsProcess</span></span>](windowsProcessResource.md)
  * <span data-ttu-id="f1b32-157">WaitForAll (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-157">WaitForAll (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="f1b32-158">WaitForAny (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-158">WaitForAny (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="f1b32-159">WaitForSome (см. раздел [Указание межузловых зависимостей](crossNodeDependencies.md)).</span><span class="sxs-lookup"><span data-stu-id="f1b32-159">WaitForSome (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>

* <span data-ttu-id="f1b32-160">Ресурсы, функциональность которых не полная.</span><span class="sxs-lookup"><span data-stu-id="f1b32-160">Resources that are partially functional</span></span>
  * [<span data-ttu-id="f1b32-161">Группа</span><span class="sxs-lookup"><span data-stu-id="f1b32-161">Group</span></span>](groupResource.md)
  * <span data-ttu-id="f1b32-162">GroupSet</span><span class="sxs-lookup"><span data-stu-id="f1b32-162">GroupSet</span></span>
  
  <span data-ttu-id="f1b32-163">**Проблема**. Приведенные выше ресурсы не работают, если определенный экземпляр вызывается дважды (дважды запускается одна и та же конфигурация).</span><span class="sxs-lookup"><span data-stu-id="f1b32-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>
  
  * [<span data-ttu-id="f1b32-164">Служба</span><span class="sxs-lookup"><span data-stu-id="f1b32-164">Service</span></span>](serviceResource.md)
  * <span data-ttu-id="f1b32-165">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="f1b32-165">ServiceSet</span></span>
  
  <span data-ttu-id="f1b32-166">**Проблема**. Работает только для запуска или остановки службы (атрибут status).</span><span class="sxs-lookup"><span data-stu-id="f1b32-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="f1b32-167">Не работает при попытке изменить другие атрибуты службы, например startuptype, credentials, description и т. д.</span><span class="sxs-lookup"><span data-stu-id="f1b32-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="f1b32-168">Возникает ошибка такого вида.</span><span class="sxs-lookup"><span data-stu-id="f1b32-168">The error thrown is similar to:</span></span>
  
  <span data-ttu-id="f1b32-169">*Не удается найти тип [management.managementobject]: убедитесь в том, что сборка, содержащая этот тип, загружена.*</span><span class="sxs-lookup"><span data-stu-id="f1b32-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>
  
* <span data-ttu-id="f1b32-170">Нефункционирующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f1b32-170">Resources that are not functional</span></span>
  * [<span data-ttu-id="f1b32-171">User</span><span class="sxs-lookup"><span data-stu-id="f1b32-171">User</span></span>](userResource.md)
  

## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="f1b32-172">Функции DSC, недоступные на сервере Nano Server</span><span class="sxs-lookup"><span data-stu-id="f1b32-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="f1b32-173">Следующие функции DSC в настоящее время недоступны для Nano Server:</span><span class="sxs-lookup"><span data-stu-id="f1b32-173">The following DSC features are not currently available on Nano Server:</span></span>

* <span data-ttu-id="f1b32-174">Расшифровка документа MOF с помощью зашифрованных паролей.</span><span class="sxs-lookup"><span data-stu-id="f1b32-174">Decrypting MOF document with encrypted password(s)</span></span> 
* <span data-ttu-id="f1b32-175">Опрашивающий сервер — в настоящее время опрашивающий сервер нельзя настроить на сервере Nano Server.</span><span class="sxs-lookup"><span data-stu-id="f1b32-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
* <span data-ttu-id="f1b32-176">Все компоненты, не указанные в списке функций, работают.</span><span class="sxs-lookup"><span data-stu-id="f1b32-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="f1b32-177">Использование настраиваемых ресурсов DSC на сервере Nano Server</span><span class="sxs-lookup"><span data-stu-id="f1b32-177">Using custom DSC resources on Nano Server</span></span>
 
<span data-ttu-id="f1b32-178">Поскольку набор API Windows и библиотек CLR, доступный на сервере Nano Server, ограничен, ресурсы DSC, работающие в полной версии среды выполнения Windows, не всегда работают в Nano Server.</span><span class="sxs-lookup"><span data-stu-id="f1b32-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span> <span data-ttu-id="f1b32-179">Перед развертыванием каких-либо настраиваемых ресурсов DSC в рабочей среде рекомендуется выполнять их полное и всестороннее тестирование.</span><span class="sxs-lookup"><span data-stu-id="f1b32-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="f1b32-180">См. также</span><span class="sxs-lookup"><span data-stu-id="f1b32-180">See Also</span></span>
- [<span data-ttu-id="f1b32-181">Начало работы с сервером Nano Server</span><span class="sxs-lookup"><span data-stu-id="f1b32-181">Getting Started with Nano Server</span></span>](https://technet.microsoft.com/library/mt126167.aspx)

