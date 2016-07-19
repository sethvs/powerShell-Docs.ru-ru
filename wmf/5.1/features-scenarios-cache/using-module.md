---
title: "FullyQuilifiedModuleName для \"using module\""
author: jaimeo
contributor: vors
translationtype: Human Translation
ms.sourcegitcommit: e39aa2e5cbda0c83e24e21c4459d957d8baaff25
ms.openlocfilehash: e09cfe0994ac523fd10658955731a93b6c176c88

---

FullyQuilifiedModuleName для "using module"
=========================

`using module` теперь работает так же, как другие связанные с модулями конструкции в PowerShell.

Проблемы в WMF 5.0
----------

* У пользователя нет возможности указать версию модуля в `using module`.
* Если в системе есть несколько версий модуля, пользователь получит ошибку.

WMF 5.1
----------

* Пользователь может использовать [хэш-таблицу](https://msdn.microsoft.com/en-us/library/jj136290(v=vs.85).aspx) `ModuleSpecification`. Она имеет тот же формат, что и `Get-Module -FullyQualifiedName`

**Пример:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

* Если имеется несколько версий модуля, в PowerShell используется **та же логика разрешения**, что и в `Import-Module`, и ошибка не выводится.

* Это позволяет согласовать поведение `using module` с `Import-Module` и `Import-DscResource`.



<!--HONumber=Jul16_HO3-->


