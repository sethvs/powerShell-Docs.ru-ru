---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: 2c3cc6d5d226daf22c7ee83a1b7068d6a08b7f45
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="script-tracing-and-logging"></a><span data-ttu-id="90506-102">Трассировка сценариев и ведения журналов для них</span><span class="sxs-lookup"><span data-stu-id="90506-102">Script Tracing and Logging</span></span>

<span data-ttu-id="90506-103">Хотя Windows PowerShell уже имеет параметр групповой политики **LogPipelineExecutionDetails** для регистрации вызовов командлетов, язык сценариев PowerShell имеет множество функций, для которых может потребоваться ведение журнала и/или аудит.</span><span class="sxs-lookup"><span data-stu-id="90506-103">While Windows PowerShell already has the **LogPipelineExecutionDetails** Group Policy setting to log the invocation of cmdlets, PowerShell’s scripting language has plenty of features that you might want to log and/or audit.</span></span> <span data-ttu-id="90506-104">Новая функция подробной трассировки сценариев позволяет включить подробное отслеживание и анализ для используемых в системе сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90506-104">The new Detailed Script Tracing feature lets you enable detailed tracking and analysis of Windows PowerShell scripting use on a system.</span></span> <span data-ttu-id="90506-105">После включения этой функции Windows PowerShell регистрирует все блоки сценариев в журнале событий трассировки Windows — **Microsoft-Windows-PowerShell/Operational**.</span><span class="sxs-lookup"><span data-stu-id="90506-105">After you enable detailed script tracing, Windows PowerShell logs all script blocks to the ETW event log, **Microsoft-Windows-PowerShell/Operational**.</span></span> <span data-ttu-id="90506-106">Если один блок сценария создает другой блок сценария (например, сценарий, который вызывает командлет Invoke-Expression для строки), этот итоговый блок также регистрируется.</span><span class="sxs-lookup"><span data-stu-id="90506-106">If a script block creates another script block (for example, a script that calls the Invoke-Expression cmdlet on a string), that resulting script block is logged as well.</span></span>

<span data-ttu-id="90506-107">Ведение журнала этих событий можно включить с помощью параметра групповой политики **Включить регистрацию блоков сценариев PowerShell** ("Административные шаблоны" -> "Компоненты Windows" -> "Windows PowerShell").</span><span class="sxs-lookup"><span data-stu-id="90506-107">Logging of these events can be enabled through the **Turn on PowerShell Script Block Logging** Group Policy setting (in Administrative Templates -> Windows Components -> Windows PowerShell).</span></span>

<span data-ttu-id="90506-108">Доступны следующие события.</span><span class="sxs-lookup"><span data-stu-id="90506-108">The events are:</span></span>

| <span data-ttu-id="90506-109">Канал</span><span class="sxs-lookup"><span data-stu-id="90506-109">Channel</span></span> | <span data-ttu-id="90506-110">Operational</span><span class="sxs-lookup"><span data-stu-id="90506-110">Operational</span></span>                                 |
|---------|---------------------------------------------|
| <span data-ttu-id="90506-111">Уровень</span><span class="sxs-lookup"><span data-stu-id="90506-111">Level</span></span>   | <span data-ttu-id="90506-112">Verbose</span><span class="sxs-lookup"><span data-stu-id="90506-112">Verbose</span></span>                                     |
| <span data-ttu-id="90506-113">Код операции</span><span class="sxs-lookup"><span data-stu-id="90506-113">Opcode</span></span>  | <span data-ttu-id="90506-114">Создать</span><span class="sxs-lookup"><span data-stu-id="90506-114">Create</span></span>                                      |
| <span data-ttu-id="90506-115">Задача</span><span class="sxs-lookup"><span data-stu-id="90506-115">Task</span></span>    | <span data-ttu-id="90506-116">CommandStart</span><span class="sxs-lookup"><span data-stu-id="90506-116">CommandStart</span></span>                                |
| <span data-ttu-id="90506-117">Ключевое слово</span><span class="sxs-lookup"><span data-stu-id="90506-117">Keyword</span></span> | <span data-ttu-id="90506-118">Пространство выполнения</span><span class="sxs-lookup"><span data-stu-id="90506-118">Runspace</span></span>                                    |
| <span data-ttu-id="90506-119">Код события</span><span class="sxs-lookup"><span data-stu-id="90506-119">EventId</span></span> | <span data-ttu-id="90506-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span><span class="sxs-lookup"><span data-stu-id="90506-120">Engine_ScriptBlockCompiled (0x1008 = 4104)</span></span>  |
| <span data-ttu-id="90506-121">Сообщение</span><span class="sxs-lookup"><span data-stu-id="90506-121">Message</span></span> | <span data-ttu-id="90506-122">Создание текста Scriptblock (%1 из %2):</span><span class="sxs-lookup"><span data-stu-id="90506-122">Creating Scriptblock text (%1 of %2):</span></span> </br> <span data-ttu-id="90506-123">%3</span><span class="sxs-lookup"><span data-stu-id="90506-123">%3</span></span> </br> <span data-ttu-id="90506-124">ИД ScriptBlock: %4</span><span class="sxs-lookup"><span data-stu-id="90506-124">ScriptBlock ID: %4</span></span> |


