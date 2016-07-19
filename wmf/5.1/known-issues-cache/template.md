---
title: "пример шаблона с описанием известной проблемы или ограничения"
contributor: 
translationtype: Human Translation
ms.sourcegitcommit: a952a27ec1695ce9951c352446194cf72d18f50a
ms.openlocfilehash: cfe0a6562743f1df81acb81e33c120cb67f9042c

---

>Примечание. Предоставьте предложенное описательное название и краткое описание.

## Пример. Ложные ошибки ExecutionPolicy ##
В Windows 7 использование модулей PowerShell и ресурсов DSC может привести к возникновению ошибок, связанных с ExecutionPolicy.

### Разрешение

Чтобы устранить проблему, задайте для **ExecutionPolicy** значение **RemoteSigned**, выполнив следующую команду в сеансе PowerShell с повышенными правами ("Запуск от имени администратора"):

```powershell
Set-ExecutionPolicy RemoteSigned
```



<!--HONumber=Jul16_HO1-->


