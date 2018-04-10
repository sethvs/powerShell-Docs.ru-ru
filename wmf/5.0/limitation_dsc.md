---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 66ceea383b78b2654caa4f1de16a30beea0e7fd3
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a>Известные проблемы и ограничения настройки требуемого состояния (DSC)

<a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a>Критическое изменение: сертификаты, используемые для шифрования и расшифровки паролей в конфигурациях DSC, могут не работать после установки WMF 5.0 RTM
--------------------------------------------------------------------------------------------------------------------------------

В выпусках WMF 4.0 и WMF 5.0 Preview DSC не позволял использовать в конфигурациях пароли длиннее 121 символов. DSC требовал использования коротких паролей даже в тех случаях, когда были нужны длинные и надежные пароли. Это критическое изменение позволяет использовать в конфигурации DSC пароли произвольной длины.

**Разрешение.** Повторно создайте сертификат с использованием шифрования ключа или данных и расширенного ключа шифрования документов (1.3.6.1.4.1.311.80.1). Дополнительные сведения см. в статье TechNet <https://technet.microsoft.com/library/dn807171.aspx>.


<a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a>После установки WMF 5.0 RTM может произойти сбой командлетов DSC
------------------------------------------------------------------------------------
Start-DscConfiguration и другие командлеты DSC могут завершаться со сбоем после установки WMF 5.0 RTM, выдавая следующую ошибку:
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

**Решение.** Удалите DSCEngineCache.mof, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):

```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


<a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a>Командлеты DSC могут не работать в случае установки WMF 5.0 RTM поверх WMF 5.0 Production Preview
------------------------------------------------------
**Решение.** Выполните следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


<a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a>LCM может перейти в нестабильное состояние при использовании Get-DscConfiguration в DebugMode
-------------------------------------------------------------------------------

Когда LCM находится в режиме DebugMode, нажатие клавиш CTRL+C для остановки обработки Get-DscConfiguration может привести к переключению LCM в нестабильное состояние, в котором не работает большинство командлетов DSC.

**Решение.** Не нажимайте клавиши CTRL+C во время отладки командлет Get-DscConfiguration.


<a name="stop-dscconfiguration-may-hang-in-debugmode"></a>STOP-DscConfiguration может зависнуть в DebugMode
------------------------------------------------------------------------------------------------------------------------
Когда LCM находится в DebugMode, может зависнуть Stop-DscConfiguration при попытке остановить операцию, запущенную Get-DscConfiguration.

**Решение.** Завершите отладку операции, запущенной Get-DscConfiguration, как описано в разделе [Отладка ресурсов DSC](https://msdn.microsoft.com/powershell/dsc/debugresource).


<a name="no-verbose-error-messages-are-shown-in-debugmode"></a>В DebugMode не отображаются подробные сообщения об ошибках
-----------------------------------------------------------------------------------
Когда LCM находится в DebugMode, не отображаются подробные сообщения об ошибках из ресурсов DSC.

**Решение.** Отключите *DebugMode* для просмотра подробных сообщений из ресурсов.


<a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a>Командлету Get-DscConfigurationStatus не удается получить операции Invoke-DscResource
--------------------------------------------------------------------------------------
После использования командлета Invoke-DscResource для прямого вызова методов любого ресурса позднее записи такой операции не удается извлечь с помощью Get-DscConfigurationStatus.

**Решение.** Отсутствует.


<a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a>Get-DscConfigurationStatus возвращает операции цикла извлечения с типом *Consistency*
---------------------------------------------------------------------------------
Когда узел переведен в режим обновления PULL, для каждой выполненной операции извлечения командлет Get-DscConfigurationStatus сообщает тип операции, как *Consistency*, а не *Initial*.

**Решение.** Отсутствует.

<a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a>Командлет Invoke-DscResource не возвращает сообщения в том порядке, в котором они были созданы
---------------------------------------------------------------------------------
Командлет Invoke-DscResource не возвращает подробные сообщения, предупреждения и сообщения об ошибках в том порядке, в котором они были созданы LCM или ресурсом DSC.

**Решение.** Отсутствует.


<a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a>Невозможна простая отладка ресурсов DSC при использовании Invoke-DscResource
-----------------------------------------------------------------------
Когда LCM работает в режиме отладки (дополнительные сведения см. в разделе [Отладка ресурсов DSC](https://msdn.microsoft.com/powershell/dsc/debugresource)), командлет Invoke-DscResource не предоставляет сведения о пространстве выполнения, к которому требуется подключиться для отладки.
**Решение.** Найдите пространство выполнения и подключитесь к нему с помощью командлетов **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-Runspace** и **Debug-Runspace** для отладки ресурса DSC.

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```