<span data-ttu-id="90506-125">Текст, внедренный в сообщение, является экстентом скомпилированного блока скрипта.</span><span class="sxs-lookup"><span data-stu-id="90506-125">The text embedded in the message is the extent of the script block compiled.</span></span> <span data-ttu-id="90506-126">Идентификатор — это GUID, который хранится в течение жизненного цикла блока скрипта.</span><span class="sxs-lookup"><span data-stu-id="90506-126">The ID is a GUID that is retained for the life of the script block.</span></span>

<span data-ttu-id="90506-127">При включении подробного ведения журналов функция записывает начальный и конечный маркеры:</span><span class="sxs-lookup"><span data-stu-id="90506-127">When you enable verbose logging, the feature writes begin and end markers:</span></span>

| <span data-ttu-id="90506-128">Канал</span><span class="sxs-lookup"><span data-stu-id="90506-128">Channel</span></span> | <span data-ttu-id="90506-129">Operational</span><span class="sxs-lookup"><span data-stu-id="90506-129">Operational</span></span>                                            |
|---------|--------------------------------------------------------|
| <span data-ttu-id="90506-130">Уровень</span><span class="sxs-lookup"><span data-stu-id="90506-130">Level</span></span>   | <span data-ttu-id="90506-131">Verbose</span><span class="sxs-lookup"><span data-stu-id="90506-131">Verbose</span></span>                                                |
| <span data-ttu-id="90506-132">Код операции</span><span class="sxs-lookup"><span data-stu-id="90506-132">Opcode</span></span>  | <span data-ttu-id="90506-133">Откройте (или закрыть)Open (/ Close)</span><span class="sxs-lookup"><span data-stu-id="90506-133">Open (/ Close)</span></span>                                         |
| <span data-ttu-id="90506-134">Задача</span><span class="sxs-lookup"><span data-stu-id="90506-134">Task</span></span>    | <span data-ttu-id="90506-135">CommandStart (/ CommandStop)</span><span class="sxs-lookup"><span data-stu-id="90506-135">CommandStart (/ CommandStop)</span></span>                           |
| <span data-ttu-id="90506-136">Ключевое слово</span><span class="sxs-lookup"><span data-stu-id="90506-136">Keyword</span></span> | <span data-ttu-id="90506-137">Пространство выполнения</span><span class="sxs-lookup"><span data-stu-id="90506-137">Runspace</span></span>                                               |
| <span data-ttu-id="90506-138">Код события</span><span class="sxs-lookup"><span data-stu-id="90506-138">EventId</span></span> | <span data-ttu-id="90506-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span><span class="sxs-lookup"><span data-stu-id="90506-139">ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) /</span></span> </br> <span data-ttu-id="90506-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span><span class="sxs-lookup"><span data-stu-id="90506-140">ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106)</span></span> |
| <span data-ttu-id="90506-141">Сообщение</span><span class="sxs-lookup"><span data-stu-id="90506-141">Message</span></span> | <span data-ttu-id="90506-142">Запущен/Завершен вызов ИД ScriptBlock: %1</span><span class="sxs-lookup"><span data-stu-id="90506-142">Started (/ Completed) invocation of ScriptBlock ID: %1</span></span> </br> <span data-ttu-id="90506-143">ИД пространства выполнения: %2</span><span class="sxs-lookup"><span data-stu-id="90506-143">Runspace ID: %2</span></span> |

