---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 2d629d98b59c455011f4a5d955ef666218ae2f3f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="63b6a-102">Командлет Test-DscConfiguration поддерживает проектные конфигурации</span><span class="sxs-lookup"><span data-stu-id="63b6a-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="63b6a-103">Командлет Test-DscConfiguration был обновлен, чтобы обеспечить тестирование требуемого состояния конфигурации для одного или нескольких целевых узлов путем указания документа проектной конфигурации для сравнения.</span><span class="sxs-lookup"><span data-stu-id="63b6a-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="63b6a-104">Приведенные ниже новые наборы параметров используют конфигурации DSC по указанному пути только для тестирования и никогда не применяют их к указанным целевым узлам.</span><span class="sxs-lookup"><span data-stu-id="63b6a-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="63b6a-105">Как и в случае с Start-DscConfiguration и другими командлетами DSC, имя каждого MOF-файла позволяет определить, для какого целевого узла требуется протестировать конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="63b6a-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span> 

```PowerShell
Test-DscConfiguration   [-Path] <string> 
                        [[-ComputerName] <string[]>] 
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   [-Path] <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```

<span data-ttu-id="63b6a-106">Приведенные ниже новые наборы параметров используют отдельную конфигурацию DSC только для тестирования и никогда не применяют ее к указанным целевым узлам.</span><span class="sxs-lookup"><span data-stu-id="63b6a-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span> 

```PowerShell
Test-DscConfiguration   -ReferenceConfiguration <string> 
                        [[-ComputerName] <string[]>]
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   -ReferenceConfiguration <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```