<a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a>Различные документы неполной конфигурации для одного узла не могут иметь одинаковые имена ресурсов
------------------------------------------------------------------------------------------

Идентичные имена ресурсов для нескольких неполных конфигураций, развернутых на одном узле, приводят к ошибке во время выполнения.

**Решение.** Используйте разные имена для одинаковых ресурсов в различных неполных конфигурациях.


<a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a>Start-DscConfiguration –UseExisting не работает с параметром -Credential
------------------------------------------------------------------

При использовании Start-DscConfiguration с параметром –UseExisting параметр –Credential игнорируется. DSC использует удостоверение процесса по умолчанию для продолжения операции. Это вызывает ошибку, если для продолжения работы на удаленном узле требуются другие учетные данные.

**Решение.** Используйте сеанс CIM для удаленных операций DSC:
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


<a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a>IPv6-адреса в качестве имен узлов в конфигурациях DSC
--------------------------------------------------
В этом выпуске не поддерживается использование IPv6-адресов в качестве имен узлов в сценариях конфигурации DSC.

**Решение.** Отсутствует.


<a name="debugging-of-class-based-dsc-resources"></a>Отладка ресурсов DSC, основанных на классах
--------------------------------------
В этом выпуске отладка ресурсов DSC на основе классов не поддерживается.

**Решение.** Отсутствует.


<a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a>Переменные и функции, определенные в области $script основанного на классе ресурса DSC, не сохраняются между несколькими вызовами ресурса DSC
-------------------------------------------------------------------------------------------------------------------------------------

Несколько последовательных вызовов Start-DSCConfiguration завершаются ошибкой, если конфигурация использует любой ресурс на основе класса, у которого переменные или функции определены в области $script.

**Решение.** Определите все переменные и функции в самом классе ресурса DSC. Переменных и функций области $script быть не должно.


<a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a>Отладка ресурсов DSC, когда ресурс использует PSDscRunAsCredential
----------------------------------------------------------------------
В этом выпуске отладка ресурсов DSC, когда ресурс использует свойство *PSDscRunAsCredential* в конфигурации, не поддерживается .

**Решение.** Отсутствует.


<a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a>PsDscRunAsCredential не поддерживается для составных ресурсов DSC
----------------------------------------------------------------

**Решение.** Используйте свойство Credential, если оно доступно. Например, ServiceSet и WindowsFeatureSet.


<a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a>*Get-DscResource -Syntax* неправильно отражает PsDscRunAsCredential
-------------------------------------------------------------------------
Get-DscResource -Synta отражает PsDscRunAsCredential неправильно, когда ресурс помечает его как обязательный или не поддерживает его.

**Решение.** Отсутствует. Однако создание конфигурации в интегрированной среде сценариев отражает правильные метаданные о свойстве PsDscRunAsCredential при использовании технологии IntelliSense.


<a name="windowsoptionalfeature-is-not-available-in-windows-7"></a>WindowsOptionalFeature недоступен в Windows 7
-----------------------------------------------------

Ресурс DSC WindowsOptionalFeature недоступен в Windows 7. Он требует наличия модуля и командлетов DISM, которые доступны только в Windows 8 и более поздних выпусках.

<a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a>Для ресурсов DSC на основе классов командлет Import-DscResource -ModuleVersion может не работать, как ожидалось
------------------------------------------------------------------------------------------
Если у узла компиляции нескольких версий модуля ресурса DSC на основе класса, `Import-DscResource -ModuleVersion` не может получить указанную версию и вызывает следующую ошибку компиляции.

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

**Решение**. Импортируйте требуемую версию, определив объект *ModuleSpecification* для `-ModuleName` с ключом `RequiredVersion`, указанным следующим образом:
``` PowerShell
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}
```

<a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a>Для обработки запросов некоторым ресурсам DSC, например ресурсу реестра, может требоваться много времени.
--------------------------------------------------------------------------------------------------------------------------------

**Решение 1.** Создайте запланированную задачу, которая периодически очищает папку.
``` PowerShell
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis
```

**Решение 2.** Измените конфигурацию DSC так, чтобы очистка папки *CommandAnalysis* выполнялась в конце конфигурации.
``` PowerShell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```