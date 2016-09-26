---
title: "Известные проблемы в WMF 5.1 (предварительная версия)"
ms.date: 2016-07-13
keywords: PowerShell, DSC, WMF
description: 
ms.topic: article
author: krishna
manager: dongill
ms.prod: powershell
ms.technology: WMF
translationtype: Human Translation
ms.sourcegitcommit: f413ba6470985622e55bb4bd175d7c5d4b94c7d9
ms.openlocfilehash: e545d49381a92ef3f7cc6a27316cbfc3a036a8c9

---

#Известные проблемы в WMF 5.1 (предварительная версия) #

> Примечание. Эта информация является предварительной и может быть изменена.

##Pester
В этом выпуске существует две проблемы, которые следует иметь в виду при использовании Pester на сервере Nano.

* Запуск тестов для самого Pester может привести к некоторым ошибкам из-за различий между FULL CLR и CORE CLR. В частности, для типа XmlDocument недоступен метод Validate. Известно, что шесть проверок схемы журналов вывода NUnit завершаются сбоем. 
* Один из тестов объема протестированного кода сейчас завершается сбоем из-за того, что ресурс DSC *WindowsFeature* не существует на сервере Nano Server. Тем не менее эти ошибки обычно носят информационный характер, и их можно спокойно пропустить.

##Проверка операций 

* Операция Update-Help над модулем Microsoft.PowerShell.Operation.Validation завершится ошибкой, так как URI справки не работает.



<!--HONumber=Sep16_HO3-->


