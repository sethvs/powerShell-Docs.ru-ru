---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: aaf1809277f072c82e5a1a862ea64b75586e32d1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
<a id="improvements-in-powershell-script-debugging" class="xliff"></a>
# Усовершенствования отладки сценариев PowerShell

В PowerShell 5.0 было внесено несколько усовершенствований, направленных на улучшение процедуры отладки.

<a id="break-all" class="xliff"></a>
## Команда "Прервать все"

Консоль PowerShell и интегрированная среда сценариев Windows PowerShell теперь позволяют переходить в режим отладчика при выполнении сценариев. Это работает как в локальных, так и в удаленных сеансах.

В окне консоли нажмите клавиши **CTRL+BREAK**.

В интегрированной среде сценариев нажмите клавиши **CTRL+B** или воспользуйтесь командой меню **Отладка -> Прервать все**.

<a id="remote-debugging-and-remote-file-editing-in-windows-powershell-ise" class="xliff"></a>
## Удаленная отладка и удаленное редактирование файлов в интегрированной среде сценариев Windows PowerShell

Теперь среда Windows PowerShell позволяет открывать и редактировать файлы в удаленном сеансе, выполнив команду PSEdit.
Например, во время удаленного сеанса можно открыть файл для редактирования из командной строки, как показано ниже:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Кроме того, можно вносить изменения и сохранять их в удаленном файле, который автоматически открывается в среде Windows PowerShell при попадании в точку останова.
Теперь можно выполнить отладку файла сценария, выполняемого на удаленном компьютере, отредактировать файл, чтобы исправить ошибку, а затем снова запустить обновленный сценарий.

<a id="advanced-script-debugging" class="xliff"></a>
## Расширенная отладка сценариев

Появились новые расширенные функции отладки, которые позволяют подключиться к любому процессу локального компьютера, загруженному в Windows PowerShell, и осуществить отладку произвольных пространств выполнения в нем.

<a id="runspace-debugging" class="xliff"></a>
### Отладка пространств выполнения

Были добавлены новые командлеты, позволяющие вывести список текущих пространств выполнения в процессе, а также подключить консоль Windows PowerShell или отладчик интегрированной среды сценариев к такому пространству для отладки сценариев:

-   Get-Runspace
-   Debug-Runspace
-   Enable-RunspaceDebug
-   Disable-RunspaceDebug
-   Get-RunspaceDebug

<a id="attach-to-process-hosting-powershell" class="xliff"></a>
### Подключение к процессу, в котором размещается PowerShell

Теперь вы можете подключиться к любому процессу на компьютере компьютера, в котором загружен Windows PowerShell. Это можно сделать, перейдя в интерактивный сеанс с процессом, по аналогии со входом в интерактивный удаленный сеанс с помощью командлета Enter-PSSession:

-   Enter-PSHostProcess
-   Exit-PSHostProcess

