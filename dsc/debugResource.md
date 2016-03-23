# Отладка ресурсов DSC

> Область применения: Windows PowerShell 5.0

В PowerShell 5.0 в DSC появилась новая функция, позволяющая выполнять отладку ресурса DSC при применении конфигурации.

## Включение отладки DSC
Перед отладкой ресурса необходимо включить отладку с помощью командлета [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx). Он принимает обязательный параметр **BreakAll**. Убедитесь, что отладка включена, вызвав командлет [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) и проверив результат. Следующие выходные данные PowerShell демонстрируют результат включения отладки:


```powershell
PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
NONE

PS C:\DebugTest> Enable-DscDebug -BreakAll

PS C:\DebugTest> $LCM = Get-DscLocalConfigurationManager

PS C:\DebugTest> $LCM.DebugMode
ForceModuleImport
ResourceScriptBreakAll

PS C:\DebugTest>
```


## Запуск конфигурации с включенной функцией отладки
Для отладки ресурса DSC необходимо запустить конфигурацию, вызывающую этот ресурс. В этом примере мы рассмотрим простую конфигурацию, которая вызывает ресурс [WindowsFeature](windowsfeatureResource.md), чтобы проверить, установлен ли компонент WindowsPowerShellWebAccess:

```powershell
Configuration PSWebAccess
    {
    Import-DscResource -ModuleName 'PsDesiredStateConfiguration'
    Node localhost
        {
        WindowsFeature PSWA
            {
            Name = 'WindowsPowerShellWebAccess'
            Ensure = 'Present'
            }
        }
    }
PSWebAccess
```
Скомпилировав конфигурацию, запустите ее, вызвав командлет [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx). Конфигурация остановится, когда
локальный диспетчер конфигураций (LCM) вызовет первый ресурс в конфигурации. Если используются параметры `-Verbose` и `-Wait`, выходные данные будут содержать строки, которые нужно ввести
для запуска отладки.

```powershell
PS C:\DebugTest> Start-DscConfiguration .\PSWebAccess -Wait -Verbose
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' = SendConfigurationApply,'className' = MSFT_DSCLocalConfiguration
Manager,'namespaceName' = root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: An LCM method call arrived from computer TEST-SRV with user sid S-1-5-21-2127521184-1604012920-1887927527-108583.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Set      ]
WARNING: [TEST-SRV]:                            [DSCEngine] Warning LCM is in Debug 'ResourceScriptBreakAll' mode.  Resource script processing will 
be stopped to wait for PowerShell script debugger to attach.
VERBOSE: [TEST-SRV]:                            [DSCEngine] Importing the module C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateCo
nfiguration\DscResources\MSFT_RoleResource\MSFT_RoleResource.psm1 in force mode.
VERBOSE: [TEST-SRV]: LCM:  [ Start  Resource ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]: LCM:  [ Start  Test     ]  [[WindowsFeature]PSWA]
VERBOSE: [TEST-SRV]:                            [[WindowsFeature]PSWA] Importing the module MSFT_RoleResource in force mode.
WARNING: [TEST-SRV]:                            [[WindowsFeature]PSWA] Resource is waiting for PowerShell script debugger to attach.  Use the follow
ing commands to begin debugging this resource script:
Enter-PSSession -ComputerName TEST-SRV -Credential <credentials>
Enter-PSHostProcess -Id 9000 -AppDomainName DscPsPluginWkr_AppDomain
Debug-Runspace -Id 9
```
К этому моменту LCM вызвал ресурс и достиг первой контрольной точки. Последние три строки выходных данных показывают, как присоединиться к процессу и запустить отладку сценария ресурса.

## Отладка сценария ресурса

Запустите новый экземпляр интегрированной среды сценариев PowerShell. В консоли введите последние три строки выходных данных `Start-DscConifiguration` в виде команд, заменив `<credentials>` на
действительные учетные данные пользователя. Вы получите следующие выходные данные.



<!--HONumber=Feb16_HO4-->
