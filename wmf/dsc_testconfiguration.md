# Командлет Test-DscConfiguration поддерживает проектные конфигурации

Командлет Test-DscConfiguration был обновлен, чтобы обеспечить тестирование требуемого состояния конфигурации для одного или нескольких целевых узлов путем указания документа проектной конфигурации для сравнения.

Приведенные ниже новые наборы параметров используют конфигурации DSC по указанному пути только для выполнения тестирования и никогда не применяют их к указанным целевым узлам. Как и в случае с Start-DscConfiguration и другими командлетами DSC, имя каждого MOF-файла позволяет определить, для какого целевого узла требуется протестировать конфигурацию. 

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

Приведенные ниже новые наборы параметров используют отдельную конфигурацию DSC только для выполнения тестирования и никогда не применяют ее к указанным целевым узлам. 

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
```<!--HONumber=Mar16_HO2-->
