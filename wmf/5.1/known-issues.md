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
ms.sourcegitcommit: 57049ff138604b0e13c8fd949ae14da05cb03a4b
ms.openlocfilehash: 387ebc0467b9f154444292f391af0f4b77123639

---

#Известные проблемы в WMF 5.1 (предварительная версия) #

> Примечание. Эта информация является предварительной и может быть изменена.

##Проблемы Pester
В этом выпуске существует две проблемы, которые следует иметь в виду при использовании Pester на сервере Nano.

* Запуск тестов для самого Pester может привести к некоторым ошибкам из-за различий между FULL CLR и CORE CLR. В частности, для типа XmlDocument недоступен метод Validate. Известно, что шесть проверок схемы журналов вывода nunit завершаются неудачно. 
* Один из тестов покрытия кода сейчас завершается неудачно из-за того, что ресурс DSC *WindowsFeature* не существует на сервере Nano. Тем не менее эти ошибки обычно носят информационный характер, и их можно спокойно пропустить.


<!--HONumber=Jul16_HO3-->


