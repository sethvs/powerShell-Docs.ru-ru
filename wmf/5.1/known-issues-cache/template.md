---
title: "пример шаблона с описанием известной проблемы или ограничения"
contributor: 
ms.openlocfilehash: e3b98044902cb6665e06582c8259bd5defd6f2ca
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
>Примечание. Предоставьте предложенное описательное название и краткое описание.

## <a name="example-erroneous-executionpolicy-errors"></a>Пример. Ложные ошибки ExecutionPolicy ##
В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.

### <a name="resolution"></a>Разрешение

Чтобы устранить проблему, задайте для **ExecutionPolicy** значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):

```powershell
Set-ExecutionPolicy RemoteSigned
```
