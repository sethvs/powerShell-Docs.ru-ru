---
title:  Управление процессами с помощью командлетов Process
ms.date:  2016-05-11
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
ms.assetid:  5038f612-d149-4698-8bbb-999986959e31
---

# Управление процессами с помощью командлетов Process
Командлеты Process в Windows PowerShell позволяют управлять локальными и удаленными процессами в Windows PowerShell.

## Получение процессов (Get-Process)
Для получения процессов, запущенных на локальном компьютере, выполните **Get-Process** без параметров.

Отдельные процессы можно получить, указав их имена или идентификаторы. Следующая команда возвращает процесс Idle:

```
PS> Get-Process -id 0
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
      0       0        0         16     0               0 Idle
```

То, что в некоторых ситуациях командлеты не возвращают данные, является нормальным. Однако если при указании процесса по его идентификатору **Get-Process** не находит совпадений, он выдает ошибку, так как стандартной целью является получение известного выполняющегося процесса. Если процесс с указанным идентификатором отсутствует, весьма вероятно, что идентификатор неправильный или нужный процесс уже завершился:

```
PS> Get-Process -Id 99
Get-Process : No process with process ID 99 was found.
At line:1 char:12
+ Get-Process  <<<< -Id 99
```

Параметр Name командлета Get-Process можно использовать для указания подмножества процессов на основе имени процесса. Параметр Name может принимать несколько имен в виде списка с разделителями-запятыми и поддерживает использование подстановочных знаков, что позволяет задавать шаблоны имен.

Например, следующая команда возвращает процессы, имена которых начинаются с "ex.".

```
PS> Get-Process -Name ex*
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    234       7     5572      12484   134     2.98   1684 EXCEL
    555      15    34500      12384   134   105.25    728 explorer
```

Поскольку класс System.Diagnostics.Process .NET является основой для процессов Windows PowerShell, он удовлетворяет некоторым соглашениям, используемым System.Diagnostics.Process. Одно из таких соглашений требует, чтобы имя процесса для исполняемого файла никогда не содержало ".exe" в конце имени этого файла.

**Get-Process** также принимает несколько значений для параметра Name.

```
PS> Get-Process -Name exp*,power* 
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    540      15    35172      48148   141    88.44    408 explorer
    605       9    30668      29800   155     7.11   3052 powershell
```

Параметр ComputerName командлета Get-Process можно использовать для получения процессов на удаленных компьютерах. Например, следующая команда получает процессы PowerShell на локальном (представленным "localhost") и двух удаленных компьютерах.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server02
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    258       8    29772      38636   130            3700 powershell
    398      24    75988      76800   572            5816 powershell
    605       9    30668      29800   155     7.11   3052 powershell
```

Имена компьютеров в этих данных не указаны, однако они хранятся в свойстве MachineName объектов процесса, возвращаемых Get-Process. Следующая команда использует командлет Format-Table для отображения свойств ID, ProcessName и MachineName (ComputerName) объектов процесса.

```
PS> Get-Process -Name PowerShell -ComputerName localhost, Server01, Server01 | Format-Table -Property ID, ProcessName, MachineName
  Id ProcessName MachineName
  -- ----------- -----------
3700 powershell  Server01
3052 powershell  Server02
5816 powershell  localhost
```

Эта более сложная команда добавляет в стандартные отображаемые данные Get-Process свойство MachineName. Обратный апостроф (`) (ASCII 96) является символом продолжения Windows PowerShell.

