---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
title: "пример шаблона с описанием известной проблемы или ограничения"
ms.openlocfilehash: b93393b2c84e76a301e6406d1388e82e95a2959c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
>Примечание. Предоставьте предложенное описательное название и краткое описание.

## <a name="example-erroneous-executionpolicy-errors"></a>Пример. Ложные ошибки ExecutionPolicy ##
В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.

### <a name="resolution"></a>Разрешение

Чтобы устранить проблему, задайте для **ExecutionPolicy** значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):

```powershell
Set-ExecutionPolicy RemoteSigned
```