<span data-ttu-id="90506-144">Идентификатор — это GUID, представляющий блок сценария (который может быть связан с идентификатором событиями 0x1008), а идентификатор пространства выполнения представляет пространство, в котором был запущен этот блок скрипта.</span><span class="sxs-lookup"><span data-stu-id="90506-144">The ID is the GUID representing the script block (that can be correlated with event ID 0x1008), and the Runspace ID represents the runspace in which this script block was run.</span></span>

<span data-ttu-id="90506-145">Знаки процента в сообщении вызова представляют структурированные свойства трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="90506-145">Percent signs in the invocation message represent structured ETW properties.</span></span> <span data-ttu-id="90506-146">Хотя они заменяются фактическими значениями в тексте сообщения, более надежным способом доступа к ним является получение сообщения с помощью командлета Get-WinEvent с последующим использованием массива **Properties** сообщения.</span><span class="sxs-lookup"><span data-stu-id="90506-146">While they are replaced with the actual values in the message text, a more robust way to access them is to retrieve the message with the Get-WinEvent cmdlet, and then use the **Properties** array of the message.</span></span>

<span data-ttu-id="90506-147">Ниже приведен пример того, как эта функциональность помогает раскрыть злонамеренную попытку шифрования и маскировки сценария:</span><span class="sxs-lookup"><span data-stu-id="90506-147">Here's an example of how this functionality can help unwrap a malicious attempt to encrypt and obfuscate a script:</span></span>

```powershell
## Malware
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
             
    ## XOR “encryption”
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)
}

$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
Invoke-Expression $decrypted
```

<span data-ttu-id="90506-148">При выполнении этого кода создаются следующие записи журнала:</span><span class="sxs-lookup"><span data-stu-id="90506-148">Running this generates the following log entries:</span></span>

```
Compiling Scriptblock text (1 of 1):
function SuperDecrypt
{
    param($script)
    $bytes = [Convert]::FromBase64String($script)
    ## XOR "encryption"
    $xorKey = 0x42
    for($counter = 0; $counter -lt $bytes.Length; $counter++)
    {
        $bytes[$counter] = $bytes[$counter] -bxor $xorKey
    }
    [System.Text.Encoding]::Unicode.GetString($bytes)

}
ScriptBlock ID: ad8ae740-1f33-42aa-8dfc-1314411877e3

Compiling Scriptblock text (1 of 1):
$decrypted = SuperDecrypt "FUIwQitCNkInQm9CCkItQjFCNkJiQmVCEkI1QixCJkJlQg=="
ScriptBlock ID: ba11c155-d34c-4004-88e3-6502ecb50f52

Compiling Scriptblock text (1 of 1):
Invoke-Expression $decrypted
ScriptBlock ID: 856c01ca-85d7-4989-b47f-e6a09ee4eeb3

Compiling Scriptblock text (1 of 1):
Write-Host 'Pwnd'
ScriptBlock ID: 5e618414-4e77-48e3-8f65-9a863f54b4c8
```

Если длина блока сценария превышает вместимость одного события в рамках трассировки событий Windows, Windows PowerShell разбивает сценарий на несколько частей. <span data-ttu-id="90506-150">Ниже приведен пример кода для воссоединения сценария из сообщений журнала:</span><span class="sxs-lookup"><span data-stu-id="90506-150">Here is sample code to recombine a script from its log messages:</span></span>

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

<span data-ttu-id="90506-151">Как и в случае со всеми системами ведения журнала с ограниченным буфером хранения (например, журналы трассировки событий Windows), одна из атак на такую инфраструктуру заключается в переполнении журнала ложными событиями для сокрытия полученных ранее свидетельств.</span><span class="sxs-lookup"><span data-stu-id="90506-151">As with all logging systems that have a limited retention buffer (i.e. ETW logs), one attack against this infrastructure is to flood the log with spurious events to hide earlier evidence.</span></span> <span data-ttu-id="90506-152">Для защиты от такой атаки убедитесь, что настроена определенная форма сбора данных из журналов событий (например, пересылка событий Windows, [выявление злоумышленника с помощью мониторинга журналов событий Windows](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)), позволяющая как можно скорее убрать журналы событий с компьютера.</span><span class="sxs-lookup"><span data-stu-id="90506-152">To protect yourself from this attack, ensure that you have some form of event log collection set up (i.e., Windows Event Forwarding, [Spotting the Adversary with Windows Event Log Monitoring](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)) to move event logs off of the computer as soon as possible.</span></span>

