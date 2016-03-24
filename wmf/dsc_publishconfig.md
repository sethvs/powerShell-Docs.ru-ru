# Доставка документа конфигурации без применения

Командлет **Publish-DscConfiguration** копирует MOF-файл на целевой узел без применения конфигурации. Она применяется во время следующей проверки согласованности или при запуске командлета `Update-DscConfiguration`.

```powershell
Publish-DscConfiguration [-Path] <string> [[-ComputerName] <string[]>] [-Force] [-Credential <pscredential>] [-ThrottleLimit <int>] [-WhatIf] [-Confirm] [<CommonParameters>]

Publish-DscConfiguration [-Path] <string> -CimSession <CimSession[]> [-Force] [-ThrottleLimit <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<!--HONumber=Mar16_HO2-->
