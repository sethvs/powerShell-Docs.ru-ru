---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 676d25f945e5a2176ed1d6108f703b21581bd036
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="set-dsclocalconfigurationmanager-cmdlet-supports--force-parameter"></a><span data-ttu-id="8ae4c-102">Командлет Set-DscLocalConfigurationManager поддерживает параметр -force</span><span class="sxs-lookup"><span data-stu-id="8ae4c-102">Set-DscLocalConfigurationManager cmdlet supports -force parameter</span></span>

<span data-ttu-id="8ae4c-103">Для командлета Set-DscLocalConfigurationManager добавлена поддержка нового параметра.</span><span class="sxs-lookup"><span data-stu-id="8ae4c-103">We have added a support for new parameter to Set-DscLocalConfigurationManager cmdlet.</span></span> <span data-ttu-id="8ae4c-104">Это позволит пользователю детерминировано выполнить сброс метаконфигурации на компьютере, когда в фоновом режиме выполняются другие операции, такие как проверка согласованности, так как это приведет к их остановке.</span><span class="sxs-lookup"><span data-stu-id="8ae4c-104">This will allow the user to reset meta configuration on machine deterministically when other operations like consistency check are running in background as it will cause all running operations to be stopped.</span></span>

<span data-ttu-id="8ae4c-105">При попытке установить метаконфигурацию без параметра –Force процедура выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8ae4c-105">The experience looks like this when trying to set meta configuration without –Force parameter.</span></span>
```powershell
PS C:\\Configs&gt; Set-DscLocalConfigurationManager -Path .\\MetaTest1\\ -Verbose
VERBOSE: Performing the operation "Start-DscConfiguration: SendMetaConfigurationApply" on target "MSFT\_DSCLocalConfigurationManager".
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendMetaConfigurationApply,'className' = MSFT\_DSCLocalConfigurationManager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer DEV-10586-465 with user sid S-1-5-21-2127521184-1604012920-1887927527-5557045.
Cannot invoke the Set-DscLocalConfigurationManager cmdlet. The Consistency Check or Pull cmdlet is in progress and must return before
Set-DscLocalConfigurationManager can be invoked. Use -Force option if that is available to cancel the current operation.
+ CategoryInfo : NotSpecified: (root/Microsoft/...gurationManager:String) \[\], CimException
+ FullyQualifiedErrorId : MI RESULT 1
+ PSComputerName : localhost
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Set-DscLocalConfigurationManager finished in 0.046 seconds.
```

<span data-ttu-id="8ae4c-106">При использовании –force метаконфигурация в системе успешно обновляется путем отмены выполнения текущей операции на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8ae4c-106">When we use –force it successfully updates the meta configuration on system by canceling the current running operation on the machine.</span></span>
```powershell
PS C:\\Configs&gt; Set-DscLocalConfigurationManager -Path .\\MetaTest1\\ -Verbose -Force
VERBOSE: Performing the operation "Start-DscConfiguration: SendMetaConfigurationApply" on target "MSFT\_DSCLocalConfigurationManager".
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendMetaConfigurationApply,'className' = MSFT\_DSCLocalConfigurationManager,'n
amespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer DEV-10586-465 with user sid S-1-5-21-2127521184-1604012920-1887927527-5557045.
VERBOSE: The -Force option was specified with the Stop operation. The current configuration has been successfully cancelled.
VERBOSE: An LCM method call arrived from computer DEV-10586-465 with user sid S-1-5-21-2127521184-1604012920-1887927527-5557045.
VERBOSE: \[DEV-10586-465\]: LCM: \[ Start Set \]
VERBOSE: \[DEV-10586-465\]: LCM: \[ Start Resource \] \[MSFT\_DSCMetaConfiguration\]
VERBOSE: \[DEV-10586-465\]: LCM: \[ Start Set \] \[MSFT\_DSCMetaConfiguration\]
VERBOSE: \[DEV-10586-465\]: LCM: \[ End Set \] \[MSFT\_DSCMetaConfiguration\] in 0.0310 seconds.
VERBOSE: \[DEV-10586-465\]: LCM: \[ End Resource \] \[MSFT\_DSCMetaConfiguration\]
VERBOSE: \[DEV-10586-465\]: LCM: \[ End Set \]
VERBOSE: \[DEV-10586-465\]: LCM: \[ End Set \] in 0.1410 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Set-DscLocalConfigurationManager finished in 0.421 seconds.
```