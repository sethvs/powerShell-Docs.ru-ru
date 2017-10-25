---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "wmf,powershell,установка"
ms.openlocfilehash: b839b476bb4ef7f8d73b158d61f0e8cbc1265e60
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/12/2017
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a>Ключевое слово Import-DscResource поддерживает параметр -moduleversion

Мы добавили в динамическое ключевое слово `Import-DscResource` новый параметр, доступный при создании конфигураций DSC. Авторы конфигурации теперь могут указать, из какой именно версии модуля следует загружать ресурсы DSC. Новый синтаксис ключевого слова имеет следующий вид.

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **Name:** имена одного или нескольких импортируемых ресурсов.
* **Имя ModuleName**: имена или объекты ModuleSpecification одного или нескольких импортируемых модулей.
* **ModuleVersion**: версия импортируемого модуля. При использовании значение ModuleName должно представлять по имени всего один модуль. 

В интегрированной среде сценариев Windows PowerShell оно отображается с IntelliSense:

![](../images/Import-DscResource-Modversion.jpg)

**Примечание**. Параметр `–ModuleVersion` можно использовать только вместе с параметром `–ModuleName`. Его нельзя использовать с именами ресурсов, используя только параметр `–Name`.

До этого единственный способ для указания версии модуля при загрузке ресурсов DSC заключался в использовании объекта спецификации модуля, например `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`.

