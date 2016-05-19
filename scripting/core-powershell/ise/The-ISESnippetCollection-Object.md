---
title: Объект ISESnippetCollection
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
---
# Объект ISESnippetCollection
  Объект **ISESnippetCollection** — это коллекция объектов **ISESnippet**. Коллекция файлов, с которой связан объект **PowerShellTab**, является членом этого класса. Примером является коллекция **$psISE.CurrentPowerShellTab.Files**.

## Методы

### Load( FilePathName )
  Поддерживается в интегрированной среде сценариев Windows PowerShell 3.0 и более поздних версия и отсутствует в более ранних версиях. 

 Загружает SNIPPETS.PS1XML-файл, содержащий определяемые пользователем фрагменты кода. Для создания фрагментов кода проще всего использовать командлет New-IseSnippet, который автоматически сохраняет фрагменты в папке профиля, чтобы загружать их при каждом запуске интегрированной среды сценариев Windows PowerShell.

 **FilePathName** — строка.
 Путь и имя SNIPPETS.PS1XML-файла, содержащего определения фрагментов.

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## См. также
 [Объект ISESnippet](The-ISESnippetObject.md) 
 [Объектная модель сценариев интегрированной среды сценариев Windows PowerShell](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
 [Справочник по объектной модели интегрированной среды сценариев Windows PowerShell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Иерархия объектной модели интегрированной среды сценариев](The-ISE-Object-Model-Hierarchy.md)

  


<!--HONumber=May16_HO2-->


