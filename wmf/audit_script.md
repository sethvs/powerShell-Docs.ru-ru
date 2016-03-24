# Трассировка сценариев и ведения журналов для них

Хотя Windows PowerShell уже имеет параметр групповой политики **LogPipelineExecutionDetails** для регистрации вызовов командлетов, язык сценариев PowerShell имеет множество функций, для которых может потребоваться ведение журнала и/или аудит. Новая функция подробной трассировки сценариев позволяет включить подробное отслеживание и анализ для используемых в системе сценариев Windows PowerShell. После включения этой функции Windows PowerShell регистрирует все блоки сценариев в журнале событий трассировки Windows — **Microsoft-Windows-PowerShell/Operational**. Если один блок сценария создает другой блок сценария (например, сценарий, который вызывает командлет Invoke-Expression для строки), этот итоговый блок также регистрируется.

Ведение журнала этих событий можно включить с помощью параметра групповой политики **Включить регистрацию блоков сценариев PowerShell** ("Административные шаблоны" -> "Компоненты Windows" -> "Windows PowerShell").

Доступны следующие события.

| Канал | Operational                                 |
|---------|---------------------------------------------|
| Уровень   | Verbose                                     |
| Код операции  | Создать                                      |
| Задача    | CommandStart                                |
| Ключевое слово | Пространство выполнения                                    |
| Код события | Engine_ScriptBlockCompiled (0x1008 = 4104)  |
| Сообщение | Создание текста Scriptblock (%1 из %2): </br> %3 </br> ИД ScriptBlock: %4 |


Текст, внедренный в сообщение, является экстентом скомпилированного блока скрипта. Идентификатор — это GUID, который хранится в течение жизненного цикла блока скрипта.

При включении подробного ведения журналов функция записывает начальный и конечный маркеры:

| Канал | Operational                                            |
|---------|--------------------------------------------------------|
| Уровень   | Verbose                                                |
| Код операции  | Откройте (или закрыть)Open (/ Close)                                         |
| Задача    | CommandStart (/ CommandStop)                           |
| Ключевое слово | Пространство выполнения                                               |
| Код события | ScriptBlock\_Invoke\_Start\_Detail (0x1009 = 4105) / </br> ScriptBlock\_Invoke\_Complete\_Detail (0x100A = 4106) |
| Сообщение | Запущен/Завершен вызов ИД ScriptBlock: %1 </br> ИД пространства выполнения: %2 |

Идентификатор — это GUID, представляющий блок сценария (который может быть связан с идентификатором событиями 0x1008), а идентификатор пространства выполнения представляет пространство, в котором был запущен этот блок скрипта.

Знаки процента в сообщении вызова представляют структурированные свойства трассировки событий Windows. Хотя они заменяются фактическими значениями в тексте сообщения, более надежным способом доступа к ним является получение сообщения с помощью командлета Get-WinEvent с последующим использованием массива **Properties** сообщения.

Ниже приведен пример того, как эта функциональность помогает раскрыть злонамеренную попытку шифрования и маскировки сценария:

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

При выполнении этого кода создаются следующие записи журнала:

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

Если длина блока сценария превышает вместимость одного события в рамках трассировки событий Windows, Windows PowerShell разбивает сценарий на несколько частей. Ниже приведен пример кода для воссоединения сценария из сообщений журнала:

```powershell
$created = Get-WinEvent -FilterHashtable @{ ProviderName="Microsoft-Windows-PowerShell"; Id = 4104 } | Where-Object { $_.<...> }
$sortedScripts = $created | sort { $_.Properties[0].Value }
$mergedScript = -join ($sortedScripts | % { $_.Properties[2].Value })
```

Как и в случае со всеми системами ведения журнала с ограниченным буфером хранения (например, журналы трассировки событий Windows), одна из атак на такую инфраструктуру заключается в переполнении журнала ложными событиями для сокрытия полученных ранее свидетельств. Для защиты от такой атаки убедитесь, что настроена определенная форма сбора данных из журналов событий (например, пересылка событий Windows, [выявление злоумышленника с помощью мониторинга журналов событий Windows](http://www.nsa.gov/ia/_files/app/Spotting_the_Adversary_with_Windows_Event_Log_Monitoring.pdf)), позволяющая как можно скорее убрать журналы событий с компьютера.
<!--HONumber=Mar16_HO2-->
