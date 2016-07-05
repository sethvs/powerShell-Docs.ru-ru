---
description: 
manager: dongill
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-06-22
title: "обслуживание и развертывание на нескольких компьютерах"
ms.technology: powershell
ms.sourcegitcommit: 7504fe496a8913718847e45115d126caf4049bef
ms.openlocfilehash: 784806197a64eb30af1ecea4af55575434ce7b87

---

# Обслуживание и развертывание на нескольких компьютерах
К этому моменту вы уже неоднократно развертывали JEA в локальных системах.
Так как ваша рабочая среда может включать не один компьютер, а несколько, нужно выполнить критически важные шаги в процессе развертывания и повторить их на каждом компьютере.

## Шаги на высоком уровне.
1.  Скопируйте модули (с возможностями ролей) в каждый узел.
2.  Скопируйте файлы конфигурации сеансов на каждый узел.
3.  Выполните `Register-PSSessionConfiguration` с конфигурацией сеанса.
4.  Сохраните копию конфигурации сеанса и наборы инструментов в безопасном месте.
Внося изменения, хорошо иметь исходный эталонный образец.

## Пример сценария
Рассмотрим пример сценария развертывания.
Чтобы использовать его в среде, необходимо вставить имена и пути реальных общих папок и модулей.
```PowerShell
# First, copy the session configuration and modules (containing role capability files) onto a file share you have access to.
Copy-Item -Path 'C:\Demo\Demo.pssc' -Destination '\\FileShare\JEA\Demo.pssc'
Copy-Item -Path 'C:\Program Files\WindowsPowerShell\Modules\SomeModule\' -Recurse -Destination '\\FileShare\JEA\SomeModule'

# Next, author a setup script (C:\JEA\Deploy.ps1) to run on each individual node
    # Contents of C:\JEA\Deploy.ps1
    New-Item -ItemType Directory -Path C:\JEADeploy
    Copy-Item -Path '\\FileShare\JEA\Demo.pssc' -Destination 'C:\JEADeploy\'
    Copy-Item -Path '\\FileShare\JEA\SomeModule' -Recurse -Destination 'C:\Program Files\WindowsPowerShell\Modules' # Remember, Role Capability Files are found in modules
    if (Get-PSSessionConfiguration -Name JEADemo -ErrorAction SilentlyContinue)
    {
        Unregister-PSSessionConfiguration -Name JEADemo -ErrorAction Stop
    }

    Register-PSSessionConfiguration -Name JEADemo -Path 'C:\JEADeploy\Demo.pssc'
    Remove-Item -Path 'C:\JEADeploy' # Don't forget to clean up!

# Now, invoke the script on all of the target machines.
# Note: this requires PowerShell Remoting be enabled on each machine. Enabling PowerShell remoting is a requirement to use JEA as well.
# You may need to provide the "-Credential" parameter if your current user account does not have admin permissions on these machines.
Invoke-Command –ComputerName 'Node1', 'Node2', 'Node3', 'NodeN' -FilePath 'C:\JEA\Deploy.ps1'

# Finally, delete the session configuration and role capability files from the file share.
Remove-Item -Path '\\FileShare\JEA\Demo.pssc'
Remove-Item -Path '\\FileShare\JEA\SomeModule' -Recurse
```
## Изменение возможностей
При работе с несколькими компьютерами важно вносить изменения согласованно.
Когда у JEA появится ресурс DSC, это позволит обеспечить синхронизацию среды.
Пока же настоятельно рекомендуем сохранять мастер-копии конфигураций сеансов и обращаться к ним при каждом изменении.

## Удаление возможностей
Чтобы удалить конфигурацию JEA из системы, выполните на каждом компьютере следующую команду:
```PowerShell
Unregister-PSSessionConfiguration -Name JEADemo
```




<!--HONumber=Jun16_HO4-->


