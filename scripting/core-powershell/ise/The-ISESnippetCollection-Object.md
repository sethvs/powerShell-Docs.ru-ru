---
title: "Объект ISESnippetCollection"
ms.date: 2016-05-11
keywords: "powershell,командлет"
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
translationtype: Human Translation
ms.sourcegitcommit: 6c666e2e23cb74818e37293410dafc9033057733
ms.openlocfilehash: 410cd4503883ea2cc02936044d7357b9cb029274

---

# <a name="the-isesnippetcollection-object"></a>Объект ISESnippetCollection
  Объект **ISESnippetCollection** — это коллекция объектов **ISESnippet**. Коллекция файлов, с которой связан объект **PowerShellTab**, является членом этого класса. Примером является коллекция **$psISE.CurrentPowerShellTab.Files**.

## <a name="methods"></a>Методы

### <a name="load-filepathname-"></a>Load\( FilePathName \)
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Загружает SNIPPETS.PS1XML-файл, содержащий определяемые пользователем фрагменты кода. Для создания фрагментов кода проще всего использовать командлет New-IseSnippet, который автоматически сохраняет фрагменты в папке профиля, чтобы загружать их при каждом запуске интегрированной среды сценариев Windows PowerShell.

 **FilePathName** — строка. Путь к файлу с расширением SNIPPETS.PS1XML и его имя. В нем содержатся определения фрагментов.

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a>См. также
- [Объект ISESnippet](The-ISESnippetObject.md) 
- [Объектная модель скриптов интегрированной среды скриптов Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Справочник по объектной модели интегрированной среды скриптов Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Иерархия объектной модели интегрированной среды скриптов](The-ISE-Object-Model-Hierarchy.md)

  



<!--HONumber=Nov16_HO3-->


