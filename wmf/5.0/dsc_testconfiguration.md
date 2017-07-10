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
<a id="test-dscconfiguration-cmdlet-supports-reference-configurations" class="xliff"></a>
# Командлет Test-DscConfiguration поддерживает проектные конфигурации

Командлет Test-DscConfiguration был обновлен, чтобы обеспечить тестирование требуемого состояния конфигурации для одного или нескольких целевых узлов путем указания документа проектной конфигурации для сравнения.

Приведенные ниже новые наборы параметров используют конфигурации DSC по указанному пути только для тестирования и никогда не применяют их к указанным целевым узлам. Как и в случае с Start-DscConfiguration и другими командлетами DSC, имя каждого MOF-файла позволяет определить, для какого целевого узла требуется протестировать конфигурацию. 

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

Приведенные ниже новые наборы параметров используют отдельную конфигурацию DSC только для тестирования и никогда не применяют ее к указанным целевым узлам. 

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

