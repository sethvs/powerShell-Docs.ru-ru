---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,установка
ms.openlocfilehash: 9065315ef39129e6a28234d972fe350fd5e7e11d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2018
---
# <a name="creating-and-connecting-to-a-jea-endpoint"></a><span data-ttu-id="37867-102">Создание конечной точки JEA и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="37867-102">Creating and Connecting to a JEA Endpoint</span></span>
<span data-ttu-id="37867-103">Чтобы создать конечную точку JEA, необходимо создать и зарегистрировать специально настроенный файл конфигурации сеанса PowerShell. Для этого можно воспользоваться командлетом **New-PSSessionConfigurationFile**.</span><span class="sxs-lookup"><span data-stu-id="37867-103">To create a JEA endpoint, you need to create and register a specially-configured PowerShell Session Configuration file, which can be generated with the **New-PSSessionConfigurationFile** cmdlet.</span></span>

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -TranscriptDirectory "C:\ProgramData\JEATranscripts" -RunAsVirtualAccount -RoleDefinitions @{ 'CONTOSO\NonAdmin_Operators' = @{ RoleCapabilities = 'Maintenance' }} -Path "$env:ProgramData\JEAConfiguration\Demo.pssc"
```

<span data-ttu-id="37867-104">В результате получается файл конфигурации сеанса, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="37867-104">This will create a session configuration file that looks like this:</span></span>
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
<span data-ttu-id="37867-105">При создании конечной точки JEA необходимо настроить следующие параметры команды (и соответствующие ключи в файле):</span><span class="sxs-lookup"><span data-stu-id="37867-105">When creating a JEA endpoint, the following parameters of the command (and corresponding keys in the file) must be set:</span></span>
1.  <span data-ttu-id="37867-106">Установите для SessionType значение RestrictedRemoteServer.</span><span class="sxs-lookup"><span data-stu-id="37867-106">SessionType to RestrictedRemoteServer</span></span>
2.  <span data-ttu-id="37867-107">Установите для RunAsVirtualAccount значение **$true**.</span><span class="sxs-lookup"><span data-stu-id="37867-107">RunAsVirtualAccount to **$true**</span></span>
3.  <span data-ttu-id="37867-108">Установите для TranscriptPath каталог, где после каждого сеанса будут сохраняться записи с запросом на повышение прав.</span><span class="sxs-lookup"><span data-stu-id="37867-108">TranscriptPath to the directory where “over the shoulder” transcripts will be saved after each session</span></span>
4.  <span data-ttu-id="37867-109">Задайте для RoleDefinitions хэш-таблицу, определяющую, какие группы имеют доступ к отдельным возможностям роли.</span><span class="sxs-lookup"><span data-stu-id="37867-109">RoleDefinitions to a hashtable that defines which groups have access to which “Role Capabilities.”</span></span>  <span data-ttu-id="37867-110">Это поле определяет, **кто** и какие **действия** может выполнять на этой конечной точке.</span><span class="sxs-lookup"><span data-stu-id="37867-110">This field defines **who** can do **what** on this endpoint.</span></span>   <span data-ttu-id="37867-111">Возможности роли — это специальные файлы, которые будут описаны чуть позже.</span><span class="sxs-lookup"><span data-stu-id="37867-111">Role Capabilities are special files that will be explained shortly.</span></span>


<span data-ttu-id="37867-112">Поле RoleDefinitions определяет, какие группы имеют доступ к отдельным возможностям роли.</span><span class="sxs-lookup"><span data-stu-id="37867-112">The RoleDefinitions field defines which groups had access to which Role Capabilities.</span></span>  <span data-ttu-id="37867-113">Возможность роли — это файл, который определяет набор возможностей, предоставляемых подключающимся пользователям.</span><span class="sxs-lookup"><span data-stu-id="37867-113">A Role Capability is a file that defines a set of capabilities that will be exposed to connecting users.</span></span>  <span data-ttu-id="37867-114">Возможности роли можно создать с помощью команды **New-PSRoleCapabilityFile**.</span><span class="sxs-lookup"><span data-stu-id="37867-114">You can create Role Capabilities with the **New-PSRoleCapabilityFile** command.</span></span>

```powershell
New-PSRoleCapabilityFile -Path "$env:ProgramFiles\WindowsPowerShell\Modules\DemoModule\RoleCapabilities\Maintenance.psrc"
```

<span data-ttu-id="37867-115">Она создает шаблон возможности роли, имеющий следующий вид:</span><span class="sxs-lookup"><span data-stu-id="37867-115">This will generate a template role capability that looks like this:</span></span>
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
<span data-ttu-id="37867-116">Для использования в конфигурации сеанса JEA возможности роли следует сохранить как допустимый модуль PowerShell в каталоге RoleCapabilities.</span><span class="sxs-lookup"><span data-stu-id="37867-116">To be used by a JEA session configuration, Role Capabilities must be saved as a valid PowerShell module in a directory named “RoleCapabilities”.</span></span> <span data-ttu-id="37867-117">При необходимости модуль может иметь несколько файлов возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="37867-117">A module may have multiple role capability files, if desired.</span></span>

<span data-ttu-id="37867-118">Чтобы приступить к настройке того, какие командлеты, функции, псевдонимы и сценарии доступны пользователю при подключении к сеансу JEA, добавьте в файл возможности роли свои правила, следуя закомментированному шаблону.</span><span class="sxs-lookup"><span data-stu-id="37867-118">To start configuring which cmdlets, functions, aliases, and scripts a user may access when connecting to a JEA session, add your own rules to the Role Capability file following the commented out templates.</span></span> <span data-ttu-id="37867-119">Более подробные сведения о настройке возможностей роли см. в полном [руководстве по работе](http://aka.ms/JEA).</span><span class="sxs-lookup"><span data-stu-id="37867-119">For a deeper look into how you can configure Role Capabilities, check out the full [experience guide](http://aka.ms/JEA).</span></span>

<span data-ttu-id="37867-120">Наконец, завершив настройку конфигурации сеанса и соответствующих возможностей роли, зарегистрируйте эту конфигурацию сеанса и создайте конечную точку, запустив **Register-PSSessionConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="37867-120">Finally, once you have finished customizing your session configuration and related Role Capabilities, register this session configuration and create the endpoint by running **Register-PSSessionConfiguration**.</span></span>

```powershell
Register-PSSessionConfiguration -Name Maintenance -Path "C:\ProgramData\JEAConfiguration\Demo.pssc"
```

## <a name="connect-to-a-jea-endpoint"></a><span data-ttu-id="37867-121">Подключение к конечной точке JEA</span><span class="sxs-lookup"><span data-stu-id="37867-121">Connect to a JEA Endpoint</span></span>
<span data-ttu-id="37867-122">Подключение к конечной точке JEA осуществляется аналогично подключению к любой конечной точке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37867-122">Connecting to a JEA Endpoint works the same way connecting to any other PowerShell endpoint works.</span></span>  <span data-ttu-id="37867-123">Необходимо просто назначить конечной точке JEA имя в качестве параметра ConfigurationName для **New-PSSession**, **Invoke-Command** или **Enter-PSSession**.</span><span class="sxs-lookup"><span data-stu-id="37867-123">You simply have to give your JEA endpoint name as the “ConfigurationName” parameter for **New-PSSession**, **Invoke-Command**, or **Enter-PSSession**.</span></span>

```powershell
Enter-PSSession -ConfigurationName Maintenance -ComputerName localhost
```
<span data-ttu-id="37867-124">После подключения к сеансу JEA вы сможете выполнять только те команды, которые входят в число разрешенных для доступных вам возможностей роли.</span><span class="sxs-lookup"><span data-stu-id="37867-124">Once you have connected to the JEA session, you will be limited to running the commands whitelisted in the Role Capabilities that you have access to.</span></span> <span data-ttu-id="37867-125">При попытке запустить любую другую команду возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="37867-125">If you try to run any command not allowed for your role, you will encounter an error.</span></span>