```
get-process powershell -computername localhost, Server01, Server02 | format-table -property Handles, `
                    @{Label="NPM(K)";Expression={[int]($_.NPM/1024)}}, `
                    @{Label="PM(K)";Expression={[int]($_.PM/1024)}}, `
                    @{Label="WS(K)";Expression={[int]($_.WS/1024)}}, `
                    @{Label="VM(M)";Expression={[int]($_.VM/1MB)}}, `
                    @{Label="CPU(s)";Expression={if ($_.CPU -ne $()` 
                    {$_.CPU.ToString("N")}}}, `                                                                         
                    Id, ProcessName, MachineName -auto

Handles  NPM(K)  PM(K) WS(K) VM(M) CPU(s)  Id ProcessName  MachineName
-------  ------  ----- ----- ----- ------  -- -----------  -----------
    258       8  29772 38636   130         3700 powershell Server01
    398      24  75988 76800   572         5816 powershell localhost
    605       9  30668 29800   155 7.11    3052 powershell Server02
```

## Остановка процессов (Stop-Process)
Windows PowerShell позволяет гибко выводить списки процессов, но как обстоят дела с остановкой процесса?

Командлет **Stop-Process** принимает имя или идентификатор, указывающие останавливаемый процесс. Возможность остановки процессов зависит от ваших разрешений. Некоторые процессы остановить нельзя. Например, при попытке остановить неактивный процесс возникает ошибка:

```
PS> Stop-Process -Name Idle
Stop-Process : Process 'Idle (0)' cannot be stopped due to the following error:
 Access is denied
At line:1 char:13
+ Stop-Process  <<<< -Name Idle
```

Можно также принудительно вывести запрос с помощью параметра **Confirm**. Он особенно удобен при использовании подстановочного знака в имени процесса, так как случайно может быть определено соответствие с некоторыми процессами, которые не нужно останавливать:

```
PS> Stop-Process -Name t*,e* -Confirm
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "explorer (408)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
Confirm
Are you sure you want to perform this action?
Performing operation "Stop-Process" on Target "taskmgr (4072)".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):n
```

Сложную обработку процессов можно реализовать с помощью командлетов фильтрации объектов. Так как объект Process имеет свойство Responding, которое равно true, если он перестал отвечать, вы можете остановить все неотвечающие приложения с помощью следующей команды:

```
Get-Process | Where-Object -FilterScript {$_.Responding -eq $false} | Stop-Process
```

Аналогичный подход возможен и в других ситуациях. Предположим, например, что приложение дополнительной области уведомлений запускается автоматически при открытии другого приложения. Эта процедура может работать неправильно в сеансах служб терминалов, однако вам все равно нужно сохранить ее в сеансах, выполняемых в консоли физического компьютера. Сеансы, подключенные к рабочему столу физического компьютера, всегда имеют идентификатор сеанса 0, поэтому можно остановить все экземпляры процесса, находящиеся в других сеансах, с помощью **Where-Object** , **SessionId** процесса:

```
Get-Process -Name BadApp | Where-Object -FilterScript {$_.SessionId -neq 0} | Stop-Process
```

Командлет Stop-Process не использует параметр ComputerName. Поэтому для выполнения команды остановки процесса на удаленном компьютере необходимо использовать командлет Invoke-Command. Например, чтобы остановить процесс PowerShell на удаленном компьютере Server01, введите:

```
Invoke-Command -ComputerName Server01 {Stop-Process Powershell}
```

## Остановка всех остальных сеансов Windows PowerShell
В некоторых случаях может пригодиться возможность остановки всех выполняющихся сеансов Windows PowerShell, отличных от текущего. Если сеанс использует слишком много ресурсов или недоступен (он может выполняться удаленно или в другом сеансе), возможно, остановить его напрямую не получится. При попытке остановить все выполняющиеся сеансы может быть завершен текущий сеанс.

Каждый сеанс Windows PowerShell имеет переменную среды PID, содержащую идентификатор процесса Windows PowerShell. Можно проверить переменную $PID на наличие идентификатора каждого сеанса и завершить только сеансы Windows PowerShell с другим идентификатором. Следующая команда конвейера делает именно это и возвращает список завершенных сеансов (из-за использования параметра **PassThru**):

```
PS> Get-Process -Name powershell | Where-Object -FilterScript {$_.Id -ne $PID} | Stop-Process -
PassThru
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    334       9    23348      29136   143     1.03    388 powershell
    304       9    23152      29040   143     1.03    632 powershell
    302       9    20916      26804   143     1.03   1116 powershell
    335       9    25656      31412   143     1.09   3452 powershell
    303       9    23156      29044   143     1.05   3608 powershell
    287       9    21044      26928   143     1.02   3672 powershell
```

## Запуск, отладка и ожидание процессов
Windows PowerShell также имеет командлеты для запуска (или перезапуска), отладки процесса и ожидания завершения процесса перед выполнением команды. Дополнительные сведения об этих командлетах см. в разделах справки по каждому из них.

## См. также
[Get-Process [m2]](https://technet.microsoft.com/en-us/library/27a05dbd-4b69-48a3-8d55-b295f6225f15)
[Stop-Process [m2]](https://technet.microsoft.com/en-us/library/12454238-9881-457a-bde4-fb6cd124deec)
[Start-Process](https://technet.microsoft.com/en-us/library/41a7e43c-9bb3-4dc2-8b0c-f6c32962e72c)
[Wait-Process](https://technet.microsoft.com/en-us/library/9222af7a-789d-4a09-aa90-09d7c256c799)
[Debug-Process](https://technet.microsoft.com/en-us/library/eea1dace-3913-4dbd-b659-5a94a610eee1)
[Invoke-Command](https://technet.microsoft.com/en-us/library/22fd98ba-1874-492e-95a5-c069467b8462)



<!--HONumber=May16_HO2-->


