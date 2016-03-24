# Создание конечной точки JEA и подключение к ней
Чтобы создать конечную точку JEA, необходимо создать и зарегистрировать специально настроенный файл конфигурации сеанса PowerShell. Для этого можно воспользоваться командлетом **New-PSSessionConfigurationFile**.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc" 
```

В результате получается файл конфигурации сеанса, который выглядит следующим образом: 
```powershell
@{

# Version number of the schema used for this document
SchemaVersion = '2.0.0.0'

# ID used to uniquely identify this document
GUID = 'a384fdd3-5830-4a2c-ac86-cdd1822c3afd'

# Author of this document
Author = 'Administrator'

# Description of the functionality provided by these settings
# Description = ''

# Session type defaults to apply for this session configuration. Can be 'RestrictedRemoteServer' (recommended), 'Empty', or 'Default'
SessionType = 'RestrictedRemoteServer'

# Directory to place session transcripts for this session configuration
TranscriptDirectory = 'C:\ProgramData\JEATranscripts'

# Whether to run this session configuration as the machine's (virtual) administrator account
RunAsVirtualAccount = $true

# Groups associated with machine's (virtual) administrator account
# RunAsVirtualAccountGroups = 'Remote Desktop Users', 'Remote Management Users'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# User roles (security groups), and the Role Capabilities that should be applied to them when applied to a session
RoleDefinitions = @{
    'CONTOSO\NonAdmin_Operators' = @{
        'RoleCapabilities' = 'Maintenance' } }

} 
```
При создании конечной точки JEA необходимо настроить следующие параметры команды (и соответствующие ключи в файле):
1.  Установите для SessionType значение RestrictedRemoteServer.
2.  Установите для RunAsVirtualAccount значение **$true**.
3.  Установите для TranscriptPath каталог, где после каждого сеанса будут сохраняться записи с запросом на повышение прав.
4.  Задайте для RoleDefinitions хэш-таблицу, определяющую, какие группы имеют доступ к отдельным возможностям роли.  Это поле определяет, **кто** и какие **действия** может выполнять на этой конечной точке.   Возможности роли — это специальные файлы, которые будут описаны чуть позже.


Поле RoleDefinitions определяет, какие группы имеют доступ к отдельным возможностям роли.  Возможность роли — это файл, который определяет набор возможностей, предоставляемых подключающимся пользователям.  Возможности роли можно создать с помощью команды **New-PSRoleCapabilityFile**.

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc" 
```

Она создает шаблон возможности роли, имеющий следующий вид:
```
@{

# ID used to uniquely identify this document
GUID = '9287a34f-3f0e-4fbe-9dd7-f1361ba9fd65'

# Author of this document
Author = 'Administrator'

# Description of the functionality provided by these settings
# Description = ''

# Company associated with this document
CompanyName = 'Unknown'

# Copyright statement for this document
Copyright = '(c) 2015 Administrator. All rights reserved.'

# Modules to import when applied to a session
# ModulesToImport = 'MyCustomModule', @{ ModuleName = 'MyCustomModule'; ModuleVersion = '1.0.0.0'; GUID = '4d30d5f0-cb16-4898-812d-f20a6c596bdf' }

# Aliases to make visible when applied to a session
# VisibleAliases = 'Item1', 'Item2'

# Cmdlets to make visible when applied to a session
# VisibleCmdlets = 'Invoke-Cmdlet1', @{ Name = 'Invoke-Cmdlet2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

# Functions to make visible when applied to a session
# VisibleFunctions = 'Invoke-Function1', @{ Name = 'Invoke-Function2'; Parameters = @{ Name = 'Parameter1'; ValidateSet = 'Item1', 'Item2' }, @{ Name = 'Parameter2'; ValidatePattern = 'L*' } }

# External commands (scripts and applications) to make visible when applied to a session
# VisibleExternalCommands = 'Item1', 'Item2'

# Providers to make visible when applied to a session
# VisibleProviders = 'Item1', 'Item2'

# Scripts to run when applied to a session
# ScriptsToProcess = 'C:\ConfigData\InitScript1.ps1', 'C:\ConfigData\InitScript2.ps1'

# Aliases to be defined when applied to a session
# AliasDefinitions = @{ Name = 'Alias1'; Value = 'Invoke-Alias1'}, @{ Name = 'Alias2'; Value = 'Invoke-Alias2'}

# Functions to define when applied to a session
# FunctionDefinitions = @{ Name = 'MyFunction'; ScriptBlock = { param($MyInput) $MyInput } }

# Variables to define when applied to a session
# VariableDefinitions = @{ Name = 'Variable1'; Value = { 'Dynamic' + 'InitialValue' } }, @{ Name = 'Variable2'; Value = 'StaticInitialValue' }

# Environment variables to define when applied to a session
# EnvironmentVariables = @{ Variable1 = 'Value1'; Variable2 = 'Value2' }

# Type files (.ps1xml) to load when applied to a session
# TypesToProcess = 'C:\ConfigData\MyTypes.ps1xml', 'C:\ConfigData\OtherTypes.ps1xml'

# Format files (.ps1xml) to load when applied to a session
# FormatsToProcess = 'C:\ConfigData\MyFormats.ps1xml', 'C:\ConfigData\OtherFormats.ps1xml'

# Assemblies to load when applied to a session
# AssembliesToLoad = 'System.Web', 'System.OtherAssembly, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

} 

```
Для использования в конфигурации сеанса JEA возможности роли следует сохранить как допустимый модуль PowerShell в каталоге RoleCapabilities. При необходимости модуль может иметь несколько файлов возможностей роли.

Чтобы приступить к настройке того, какие командлеты, функции, псевдонимы и сценарии доступны пользователю при подключении к сеансу JEA, добавьте в файл возможности роли свои правила, следуя закомментированному шаблону. Более подробные сведения о настройке возможностей роли см. в полном [руководстве по работе](http://aka.ms/JEA).

Наконец, завершив настройку конфигурации сеанса и соответствующих возможностей роли, зарегистрируйте эту конфигурацию сеанса и создайте конечную точку, запустив **Register-PSSessionConfiguration**.

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc" 
```

## Подключение к конечной точке JEA
Подключение к конечной точке JEA осуществляется аналогично подключению к любой конечной точке PowerShell.  Необходимо просто назначить конечной точке JEA имя в качестве параметра ConfigurationName для **New-PSSession**, **Invoke-Command** или **Enter-PSSession**.

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```
После подключения к сеансу JEA вы сможете выполнять только те команды, которые входят в число разрешенных для доступных вам возможностей роли. При попытке запустить любую другую команду возникает ошибка.<!--HONumber=Mar16_HO2-->
